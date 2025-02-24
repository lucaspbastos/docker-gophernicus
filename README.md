# docker-gophernicus

**Fork of [Kaiju's Docker Gophernicus](https://github.com/kaiju/docker-gophernicus) that has a few fixes and multi-arch support for ARMv6, ARMv7, ARM64, and x86_64**
An Alpine Linux based Docker image for the [Gophernicus Gopher server](https://github.com/gophernicus/gophernicus).

Do you just want to run a simple Gopher service? Do you not want to mess the hassle of setting up old-school inetd/xinetd/systemd sockets/etc? Are you already running all your other services as containers? Me too!

This image runs Gophernicus via xinetd on an Alpine Linux base for a Docker image that weighs in at just a smidge under 7MB. Set your hostname, map your favorite volume at `/var/gopher`, bind port 70 and go!

ex:
```
docker run --name gophernicus \
    --hostname '<your gopher hostname>' \
    -p 70:70 \
    -v <your gopher root>:/var/gopher \
    lucaspbastos/gophernicus
```

## Configuration

Set the hostname of your container to the FQDN of your gopher site to ensure that links work correctly.

The majority of [Gophernicus settings](https://github.com/gophernicus/gophernicus#command-line-options) can be configured via environment variables. All Gophernicus defaults apply except where otherwise noted.

```
PORT                Server Port (-p, default 70)
TLS_PORT            TLS/SSL Port (-T)
GOPHER_ROOT         Document root (-r, default: /var/gopher)
DEFAULT_FILE_TYPE   Default Gopher file type (-t)
GOPHER_MAPFILE      Gophermap file (-g)
GOPHER_TAGFILE      Gophertag file (-a)
CGI_DIR             CGI script directory (-c)
USER_DIR            Name of personal gopherspace directory to find in user home dirs (-u)
LOG_FILE            Filename to write apache style access logs (-l, default /var/log/gophernicus.log)
DEFAULT_WIDTH       Default page width (-w)
DEFAULT_CHARSET     Default character set (-o)
SESSION_TIMEOUT     Session timeout in seconds (-s)
MAX_HITS            Maximum hits before throttling (-i)
MAX_TRANSFER_KB     Maximum transfer in kb until throttling (-k)
FILTER_DIR          Directory for output filters (-f)
```
Some configuration arguments can be set by defining environment variables with any value:
```
DISABLE_VHOSTS              Disable virtual hosts (-nv)
DISABLE_PARENT_DIR_LINKS    Disable parent directory links (-nl)
DISABLE_HEADER              Disable menu header (-nh)
DISABLE_FOOTER              Disable menu footer (-nf)
DISABLE_MENU_METADATA       Disable dates and filesizes in menus (-nd)
DISABLE_CONTENT_DETECTION   Disable file content detection (-nc)
DISABLE_CHARSET_CONV        Disable character set conversion (-no)
DISABLE_QUERY_STRINGS       Disable HTTP style query strings (-nq)
DISABLE_SYSLOG              Disable logging to syslog (-ns)
DISABLE_AUTOGEN_CAPS        Disable autogenerated caps.txt (-na)
DISABLE_SERVER_STATUS       Disable server status endpoint (-nt)
DISABLE_HAPROXY             Disable HAProxy protocol support (-np)
DISABLE_EXECUTABLES         Disable executable scripts (-nx)
DISABLE_USERDIRS            Disable personal gopherspaces in homedirs (-nu)
```

## TODO

- Allow configuration of some of the more complicated arguments (filetype mapping, selectors)
