These are files that allow "Loging with Twitter". With dev_appserver on localhost standard login is used. It is replaced with Twitter login in production.

based on http://github.com/tav/tweetapp

probably, needs to be updated to some other up-to-date libraries, e.g.
http://github.com/mikeknapp/AppEngine-OAuth-Library

To use it the following modifications need to be made:

1. register the application at http://twitter.com/apps/new with callback URL 
   http://your.app.url/oauth/twitter/callback
2. twitter_oauth_handler.py: put corresponding CONSUMER_KEY and CONSUMER_SECRET,
3. users.py: update APP_NAME (if the app main URL is not on appspot).

How to use:

::

    import users
    from twitter_oauth_handler import OAuthHandler

    user = users.get_current_user(self)
    if user:
        login_logout_link = "<strong>%s</strong><br/><a href=\"%s\">Logout</a>" % (user, users.create_logout_url(self, "/"))
    else:
        login_logout_link = "<a href=\"%s\">Login with Twitter</a>" % users.create_login_url(self, "/")

    application = webapp.WSGIApplication([
                                        ('/oauth/(.*)/(.*)', OAuthHandler),
                                        ])
