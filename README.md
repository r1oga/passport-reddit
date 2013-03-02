# Passport-Reddit

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Reddit](http://reddit.com/) using the OAuth 2.0 API.

This module lets you authenticate using Reddit in your Node.js applications.
By plugging into Passport, Reddit authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-reddit

## Usage

#### Configure Strategy

The Reddit authentication strategy authenticates users using a Reddit
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new RedditStrategy({
        clientID: REDDIT_CONSUMER_KEY,
        clientSecret: REDDIT_CONSUMER_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/reddit/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ redditId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'reddit'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/reddit',
      passport.authenticate('reddit'));

    app.get('/auth/reddit/callback',
      passport.authenticate('reddit', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Examples

For a complete, working example, refer to the [login example](https://github.com/slotos/passport-reddit/tree/master/examples/login).

## Tests

    $ npm install --dev
    $ make test

[![Build Status](https://secure.travis-ci.org/Slotos/passport-reddit.png)](http://travis-ci.org/Slotos/passport-reddit)

## Credits

  - [Jared Hanson](http://github.com/jaredhanson)
  - [Dmytro Soltys](http://github.com/slotos)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Original work Copyright (c) 2012-2013 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
Modified work Copyright (c) 2013 Dmytro Soltys <[http://slotos.net/](http://slotos.net/)>
