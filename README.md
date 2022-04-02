# First Electron app

1. 폴더 생성

2. 프로젝트 생성

```bash
npm init
```

3. Electron Package  추가

```bash
npm install --save-dev electron
```

4. 패키징과 배포

```bash
npm install --save-dev @electron-forge/cli
npx electron-forge import

npm run make
```

5. React package 추가하기

```bash
npm install --save react react-dom
```

6. React 소스 폴더 만들기

```bash
mkdir src/js
```

7. 웹팩용 패키지 추가

```bash
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader style-loader sass-loader sass webpack webpack-cli
```

8. webpack.common.js 추가

```js
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/js/index.js',
  devtool: 'inline-source-map',
  target: 'electron-renderer',
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [[
              '@babel/preset-env', {
                targets: {
                  esmodules: true
                }
              }],
              '@babel/preset-react']
          }
        }
      },
      {
        test: [/\.s[ac]ss$/i, /\.css$/i],
        use: [
          // Creates `style` nodes from JS strings
          'style-loader',
          // Translates CSS into CommonJS
          'css-loader',
          // Compiles Sass to CSS
          'sass-loader',
        ],
      }
    ]
  },
  resolve: {
    extensions: ['.js'],
  },
  output: {
    filename: 'app.js',
    path: path.resolve(__dirname, 'build', 'js'),
  },
};
```

9. package.json에 webpack 스크립트 추가

```js
"watch": "webpack --config webpack.common.js --watch",
```

```
npm run watch
```