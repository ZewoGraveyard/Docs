## Developing with Xcode

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

Look for **Swift Command Line Application** under Templates in Alcatraz and install it.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/SwiftCommandLineApplicationAlcatraz.png)

##### Configuring Xcode toolchain
You can use any version of Xcode, but you need to launch it with the correct toolchain. Right now it's `swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a`.

In Xcode 7.3, you can easily switch between toolchains with `Preferences > Components > Toolchains`.

If you're using Xcode 7.2, you have to launch Xcode from the command line.
```sh
xcrun launch-with-toolchain /Library/Developer/Toolchains/swift-DEVELOPMENT-SNAPSHOT-2016-02-08-a.xctoolchain/
```

Once you have restarted Xcode, go to `File > New > Projects` and choose **Swift Command Line Application**. Save the project on the `Xcode` directory you just created.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/SwiftCommandLineApplicationProject.png)

Remove the `main.swift` file that was generated and add the `Sources` directory from your app's root directory.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/HelloMainXcode.png)

### Install zewo-dev

This tool will clone all repos from Zewo and generate Xcode projects for them.

```sh
gem install zewo-dev
```

Inside the Xcode directory create a directory for Zewo's Xcode projects.

```sh
mkdir Zewo && cd Zewo
```

Pull the repos and generate Xcode projects. We're using `0.2` and `0.3` versions of Zewo libraries because they work with Swift `DEVELOPMENT-SNAPSHOT-2016-02-08-a` version.

```sh
zewodev init && zewodev checkout --tag 0.2 && zewodev checkout --tag 0.3 && zewodev make_projects
```

### Add Zewo subprojects

With your app's Xcode project opened, drag and drop the required Xcode projects from Zewo to your project. In our example we should bring `HTTPServer.xcodeproj`, `Router.xcodeproj` and `LogMiddleware.xcodeproj`.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/AddXcodeSubprojects.gif)

Go to your app's target `Build Phases > Target Dependencies` and add `HTTPServer`, `Router` and `LogMiddleware` frameworks.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/AddBuildPhaseDependencies.gif)

Now build and run as usual. After this you can open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` again, but now running from Xcode. 😎

### Troubleshooting

If build fails because Xcode cannot find `http_parser.h` in path `/usr/local/include/http_parser/http_parser.h`, it means that you've already installed http-parser from source or from standalone homebrew formula. To solve the problem, you need to add link:

```sh
brew link --overwrite http_parser
```
