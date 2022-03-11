---
layout: post
title: Migrating From Sprockets to Webpacker
categories: writing
image: https://user-images.githubusercontent.com/1744567/157798874-7df0f894-eb4d-4b29-af7b-930ba87201af.jpeg
image_alt: piping on a roof
---

Starting with Rails 6, Webpacker became the default asset compiler, replacing sprockets–better known as the asset pipeline. While the asset pipeline was a big step for its time in making it easy to package JS, CSS, and images, webpack has matured enough to do all of the above and more, due to modern JavaScript’s support for modular imports and exports.

## Why Migrate?
Personally, the biggest benefit of webpacker is how it encourages me to think about structuring assets as components, so that they are theoretically portable and do not rely on hidden globals. And by using an extensible tool like webpack under the hood, you can take advantage of popular plugins and customizations to tune what you need – like deduplicating shared imports, in both JS and CSS. Finally, you’re not limited to just extending webpack: it’s much easier to tap into the huge ecosystem of npm packages. Below is a breakdown of how to start moving from sprockets to webpacker.

## Directory Conventions

In Rails projects that use the asset pipleine, we are accustomed to seeing the frontend assets organized like so:

```
app
  assets
    images
    javascripts
    stylesheets
```

With webpacker, the project will end up looking like:

```
app
  javascript
    images
    packs
    stylesheets
```

## Add Webpacker to an Existing Project

```sh
bundle add webpacker
bundle exec rails webpacker:install
bundle exec rails webpacker:install:react  # To optionally add React support. See Webpacker documentation for other supported frontend frameworks
```

## Migrating JavaScript

The JS entrypoint changes from app/assets/javascripts/application.js to app/javascript/packs/application.js.

### Add Polyfills

These polyfills ensure that modern JS features (promises, async/await, arrow function expressions, and more) are available on the browsers you intend to support, which is indicated by the .browserslistrc file.

```sh
yarn add core-js regenerator-runtime  # Yarn is a pre-requisite: https://yarnpkg.com/
```

Then at the top of your new entrypoint:

```js
// app/javascript/packs/application.js
import "core-js/stable";
import "regenerator-runtime/runtime";
```

### Use the new view helper

```erb
# E.g. app/views/layouts/application.html.erb
javascript_include_tag "application"
```

can be replaced by

```erb
javascript_pack_tag "application"
```

## Migrating Stylesheets

Stylesheets can move directories:

```
app/assets/stylesheets => app/javascript/stylesheets
```

To get Webpacker to handle your styles, you need your JS entry point to import your stylesheet:

```js
// app/javascript/packs/application.js

/**
 * Refers to app/javascript/stylesheets/application.scss (or application.css)
 * Note that we don't need to preface this path with "app/javascript" due to the `source_path` config set in config/webpacker.yml. Magical!
 * The file extension can be left off due to the `extensions` config in config/webpacker.yml.
 */
import "stylesheets/application";
```

### Use the new view helper

```erb
# E.g. app/views/layouts/application.html.erb
stylesheet_link_tag "application"
```

can be replaced by

```erb
stylesheet_pack_tag "application"
```

## Migrating Images

Images can move directories:

```
app/assets/images => app/javascript/images
```

Uncomment the generated block to make your pack aware of everything in the images directory:

```js
// app/javascript/packs/application.js
const images = require.context("../images", true);
const imagePath = (name) => images(name, true);
```

### Use the new view helper

```erb
# E.g. app/views/layouts/application.html.erb
image_tag "foo/bar"
```

Can be replaced by:

```erb
image_pack_tag "foo/bar"
```

## Continuous Integration and Deployments
Update your CI and deployment processes to fetch npm dependencies. For an example, see the CircleCI config in the Carbon Five Rails template app: https://github.com/carbonfive/raygun-rails/blob/master/.circleci/config.yml


## Optional: Enable SplitChunks
Webpack 4 has a new plugin to split chunks, which allows for shared dependencies to be broken into their own file (“chunk”). These dependencies can be more easily cached independently of your application code. To opt into using split chunks, enable the config and update your views:

```js
// config/webpack/environment.js
const { environment } = require("@rails/webpacker");

environment.splitChunks();

module.exports = environment;
```

```erb
# E.g. app/views/layouts/application.html.erb
javascript_packs_with_chunks_tag "application" # Replaces javascript_pack_tag "application"
stylesheet_packs_with_chunks_tag "application" # Replaces stylesheet_pack_tag "application"
```

## Optional: Customizing Project Structure
If you find it strange to nest stylesheets and images under a “javascript” folder, Webpacker allows you to rename this directory, with minimal configuration changes.

```sh
mv app/javascript app/frontend
```

```
// config/webpacker.yml
source_path: app/frontend
```

## Cleaning Up

### Gems
Frontend gems can be replaced by corresponding npm packages. For example, we removed these four from our Rails app template:

* autoprefixer-rails: functionality is handled by Webpacker by default
* bootstrap-rails: https://www.npmjs.com/package/bootstrap
* sass-rails/sassc-rails: functionality is handled by Webpacker by default
* uglifier: functionality is handled by Webpacker by default

### Disable Sprockets

Remove the Sprockets railtie from config/application.rb. You may need to expand the default require statement (“rails/all”) and explicitly state which railties you want to use. For reference, see the list of ‘all’ railties for the version of rails you are using: https://github.com/rails/rails/blob/master/railties/lib/rails/all.rb

```rb
# E.g. config/application.rb
require "active_job/railtie"
require "active_record/railtie"
# require "sprockets/railtie"
```

### Remove any additional assets config

Remove any configs still in the `Rails.application.config.assets` namespace.
