## Reason why this doesnt't work (read first!)

When I forked this repo I thought it was a cool idea to use heroku for an icecast server. However, after spending a few hours reworking the build pack to compile from source. I realized this is more work to setup than it should be. The main issue (mentiond later in this original readme) is that the source connection requests won't get through to the server. That's because icecast uses a non-standard HTTP verb (`SOURCE`) to connect to the server for streaming. Heroku's router only supports the standard verbs (`GET`, `POST`, etc..).

In icecast 2.4 it IS possible to use `PUT` to conect a source to the server, but in practice no source clients support this.

---

Icecast on Heroku
=================

Because why the fuck would you wanna pay for bandwidth to stream to folks?

At GitHub we've been having a lot of fun playing music with [Traktor Pro 2](http://www.native-instruments.com/#/en/products/dj/traktor-pro-2/).  I wanted to be able to have people share the music they're playing with each other.  

This is a heroku buildpack that runs an icecast server that's friendly to the
heroku environment.  If you use it, it requires a `config/icecast.xml` file to
be in your heroku application's directory structure.

This is still pretty hacky and experimental, and requires some SSL load
balancer options that heroku doesn't offer by default right now.

Installation
------------

  * Create your heroku application
  * Supply the `BUILDPACK_URL` env variable 

```
heroku config:add BUILDPACK_URL="https://github.com/atmos/heroku-buildpack-icecast.git"
```

Modify your configuration file to suit your needs.  Enjoi.
