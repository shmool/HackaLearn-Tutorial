---
description: Set up your Angular environment and create your app
---

# Angular App

## Angular for beginners tutorial

To get started with Angular and understand the basic concepts, I recommend the free [ngGirls To-do-List tutorial](https://ng-girls.gitbook.io/todo-list-tutorial/). It covers components, template syntax, inputs, outputs, and services, not only telling what and how, but why. 

In this section you'll learn how to set up a starter Angular app.

## Angular CLI

The [Angular CLI](https://cli.angular.io) is a powerful tool that simplifies a lot of the development process. It also installs libraries you'll use in your current and future projects.

There are two options for using the Angular CLI:

1. Install it globally on your computer
2. Create a project without installing it by running: `npx @angular/cli@latest new HackaLearn`. .

We'll cover the first option here. If you're familiar with npx, feel free to use it.

## Install the Angular CLI

Check whether you already have the Angular CLI installed, and whether it's [the latest version](https://github.com/angular/angular-cli/releases).

```text
ng v
```

If the command `ng` is not known, it's not installed on your computer.

If it is, and the version is less than the latest, uninstall it and verify the cache.

```text
npm uninstall -g @angular/cli
npm cache verify
```

Use NPM to download and install the Angular CLI library:

```text
npm i -g @angular/cli
```

Go to your projects folder and create a new Angular project:

```text
ng new HackaLearn
```

You will ne

With a relatively new feature of NPM, you don't need to install the Angular CLI on your computer to create a project. The command `npx` knows where to find the Angular-CLI package by its name `@angular/cli` . It will download the package \(if you don't already have it installed\) and run its command `new` .

> Even if you have Angular-CLI installed from a previous project you were working on, we'll tell npx to use the latest version. So if your installed version is an old one, you'll still get a project created with the newest version.

First, create a folder to store all your projects, for example _myProjects_, and then go into the folder, using the command line:

{% code title="command-line" %}
```text
cd the-path-to-your-folder/myProjects
```
{% endcode %}

Now, create an Angular project by running:

```text
npx @angular/cli@latest new todo-list
```

Angular CLI will ask a couple of questions to help create a new application. Answer the questions as shown below:

1. Do you want to enforce stricter type checking and stricter bundle budgets in the workspace? \(y/N\): **N**
2. Would you like to add Angular routing? \(y/N\): **N** 
3. Which stylesheet format would you like to use? \(Use arrow keys\): Select **SCSS**

This can take a while, since many packages are being downloaded from the web and installed.

_**If, for any reason the command `npx` doesn't work, follow the**_[ _**instructions in the bottom of this page**_]()_**, and then come back here to run your project.**_

Read more about the Angular CLI in the following section.

### Running your Project

Enter the new folder that the Angular-CLI created for this project:

{% code title="command-line" %}
```text
cd todo-list
```
{% endcode %}

Once inside the folder of the application, run the application by using the following command:

{% code title="command-line" %}
```bash
ng serve -o
```
{% endcode %}

`ng` is the command that runs the local version of Angular-CLI that's installed in your project. We will use this command to create new components, build the project, and more.

The flag `-o` is a short for `--open`, which will open your browser in the right URL: [`localhost:4200`](http://localhost:4200)

You should see the page like this:

## Congratulations!

You have a running Angular application! **Keep the terminal where you ran the `ng serve` command open as you're working on the application.** Changes you make to the project code is immediately reflected in the web browser.  
You can open another terminal to perform tasks in parallel.

To stop the app from running, press `Ctrl+C` in the terminal, or close the terminal.

Now we're ready to start developing!

{% hint style="success" %}
[See the results on StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/0_01-installations)
{% endhint %}

## 

