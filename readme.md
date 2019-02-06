# Run private npm repository
`sinopia`
`npm set registry http://localhost:4873`
`npm adduser --registry http://localhost:4873/`

# Initialize project
`lerna init`

# Setup Yarn Workspaces
/package.json
```json
{
  "private": true,
  "workspaces": [
    "packages/*"
  ]
}
```

lerna.json
```json
{"npmClient": "yarn",
"useWorkspaces": true,}
```

`lerna create calculator`
Add calculator function, which sums up.
`git add . && git commit -am 'chore(calculator) add sum' && git push`
`lerna publish`

`lerna create my-app`
`git add . && git commit -am 'chore(my-app) create app' && git push`
`lerna publish`

`lerna bootstrap`
```javascript
const calc = require('calculator');
function myApp() {
    console.log(calc(1,2));
}
myApp();
```
`lerna add calculator --scope my-app`

my-app package.json
```json
{"start": "node ./src/my-app"}
```

`lerna run start --stream --scope my-app


GraphQL
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

add
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