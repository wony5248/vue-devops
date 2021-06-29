# vue-devops

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Run your unit tests
```
yarn test:unit
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


# process


### 사전 환경 구성
* yarn 이용

``` 
npm install yarn
yarn global add @vue/cli
vue -V
```

### Vue 프로젝트 생성 및 실행
* 유저 정보 확인
```
git config -l
```
* 프로젝트 생성
```
vue create vue-devops
cd vue-devops
yarn serve
```


### github repository 생성 및 연동
* vue-devops라는 이름의 repository 생성
``` 
git remote add origin https://github.com/wony5248/vue-devops.git
git push -u origin master
```

### 배포하기 위한 라이브러리 추가
```
yarn add gh-pages -D
```
* package.json 수정
```
"scripts": {
        "serve": "vue-cli-service serve",
        "build": "vue-cli-service build",
        "predeploy": "vue-cli-service build",
        "deploy": "gh-pages -d dist",
        "clean": "gh-pages-clean",
        "test:unit": "vue-cli-service test:unit",
        "lint": "vue-cli-service lint"
    },
```

### publicPath 설정
*최상단 디렉토리에 vue-config.js 생성
```
module.exports = {
    publicPath: "/vue-devops/",
    outputDir: "dist"
}
```

### 배포
```
yarn deploy
```

### github Actions workflow 배포 자동화
* github actions -> simple workflow -> deploy.yml 수정
* name : Deployment로 수정 -> commit -> pull


### deploy.yml 파일 수정
```
jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@master

      - name: Set up Node.js
        uses: actions/setup-node@master
        with:
          node-version: 14.x

      - name: Install dependencies
        run: yarn install
      
      - name: Test unit
        run: yarn test:unit

      - name: Build page
        run: yarn build
        env:
          NODE_ENV: production

      - name: Deploy to gh-pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```
* commit -> push






