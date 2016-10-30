# Next.js on Heroku

Deploy [Next.js](https://zeit.co/blog/next) universal web apps on [Heroku](https://www.heroku.com/home).

**Demo deployment** from this repo:  
https://nextjs.herokuapp.com

[Download this repo](https://github.com/mars/heroku-nextjs/archive/master.zip) as a Heroku-ready app template, or follow [Production Deployment](#production-deployment) to push an existing app to Heroku.

## Requires

* Heroku
  * [command-line tools (CLI)](https://devcenter.heroku.com/articles/heroku-command-line)
  * [a free account](https://signup.heroku.com)
* [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org)
* [Next.js](https://github.com/zeit/next.js)

## Production deployment

Once you have a [Next.js app working locally](https://github.com/zeit/next.js#how-to-use), you may deploy it for public access.

✏️ *In the following instructions, replace `$my-app-name` with your own unique app name.*

1. Add the Heroku build adapter
  1. Add [`bin/heroku-nextjs-build`](bin/heroku-nextjs-build) to your app
  1. Make sure it is executable: `chmod +x bin/heroku-nextjs-build`
1. Edit `package.json` to resemble:

  ```json
  {
    "name": "$my-app-name",
    "dependencies": {
      "next": "latest"
    },
    "scripts": {
      "dev": "next",
      "build": "next build",
      "start": "next start -p $PORT",
      "postinstall": "bin/heroku-nextjs-build"
    },
    "cacheDirectories": [
      "nextjs/node_modules"
    ]
  }
  ```
1. Ensure the app is a git repo, ignoring local-only directories:

  ```bash
  git init
  (echo node_modules/ && echo .next/) >> .gitignore
  ```
1. Create the Heroku app:

  ```bash
  heroku create $my-app-name
  ```
1. 🚀 Deploy:

  ```bash
  git add .
  git commit -m 'Next.js app on Heroku'
  git push heroku master
  ```
1. ♻️ Deploy changes: add, commit, & push again.
