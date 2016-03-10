# Getting started

**Zewo** is a set of libraries for server side development. With **Zewo** you can write your web app, REST API, command line tool, database driver, etc. Our goal is to create an ecosystem around the modules and tools we provide so you can focus on developing your application or library, instead of doing everything from scratch.

Currently, we have around 50+ packages. This list grows very fast so it might be outdated. To be sure just check our GitHub [organization](https://github.com/Zewo).

## Zewo Packages

- [Base64](https://github.com/Zewo/Base64)
- [BasicAuthMiddleware](https://github.com/Zewo/BasicAuthMiddleware)
- [ChannelStream](https://github.com/Zewo/ChannelStream)
- [CHTTPParser](https://github.com/Zewo/CHTTPParser)
- [CLibpq](https://github.com/Zewo/CLibpq)
- [CLibpq-OSX](https://github.com/Zewo/CLibpq-OSX)
- [CLibvenice](https://github.com/Zewo/CLibvenice)
- [CMySQL](https://github.com/Zewo/CMySQL)
- [CMySQL-OSX](https://github.com/Zewo/CMySQL-OSX)
- [ContentNegotiationMiddleware](https://github.com/Zewo/ContentNegotiationMiddleware)
- [COpenSSL](https://github.com/Zewo/COpenSSL)
- [COpenSSL-OSX](https://github.com/Zewo/COpenSSL-OSX)
- [CURIParser](https://github.com/Zewo/CURIParser)
- [CZeroMQ](https://github.com/Zewo/CZeroMQ)
- [Data](https://github.com/Zewo/Data)
- [Event](https://github.com/Zewo/Event)
- [File](https://github.com/Zewo/File)
- [HTTP](https://github.com/Zewo/HTTP)
- [http_parser](https://github.com/Zewo/http_parser)
- [HTTPClient](https://github.com/Zewo/HTTPClient)
- [HTTPFile](https://github.com/Zewo/HTTPFile)
- [HTTPSClient](https://github.com/Zewo/HTTPSClient)
- [HTTPSServer](https://github.com/Zewo/HTTPSServer)
- [InterchangeData](https://github.com/Zewo/InterchangeData)
- [IP](https://github.com/Zewo/IP)
- [JSON](https://github.com/Zewo/JSON)
- [JSONMediaType](https://github.com/Zewo/JSONMediaType)
- [libvenice](https://github.com/Zewo/libvenice)
- [Log](https://github.com/Zewo/Log)
- [LogMiddleware](https://github.com/Zewo/LogMiddleware)
- [MediaType](https://github.com/Zewo/MediaType)
- [Mustache](https://github.com/Zewo/Mustache)
- [MySQL](https://github.com/Zewo/MySQL)
- [OpenSSL](https://github.com/Zewo/OpenSSL)
- [POSIXRegex](https://github.com/Zewo/POSIXRegex)
- [PostgreSQL](https://github.com/Zewo/PostgreSQL)
- [RegexRouteMatcher](https://github.com/Zewo/RegexRouteMatcher)
- [Router](https://github.com/Zewo/Router)
- [Sideburns](https://github.com/Zewo/Sideburns)
- [SQL](https://github.com/Zewo/SQL)
- [Stream](https://github.com/Zewo/Stream)
- [String](https://github.com/Zewo/String)
- [System](https://github.com/Zewo/System)
- [TCP](https://github.com/Zewo/TCP)
- [TCPSSL](https://github.com/Zewo/TCPSSL)
- [TrieRouteMatcher](https://github.com/Zewo/TrieRouteMatcher)
- [UDP](https://github.com/Zewo/UDP)
- [URI](https://github.com/Zewo/URI)
- [uri_parser](https://github.com/Zewo/uri_parser)
- [URLEncodedForm](https://github.com/Zewo/URLEncodedForm)
- [Venice](https://github.com/Zewo/Venice)
- [WebSocket](https://github.com/Zewo/WebSocket)
- [Zewo](https://github.com/Zewo/Zewo)

## External Packages

- [Swift-Redis](https://github.com/rabc/Swift-Redis/)
- [MiniRouter](https://github.com/paulofaria/MiniRouter)

## Installation

Before we start we need to install some tools and dependencies. If you already installed just skip them.

## OS X

### Install Xcode 7.3+

[Xcode](https://developer.apple.com/xcode/) is apple's software development IDE.

- [Xcode Download](https://developer.apple.com/xcode/download/)

### Install Homebrew

[Homebrew](http://brew.sh/) is a package manager for OS X.

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Install Swiftenv

[Swiftenv](https://github.com/kylef/swiftenv) is a version manager for Swift.

```sh
brew install kylef/formulae/swiftenv
```

After installing you need to configure your shell.

**Bash**

```sh
echo 'if which swiftenv > /dev/null; then eval "$(swiftenv init -)"; fi' >> ~/.bash_profile
```
> On some platforms, you may need to modify ~/.bashrc instead of ~/.bash_profile.

**ZSH**

```sh
echo 'if which swiftenv > /dev/null; then eval "$(swiftenv init -)"; fi' >> ~/.zshrc
```

**Fish**

```sh
echo 'status --is-interactive; and . (swiftenv init -|psub)' >> ~/.config/fish/config.fish
```

### Install Zewo

This brew formula installs all **Zewo** dependencies.

```sh
brew install zewo/tap/zewo
```

## Linux

### Install Clang and ICU

```sh
sudo apt-get install clang libicu-dev
```

### Install Swiftenv

[Swiftenv](https://github.com/kylef/swiftenv) is a version manager for Swift.

```sh
git clone https://github.com/kylef/swiftenv.git ~/.swiftenv
```

After installing you need to configure your shell.

**Bash**

```sh
echo 'export SWIFTENV_ROOT="$HOME/.swiftenv"' >> ~/.bashrc
echo 'export PATH="$SWIFTENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(swiftenv init -)"' >> ~/.bashrc
```
> On some platforms, you may need to modify ~/.bash_profile instead of ~/.bashrc.

**ZSH**

```sh
echo 'export SWIFTENV_ROOT="$HOME/.swiftenv"' >> ~/.zshenv
echo 'export PATH="$SWIFTENV_ROOT/bin:$PATH"' >> ~/.zshenv
echo 'eval "$(swiftenv init -)"' >> ~/.zshenv
```

**Fish**

```sh
echo 'setenv SWIFTENV_ROOT "$HOME/.swiftenv"' >> ~/.config/fish/config.fish
echo 'setenv PATH "$SWIFTENV_ROOT/bin" $PATH' >> ~/.config/fish/config.fish
echo 'status --is-interactive; and . (swiftenv init -|psub)' >> ~/.config/fish/config.fish
```

Restart your shell so the changes take effect.

### Install Zewo

```sh
echo "deb [trusted=yes] http://apt.zewo.io/deb ./" | sudo tee --append /etc/apt/sources.list
sudo apt-get update
sudo apt-get install zewo
```

## Hello World Web App

To showcase what **Zewo** can do we'll create a hello world web app.

### Configure your project

First we need to create a directory for our app.

```sh
mkdir hello && cd hello
```

Then we install Swift Development Snapshot from **February 8, 2016**.

```sh
swiftenv install DEVELOPMENT-SNAPSHOT-2016-02-08-a
swiftenv local DEVELOPMENT-SNAPSHOT-2016-02-08-a
```

Now we initialize the project with Swift Package Manager (**SPM**).

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
        .Package(url: "https://github.com/Zewo/HTTPServer.git", majorVersion: 0, minor: 3),
        .Package(url: "https://github.com/Zewo/Router.git", majorVersion: 0, minor: 3),
        .Package(url: "https://github.com/Zewo/LogMiddleware.git", majorVersion: 0, minor: 3)
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
