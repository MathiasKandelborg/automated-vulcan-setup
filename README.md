# Automated Vulcan.js setup

This repository contains all the needed instructions to get a development environment up and running on any computer or OS. The only requirements are VirtualBox and Vagrant.

This is made possible with a [virtual machine](https://en.wikipedia.org/wiki/Virtual_machine). This one contains the instructions for setting up and downloading the required software for a setting up a development environment for a [Vulcan.js](http://vulcanjs.org/) project.

## Getting started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Make sure [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/downloads.html) are installed. If they aren't installed yet, it's quite easy to get done by going to their websites and following the instructions for your OS.

- 6GB of RAM - This is due to the needs of the development server.

### Installing

Open a terminal and make a new project folder, then download this repository:

```bash
mkdir vulcan-project && cd vulcan-project
git clone https://github.com/MathiasKandelborg/automated-vulcan-setup.git .
```

Now it's time to setup the VM. This generally takes some time as you computer is downloading, installing _and running_ an entire OS, in your current OS.

```bash
vagrant up
```

When the installation processes are done, proceed to access the newly created VM with this command:

```bash
vagrant ssh
```

You are now in an Ubuntu v18.04 env with all the required software installed for running a Vulcan.js project.

Run the following commands right after `vagrant ssh`:

> Press (y) on all choices for the fastest installation of Vulcan.js

```bash
cd app
./scripts/download-vulcan.sh
```

This takes some time as we're now downloading the Vulcan Core & Starter repositories and are running `npm install` in both.

Just one last thing before we start our development server: Since this is a 'clean' install, we need to make sure the Vulcan Core packages are used. We do this by defining an ENV variable in our projects start script. Just run the following commands and everything will be ready!

```bash
cd Starter
sed -i -e '/^    "start": "meteor --settings settings.json",/s/^.*$/    "start": "METEOR_PACKAGE_DIRS=\\\"\/home\/vagrant\/app\/Core\/packages\\\" meteor --settings settings.json",/' package.json
```

Start the development server

```bash
npm start
```

When it's ready, your dev environment is all set up and `localhost:3000` is available and showing the current state of your project.

### Development

> If you've never tried Vulcan.js, it is recommended to follow the built-in tutorials to get a grip of how things work. After starting the project with `npm install`, you can simply go to `localhost:3000` and start following along.

You can access your application from the `app` folder on your computer. In here you can make changes to files, save them and it will get synced to the VM, which will reload your application if the server is running.

#### Stopping the dev server and VM

In order to stop the VM while saving the setup:

- Press CTRL+C to cancel the `npm start` command
- Write `exit` until you are in your own terminal
- Run `vagrant halt`

If you aren't inside the VM  (`vagrant ssh`) in the terminal, you can simply run `vagrant halt` in the project folder.

#### Starting the VM & development server again

- Go to the root of the project folder

```bash
vagrant up
vagrant ssh
cd app/Starter && npm start
```

___

## Author

**Mathias Wøbbe** - *Initial work* - [MathiasKandelborg](https://github.com/MathiasKandelborg)
