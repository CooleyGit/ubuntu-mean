ubuntu-mean
===========

Basic setup notes for mean stack install on AWS Ubuntu 14.04. I am assuming you have AWS account and a pem file somewhere on your local. Launch new EC2 instance on AWS you can use the default AWS Ubuntu 14.04 server all settings can be default except security group. 

####Security group:
*(I use these basic settings to get started. You should be using your computer ip for security otherwise anyone can hit your server)*
```
* SSH            TCP     22     <ip>
* HTTP           TCP     80     <ip>
* All traffic    All     All    <ip>
``` 

####Install Node and npm 
*Note: This is installed from apt-get so it may not be the latest version alternative install with ppa (chris lea repo) to get a more uptodate version*
```
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
```
####Create a symlink in your path to use the `node` comand
*Note: If you install using nvm you dont need to do this*
```
sudo ln -s `which nodejs` /usr/local/bin/node
```

####Install mongodb
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
sudo apt-get install mongodb-org
```

####Install Express
```
sudo npm install -g express
```

>Main install done


##Get project running on server 
*Note: A good Yeoman project to start with is [DaftMonk/generator-angular-fullstack](https://github.com/DaftMonk/generator-angular-fullstack)*

####SCP your project to the ubuntu directory 
*Note: replace <server ip> with your ip, you should be running this from your local*
```
scp -i ~/.ssh/your-pem-file.pem -r ~/local-project-path ubuntu@<server ip>:/home/ubuntu
```

####Run npm in your project root 
```
sudo npm install
```

##Start the server with `node` comand 
*Note: this will only run while your terminal session is open, use pm2 to keep server running*
```
cd path/to/server/file
node app.js
```

##PM2 options

####Install PM2 
*Note: pm2 will allow you to keep your server running and create clusters*
```
sudo npm install -g pm2
```

####Start PM2 
*Note: The below example will start 4 clusters*
```
sudo pm2 start <server file> -i 4
```

####Other pm2 options
```
sudo pm2 stop <server file>
sudo pm2 restart <server file>
sudo pm2 delete <server file>
```

####Different ways to launch a PM2 process 
*Note: More options @ [https://www.npmjs.org/package/pm2](https://www.npmjs.org/package/pm2)*
```
pm2 start app.js -i max  # Will start maximum processes depending on available CPUs
pm2 start app.js -i 3    # Will start 3 processes
pm2 start app.js -i max -- -a 23  # Pass arguments after -- to app.js
```



