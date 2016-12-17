# vue-cli [![Build Status](https://img.shields.io/circleci/project/vuejs/vue-cli/master.svg)](https://circleci.com/gh/vuejs/vue-cli) [![npm package](https://img.shields.io/npm/v/vue-cli.svg)](https://www.npmjs.com/package/vue-cli)

Vue.js 프로젝트를 스캐폴딩하는 간단한 커맨드라인 인터페이스(CLI) 입니다.

### 설치

사전 필요 도구: [Node.js](https://nodejs.org/en/) (>=4.x, 6.x 추천) 와 [Git](https://git-scm.com/).

``` bash
$ npm install -g vue-cli
```

### 사용하기

``` bash
$ vue init <템플릿 이름> <프로젝트 이름>
```

예제:

``` bash
$ vue init webpack my-project
```

위의 명령어는 템플릿을 [vuejs-templates / webpack](https://github.com/vuejs-templates/webpack)에서 가져와 몇 가지 질문을 한 후 `./my-project/`에 프로젝트를 생성합니다.

### 공식 템플릿 목록

공식 Vue 프로젝트 템플릿이 존재하는 목적은 사용자가 가능한 한 빨리 실제 애플리케이션 코드 작성을 시작할 수 있도록 대부분의 기능을 갖춘 개발 도구 설정을 제공하는 것입니다. 그러나 이러한 템플릿은 Vue.js 외에도 사용하는 라이브러리와 애플리케이션 코드를 구성하는 방법에 대해 논쟁의 여지가 없습니다.

모든 공식 프로젝트 템플릿은 [vuejs-templates 조직](https://github.com/vuejs-templates)에 있습니다. 새로운 템플릿이 추가되면 `vue init <템플릿 이름> <프로젝트 이름>`을 실행하여 해당 템플릿을 사용할 수 있습니다. `vue list`를 실행하여 사용 가능한 모든 공식 템플릿을 볼 수도 있습니다.

현재 사용할 수 있는 템플릿 목록입니다.

- [webpack](https://github.com/vuejs-templates/webpack) - hot-reload, linting, 테스트 및 CSS 추출 기능을 갖춘 대부분의 기능을 갖추고 있는 Webpack + vue-loader 설정입니다.

- [webpack-simple](https://github.com/vuejs-templates/webpack-simple) - 단순히 Webpack과 vue-loader만 포함합니다. 빠르게 프로토타입을 만들 때 사용합니다.

- [browserify](https://github.com/vuejs-templates/browserify) - hot-reload, linting 및 단위 테스팅 등 대부분의 기능을 갖춘 Browserify + vueify 설정입니다.

- [browserify-simple](https://github.com/vuejs-templates/browserify-simple) 단순히 Browserify와 vueify만 포함합니다. 빠르게 프로토타입을 만들 때 사용합니다.


- [simple](https://github.com/vuejs-templates/simple) - 가장 단순하게 한 HTML 파일에 Vue 설정을 담고 있습니다.

### 사용자 정의 템플릿

공식 템플릿을 사용하여 모두를 만족 시킬 수는 없습니다. 공식 템플릿을 fork 한 다음 `vue-cli`를 통해 다음과 같이 사용할 수 있습니다.

``` bash
vue init username/repo my-project
```

`username/repo`는 fork 한 Github 프로젝트 입니다.

이 저장소 표기법은 [download-git-repo] (https://github.com/flipxfx/download-git-repo)를 통해 처리되므로 Bitbucket을 사용하는 경우 `bitbucket:username/repo`로 사용하면 됩니다. 태그 또는 브랜치를 이용하는 경우 `username/repo#branch`로 사용하십시오.


개인 저장소에서 다운로드하고 싶다면 `--clone` 플래그를 추가하십시오. 그러면 cli는 SSH 키를 사용하여 `git clone` 을 합니다.

### 로컬 템플릿

GitHub 저장소 대신 로컬 파일 시스템의 템플릿을 사용할 수도 있습니다.

``` bash
vue init ~/fs/path/to-custom-template my-project
```

### 사용자 정의 템플릿 작성해보기

- 템플릿 저장소는  템플릿 파일을 보유하고있는 `template` 디렉토리가 **반드시** 있어야합니다.

- 템플릿 저장소는 템플릿을 위한 메타 데이터 파일을 `meta.js` 또는 `meta.json` 파일로 사용할 수 있습니다. 다음 필드를 포함할 수 있습니다.

  - `prompts`: 사용자 옵션 데이터를 수집하는 데 사용됩니다.

  - `filters`: 조건부 필터 파일을 렌더링하는 데 사용됩니다.

  - `completeMessage`: 템플릿이 생성되었을 때 사용자에게 표시 될 메시지. 여기서 사용자 정의 명령어를 포함 할 수 있습니다.




#### prompts

메타 데이터 파일의 `prompts` 필드는 사용자를 위한 프롬프트를 포함하는 해시 객체여야 합니다. 각 항목에 대해 키는 변수 이름이고 값은 [Inquirer.js 질문 객체](https://github.com/SBoudrias/Inquirer.js/#question)입니다. 예:

``` json
{
  "prompts": {
    "name": {
      "type": "string",
      "required": true,
      "message": "Project name"
    }
  }
}
```

모든 프롬프트가 끝나면 `template` 안의 모든 파일은 [Handlebars](http://handlebarsjs.com/)를 사용해 렌더링하며, 프롬프트 결과가 데이터로 표시됩니다.

##### 조건부 프롬프트

프롬프트는 `when` 필드를 추가하여 조건부로 만들 수 있습니다. 이 필드는 이전 프롬프트에서 수집한 데이터인 JavaScript 표현식이어야합니다. 예:


``` json
{
  "prompts": {
    "lint": {
      "type": "confirm",
      "message": "Use a linter?"
    },
    "lintConfig": {
      "when": "lint",
      "type": "list",
      "message": "Pick a lint config",
      "choices": [
        "standard",
        "airbnb",
        "none"
      ]
    }
  }
}
```

`lintConfig`에 대한 프롬프트는 사용자가 `lint` 프롬프트에 yes라고 대답했을때에 만 트리거됩니다.

##### 사전 등록된 Handlebars 헬퍼

일반적으로 사용되는 Handlebars 헬퍼인 `if_eq`와 `unless_eq`는 사전에 등록되어 사용할 수 있습니다.

``` handlebars
{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
```

##### 사용자 정의 Handlebars 헬퍼

메타 데이터 파일의 `helpers` 속성을 사용하여 추가 Handlebars 헬퍼를 등록 할 수 있습니다. 객체의 키는 헬퍼 이름입니다.

``` js
module.exports = {
  helpers: {
    lowercase: str => str.toLowerCase()
  }
}
```

등록시 다음과 같이 사용할 수 있습니다.

``` handlebars
{{ lowercase name }}
```

#### 파일 필터

메타 데이터 파일의 `filters` 필드는 파일 필터링 규칙을 포함하는 해시 객체여야합니다. 각 항목에 대해 키는 [minimatch glob 패턴](https://github.com/isaacs/minimatch)이고 값은 프롬프트 응답 데이터의 컨텍스트에서 처리된 JavaScript 표현식입니다. 예:

``` json
{
  "filters": {
    "test/**/*": "needTests"
  }
}
```

`test`에 있는 파일은 사용자가 `needTests`에 대한 프롬프트에 대해 yes라고 답한 경우에만 생성됩니다.

minimatch의 `dot` 옵션은`true`로 설정되어 있습니다. 그래서 glob 패턴은 기본적으로 dotfile과 일치합니다.

#### Skip 렌더링

메타 데이터 파일의 `skipInterpolation` 필드는 [minimatch glob 패턴](https://github.com/isaacs/minimatch)이어야 합니다. 일치하는 파일은 렌더링을 건너 뜁니다. 예:

``` json
{
  "skipInterpolation": "src/**/*.vue"
}
```

#### meta.{js, json}에서 사용할 수 있는 추가 데이터

- `destDirName` - 목적지 디렉터리 이름

```json
{
  "completeMessage": "To get started:\n\n  cd {{destDirName}}\n  npm install\n  npm run dev"
}
```

- `inPlace` - 현재 디렉터리에 템플릿 생성

```json
{
  "completeMessage": "{{#inPlace}}To get started:\n\n  npm install\n  npm run dev.{{else}}To get started:\n\n  cd {{destDirName}}\n  npm install\n  npm run dev.{{/inPlace}}"
}
```

### 특정 템플릿 버전 설치하기

`vue-cli`는 공식 템플릿을 다운로드하기 위해 [`download-git-repo`](https://github.com/flipxfx/download-git-repo) 도구를 사용합니다. `download-git-repo` 도구는 파운드 기호 (`#`) 뒤에 원하는 브랜치 이름을 추가하여 저장소에 대한 특정 브랜치를 가져올 수 있도록 합니다..

특정 공식 템플릿에 필요한 포맷은 다음과 같습니다.

``` bash
vue init <템플릿 이름>#<브랜치 이름> <프로젝트 이름>
```

예제:

webpack-simple vue 템플릿의 [`1.0` branch](https://github.com/vuejs-templates/webpack-simple/tree/1.0) 설치하기:

``` bash
vue init webpack-simple#1.0 mynewproject
```


### 라이센스

[MIT](http://opensource.org/licenses/MIT)
