# Run private npm repository
`sinopia`
`npm set registry http://localhost:4873`
`npm adduser --registry http://localhost:4873/`

# Initialize project
`git init lerna-demo && cd lerna-demo`
`git remote add origin https://github.com/emielkwakkel/lerna-demo.git`
`git push -u origin master`
`lerna init`

# Set registry
.npmrc
```bash
@types:registry=http://registry.npmjs.org
#registry=http://localhost:4873/
registry=http://registry.npmjs.org
progress=false
strict-ssl=false
```

.gitignore
```bash
node_modules
```

`lerna create calculator`
Add Calculator class with sum method.
`git add . && git commit -am 'chore(calculator) add sum' && git push`
`lerna publish`

`lerna create my-app`
`git add . && git commit -am 'chore(@hr-apps/my-app) create app' && git push`
`lerna publish`


`lerna bootstrap`
```
const calc = require('calculator');

function myApp() {
    console.log(calc(1,2));
}

myApp();
```

`lerna add @hr-shared/calculator --scope @hr-apps/my-app`