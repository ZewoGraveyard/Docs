# Getting started

**Zewo** is a set of libraries aimed at server side development. With **Zewo** you can write your web app, REST API, command line tool, database driver, etc. Our goal is to create an ecosystem around the modules and tools we provide so you can focus on developing your application or library, instead of doing everything from scratch.

## Installation

Before we start we need to install the approriate **Swift** binaries and **Zewo** dependencies.

### Install Swift

 **Zewo 0.2** requires February 8, 2016 Swift Development Snapshot.

#### OS X

Download and install Xcode 7.3 or greater.

- [Xcode Download](https://developer.apple.com/xcode/download/)

Download the Swift Development Snapshot and optionally the Debugging Symbols.

- [Swift Development Snapshot](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx.pkg)
- [Debugging Symbols (Optional)](https://swift.org/builds/development/xcode/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-osx-symbols.pkg)

After installing add the swift toolchain to your path.

```sh
export PATH=/Library/Developer/Toolchains/swift-latest.xctoolchain/usr/bin:"${PATH}"
```

If you're using **Xcode** you can choose the appropriate toolchain from `Preferences > Componentes > Toolchains`. 
 
#### Linux 
 
On linux you have to install swift dependencies.

```sh
sudo apt-get install clang libicu-dev
``` 

Download the Swift Development Snapshot
 
##### Ubuntu 15.10

- [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1510/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu15.10.tar.gz)

##### Ubuntu 14.04

 - [Swift Development Snapshot](https://swift.org/builds/development/ubuntu1404/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a-ubuntu14.04.tar.gz)

After the download extract the archive. This creates a `usr/` directory in the location of the archive.

```sh
tar xzf swift-<VERSION>-<PLATFORM>.tar.gz
```

Add the Swift toolchain to your path.

```sh
export PATH=/path/to/usr/bin:"${PATH}"
```

### Install Zewo

After installing Swift we need to install Zewo's dependencies.

#### OS X
```sh
brew tap zewo/tap
brew install zewo
```

#### Linux
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

### Do your magic

Open `main.swift` and make it look like this:

```swift
import HTTPServer
import Router

let router = Router { route in
    route.get("/hello") { _ in
        return Response(body: "hello world")
    }
}

try Server(responder: router).start()
```

This will create an HTTP server and router which will route `/hello` to a responder that responds with `"hello world"`.

### Build and run

Now let's build the app.

```sh
swift build
```

After it compiles, run it.

```sh
.build/debug/hello
```

Now open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` in your browser's window 😊.

## Using Xcode for development

Using Xcode for development can dramatically improve your productivity. For this reason we developed a tool called [zewo-dev](https://github.com/Zewo/zewo-dev) to helps us.

### Create App's Xcode project

First, let's configure an Xcode project for you app. Create a directory for Xcode in your app's root directory.

```sh
mkdir Xcode && cd Xcode
```
 
Install [Alcatraz](https://github.com/supermarin/Alcatraz) if you haven't already.

```sh
curl -fsSL https://raw.github.com/alcatraz/Alcatraz/master/Scripts/install.sh | sh
```

Look for **Swift Command Line Application** under Templates in Alcatraz and install it. Restart Xcode and go to `File > New > Projects` and choose **Swift Command Line Application**. Save it on the `Xcode` directory you just created.

Remove the `main.swift` file that was generated and add the `Sources` directory from your app's root directory.

### Install zewo-dev

This tool will clone all repos from Zewo and generate Xcode projects for them.

```sh
gem install zewo-dev
```


Inside the Xcode directory create a directory for Zewo's Xcode projects.

```sh
mkdir Zewo && cd Zewo
```

Pull the repos and generate Xcode projects.

```sh
zewodev init && zewodev make_projects
```

### Add Zewo subprojects

With your app's Xcode project opened, drag and drop the required Xcode projects from Zewo to your project. In our example we should bring `HTTPServer.xcodeproj` and `Router.xcodeproj`.

Go to your app's target `Build Phases > Target Dependencies` and add `HTTPServer` and `Router` frameworks.

Now build and run as usual. After this you can open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` again, but now running from Xcode 😎.