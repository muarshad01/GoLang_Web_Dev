# Download & Install MongoDB (Server) and MongoDB Shell (Client)

* [How to install MongoDB on MacOS](https://www.mongodb.com/try/download/community)
* [MongoDB Shell Download](https://www.mongodb.com/try/download/shell)

***

# How to bypass the block in your Security & Privacy settings. 
1. Open the Apple menu, and click ```System Preferences```.
2. Click ```Security & Privacy```.
3. Click the ```General tab```.
4. Click the ```lock``` in the lower right corner of the window.
5. Enter your **username and password** when prompted, and click Unlock.
6. Click the ```App Store and Identified Developers``` radial button.
7. Look for “(App Name) was blocked from opening because it is not from an identified developer” and click **Open Anyway**. (In older versions of macOS, you could click Anywhere and then click Allow From Anywhere.)
Try rerunning the app.

***

# Set MongoDB 'PATH' 
```
$ vim ~/.bash_profile

$ export MONGODB_PATH=$HOME/MongoDB/mongodb-macos-x86_64-6.0.2
$ export PATH=$PATH:$MONGODB_PATH/bin
$ export MONGOSH_PATH=$HOME/MongoDB/mongosh-1.6.0-darwin-x64
$ export PATH=$PATH:$MONGOSH_PATH/bin

$ source ~/.bash_profile
```

```
$ mongod --version
```


# Start the MongoDB Server
```
$ mkdir -p ~/data/db
$ mongod --dbpath ~/data/db
```

# Start the MongoDB Shell
```
$ ./mongosh

Current Mongosh Log ID:	636e29b3ab452c8fe738a99d
Connecting to:		mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.6.0
Using MongoDB:		6.0.2
Using Mongosh:		1.6.0

For mongosh info see: https://docs.mongodb.com/mongodb-shell/
```
