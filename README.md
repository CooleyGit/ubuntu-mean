ubuntu-mean
===========

#####Basic setup notes for mean stack install on AWS Ubuntu 14.04

###Install Node and npm 
*Note: This is installed from apt-get so it may not be the latest version*
```
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
```
###Create a symlink in your path to use the `node` comand
*Note: If you install using nvm you dont need to do this*
```
sudo ln -s `which nodejs` /usr/local/bin/node
```

###Install mongodb
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
sudo apt-get install mongodb-org
```

###Install Express
```
sudo npm install -g express
```

>Main install done
