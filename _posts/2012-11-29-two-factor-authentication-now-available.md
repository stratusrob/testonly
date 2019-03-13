---
layout: post
title: Two-factor Authentication Now Available
date: 2012-11-29 01:05
author: cloudflare.com
comments: true
categories: [authy, onlinesecurity, Security, twofactorauthentication]
---
<p>With web performance and security being the core of CloudFlare, we are
always looking for ways to improve not just our customers' website
security, but their account security as well. Therefore, we are excited
to now offer two-factor authentication for all CloudFlare accounts. </p>
<p>With two-factor authentication, our customers' accounts get an added
layer of login security, ultimately adding another layer of security to
their websites. We've been working on this feature for a while, and we
are happy to announce that it's ready and available to all CloudFlare
customers.</p>
<p>To make this feature happen, we worked with
<a href="https://www.authy.com/">Authy</a>, a startup who loves security too. Authy
provides an easy-to-use, powerful two-factor authentication service.
Their mission is to turn everyone's cell phone into a secure token. The
Authy app works with iOS and Android devices and we're providing it free
to all CloudFlare account holders. Here's how it works.</p>
<h2>Easy additional account security</h2>
<p>To turn two-factor authentication on, you simply log into your
CloudFlare account, navigate to "<a href="https://www.cloudflare.com/my-account">My
account</a>" and select "two-factor
authentication with Authy."</p>
<p><img alt="Two-factor Authentication Now
Available" src="/static/images/Screen20shot202012-11-2020at2012.22.1420PM.png.scaled500.png" title="Two-factor Authentication Now Available " /></p>
<p>Once there, you will enter your mobile phone information and select
"enable two-factor authentication."</p>
<p>You will then receive a text message (your provider's standard text
messaging rates will apply). The text message includes a link to
download the Authy app. The Authy app will ask you to enter your your
mobile phone number. It will then text you a setup pin that you need to
enter into the Authy app.</p>
<p><img alt="Two-factor Authentication Now
Available" src="/static/images/authy-install-link.png.scaled500.png" title="Two-factor Authentication Now Available " /><img alt="Two-factor
Authentication Now
Available" src="/static/images/authy-registration_copy.png.scaled500.png" title="Two-factor Authentication Now Available " /></p>
<p>Once you receive your pin number via text, enter it into the Authy app.
The Authy app will then be authorized and able to generate
authentication tokens unique to your account. In the future, whenever
you access your CloudFlare account you'll need three things: 1) your
email address, 2) your password, and 3) your two-factor authentication
token.</p>
<p>When you <a href="https://www.cloudflare.com/login">login to CloudFlare</a> for the
first time after enabling two-factor authentication, you will need to
launch the Authy app on your phone. It will generate a unique, 7-digit
authentication token. The authentication token is good for 30 seconds
and then will change to a new token.</p>
<p><img alt="Two-factor Authentication Now
Available" src="/static/images/cloudflare-token.png.scaled500.png" title="Two-factor Authentication Now Available " /></p>
<p>You can store your authentication for 14 days. If you login from an
unrecognized device, or after your authentication expires, you'll need
to open the Authy app and get your new authentication token for that
device. The Authy app does not rely on you having network access, so you
can retrieve your code even if your phone is not connected to the
Internet.</p>
<p>If you ever lose your phone or get a new one you can reassociate your
account by following the <a href="https://www.authy.com/phones/reset">reset
instructions</a> on Authy's website.</p>
<p>You don't need to enable two-factor authentication in order to continue
to use CloudFlare. However, we're providing it to all CloudFlare
customers free and we recommend it for everyone who wants additional
account security.</p>
