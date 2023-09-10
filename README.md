# `server` 🖥️

> This is the central backbone of our project, taking care of all the active users & vehicles on a daily basis!

## Table Of Contents
* [What's this?](#whats-this)
   * [Role in the stack](#role-in-the-stack)
   * [Architectural Overview](#architectural-overview)
* [Setup Guide](#setup-guide)
   * [Prerequisites](#prerequisites)
   * [Build From Source](#build-from-source)
   * [Installation Instructions](#installation-instructions)

## What's this?
In order for the core functionalities to work, there should be a central messaging platform where users & vehicles can connect to and communicate with each other, in a secure yet performant way. This server is the means for doing so.

### Role in the stack
This server is the backbone of the system. It has the following core functionalities & duties in the stack as a whole:
* Act as a central messaging platform for users & vehicles
* Provide a central storage mechanism for storing all user & vehicle data including logs in an organized manner
* Expose an abstracted endpoint set for easy front end development

### Architectural Overview
This is written from the high level system architecture shown below. You can find some pointers below highlighting the core idea in a nutshell. The [routes](#routes) & [messaging](#messaging) sections may not even make sense to you if you don't have an understanding of what's going on. Feel free to open a new issue if you find any part of this documentation confusing or hard to understand.

<img width="921" alt="241353715-3eb63d26-cace-4e03-8e61-8d79be6b2043" src="https://github.com/Tecathlon-STIST/server/assets/109507621/fb582df6-fb01-436f-b617-94c681362767">

*In a nutshell...*
  * Each vehicle can register itself to the server & get a corresponding `vid`. It can then create & host a room for itself in the server, which will be identified by this `vid`. The vehicle will be in control of that room.
  * Users can signup their accounts and pair them to multiple vehicles. They can then join any of the rooms hosted by a paired vehicle. Users can request vehicles to perform certain actions but cannot enforce or command the same.
  * Any messages being sent over the room can be seen by the server itself. However, messages from one room cannot & should not leak into or be accessible from another as that would be a security issue.

## Setup Guide
You can follow this guide to run the server on a machine of your choice. If you want to run the server, install all the prerequisites except the first one & skip to the [installation instructions](#installation-instrcutions). Make sure you're running on a Linux OS, preferably [Ubuntu](https://ubuntu.com/) If you wanna develop or build from source, continue below.
### Prerequisites
* The Rust toolchain, including cargo: Install from [here](https://www.rust-lang.org/tools/install) by downloading the `rustup-init` executable for your platform. Alternatively, download & run the standalone installer for your platform from the links provided [here](https://forge.rust-lang.org/infra/other-installation-methods.html#standalone-installers).
* Git CLI: Install by running the executable for your platform available [here](https://git-scm.com/downloads).
* MongoDB Community Server: After running the installer found [here](https://www.mongodb.com/try/download/community), make sure that the server is up and running on port **27017**. 

    > **Note**
    > 27017 is of course the default port that it'd be running on. If you somehow end up running it on a different port, make sure to update it in the code.
### Build From Source
After making sure that all prerequisites are satisfied, follow the steps one by one to build and run the code.
1. Either clone this repo

    ```
    git clone https://github.com/Tecathlon-STIST/server.git
    cd server
    ```
   or make a new directory and pull the code
  
    ```
    mkdir server && cd server
    git init
    git remote add origin https://github.com/Tecathlon-STIST/server.git
    git pull origin main
    ```
2. Start the API server

    ```
    cargo run
    ```
  
The server will now be served on port **7878**, which you can view by visiting [localhost:7878](http://localhost:7878) in your browser. A simple HTML page with a logo can be seen. That's it, happy hacking! :beers:
  
### Installation Instructions
These instructions define how you can run a production server on port 7878. Make sure you have a Linux x86 OS installed.
1. Clone this repository and change working directory
  
    ```
    git clone https://github.com/Tecathlon-STIST/server.git
    cd server/
    ```
2. Switch to the `build` branch
  
    ```
    git fetch origin
    git checkout build
    ```
3. Run the binary directly
  
    ```
    ./release/server
    ```

You can keep the server running using the `screen` utility. [Here](https://linuxize.com/post/how-to-use-linux-screen/) is a beginner friendly guide for getting started. You can then link your domain name (if you have one) and route the connection using [Nginx](https://www.nginx.com/) for deploying this to the cloud. If you find anything missing or wrong in this documentation, make sure to open an issue, we're happy to help or correct ourselves! 🖤
