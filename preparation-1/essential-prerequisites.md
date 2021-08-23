---
description: What you need to prepare before starting the tutorial
---

# Essential Prerequisites

We're going to develop and deploy a web application. There are several tools and services that will help us in our work. 

## Browser

You probably have a browser installed and are using it right now. Make sure your browser is up to date \(the modern browsers are "evergreen", meaning they update whenever you close and reopen them\) and have rich developer tools. We recommend [Microsoft Edge](https://www.microsoft.com/edge?WT.mc_id=javascript-11627-shjacobs).

## IDE

IDE is a rich text editor which heavily supports writing code. It shows you suggestions, warnings, errors and more while you type, and allows you to easily explore the code of your project and the libraries you use. 

[Visual Studio Code](https://code.visualstudio.com/?WT.mc_id=javascript-38439-shjacobs&WT.mc_id=javascript-11627-shjacobs) \(VS Code\) is a highly popular IDE. It's lightweight, extendable, open-source, and **free**. You can find many plugins to boost your productivity or just for fun, or even write your own.

## Terminal / Command Line

Most chances your operating system comes with a terminal or a command-line tool. IDEs also have a built-in terminal which is useful while you're coding. Several terminals may be opened in parallel to run different commands and tools.

## NodeJS and NPM

Web developers that work with JavaScript rely heavily on NodeJS and NPM. NodeJS lets you run applications written in JavaScript code on your computer. Many tools that help you develop your app are written in NodeJS. For instance, it is used to run local servers which serve the project files to the browser or the API functions and simulate a real running website.

NPM is installed together with NodeJS. It allows you to easily download and install different libraries from the internet and manage their versions.

[Download NodeJS](https://nodejs.org/)

If you already have NodeJS installed, make sure you check that the version matches the prerequisites by running this in your command line / terminal:

{% code title="Terminal" %}
```text
npm -v
```
{% endcode %}

\(`-v` stands for 'version'.\)

If it's lower than required, you need to be careful installing a new version, since you might have projects that rely on the version you have. Use Node Version Manager \(NVM\) to install the required version. Check this [Stack Overflow question](https://stackoverflow.com/questions/8191459/how-do-i-update-node-js) to learn how.

Once installed, you should also have NPM installed. Check its version by running:

{% code title="Terminal" %}
```text
node -v
```
{% endcode %}

## Git

Git is the world's leading version control tool, and it's essential for developers. With Git you can track your own changes and collaborate with others. It's open-source, simple, powerful, and robust. If you don't have it yet, [install Git from the official website](https://git-scm.com/) and complete the [Introduction to Git Learn Module](https://docs.microsoft.com/learn/modules/intro-to-git/?WT.mc_id=javascript-11627-shjacobs) to understand how it works. You can complete the whole [Git Learning Path](https://docs.microsoft.com/learn/paths/intro-to-vc-git/?WT.mc_id=javascript-11627-shjacobs) \(three modules\) to dig a little deeper and learn about branching, merging and collaborating.

## GitHub

GitHub is a development platform which integrates with Git. Once your project resides on GitHub as a public or a private repository, not only can you access it from different devices and collaborate with others, but you're able to use powerful tools for tracking issues and running triggered actions. Visit [GitHub](https://github.com/) to open an account and take [GitHub's no-code 10-minute tutoria](https://guides.github.com/activities/hello-world/)l to learn the basics or the [Learning Path: Manage the lifecycle of your projects on GitHub](https://docs.microsoft.com/learn/paths/manage-project-lifecycle-github/?WT.mc_id=javascript-11627-shjacobs). 

## Azure

HackaLearn involves learning and using Azure, specifically Static Web Apps and Cosmos DB. You can set up an Azure account with many services to try out for free for a year plus $200 credit for the paid ones, in addition to services that are always free. The services we'll use are always free for a specific amount of usage \(more than enough for this workshop\) either by a free tier or a Serverless plan. [Click here for more information and to open a new Azure Account with these benefits](https://azure.microsoft.com/free/open-source/?WT.mc_id=javascript-11627-shjacobs).   
At some workshops you may get an Azure Pass to help you set up an Azure account quickly. However, this pass has a limited time and value. If you'd like to keep working with Azure, it's recommended to open a regular Azure account.

## Next - create your front-end app

Choose your favorite front-end framework and create an app. In the following chapters you'll find instructions to do so. No matter which framework you choose, working with SWA, Functions and Cosmos DB will be almost the same.

