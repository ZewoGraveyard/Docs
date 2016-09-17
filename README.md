# Getting started

## Install Swiftenv

[Swiftenv](https://github.com/kylef/swiftenv) allows you to easily install, and switch between multiple versions of Swift. You can install swiftenv following official [instructions](https://github.com/kylef/swiftenv#installation).

⚠️ With **homebrew** use `brew install kylef/formulae/swiftenv --HEAD`.

## Install Swift 3.0 Release

Once you have it, install the Swift 3.0 Release

```sh
swiftenv install 3.0
```

## Create your first Zewo web application

First we need to create a directory for our app.

```sh
mkdir hello && cd hello
```

Now we select Swift 3.0 Release with Swiftenv and initialize the project with the Swift Package Manager (**SwiftPM**).

```sh
swiftenv local 3.0
swift package init --type executable
```

This command will create the basic structure for our app.

```
.
├── Package.swift
├── Sources
│   └── main.swift
└── Tests
```

Open `Package.swift` with your favorite editor and add `HTTPServer` as a dependency.

```swift
import PackageDescription

let package = Package(
    name: "hello",
    dependencies: [
        .Package(url: "https://github.com/VeniceX/HTTPServer.git", majorVersion: 0, minor: 13),
    ]
)
```

## Do your magic

Open `main.swift` and make it look like this:

```swift
import HTTPServer

let router = BasicRouter { route in
    route.get("/hello") { request in
        return Response(body: "Hello, world!")
    }
}

let server = try Server(configuration: ["port": 8080], responder: router)
try server.start()
```

This code:

- Imports the `HTTPServer` module
- Creates a `BasicRouter`
- Configures a route matching any `Request` with **GET** as the HTTP method and **/hello** as the path.
- Returns a `Response` with `"Hello, world!"` as the body for requests matching the route.
- Creates an HTTP server that listens on port `8080`.
- Starts the server.

## Build and run
Now let's build the app.

```sh
swift build
```

After it compiles, run it.

```sh
.build/debug/hello
```

![Terminal Server](https://github.com/Zewo/Zewo/raw/master/Images/Terminal-server.png)

Now open your favorite browser and go to [http://localhost:8080/hello](http://localhost:8080/hello). You should see **Hello, world!** in your browser's window. 😊

![Safari Hello](https://github.com/Zewo/Zewo/raw/master/Images/Safari-hello.png)

By default the server will log the requests/responses.

![Terminal Log](https://github.com/Zewo/Zewo/raw/master/Images/Terminal-log.png)

Press `control + c` to stop the server.

## Xcode

Using an IDE can be a huge boost to productivity. Luckily, **SwiftPM** has Xcode project generation support built in.

To generate your Zewo Xcode project simply run:

```sh
swift package generate-xcodeproj
```

Open your Xcode project by double clicking it on Finder or with:

```sh
open hello.xcodeproj
```

To run the application select the command line application scheme `hello` on Xcode.

![Xcode Scheme](https://github.com/Zewo/Zewo/raw/master/Images/Xcode-scheme.png)

Now click the run button ► or use the shortcut `⌘R`. You should see the server running directly from your Xcode.

![Xcode Console](https://github.com/Zewo/Zewo/raw/master/Images/Xcode-console.png)

You can set breakpoints in your code and debug it as usual.

![Xcode Debug](https://github.com/Zewo/Zewo/raw/master/Images/Xcode-debug.png)

To stop the server just click the stop button ■ or use the shortcut `⌘.`.

## What's next?

Check out our [organization](https://github.com/Zewo) for more. You can also take a look at our [documentation](http://zewo.readme.io). If you have any doubts you can reach us at our [slack](http://slack.zewo.io). We're very active and always ready to help.