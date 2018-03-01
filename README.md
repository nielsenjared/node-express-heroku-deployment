# Deploying a Node Express Web Server to Heroku

If you cloned a repository you can [skip straight to deployment](#deploy-to-heroku).

See the deployed application here: https://node-express-heroku-deployment.herokuapp.com/


## Initialize Your Project with npm
```
mkdir node-express-heroku-deployment-guide
cd node-express-heroku-deployment-guide
npm init
```

During the init process you will be prompted to add a GitHub repository. Now would be a good time to make a new project on GitHub. Add the repo link to your `package.json` when prompted.


## Initialize Your Project with git

```
git init
git remote add origin <URL-to-your-repo>
```

Create a `.gitignore` file and add `node_modules` to it.


## Set Up a Simple Express Server

```
npm install express --save
```

Add a `server.js` file:

```
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send("Hello World!");
});

const PORT = process.env.PORT || 3001;
app.listen(PORT);
```

Start the server and navigate to [localhost:3001](http://localhost:3001) to verify that it works.


## Deploy to Heroku

In `package.json`, verify your 'start' script:
```
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "start": "node server.js"
  },
```

This tells Heroku which file to run to start your app. In our case it is `server.js`.

Then log into Heroku via the command line and create a new Heroku app:
```
heroku login
heroku create
```

Verify the creation of your Heroku app by running `git remote -v`.

Then run the following:
```
git add .
git commit -m “First”
git push -u origin master
git push heroku master
```

Navigate to the URL provided to verify deployment. It will be something poetic, like: https://dry-chamber-49146.herokuapp.com/

Hello, world!

In the future:
```
git add .
git commit -m “Ch-ch-ch-changes…”
git push heroku master
```

Finally, and optionally, change the name of your Heroku app to something more descriptive. On Heroku.com, under the Settings for your application, edit the Name field.

You will then need to update your remote locally. At the command line, run:
```
git remote rm heroku

heroku git:remote -a <newname>
```
Where `<newname>` is the new name of your application.
