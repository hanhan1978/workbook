

> check node version

node -v

> create directory for projects

mkdir sample && cd sample

> initialize npm

npm init

> install webpack

npm install --save-dev webpack webpack-cli


> create src js 

mkdir src && vi src/index.js

```
function component() {
  var element = document.createElement('div');

  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());
```


> create dist & index.html

mkdir dist && vi dist/index.html

```
<!doctype html>
<html>
    <head> </head>
    <body>
        <script src='bundle.js'></script>
    </body>
</html>
```

> create webpack.config.js

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

> execute webpack

npx webpack


> check output

npm install browser-sync -D
browser-sync dist/
