# Webpack

## 참고 링크 
- [웹팩 핸드북](https://joshua1988.github.io/webpack-guide/guide.html)  
- [webpack github 예제](https://github.com/joshua1988/LearnWebpack)

<div id="contents">  

## 목차
1. [Webpack 소개 및 배경](#1)
2. [Webpack Getting started](#2) 
3. [Webpack Entry](#3)
4. [Webpack Output](#4)
5. [Webpack Loader](#5)
6. [Webpack Plugins](#6)
7. [Webpack Resolve](#7)
8. [Webpack Dev Serve](#8)
9. [Webpack Dev Middleware](#9)
10. [Webpack 개발환경 설정](#10)
</div>

## 개요
- React, Angular, Vue에서 권고하는 Webpack 설정 
- Webpack 주요 설정 Entry, Output, Loader, Plugins, Resolve 
- Webpack 개발환경 설정방법
    
![웹팩 4가지 주요 속성](https://joshua1988.github.io/webpack-guide/assets/img/diagram.519da03f.png)    
***

<div id="1">

## 1.Webpack이란?
서로 연관관계가 있는 웹자원들을 js, css, img와 같은 static한 자원으로 변환해주는 모듈 번들러
의존성 모듈 => 압축, 변환 => 정적 파일  
![webpack의 역할](https://miro.medium.com/max/3200/1*Wi3B-Qq_DVDNVXstaag9BQ.png)

### Webpack을 사용하는 이유 & 배경
1. 새로운 형태의 Web Task Manager
   - 기존 Gulp, Grunt의 기능 + 모듈 의존성 관리 
   - minification을 webpack default cli로 실행 가능

> webpack -p

2. 자바스크립트 Code based Modules 관리 
   - 자바스크립트 모듈화의 필요성 : AMD(비동기 모듈 정의), Common js, ES6(Modules)
   - 기존 모듈 로더들과의 차이점 : 모듈 간의 관계를 청크(Chunk) 단위로 나눠 필요할 때 로딩
   - 현대의 웹에서 JS역할이 커짐에 따라, Client Slide에 들어가는 코드량이 많아지고 복잡하짐
   - 복잡한 웹 앱을 관리하기 위해 모듈 단위로 관리하는 AMD(비동기 모듈 정의), Common js, ES6(Modules)등이 등장
   - 가독성이나 다수 모듈 미병행 처리등의 약점을 보완하기 위해 등장함

### 자바스크립트 모듈화 문제 
`script로 자바스크립트 모듈화를 진행하면?`
```
    <script src="module1.js"></script>
    <script src="module2.js"></script>
    <script src="module3.js"></script>    
```
- 전역변수 충돌
- 스크립트 로딩 순서
- 복잡도에 따른 관리상의 문제

### Webpack의 철학
1. Everything is Module 
   모든 웹 자원(js, css, html, image)이 모듈 형태로 로딩 가능
```
require('base.css');
require('main.js');
```

2. Load only 'what' you need and 'when' you need 
   초기에 불필요한 것들을 모두 로딩하지 않고 필요할 때 필요한 것만 로딩하여 사용

</div>

<div id="2">

## 2.Webpack Getting Started  
getting-started 폴더  

**실습절차**
1. webpack 전역설치
> npm i webpack -g
> npm i webpack-cli -g
2. npm init으로 package.json 생성<br>
   아래 명령어 수행 시 기본 package.json생성됨
>npm init -y
3. app/index.js, index.html 생성
4. lodash 라이브러리   
유틸리티 라이브러리로 array, collection, date, number, object 등이 있으며, 데이터를 쉽게 다룰 수 있도록 도와준다
> npm i lodash -save
5. js와 html에 코드 추가
6. webpack app/index.js dist/bundle.js 명령어 실행 후 index.html로딩 
   *app이 아닌 src폴더를 만들고 webpack 명령만 수행하면 dist/main.js로 자동 생성됨.
7. webpack.config.js파일 추가 후 webpack 명령 수행

`webpack4버전`
webpack.config.js설정 없이 webpack명령어를 수행하면 기본 dist/main.js파일이 생성된다.

`webpack.config.js`
```javascript
const path = require('path');

module.exports = {
    //생성된 main.js파일이 가독성있게 생성된다.
    mode: "development",
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'main.js',
    },
};
```

### NPM(Node Package Manager)
- js 개발자들이 편하게 개발할 수 있도록 js라이브러리들을 모아놓은 열린 공간
- front-end web apps, mobile apps, robots, routers 라이브러리들이 존재 
- Gulp, Webpack 모두 node기반, NPM을 사용하여 필요 라이브러리들을 로딩
- 재사용 가능한 code를 module, package라고 호칭
- package.json : 해당 package에 대한 파일 정보가 들어가 있음 
- keyword로 패키지 [검색](https://www.npmjs.com/)이 가능하다.

### NPM 명령어 모음 
**package.json 생성**

-y를 붙이면 default정보를 가진 파일이 생성된다.
>npm init -y

**패키지 설치 및 업데이트**

프로젝트에 사용할 node module설치 및 package.json업데이트
>npm i 패키지명

패키지 제거 
>npm uni 패키지명

**Global설치와 Local설치**
- Global설치
  
   c 드라이브(시스템 레벨) C:\Users\P-0423\AppData\Roaming\npm\node_modules

- Local설치

   프로젝트 폴더 ./node_modules

   require('모듈명')으로 사용할 때

**install --save(default)와 --save-dev** [참고1](https://ingorae.tistory.com/1754)
  
나중에 다른 곳에 해당 프로젝트를 가져오더라도 모든 모듈을 일일이 설치할 필요없이 `npm install`만 입력하면 dependencies 항목을 기반으로 필요한 모듈을 모두 자동으로 설치한다.

- --save(default) : 앱이 구동하기 위해 필요한 모듈, 라이브러리 설치 
  - --production 빌드시 해당 플러그인이 포함됩니다.
  - 제품의 릴리즈나 구동시 꼭 필요한 모듈의 경우
  - dependencies만 설치하려면 `npm install --only=prod[uction]`


```
   "dependencies": {
        "lodash": "^4.17.15"
   }
```

- --save-dev(-D) : 앱 개발시 필요한 모듈, 라이브러리 설치
  - --production 빌드시 해당 플러그인이 포함되지 않습니다.
  - 제품의 개발시에 테스트를 위해서 필요한 모듈이긴 한데 실제 릴리즈시에는 필요없는 모듈의 경우 
  - devDependencies만 설치하려면 `npm install --only=dev[elopment]` 


```
   "devDependencies": {
        "lodash": "^4.17.15"
   }
```

</div>

<div id="3">

## 3.Webpack Entry 
- webpack으로 묶은 모든 라이브러리들을 로딩할 시작점 설정(진입점)
- a,b,c라이브러리를 모두 번들링한 main.js를 로딩한다.
- 1개 또는 2개 이상의 엔트리 포인트를 설정할 수 있다.

**여러가지 entry유형**
```javascript
var contig = {
   // 간단한 설정
   entry: './src/index.js', 
   // 여러개일 경우
   entry: ['./src/index.js', './src/index2.js'], 
   // 앱 로직용, 외부 라이브러리용
   entry: {                   
      index:'./src/index.js',
      vendors:'./src/vendors.js'
   },
   //페이지당 불러오는 경우
   entry: {                   
      pageOne:'./src/pageOne/index.js',
      pageTwo:'./src/pageTwo/index.js',      
   }
};
```
**Mutiple Entry points**

```javascript
module.exports = {
   entry: {                   
      Profile:'./profile.js',
      Feed:'./feed.js'
   },
   output: {
      path: 'build',      
      //위에 지정한 entry키의 이름에 맞춰서 결과 산출
      filename: '[name].js',        
   }, 
};

// 번들파일 profile.js를 <script src="build/profile.js></script>로 html에 삽입
```
</div>

<div id="4">

## 4.Webpack Output
- 웹팩의 결과물에 대한 정보를 입력하는 속성
- filename, path를 정의

```javascript
const path = require('path');

module.exports = {
   entry: {                   
      Profile:'./profile.js',
      Feed:'./feed.js'
   },
   output: {
      path: 'build',      
      path: path.resolve(__dirname, 'build'), 
      filename: '[name].js',        
   }, 
};
```
**output name option**

1. [name] : 엔트리명에 따른 output파일명 생성
2. [hash] : 특정 webpack build에 따른 output파일명 생성
3. [chunkhash] : 특정 webpack chunk에 따른 output파일명 생성

```javascript

output:{
   filename:'[name].js',
   filename:'[hash].js',
   filename:'[chunkhash].js',
}

```
[node path](https://nodejs.org/api/path.html)

</div>


<div id="5">

## 5.Webpack Loader
- webpack은 자바스크립트 파일만 처리 가능함.
- loader를 이용하여 다른 형태의 웹 자원들(img, css와 같은 비js파일)을 js로 변환하여 로딩
- 오른쪽에서 왼쪽 순으로 적용
```javascript
var path = require('path');

module.exports = {
  entry: './app/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [{
      test: /\.css$/,
      use: ['style-loader', 'css-loader']
    }]
  },
}
```
**참고링크**  
[exporse-loader](https://www.npmjs.com/package/expose-loader)  
[imports-loader](https://github.com/webpack-contrib/imports-loader)  
[loaders 설정](https://webpack.js.org/concepts/loaders/)

### Babel Loader - es6
- preset : Babel 플러그인 리스트

> npm install --save-dev babel-loader @babel/core

```javascript
module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
```

```javascript
module: {
    rules: [{
      test: /\.js$/,
      use: [
         {
            loader:'babel-loader',
            option:{
               presets:[
                  //Tree Shaking : 모듈에서 사용되지 않는 
                  ['es2015','react',{modules:false}]
               ]
            }
         }
      ]
    }]
  },
```

**code Splitting 실습절차**  
[Code Splitting](https://webpack.js.org/guides/code-splitting/)  
[webpack4에서 extract-text-webpack-plugin적용](https://negabaro.github.io/archive/webpack-extract-text-webpack-plugin)  
example1 폴더

1. package.json생성
> npm init -y
2. loader, plugin설치 
> npm i css-loader style-loader --save-dev  
> npm i extract-text-webpack-plugin --save-dev  
> npm i extract-text-webpack-plugin@next -–save-dev //webpack4버전에서 적용
3. index.html, app/index.js, base.css생성
4. webpack.config.js 생성
5. webpack 실행

**extract-text-webpack-plugin로 css파일 분리 실습**

css를 bundle.js파일 안에 번들링 하지 않고 빌드시에 별도의 .css파일로 분리해준다.  

`webpack.config.js`
```javascript
// ...
var ExtractTextPlugin = require('extract-text-webpack-plugin');
// ...
{
  // ...
  module: {
    rules: [{
      test: /\.css$/,
      // Comment this out to load ExtractTextPlugin
      // use: ['style-loader', 'css-loader']
      use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: "css-loader"
      })
    }]
  },
  plugins: [
    new ExtractTextPlugin('styles.css')
  ]
}
```


</div>

<div id="6">

## 6.Webpack Plugins
- 플러그인은 파일별 커스텀 기능을 사용하기 위해서 사용한다.  
ex) JS minification, file extraction, alias
- 웹팩으로 변환한 파일에 추가적인 기능을 더해준다.
- 웹팩 변환 과정 전반에 대한 제어권을 가지고 있다.

**플러그인 예**
1. ProvidePlugins
   - 모든 모듈에서 사용할 수 있도록 해당 **모듈을 변수로 변환**한다.
```javascript  
new webpack.ProvidePlugin({
   $:'jquery'
})
```

2. DefinePlugin
   - 웹팩 번들링을 시작하는 시점에 사용 가능한 **상수들을 정의**한다.
   - 일반적으로 개발계 & 테스트계에 따라 다른 설정을 적용할 때 유용하다.
```javascript  
new webpack.DefinePlugin({
   PRODUCTION:JSON.stringify(true),
   VERSION:JSON.stringify('5fa3b9'),
   BROWSER_SPPORTS_HTML5:true,
   TWO:'1+1',
   'typeof window':JSON.stringify('object')
})
```

3. ManifestPlugin
   - 번들링시 생성되는 코드(라이브러리)에 대한 정보를 json파일로 저장하여 관리   
   - manifest.json을 생성해 매번 생성된 최종결과물과 매치되는 스태틱한 파일명을 alias와 같은 형태로 사용할 수 있게 해주므로 import시는 고정값을 사용가능하게 됨


```javascript  
plugins: [
   new ManifestPlugin({
      fileName: "manifest.json",
      basePath: "./dist/"
   })
],
```

**Libraries Code Splitting 실습절차**  
[splitChunks]](https://negabaro.github.io/archive/webpack-splitChunks)  
example2 폴더

1. package.json생성
2. loader, plugin 설치  
   - moment 날짜관련 작업을 위한 자바스크립트 라이브러리
>npm install webpack --save-dev  
>npm install moment lodash --save  
>npm i webpack-manifest-plugin --save-dev  
3. index.html, app/index.js 생성
4. webpack.config.js 생성
5. webpack 실행

</div>

<div id="7">

## 7.Webpack Resolve
- 웹팩의 **모듈 번들링** 관점에서 봤을 때 모듈 간의 의존성을 고려하여 모듈을 로딩해야 한다.
- 모듈을 어떤 위치에서 어떻게 로딩할지에 관해 정의를 하는 것이 바로 Module Resolution
```javascript
//일반적인 모듈 로딩 방식 
import foo from 'path/to/module'
//또는 
require('path/to/module')
```
모듈을 어떻게 로딩해올까?
1. 절대경로를 이용한 파일 로딩
   - 파일의 경로를 모두 입력해준다.
```javascript
import '/home/me/file';
import 'c:\\Users\\me\\file';
```
2. 상대경로를 이용한 파일 로딩
   - 해당 모듈이 로딩되는 시점의 위치에 기반하여 상대 경로를 절대경로로 인식하여 로딩한다.
```javascript
import '../src/file1';
import './file2';
```

### Resolve Option  
webpack.config.js에서 resolve를 추가하여 모듈 로딩에 관련된 옵션 사용  
1. alias  
특정모듈을 로딩할 때 alias옵션을 이용하면 별칭으로 더 쉽게 로딩이 가능하다.
```javascript
alias:{
   Utilities:path.resolve(__dirname, 'src/path/utilities/')
}
import Utility from '../../src/path/utilities/utility';
// alias사용시 src/path/utilities/ 대신 Utilities 활용
import Utility from 'Utilities/utility';
```
1. modules  
require() import '' 등의 모듈 로딩시에 어느 폴더를 기준할 것인지 정하는 옵션
```javascript
modules:['node_modules']//defaults
modules:[path.resolve(__dirname, 'src'),'node_modules']//src/node_modules
```

**Webpack Plugins & Resolve 실습절차**  
[Resolve](https://webpack.js.org/configuration/resolve/#root)  
[Resolve github](https://github.com/joshua1988/LearnWebpack#example-3---webpack-resolve--plugins)  
example3 폴더

1. package.json생성
2. plugin 설치     
>npm install webpack jquery --save-dev 
1. index.html, app/index.js 생성
2. webpack.config.js 생성
3. webapck실행
4. app/index.js, webpack.config.js 변경하여 alias&Provide 동작 확인

`index.js`
```javascript
// #1 - Using NPM
var $ = require('jquery');
console.log("loaded jQuery version is " + $.fn.jquery);

// #2 - Using alias
// import $ from 'Vendor/jquery-2.2.4.min.js';
// console.log("loaded jQuery version is " + $.fn.jquery);

// #3 - Using Provide Plugin
// console.log("loaded jQuery version is " + $.fn.jquery);
```

`webpack.config.js`
```javascript
var path = require('path');
var webpack = require('webpack');

module.exports = {
   entry: './app/index.js',
   output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
   },

   // #2 - Using alias
   // resolve: {
   //     alias: {
   //         Vendor: path.resolve(__dirname, './app/vendor/')
   //     }
   // }

   // #3 - Provide Plugin
    plugins: [
        new webpack.ProvidePlugin({
            $: 'jquery'
        })
    ]
};
```

</div>

<div id="8">

## 8.Webpack Dev Serve
[DevServer](https://webpack.js.org/configuration/dev-server/)
- 웹팩 자체에서 제공하는 개발 서버이고 빠른 리로딩 기능을 제공한다.
- 개인 프로젝트
- 페이지 자동고침을 제공하는 웹팩 개발용 node.js 서버

**설치 및 실행**  
- dev-server 설치 
> npm i --save-dev webpack-dev-serve
- 설치 후 아래 명령어로 서버 실행 (dist폴더가 생성)
> webpack-dev-serve --open  
- 또는 package.json에 명령어를 등록하여 간편하게 실행 (dist폴더가 물리적으로 보이지 않고 메모리상으로 실행)
`package.json`
```javascript
'script':{
   'start':'webpack-dev-serve'
}
```

**Options**
- publicPath : 웹팩으로 번들한 파일들이 위치하는 곳. default는 /
```javascript
module.exports = {
   //...
   devServer: {
      publicPath: '/assets/'
   }   
};
```

- contentBase : 서버가 로딩할 static파일 경로를 지정. default는 working directory
```javascript
module.exports = {
   //...
   devServer: {
      //절대경로를 사용할 것
      contentBase: path.join(__dirname, 'public')
      //비활성화
      contentBase: false
   }
};
```

- compress : gzip압축 방식을 이용하여 웹 자원의 사이즈를 줄인다.  
[gzip](https://ko.wikipedia.org/wiki/Gzip)
```javascript
module.exports = {
  //...
   devServer: {
      compress: true
   }
};
```

**Webpack Dev Server 실습절차**  
[Resolve github](https://github.com/joshua1988/LearnWebpack#example-4---webpack-dev-server-setting)  
example4 폴더

1. package.json생성
2. package.json의 script에 start명령어 추가
3. loader, plugin 설치     
>npm install webpack webpack-cli webpack-dev-server --save-dev

배포시에는 아래 명령어 수행  
>webpack-dev-server --open
4. index.html, app/index.js 생성
5. webpack.config.js 생성
6. npm start

## path 와 public Path 
- webpack dev server의 path, publicPath를 구분하기 위해 파악
- output의 path와 public path속성의 차이점 이해 필요  
`webpack 컴파일 로그 내용`
```
Project is running at http://localhost:9000/
webpack output is served from /dist/
```

- output.path : 번들링한 결과가 위치할 번들링 파일의 절대경로
- output.publicPath : 브라우저가 참고할 번들링 결과 파일의 URL주소를 지정
  cdn을 사용하는 경우 cdn호스트 지정

```javascript
//ex1
output:{
   path:'/home/proj/public/assets',
   publicPath:'/assets/'
}
//ex2
output:{
   path:'/home/proj/cdn/assets/[hash]',
   publicPath:'http://cdn.example.com/assets/[hash]/'
}

//development 
.image{
   background-image:url('./test.png');
}
//production 
.image{
   background-image:url('https://someCDN/test.png');
}
```


</div>

<div id="9">

## 9.Webpack Dev Middleware
- 기본에 구성한 서버에 웹팩에서 컴파일한 파일을 전달하는 middleware wrapper
- webpack에 설정한 파일을 변경시 파일에 직접 변경 내역을 저장하지 않고 메모리 공간을 활용한다.  
  따라서 변경된 파일 내역을 파일 디렉토리 구조안에서는 확인이 불가능하다.
- 서버가 이미 구성된 경우에는 웹팩을 미들웨어로 구성하여 서버와 연결한다.
- 협업 프로젝트


**Webpack Dev Middleware 실습절차**  
[live reload](https://blog.cloudboost.io/live-reload-hot-module-replacement-with-webpack-middleware-d0a10a86fc80)
[hmr example](https://github.com/cilliemalan/webpack-hmr-example)
[Webpack Dev Middleware](https://github.com/joshua1988/LearnWebpack#example-5---webpack-dev-middleware)  
example5 폴더

1. package.json생성
2. plugin 설치     
>npm install webpack ejs
>npm install webpack express webpack-dev-middleware --save-dev
1. server.js 생성 및 express & ejs추가
2. index.html, app/index.js 생성
3. webpack.config.js 생성
4. server.js 실행 
> node server
> 
"start": "node server" 설정시   
> npm start


</div>

<div id="10">

## 10.Webpack 개발환경 설정

### webpack 명렁어
- webpack : 웹팩 빌드 기본 명령어 (주로 개발용)
- webpack -p : minification 기능이 들어간 빌드 (주로 배포용)
- webpack -watch(-w) : 개발에서 빌드할 파일의 변화를 감지
- webpack -d : sourcemap 포함하여 빌드 
- webpack --display-error-details : error 발생시 디버깅 정보를 상세히 출력
- webpack --optimize-minimize --define process.env.NODE_ENV="'prouction'":배포용

### webpack watch 옵션
webpack설정에 해당되는 파일의 변경이 일어나면 자동으로 번들링을 다시 진행
>webpack --progress --watch

npm install --save-dev serve 후 package.json에 명령어 설정 가능
```javascript
"script":{
   "start":"serve"
}
```

</div>