---
layout: post
title: jQuery Sandbox
categories: kissmetrics-test
---
<form action="#" name="myForm" method="post" enctype="text/plain" class="boss" id="boss">
Name:<br />
<input type="text" name="name" placeholder="your name" /><br />
E-mail:<br />
<input type="text" name="email" placeholder="your email" /><br />
<br /><br />
<input type="checkbox" name="vehicle" value="Bike" /> I have a bike<br />
<input type="checkbox" name="vehicle" value="Car" /> I have a car <br />
<input type="submit" value="Send">
<input type="reset" value="Reset">
<br />
<a id="submit-jq">Send via jQuery</a>

<script type="text/javascript">
	$("#boss").submit(function(event) {
	  console.log('sup');
      // _kmq.push(['record', 'Test Form Submitted (jQuery)'])		
	});
</script>
<br />