# 2강 NODE JS와 EXPRESS JS 다운로드 하기

nodejs가 나오기 전에는 자바스크립트를 항상 브라우저 속에서만 사용했다. 그런데 nodejs가 나오면서 자바스크립트를 크롬이나 인터넷 익스플로러 같은 클라이언트 사이드(인터넷 브라우저)가 아닌 서버 사이드에서도 사용할 수 있게 되었다. 그래서 nodejs는 자바, php, go, python 같은 하나의 언어인 자바스크립트를 서버 사이드에서 쓸 수 있게 만들어 주는 런타임이라고 한다. 

expressjs는 nodejs를 좀 더 쉽게 이용할 수 있게 해주는 웹 애플리케이션 프레임워크이다.

> Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. [LINK](https://expressjs.com/)

오늘 배울 내용의 헤드라인은 다음과 같다.

* node 설치 여부 확인
* node 설치
* 프로젝트 디렉토리 만들기
* index.js 파일 만들기 - 백엔드 시작점
* express js 다운 받기
* node_modules 디렉토리의 정체
* index.js에서 기본적인 express js 앱 만들기
* 서버를 실행하는 start script 추가하기
* 브라우저에 가서 확인해보기

## node 설치 여부 확인

```bash
$ node -v
v10.16.2
```

위와 같이 버전 이름이 나오면 설치가 이미 된 것이고, 그렇지 않으면 설치되지 않은 것이다.

## node 설치

brew 이용하는 방법으로 추후 작성 예정

## 프로젝트 디렉토리 만들기

```bash
$ mkdir boiler-plate && cd boiler-plate
```

npm 패키지을 만들어야 한다.

```bash
$ npm init
```

아무 내용 없이 엔터를 치면 기본 값으로 설정하고, `package.json` 파일이 자동으로 생성된다. 예를 들어, `package.json` 파일의 내용은 다음과 같다:

```json
{
  "name": "boiler-plate",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "mincheo",
  "license": "ISC"
}
```

## index.js 파일 만들기 - 백엔드 시작점

프로젝트 디렉토리 내에 `index.js` 파일을 생성한다. `index.js` 파일은 백엔드 서버가 시작할 때 처음으로 바라보는 코드라고 보면 된다.

## express js 다운 받기

터미널에서 현재 위치가 프로젝트 폴더 안인 것을 확인하고 아래와 같은 명령어를 입력한다.

```bash
$ npm i express --save
```

`--save` 옵션은 본 프로젝트로 만드는 애플리케이션이 지금 설치할 라이브러리(지금의 경우 express)를 의존한다는 뜻이다.

express가 다운 완료되었다. 아까 생성된 `package.json` 파일을 다시 확인해보면 "dependencies"에 express가 추가된 것을 알 수 있다. 

```json
{
  "name": "boiler-plate",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "mincheo",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

## node_modules 디렉토리의 정체

다운 받은 dependencies들은 모두 이 디렉토리에서 관리된다.

## index.js에서 기본적인 express js 앱 만들기

[express js 다큐멘테이션](https://expressjs.com/en/starter/hello-world.html)에서 코드를 가져온다. 

```javascript
const express = require('express')
const app = express()
const port = 5000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`))
```

코드의 내용은 다음과 같다.

* 설치했던 express 모듈을 가져온다.
* express() 함수를 이용해서 새로운 앱(`app`)을 만든다.
* 백서버 port를 설정한다. (예제코드 3000을 5000으로 바꿨음)
* express app(`app`)을 설정하는데, 루트 디렉토리(`/`)로 접속(GET 요청)이 오면 `Hello world`를 출력(응답)하게 한다.
* experss app을 port 5000번에서 실행하게 하고, 실행되면 "Example app listening .." 이하 메시지를 콘솔에 출력하도록 한다.

## 서버를 실행하는 start script 추가하기

`package.json` 파일에서 "scripts"에 코드를 추가한다.

```json
{
  "name": "boiler-plate",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "mincheo",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

"scripts"에 key 값 "start"를 추가하면 bash에서 `npm run start`를 실행할 수 있게 된다. "node index.js"는 node app을 실행할 때 시작점을 `index.js` 파일로 설정한다는 뜻이다.

이제 등록한 npm script를 직접 실행해본다.

```bash
$ npm run start


> boiler-plate@1.0.0 start /Users/admin/Works/datalater/projects/node/node-react-basic/boiler-plate
> node index.js

Example app listening at http://localhost:5000
```

## 브라우저에 가서 확인해보기

크롬을 켜서 url에 `http://localhost:5000/`을 입력한다.

`index.js` 5번째 라인에 적었던 Hello World! 메시지가 브라우저에서 그대로 출력되는 것을 확인할 수 있다.

한번 Hello World! 메시지를 Hello World! 안녕하세요! 라고 코드를 바꿔본다. 그리고 서버를 껐다가(ctrl+c) 다시 `npm run start`로 서버를 켠다. 그리고 브라우저를 리프레시한다.

수정한 메시지가 그대로 반영되는 것을 확인할 수 있다.

**END**