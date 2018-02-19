# Dev Virtual Machine for Data Science
## Installation
### Requirements
You will need to install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and then [Vagrant](https://www.vagrantup.com/docs/installation/).
### Manual
Once it is done, you will be able to run the command `vagrant up dev` in this folder to start the installation of the box.
To connect to the machine the, run `vagrant ssh dev` from the same directory.
### Current actions
The machine installs for now :
* Python(latest 2.7) with the packages `virtualenv` and `virtualenvwrapper`.
* Docker.
* Deploy a `mongodb` docker container on port `27017`.
* Jupyter server running on port `8888`
