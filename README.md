# Getting started

**Zewo** is a set of libraries aimed at server side development. With **Zewo** you can write your web app, REST API, command line tool, database driver, etc. Our goal is to create an ecosystem around the modules and tools we provide so you can focus on developing your application or library, instead of doing everything from scratch.

## Installation

Before we start we need to install the appropriate **Swift** binaries and **Zewo** dependencies.

### OS X

#### Install Xcode

Download and install **Xcode 7.3** or greater.

- [Xcode Download](https://developer.apple.com/xcode/download/)

#### Install Swift

**Zewo 0.2** requires February 8, 2016 **Swift Development Snapshot**.

- [Swift Development Snapshot](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx.pkg)
- [Debugging Symbols (Optional)](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx-symbols.pkg)

After installing add the swift toolchain to your path, so you can build swift from the command line.

```sh
export PATH=/Library/Developer/Toolchains/swift-latest.xctoolchain/usr/bin:"${PATH}"
```

On **Xcode** you can choose the appropriate toolchain from `Preferences > Componentes > Toolchains`.

#### Install Zewo

After installing Swift we need to install Zewo's dependencies.

```sh
brew tap zewo/tap
brew install zewo
```


This will install our current dependencies:

- [libvenice](https://github.com/Zewo/libvenice)
- [http_parser](https://github.com/Zewo/http_parser)
- [uri_parser](https://github.com/Zewo/uri_parser)
- [openssl](https://www.openssl.org/)


### Linux

On **Linux** we provide a shell script that automates the whole installation process.

#### Ubuntu 15.10

```sh
wget https://raw.github.com/Zewo/Zewo/master/Scripts/install-zewo0.2.3-ubuntu15.10.sh -O - | sh
```

#### Ubuntu 14.04

```sh
wget https://raw.github.com/Zewo/Zewo/master/Scripts/install-zewo0.2.3-ubuntu14.04.sh -O - | sh
```

You can also install everything manually.

### Install Swift

Install swift dependencies.

```sh
sudo apt-get install clang libicu-dev
```

Download the Swift Development Snapshot

#### Ubuntu 15.10

- [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1510/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu15.10.tar.gz)

#### Ubuntu 14.04

 - [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1404/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu14.04.tar.gz)

Extract the archive. This creates a `usr` directory in the location of the archive.

```sh
tar xzf swift-<VERSION>-<PLATFORM>.tar.gz
```

Add the Swift toolchain to your path.

```sh
export PATH=/path/to/usr/bin:"${PATH}"
```

#### Install Zewo

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

## Hello World Web App

To showcase what **Zewo** can do we'll create a hello world web app.

### Configure your project

First we need to create a directory for our app.

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

Open `Package.swift` with your favorite editor and add `HTTPServer`, `Router` and `LogMiddleware` as dependencies.

```swift
import PackageDescription

let package = Package(
    name: "hello",
    dependencies: [
        .Package(url: "https://github.com/Zewo/HTTPServer.git", majorVersion: 0, minor: 2),
        .Package(url: "https://github.com/Zewo/Router.git", majorVersion: 0, minor: 2),
        .Package(url: "https://github.com/Zewo/LogMiddleware.git", majorVersion: 0, minor: 2)
    ]
)
```

### Do your magic

Open `main.swift` and make it look like this:

```swift
import HTTPServer
import Router
import LogMiddleware

let log = Log()
let logger = LogMiddleware(log: log)

let router = Router { route in
    route.get("/hello") { _ in
        return Response(body: "hello world")
    }
}

try Server(middleware: logger, responder: router).start()
```

This code:

- Creates an HTTP server that listens on port `8080` by default.
- Configures a router which will route `/hello` to a responder that responds with `"hello world"`.
- Mounts a logger middleware on the server that will log every request/response pair to the standard error stream (stderr) by default.

### Build and run

Now let's build the app.

```sh
swift build
```

After it compiles, run it.

```sh
.build/debug/hello
```

Now open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` in your browser's window. 😊

## Next steps

Now that you now how to do your stuff mannualy you can make your life easier.

- [Developing with Xcode](./Xcode.md)
- [Developing with Docker](./Docker.md)
