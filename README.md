# Getting started

**Zewo** is *not* a web framework, it's much more. **Zewo** is a set of libraries aimed at server side development. With **Zewo** you can write your web app, REST API, command line tool, etc. Although we already provide enough you could, for example, develop your own opinionated higher-level web framework on top of zewo modules.

## Installation

Before we start we need to install **Zewo**.

### OS X
```sh
brew tap zewo/tap
brew install zewo
```

### Linux
```sh
echo "deb [trusted=yes] http://apt.zewo.io/deb ./" | sudo tee --append /etc/apt/sources.list
sudo apt-get update
sudo apt-get install zewo
```

This will install our current dependencies:

- [libvenice](https://github.com/Zewo/libvenice)
- [http_parser](https://github.com/Zewo/http_parser)
- [uri_parser](https://github.com/Zewo/uri_parser)
- [openssl](https://www.openssl.org/)

**Zewo 0.2** is compatible with February 8, 2016 Swift Development Snapshot.

- OS X
 - [Swift Development Snapshot](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx.pkg)
 - [Debugging Symbols](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx-symbols.pkg)
- Ubuntu 15.10
 - [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1510/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu15.10.tar.gz)
 - [Signature](https://swift.org/builds/development/ubuntu1510/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu15.10.tar.gz.sig)
- Ubuntu 14.04
 - [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1404/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu14.04.tar.gz)
 - [Signature](https://swift.org/builds/development/ubuntu1404/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu14.04.tar.gz.sig) 

## Hello World Web App

To showcase what **Zewo** can do we'll create a hello world web app.

### Configuring your project

First we need to create a directory for your app.

```sh
mkdir hello && cd hello
```

Then we initialize the project with Swift Package Manager (SPM).

```sh
swift build --init
```

This command will create the basic structure for our app.

```
.
├── Package.swift
├── Sources
│   └── main.swift
└── Tests
```

Open `Package.swift` with your favorite editor and add `HTTPServer` and `Router` as a dependency.

```swift
import PackageDescription

let package = Package(
    name: "hello",
    dependencies: [
        .Package(url: "https://github.com/Zewo/HTTPServer.git", majorVersion: 0, minor: 2),
        .Package(url: "https://github.com/Zewo/Router.git", majorVersion: 0, minor: 2)
    ]
)
```

Now open `main.swift` and make it look like this:

```swift
import HTTPServer
import Router

let router = Router { route in
    route.get("/hello") { _ in
        return Response(body: "hello")
    }
}

try Server(responder: router).start()
```

This will create an HTTP server and router which will route `/hello` to a responder that responds with `"hello"`.

Now let's build the app.

```sh
swift build
```

After it compiles let's run it.

```sh
.build/debug/hello
```

Now open your favorite browser and go to `localhost:8080/hello`. You should see the word `hello` in your browser's window.

