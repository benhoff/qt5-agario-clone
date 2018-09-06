# Qt5 Cross Platform Applications

Course being developed with Packt Publishing showcasing the portability of Qt5 to do Cross Platform development by building out and distributing an Agar.io clone!

## Overview

There are four seperate projects contained in this repo.

1. eatem-standalone (QML/C++ Agario single player)
2. eatem (QML Agario client)
3. eatem-server (QML Agario server)
4. eatem-web (HTML/JavaScript Agario client)

The web client (eatem-web) is currently under devlopment/not working.

Recommend building/running eatem-standalone using either Qt Creator or qmake/make.

If you want to try out the client and server, please ensure that the server is running first as there is no reconnect functionality built into the client. The QML client and server are 97% game-feature complete. The client/server are currently hardcoded to serve on the localhost (ip addresss 127.0.0.1) on port 5555 and serve content unencrypted.

#### Note of Caution

Please note that the server/game was built for educational purposes, so the server is *not* performant/optimized. The server implementation is single threaded. The data structures are basic lists (vs a quadtree or some other space-based data structure). No attempts where made to reduce the networking overhead. No attempts were made with respect to DDOS prevention and some of the server endpoints could easily be abused in a game-breaking manner, as not all of them are rate-limited. You've been warned!

## Server Pre-build Instructions

Unfortunately, Qt [has a bug](https://bugreports.qt.io/browse/QTBUG-70078) that causes some stale cache issues when running the server

To clone the patched version of QtWebChannel in.

```bash
$ git clone https://github.com/PacktPublishing/Qt5-Cross-Platform-Application-Development
$ git submodule init
$ git submodule update
```

Now to compile the patched QtWebChannel

```bash
$ cd qtwebchannel
$ qmake
$ make
```

Build `eatem-server` and then use the LD_PRELOAD to point directly to your patched WebChannel library rather than the system version.

```bash
$ LD_PRELOAD=/absolute/path/here/qtwebchannel/lib/libQt5WebChannel.so.5 ./server
```
