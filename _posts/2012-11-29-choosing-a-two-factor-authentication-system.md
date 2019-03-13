---
layout: post
title: Choosing a Two-Factor Authentication System
date: 2012-11-29 04:21
author: cloudflare.com
comments: true
categories: [accountsecurity, authy, passwords, Security, twofactorauthentication]
---
<p><img alt="Choosing a Two-Factor Authentication
System" src="/static/images/two-factor-token.jpg.scaled500.jpg" title="Choosing a Two-Factor Authentication System" /></p>
<p>We've been thinking about how to best implement two-factor
authentication to better protect our customers' accounts for quite some
time now. When, about 6 months ago, my account was <a href="http://blog.cloudflare.com/post-mortem-todays-attack-apparent-google-app">targeted by
hackers</a> the
importance of a good account security became clear. However, as my
hacking case illustrates, two-factor authentication alone is not a
complete answer.</p>
<p>At CloudFlare, we considered a number of different ways to implement
two-factor authentication. We considered building it ourselves and using
Twilio, or another similar service, to send authentication codes via SMS
to our customers' mobile phones. The problem with that strategy is that
it passes the supposedly secure authentication code through your mobile
carrier's less-than-secure network. And, again, if there's a lesson to
be learned from my own hacking case it's that mobile providers' security
is not always the most robust.</p>
<p>We also considered some sort of fob-based two-factor system.
Unfortunately, these are generally very expensive and therefore
prohibitive for us to offer all our customers. We also considered
solutions like Google's Authenticator. It's a well thought out system,
and we have a ton of respect for the Google team, but we were nervous
about handing another key to identity over to a company whose primary
business is search and advertising. Not to mention a bit of a bad taste
after a <a href="http://blog.cloudflare.com/the-four-critical-security-flaws-that-resulte">flaw in Google's own implementation of their two-factor
authentication
system</a> contributed
to my hack.</p>
<h2>TOTP: Open Authentication</h2>
<p>The underlying algorithm used by several two-factor authentication
schemes, including Google's, is open and known as the <a href="http://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm">Time-based
One-time Password Algorithm
(TOTP)</a>.
TOTP was specified by the Internet Engineering Task Force (IETF)
under <a href="http://tools.ietf.org/html/rfc6238">RFC 6238</a>.</p>
<p>The mechanics of TOTP are relatively easy to understand. To begin, every
TOTP user is issued a random key. Both the server and the client has a
copy of this random key. TOTP assumes that both the server and the
client can synchronize their clocks. When a user goes to login, the
client takes the current timestamp to the previous 30-second interval.
The client then combines the key and the timestamp.</p>
<p>This combined key and timestamp value is then run through a SHA hashing
algorithm. SHA, like other cryptographic hashes, is a one-way algorithm.
That the output cannot be used to derive the input. The SHA algorithm's
output becomes the authentication code which the user can post to the
server as part of the login process.</p>
<p>Since the server has the same random key for the user, and since the
client and server clocks are synchronized, the server can also calculate
an authentication code using the SHA algorithm. If the authentication
code the server has received from the user matches the one the server
derived itself then the user's identity can be confirmed.</p>
<p>What is powerful about this scheme is that if an attacker steals the
authorization code then, within 30 seconds, it will be useless. This is
typically insufficient time for the attacker to gain access to the
account. This is particularly effective against phishing attacks, where
an attacker convinces a user to reveal their login credentials on a fake
website.</p>
<h2>Authy</h2>
<p>If the core algorithm for two-factor authentication is public, then the
question comes down to who has the best implementation. We looked at
several implementations and were particularly impressed by a company
called <a href="http://www.authy.com/">Authy</a>. The Authy team created a
beautiful, simple, elegant app that implements TOTP. Their vision is not
to create yet another app you need to install, but instead to create a
single place from which you can manage all your TOTP two-factor
authentication tokens.</p>
<p><img alt="Choosing a Two-Factor Authentication
System" src="/static/images/authy_logo.png.scaled500.png" title="Choosing a Two-Factor Authentication System" /></p>
<p>We've been using the Authy app internally for all of our administrative
systems for the last three months. The Authy team has worked with us to
refine their app to make it as simple and elegant as possible. After
months of our own tests, and spurred on by a phishing attack that
targeted CloudFlare accounts, we decided to open up two-factor
authentication as a feature for all our customers. If you're interested,
you can read about how to implement it on your account with <a href="http://blog.cloudflare.com/2-factor-authentication-now-available">just a few
easy
steps</a>.</p>
<h2>But... I've Already Installed Google Authenticator on My Phone!</h2>
<p>The biggest question we continue to get is why we didn't just use Google
Authenticator, since a number of people already have it installed on
their phones. Beyond the high-level concerns above, there were a number
of technical concerns over security and ease of use that we believe made
Authy a better choice.</p>
<p>First, with Google Authenticator if you lose your app there's no way you
can revoke the app's tokens. This is probably the biggest security flaw
with the Google Authenticator app. While it can be mitigated by password
protecting your phone, the better solution is to allow the app to be
deauthorized. Authy fixes this problem and allows you to revoke the
app's token if you lose your phone. That's a big win for Authy over
Google Authenticator.</p>
<p>Second, Google's Authenticator can get out of sync when you don't have
network access, leaving you in the frustrating situation of not being
able to access your account. Since all TOTP systems rely on the clock on
your phone to match the clock on the server, if there's not a fairly
precise match then there can be problems. I've experienced this myself
when traveling and it can be frustrating. Authy has built a significant
amount of logic into their app in order to keep clocks in sync even when
you don't have network access.</p>
<p>Third, if you upgrade your phone, with Google's Authenticator you have
to reestablish all your two-factor accounts from scratch. With Authy,
all your accounts are synced, so when you upgrade and re-install Authy
everything will be setup the way you expect it.</p>
<p>And there are a number of other well thought out details. Authy uses
SHA-2 and 256-bit keys, where Google's Authenticator uses SHA-1 and
128-bit keys — likely not a huge deal for this application, but
generally longer keys and more secure hashing protocols are better. When
you wake your phone from sleep, Authy will always start with a code good
for the next 30 seconds — it's a nice touch and removes the annoyance
with Google's Authenticator of having to wait for the timer to expire if
you don't have enough time to enter a code. And the interface is cleaner
and just nicer to use than Google's.</p>
<p>But we get it. People don't like to have to install another app on their
phones. The good news is the Authy team gets it too. They're adding
support in the next few weeks for Google Authenticator tokens to their
system as well. That way you can use Authy's great UI to access your
Google codes through one app.</p>
