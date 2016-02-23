# Getting started

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

## Hello World Web App

**Zewo** is *not* a web framework, it is much more. **Zewo** is a set of libraries for general server side development. With **Zewo** you can write your web app, REST API, command line tool, etc. Although we already provide enough, you can even develop an opinionated higher-level web framework on top of it.

To showcase what **Zewo** can do we'll create a hello world web app.

### Configuring your project

First we need to create a directory for your app.

```sh
mkdir myapp && cd myapp
```

Then we initialize the project with Swift Package Manager (SPM).

```sh
swift build --init
```

This command will create the basic structure for our app.

````
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
    name: "myapp",
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
.build/debug/myapp
```

Now open your favorite browser and go to `localhost:8080/hello`. You should see the word `hello` in your browser's window.

