# Prepare demo
## Github
- Create empty Github project, copy repository .git url
- Open empty folder in terminal: `git init .`
- `git remote add origin [url]`
- Create empty `readme.md` and `.gitignore`, add `node_modules` to gitignore
- Add .npmrc

/.npmrc
```
@types:registry=http://registry.npmjs.org
#registry=http://localhost:4873/
registry=http://registry.npmjs.org
progress=false
strict-ssl=false
```

- `git add . && git commit -am 'setup project'`
- `git push -u origin master`


## Run private npm repository
- `npm install -g verdaccio`
- `verdaccio`
- `npm unpublish [package]` to remove packages published from previous demos
- `npm set registry http://localhost:4873`
- `npm adduser --registry http://localhost:4873/`
- username / password: verdaccio

# Initialize project
- Show Github repository
- Show private npm repository
- `npm install -g lerna`
- `lerna init`

## Setup Yarn Workspaces
/package.json
```json
{
  "private": true,
  "workspaces": [
    "packages/*"
  ]
}
```

/lerna.json
```json
{
  "npmClient": "yarn",
  "useWorkspaces": true,
}
```
- `git status` > `git add .` > `git commit -am 'Setup Yarn workspaces'` > `git push`


# Add packages
## Calculator
- `lerna create @my-app/calculator`
- Add calculator function, which sums up.
``` javascript
module.exports = calculator;

function calculator(a,b) {
    return a + b;
}
```
- `git status && git add . && git commit -am 'chore(@my-app/calculator): add calculator' && git push`
- `lerna publish --conventional-commits`

## My-app
- `lerna create @my-app/web`

/packages/web/lib/my-app.js
```javascript
const calc = require('@my-app/calculator');
function myApp() {
    console.log(calc(1,2));
}
myApp();
```
- `lerna add @my-app/calculator --scope @my-app/web`
- `lerna bootstrap`

/packages/web/package.json
```json
{
  "start": "node ./src/web"
}
```

`lerna run start --stream --scope @my-app/web`
- `git add . && git commit -am 'chore(@my-app/web): create app' && git push`
- `lerna publish --conventional-commits`


# GraphQL
http://try.sangria-graphql.org/playground
```
query HumanAndDroids {
  human(id: "1003") {
    name
    appearsIn
    homePlanet
  }
}
```

## extend example
```
droid(id: "2001") {
    name
    appearsIn
    primaryFunction
}
```

## query variables
```
query HumanAndDroids($humanId: String!) {
  human(id: $humanId) {
    name
    appearsIn
    homePlanet
  }

  droid(id: "2001") {
    name
    appearsIn
    primaryFunction
  }
}

{
  "humanId":  "1003"
}
```

## Fragment
```
fragment Common on Character {
  name
  appearsIn
}
```