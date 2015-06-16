---
layout: post
title:  "Passwordless authentication: Secure, simple, and fast to deploy"
date:   2014-11-06 11:20:43
categories: github authentication passwordless
---

[Passwordless](https://passwordless.net) is an authentication middleware for Node.js that improves security for your users while being fast and easy to deploy.

The last months were very exciting for everyone interested in web security and privacy: Fantastic [articles](https://medium.com/@ninjudd/passwords-are-obsolete-9ed56d483eb), [discussions](https://news.ycombinator.com/item?id=7943365), and talks but also plenty of [incidents](http://dealbook.nytimes.com/2014/10/03/hackers-attack-cracked-10-banks-in-major-assault/?_php=true&_type=blogs&_r=0) that raised awareness. 

Most websites are, however, still stuck with the same authentication mechanism as from the earliest days of the web: username and password.

While username and password have their place, we should be much more challenging if they are the _right_ solution for our projects. We know that most people use the [same password](http://nakedsecurity.sophos.com/2013/04/23/users-same-password-most-websites/) on all the sites they visit. For projects without dedicated security experts, should we really open up our users to the risk that a breach of our site also compromises their Amazon account? Also, the classic mechanism has by default at least two attack vectors: the login page and the password recovery page. Especially the latter is often implemented hurried and hence inherently more risky.

We’ve seen quite a bit of [great ideas](https://www.mozilla.org/en-US/persona/) and I got particularly excited by one very straightforward and low-tech solution: One-time passwords. They are fast to implement, have a small attack surface, and require neither QR codes nor JavaScript. Whenever a user wants to login or has her session invalidated, she receives a short-lived one-time link with a token via email or text message. If you want to give it a spin, feel free to test the demo on [passwordless.net](https://passwordless.net).

Unfortunately—depending on your technology stack—there a few to none ready-made solutions out there. [Passwordless](https://passswordless.net) changes this for Node.js.

# Getting started on Node.js & Express
Getting started with Passwordless is straight-forward and you’ll be able to deploy a fully fledged and secure authentication solution for a small project within two hours:

`$ npm install passwordless --save`

gets you the basic framework. You'll also want to install one of the existing [storage interfaces](https://passwordless.net/plugins) such as [MongoStore](https://github.com/florianheinemann/passwordless-mongostore) which store the tokens securely:

`$ npm install passwordless-mongostore --save`

To deliver the tokens to the users, email would be the most common option (but text message is also feasible) and you’re free to pick any of the existing email frameworks such as:

`$ npm install emailjs --save`

# Setting up the basics
Let’s require all of the above mentioned modules in the same file that you use to initialise Express:

{% highlight javascript %}
var passwordless = require('passwordless');
var MongoStore = require('passwordless-mongostore');
var email   = require("emailjs");
{% endhighlight %}

If you’ve chosen [emailjs](http://emailjs.org) for delivery that would also be a great moment to connect it to your email account (e.g. a Gmail account): 

{% highlight javascript %}
var smtpServer  = email.server.connect({
   user:    yourEmail, 
   password: yourPwd, 
   host:    yourSmtp, 
   ssl:     true
});
{% endhighlight %}

The final preliminary step would be to tell Passwordless which storage interface you’ve chosen above and to initialise it:

{% highlight javascript %}
// Your MongoDB TokenStore
var pathToMongoDb = 'mongodb://localhost/passwordless-simple-mail';
passwordless.init(new MongoStore(pathToMongoDb));
{% endhighlight %}

# Delivering a token
`passwordless.addDelivery(deliver)` adds a new delivery mechanism. `deliver` is called whenever a token has to be sent. By default, the mechanism you choose should provide the user with a link in the following format:

`http://www.example.com/token={TOKEN}&uid={UID}`

`deliver` will be called with all the needed details. Hence, the delivery of the token (in this case with emailjs) can be as easy as:


{% highlight javascript %}
passwordless.addDelivery(
	function(tokenToSend, uidToSend, recipient, callback) {
		var host = 'localhost:3000';
		smtpServer.send({
			text:    'Hello!\nAccess your account here: http://' 
			+ host + '?token=' + tokenToSend + '&uid=' 
			+ encodeURIComponent(uidToSend), 
			from:    yourEmail, 
			to:      recipient,
			subject: 'Token for ' + host
		}, function(err, message) { 
			if(err) {
				console.log(err);
			}
			callback(err);
		});
});
{% endhighlight %}

# Initialising the Express middleware

{% highlight javascript %}
app.use(passwordless.sessionSupport());
app.use(passwordless.acceptToken({ successRedirect: '/'}));
{% endhighlight %}

`sessionSupport()` makes the login persistent, so the user will stay logged in while browsing your site. Please make sure that you’ve already prepared your session middleware (such as [express-session](https://github.com/expressjs/session)) beforehand.

`acceptToken()` will intercept any incoming tokens, authenticate users, and redirect them to the correct page. While the option `successRedirect` is not strictly needed, it is strongly recommended to use it to avoid leaking valid tokens via the referrer header of outgoing HTTP links on your site.

# Routing & Authenticating
The following takes for granted that you've already setup your router `var router = express.Router();` as explained in the [express docs](http://expressjs.com/4x/api.html#router)

You will need at least two URLs to:
* Display a page asking for the user's email
* Accept the form details (via POST)


{% highlight javascript %}
/* GET: login screen */
router.get('/login', function(req, res) {
   res.render('login');
});

/* POST: login details */
router.post('/sendtoken', 
	function(req, res, next) {
		// TODO: Input validation
	},
	// Turn the email address into a user ID
	passwordless.requestToken(
		function(user, delivery, callback) {
			// E.g. if you have a User model:
			User.findUser(email, function(error, user) {
				if(error) {
					callback(error.toString());
				} else if(user) {
					// return the user ID to Passwordless
					callback(null, user.id);
				} else {
					// If the user couldn’t be found: Create it!
					// You can also implement a dedicated route 
					// to e.g. capture more user details
					User.createUser(email, '', '', 
						function(error, user) {
							if(error) {
								callback(error.toString());
							} else {
								callback(null, user.id);
							}
					})
				}
		})
	}),
	function(req, res) {
		// Success! Tell your users that their token is on its way
		res.render('sent');
});
{% endhighlight %}

What happens here? `passwordless.requestToken(getUserId)` has two tasks: Making sure the email address exists _and_ transforming it into a unique user ID that can be sent out via email and can be used for identifying users later on. Usually, you’ll already have a model that is taking care of storing your user details and you can simply interact with it as shown in the example above.

In some cases (think of a blog edited by just a couple of users) you can also skip the user model entirely and just hardwire valid email addresses with their respective IDs:


{% highlight javascript %}
var users = [
	{ id: 1, email: 'marc@example.com' },
	{ id: 2, email: 'alice@example.com' }
];

/* POST: login details */
router.post('/sendtoken', 
	passwordless.requestToken(
		function(user, delivery, callback) {
			for (var i = users.length - 1; i >= 0; i--) {
				if(users[i].email === user.toLowerCase()) {
					return callback(null, users[i].id);
				}
			}
			callback(null, null);
		}),
		// Same as above…
{% endhighlight %}

# HTML pages
All it needs is a simple HTML form capturing the user’s email address. By default, Passwordless will look for an input field called `user`:

{% highlight html %}
<html>
	<body>
		<h1>Login</h1>
		<form action="/sendtoken" method="POST">
			Email:
			<br><input name="user" type="text">
			<br><input type="submit" value="Login">
		</form>
	</body>
</html>
{% endhighlight %}

# Protecting your pages
Passwordless offers middleware to ensure only authenticated users get to see certain pages:

{% highlight javascript %}
/* Protect a single page */
router.get('/restricted', passwordless.restricted(),
 function(req, res) {
  // render the secret page
});

/* Protect a path with all its children */
router.use('/admin', passwordless.restricted());
{% endhighlight %}

# Who is logged in?
By default, Passwordless makes the user ID available through the request object: `req.user`. To display or reuse the ID it to pull further details from the database you can do the following:


{% highlight javascript %}
router.get('/admin', passwordless.restricted(),
	function(req, res) {
		res.render('admin', { user: req.user });
});
{% endhighlight %}

Or, more generally, you can add another middleware that pulls the whole user record from your model and makes it available to any route on your site:

{% highlight javascript %}
app.use(function(req, res, next) {
	if(req.user) {
		User.findById(req.user, function(error, user) {
			res.locals.user = user;
			next();
		});
	} else { 
		next();
	}
})
{% endhighlight %}

# That’s it!
That’s all it takes to let your users authenticate securely and easily. For more details you should check out the [deep dive](https://passwordless.net/deepdive) which explains all the options and the [example](https://github.com/florianheinemann/passwordless/tree/master/examples/simple-mail) that will show you how to integrate all of the things above into a working solution.

# Evaluation
As mentioned earlier, all authentication systems have their tradeoffs and you should pick the right system for your needs. Token-based channels share one risk with the majority of other solutions incl. the classic username/password scheme: If the user’s email account is compromised and/or the channel between your SMTP server and the user’s, their account on your site will be compromised as well. Two default options help mitigate (but not entirely eliminate!) this risk: Short-lived tokens and automatic invalidation of tokens after they’ve been used once.

For most sites token-based authentication represents a step up in security: users don’t have to think of new passwords (which are usually too [simple](http://splashdata.com/press/worstpasswords2013.htm)) and there is no risk of them reusing passwords. For us as developers, Passwordless offers a solution that has only one (and simple!) path of authentication that is easier to understand and hence to protect. Also, we don’t have to touch any user passwords.

Another point is usability. We should consider both, the first time usage of your site and the following logons. For first-time users, token-based authentication couldn’t be more straight-forward: They will still have to validate their email address as they have to with classic login mechanisms, but in the best-case scenario there will be no additional details required. No creativity needed to come up with a password that fulfils all restrictions and nothing to memorise. If the user logins again, the experience depends on the specific use case. Most websites have relatively long session timeouts and logins are relatively rare. Or, people’s visits to the website are actually so infrequent that they will have difficulties recounting if they already had an account and if so what the password could have been. In those cases Passwordless presents a clear advantage in terms of usability. Also, there are few steps to take and those can be explained very clearly along the process. Websites that users visit frequently and/or that have conditioned people to login several times a week (think of Amazon) might however benefit from a classic (or even better: two-factor) approach as people will likely be aware of their passwords and there might be more opportunity to convince users about the importance of good passwords.

While Passwordless is considered stable, I would love your [comments and contributions](https://github.com/florianheinemann/passwordless) on GitHub or your questions on Twitter: [@thesumofall](https://twitter.com/thesumofall).

This blog post has been published on [Mozilla Hacks](https://hacks.mozilla.org/2014/10/passwordless-authentication-secure-simple-and-fast-to-deploy/).