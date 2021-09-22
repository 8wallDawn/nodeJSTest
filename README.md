# nodeJSTest
nodeJS의 NPM, NVM 에 대한 기본적인 원리 이해와 예문이다.

## NVM(Node Version Manager)

---

NodeJS의 버전을 변경할 수 있도록 하는 프로그램이다.

> 프로젝트를 진행하면서 NodeJS의 버전이 영향을 줄 수 있기 때문에 프로젝트 진행에 사용된 NodeJS의 버전을 맞추어 주어야 하기에 사용된다.

### 설치(How to Install NVM)

---

- MAC OS
    1. [README.md](http://readme.md) 에서 Install & Update Script 선택
    2. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash` 복사
    3. 터미널에 입력

    [GitHub - nvm-sh/nvm: Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions](https://github.com/nvm-sh/nvm)

    Mac OS 의 NVM

- Window OS
    1. [README.md](http://readme.md) 에서 Overview의 Download Now! 선택
    2. 설치하고자 하는 버전의 nvm-setup.zip 다운로드 및 설치 진행

    [GitHub - coreybutler/nvm-windows: A node.js version management utility for Windows. Ironically written in Go.](https://github.com/coreybutler/nvm-windows)

    Window OS 의 NVM

### 사용법(명령어)

---

Terminal 내에서의 버전 제어 방법

`$ nvm --help` - 명령어 및 사용법

- `$ nvm ls` -  현재 설치된 NodeJS 버전 목록 확인
- `$ nvm install 'nodeJS-version'` - 설치하고자 하는 NodeJS 버전 명시 및 설치
- `$ nvm uninstall 'NodeJS-version'` - 삭제하고자 하는 NodeJS 버전 명시 및 삭제
- `$ nvm use 'NodeJS-version'` - 사용하고자하는 NodeJS 버전 명시 및 적용

### 에러 코드(Error code)

---

- exit status 5

    계정에 관리자 권한 요청이 거부되었을 때 나타나는 에러 코드로 VSC를 관리자 권한으로 실행하여 해결할 수 있다.
    
---
## NPM(Node Package Manager)
NPM은 JavaScript를 위한 패키지 관리자로 NodeJS의 기본 패키지, 모듈 관리자 이다.

전 세계의 개발자들이 만든 다양한 기능(패키지, 모듈)을 관리한다.

NPM을 통해서 생성된 .cache, dist, node_modules의 파일은 따로 git의 버전관리를 해줄 필요가 없다. 위의 폴더는 package.json에 명시가 잘 되어 있다면, 언제든 `$ npm i`를 통해서 node_modules가 복구가 될 뿐 아니라 `$ npm build`(아래에서 사용한 scripts 식별어) 를 통해서 .cache, dist가 복구되며, node_modules의 경우는 프로젝트에서 사용하는 패키지 뿐 아니라 모든 패키지의 정보가 들어 있어 용량이 크기 때문에 버전 관리가 되려 비효율 적이다.

**git에서 버전관리를 하고 싶지 않은 폴더 파일을 명시한 이후 나머지 파일 및 폴더를 git에서 버전관리 하면 된다.**

> git에서 버전관리를 제외하는 방법
**.gitignore 파일 내에** `$ git init` **을 하기 이전, 버전관리에서 제외할 파일 또는 폴더를 명시하는 방법이다.**

1. .gitignore 파일 생성
2. `'폴더 및 파일 명'/`

```jsx
//예문
.cache/
dist/
node_modules/
.../
```

### 사용법(명령어)

---

프로젝트 생성 후 Terminal 내에서의 NPM 사용 방법

- `$ npm init -y` - 패키지 관리 파일 생성

    package.json 파일이 생성된다.

    ```json
    // package.json
    {
      "name": "프로젝트 명",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": { //프로젝트와 관련된 명령어 작성
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC"
    }
    ```

---

### 개발용 의존성 패키지, 일반 의존성 패키지 설치와 실행

- `$ npm install -D 'module_Name'` 에서 `-D` 유무의 차이
    - `$ npm install -D 'module_Name'` - 개발용 의존성 패키지 설치

        : 개발시에만 사용하며, 브라우저 내에서의 필요한 모듈이 아님을 구분

    - `$ npm install 'module_Name'` - 일반 의존성 패키지 설치

        : 개발 및 브라우저 내에서 동작에도 필요한 모듈임을 구분

- `$ npm i` - node_modules 등 기타 파일을 제거 한 상태에서 package.json에 모듈의 이름과 버전이 남아있다면 해당 명령어를 통해서 명시된 모든 모듈이 설치됨.

**개발용 의존성 패키지**

- `$ npm install parcel-bundler -D` - node_modules 폴더 생성 및 package-lock.json 파일 생성

    * node_modules 는 package 파일의 집합소

    ```json
    // package.json
    {
      "name": "프로젝트 명",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": { //프로젝트와 관련된 명령어 작성
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC"
    	// 설치한 parcel-bundler가 package.json에 추가됨.
    	"devDependencies": {
        "parcel-bundler": "^1.12.5"
      }
    }
    ```

    이때, 설치한 parcel-bundler 를 통해서 프로젝트 내의 index.html 을 생성한다고 하였을 때,

    Terminal에서 `$ parcel index.html`을 입력하면 parcel은 프로그램이 인식하는 실행용어가 아니다. 이를 해결하기 위해 package.json 파일의 scripts 부분을 다음과 같이 수정한다.

    ```json
    "scripts": {
    		"dev":"parcel index.html", //local 환경 내에서 개발용 서버환경 개설 및 실행
        "build": "parcel build index.html" //사용자 입장에서의 서버환경 개설 및 실행
    },
    ```

    그럼 `$ parcel index.html`이 `dev`와 `build`라는 식별자를 얻게되고 Terminal에서 `$ npm run dev` 또는 `build`를 통해서 실행할 수 있다.

    그럼 `dev` 의 경우,

    ```visual-basic
    Server running at [http://localhost:1234](http://localhost:1234/)
    √  Built in 9.88s.
    ```

    다음과 같이 서버가 구동적인 url 주소가 생성된다.

    `build`의 경우는 사용자 입장에서의 개발환경을 제공하기 때문에 dist라는 폴더가 생성이 되고, 해당 폴더 내의 변환된 html파일은 **난독화**(코드를 읽기 어렵게 만드는 과정 및 최적화)된 파일로 변환된다.

    **즉, 생성된 dist는 개발자가 아닌 사용자가 보게되는 파일이며, pacel-bunlder는 개발시에만 활용되는 개발용 의존성 패키지로, 번들(bundle)은 프로젝트 개발에 사용한 여러 모듈을 하나로 묶어내는 작업을 의미한다.**

**일반 의존성 패키지**

- `$ npm install lodash` - node_modules 폴더 생성 및 package-lock.json 파일 생성

    ```json
    // package.json
    {
      "name": "프로젝트 명",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": { //프로젝트와 관련된 명령어 작성
        "dev":"parcel index.html"
      },
      "keywords": [],
      "author": "",
      "license": "ISC"
    	"devDependencies": {
        "parcel-bundler": "^1.12.5"
      },
    	// 일반 의존성 패키지 lodash가 install 됨.
    	"dependencies": {
    	    "lodash": "^4.17.21"
    	  }
    }
    ```

    'lodash'를 js파일을 통해서 node_modules 폴더에서 불러오기 위해 다음과 같이 js파일을 작성한다.

    ```jsx
    import _ from 'lodash'
    // (데이터를)불러온다 _ 'lodash'로 부터

    //lodash 명령어 예문
    console.log(_.camelCase('hello world'));
    //> helloWorld
    ```

    명령어는 node_modules 내 lodash 폴더에서 확인이 가능하며, 로직 또한 파악할 수 있다.

---

### 패키지 설치

`$ npm install 'Module_Name'@'Version'` - 'Version'의 'Module_Name' 설치

`$ npm info 'Module_Name'` - 'Module_Name'의 정보 확인

* 해당 모듈에 대한 버전은 node_modules 폴더 내의 해당 모듈 폴더의 package.json에서 확인가능하다.

`$ npm update 'Module_Name'` - 'Module_Name'의 버전 업데이트 실행
