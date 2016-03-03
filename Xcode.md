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

Restart Xcode and go to `File > New > Projects` and choose **Swift Command Line Application**. Save the project on the `Xcode` directory you just created.

![New Project](https://raw.githubusercontent.com/Zewo/Docs/master/Images/SwiftCommandLineApplicationProject.png)

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

Now build and run as usual. After this you can open your favorite browser and go to `localhost:8080/hello`. You should see `hello world` again, but now running from Xcode. 😎
