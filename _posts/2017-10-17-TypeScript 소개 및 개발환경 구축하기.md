---
layout: post
title: TypeScript 소개 및 개발환경 구축하기
comments: true
---

## TypeScript란
 - TypeScript는 컴파일하면 Javascript가 되는(Compile-to-Javascript) 언어이다. 컴파일 시점에 에러 체크를 수행하고 전통적인 객체지향 프로그래밍 패턴을 도입한다.
 - TypeScirpt는 class, module, interface, static typing을 제공하고 이러한 기능들을 기반으로 더욱 견고한 Javascript 코드를 만들어 낼 수 있다. 
 - TypeScript는 ES5 문법의 Super Set 이며, ES6에서 제안된 여러가지 기능들을 동일한 문법으로 제공한다.

## TypeScript를 왜 사용할까 ?
아래 왼쪽 코드와 같이 Greeter 인스턴스 생성시 string으로 정의된 파라미터에 object를 할당하면 Type불일치에 따른 Compile 에러를 확인할 수 있습니다. 
![1](../assets/image/2017/10/17/post_2017-10-17-1.png)

더불어, Javascript는 언어의 표준은 게속해서 변화하지만, 실제 Javascript가 실행되는 브라우저 엔진에서 새롭게 추가된 Spec의 구현을 빠르게 업데이트 하지 못합니다. 하지만 Typescript를 통해 새로운 기능들을 빠르게 개발에 활용할 수 있으며 Compiler를 통해 브라우저 실행환경에 맞는 Javascript로 변환하여 줍니다.TypeScript 자체로는 브라우저에서 사용할 수 없으므로 반드시 Compilation 과정을 거쳐야만 합니다. 

## 장점
 - 자바스크립트 사용시 타입 체크를 위한 코드나 테스트를 작성하지 않아도 된다. 
 - 컴파일 타임 타입 체크를 해준다. 
 - ES6의 기능들을 사용할 수 있다. (클래스)

## 설치
TypeScript의 설치를 위해서는 NPM이 설치되어 있어야 하며, NodeJS를 설치하면 NPM이 번들로 설치되므로 NodeJS를 설치하도록 한다. 
 ~~~
 npm install -g typescript 
 ~~~
설치가 완료되면 tsc 명령어를 command line에서 실행시켜 수행여부를 확인한다.

## TypeScirpt Compile 명령어
typescript compiler(tsc)를 사용하여 .ts 파일을 compile 하여 .js 파일을 생성한다.
~~~
tsc helloworld.ts
~~~
위의 명령어를 실행하면 helloworld.js 의 Javascript로 변환된 파일이 생성된다. 

## TypeScript Compiler 설정
 - TypeScript v1.5 부터 TypeScript는 tsconfig.json 파일을 통해서 환경설정을 할 수 있다. 
 - tsconfig.json은 TypeScript 프로젝트의 root 디렉토리에 위치한다.
 - tsconfig.json은 **TypeScirpt의 Compiler Option**을 정의한다.
    * tsc 를 실행하면, Compiler는 자동으로 tsconfig.js를 찾는다.
 - "compilerOptions" 속성 - 생략되면 default option으로 실행된다. 
    * 옵션 리스트 : <https://www.typescriptlang.org/docs/handbook/compiler-options.html> 
    * module : module 코드 생성할때의 Style을 지정(commonjs, amd, es6, etc,.)
    * removeComments : /*! 로 시작하는 copy-right 헤더 comments외에 모든 주석 삭제(true, false)
    * outFile: "files" 속성에 정의된 ts파일들을 한개의 파일로 만든다. ("../../built/local/tsc.js")
    * sourceMap: debuggind에 사용하기 위한 map파일을 생성한다. 
 - "files" 속성 - Compile 대상이 되는 .ts 파일들을 리스트 업 한다. 
    * include: 포함대상 파일 및 디렉토리 지정
    * exclude: 제외대상 파일 및 디렉토리 지정
 - tsconfig.json Schema: <http://json.schemastore.org/tsconfig>


## TypeScript를 webpack에 연동하기 
  -  webpack을 설치한다. 
~~~
npm install webpack -g
~~~
  -  webpack이 TypeScript를 Compile 및 Transpile 할 수 있도록 TypeScript Loader인 ts-loader를 설치한다.
~~~
npm install ts-loader --save-dev
~~~
  - tsconfig.json 파일 작성
    * ts-loader에서 ts파일 compile시 이 option을 로드한다. 

  - webpack.config.js 작성
    * tsconfig.json 파일을 webpack에서  사용하기 위한 방법 
        * loader에 추가
        ~~~
        // specify option using query 
        { test: /\.tsx?$/, loader: 'ts-loader?compiler=typescript' }
        ~~~
        * ts 속성 추가:
        ~~~
        // specify option using `ts` property 
        ts: {
            compiler: 'typescript'
        }
        ~~~
    * sourcemaps 설정 
        * webpack.config.js 에 devtool 속성 추가
        ~~~
        devtool: 'sourcemaps'
        ~~~
        * tsconfig.js 의 compilerOptions 에 sourceMap 속성 추가
        ~~~
        "sourceMap": true
        ~~~
    * Javascript Minification
        * webpack.config.js plugins 속성 수정
        ~~~
        plugins: [
            new webpack.optimize.UglifyJsPlugin()
        ]
        ~~~

## d3 연동하기
 - typings 패키지 설치
    - npm install typings -g --save-dev
 - d3 설치
    - npm install d3 --save
 - d3 definition 을 정의
    - typings install d3 --save

## 개발시 사용하는 패키지
 - typescript : TypeScript 컴파일러
 - tslint: TypeScript가 tslint.json에서 정의한 coding rule에 의해서 작성되고 있는지 체크하기 위한 정적인 코드 분석 툴 이다. 
    * VSCode의 Extension으로 사용하면 편하다. 
    ~~~
    npm install tslint -g
    ~~~
 - ts-loader : webpack으로 TypeScript 파일을 Load해서 Compile 및 Transpile 하기 위한 패키지
 - typings : typings.json에 설정을 통해 TypeScirpt에서 사용하는 module을 설치하고 유지관리하는 단순한 방법을 제공한다. 상세한 사용법은 여기를 클릭 한다.
 - tsify : tsconfig.json 설정을 통해, TypeScript 로 작성된 코드를 컴파일 하기위해 사용하는 패키지 이다. 상세한 사용법은 여기를 클릭 한다.

    ~~~
    browserify playground.ts -p [tsify] | uglifyjs -c > dist/bundle.js
    ~~~

