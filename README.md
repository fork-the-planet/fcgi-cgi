# fcgi-cgi

**homepage:** https://redmine.lighttpd.net/projects/fcgi-cgi/wiki

fcgi-cgi is a FastCGI application to run normal cgi applications. It doesn't
make CGI applications faster, but it allows you to run them on a different
host and with different user permissions (without the need for suexec).

lighttpd2 won't have a mod_cgi, so you need this FastCGI wrapper to be able
to execute standard cgi applications like mailman and cgit.

fcgi-cgi is released under the [MIT license](https://git.lighttpd.net/lighttpd/fcgi-cgi/src/branch/master/COPYING).

Similar projects:

* [fcgiwrap](https://github.com/gnosek/fcgiwrap) (also available as [debian package](https://tracker.debian.org/pkg/fcgiwrap))

## Usage

Examples for spawning a fcgi-cgi instance with daemontools or runit::

```
#!/bin/sh
# run script

exec spawn-fcgi -n -s /var/run/fastcgi-cgi.sock -u www-default -U www-data -- /usr/bin/fcgi-cgi
```
## Build dependencies

* glib >= 2.16.0 (https://gitlab.gnome.org/GNOME/glib/)
* libev (https://software.schmorp.de/pkg/libev.html)
* meson (https://mesonbuild.com/)

## Build

Clone from git: ``git clone https://git.lighttpd.net/lighttpd/fcgi-cgi.git``

Setup a build directory `build`:

    meson setup build --prefix /usr/local

Compile it:

    meson compile -C build

Install:

    meson install -C build
