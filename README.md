Openbiz Startup
===============

What is it?
--------------------
The demo for how to start up with Openbiz framework. 
You can use it as a blank project template, and starts to build your own application based on it.
it is not a npm package, it an express based application

How to use it?
----------------------
You can clone the project and start to build and test your own module on it .

How to install (deploy)
-------------------------
You can follow below commands to install the openbiz development environment into your computer.
```sh
#clone this project as your project's root folder
git clone https://github.com/openbiz/openbiz-startup.git

#go into the project folder
cd openbiz-startup

#install openbiz environment
./install-openbiz.sh

#now its ready to run!
node app
```

Open your browser to go to [http://localhost:8080](http://localhost:8080).
if you have saw page loaded, means its running.


What's next ?
---------------------------------
Actually now you have already deployed the environment on your computer. 
You may want to do below things:
* Open your browser to register an openbiz account locally and experience the UI interactive experience.
* Try to use appbuilder to automatic generate an openbiz base application and see how cool is it. 
* if you want to discover more, welcome to follow us and join discussion.

How to update openbiz libs
---------------------------
For your own project, indeed you can use git pull to update, 
But for fetch the nightly update openbiz code we have build this script which make it easy for you.
```sh
./update-openbiz.sh
```

How to generate applications
-----------------------------
We have linked openbiz-appbuilder into your project folder.
```sh
#To check if appbuilder is executable
./appbuilder --help
```

We have some ready to use metadata for you to test.
You can follow below to generate an web app in a second.
```sh
#generate an app by using apps/demo/metadata/demo.json metadata file
./appbuilder -c apps/demo/metadata/demo.json -o ./apps/demo -a ./app.js -v -f

#After the app been generated, Don't forget to restart your express to reload it.
node app
```

For more info about how to use appbuilder please reference to openbiz-appbuilder page.

How to manual load your apps
-------------------------------
There are 2 places you should looks at, one is about backend another is fronted ,
To load your app on server side , you should append below line to your /app.js
Lets say your app is called "demo". below code will load the backend API route listen at /api/demo/*
and the frontend will be accessable via http://yourhost/apps/demo
```javascript
require('./apps/demo')(openbiz).loadAppToRoute('/api/demo')
		.loadUIToRoute('/apps/demo');
```
So far your just made the app's frontend accessable but you didn't tell openbiz to load it on user's browsers.
below code will register your app to the frontend.

Please find and open /public/website/app-init.js
```javascript
//You will see something like below, 
openbiz.loadApps(['apps/cubi'/*MORE_APPS*/],function(apps){...}
```
Now you can add your app's entry point after Cubi, 
the loading order is mattered and all openbiz's app has to load after openbiz-cubi.
```javascript
openbiz.loadApps(['apps/cubi','apps/demo'/*MORE_APPS*/],function(apps){...}
```

Folder Structures
-----------------------------
- apps/ 		---- you applications should goes here
- certs/ 		---- the cert files for HTTPS encryption
- public/ 		---- if your project need to build with website, in this folder you can put non-app stuff
- config.js 	---- all your project configurable setting should defines in this file.
- app.js 		---- the main entry point of your project
- appbuilder 	---- a shortcut for launch openbiz appbuilder
- install-openbiz.sh 	---- the installer script
- update-openbiz.sh 	---- the script for update openbiz libs
