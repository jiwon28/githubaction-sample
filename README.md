# Git Hub Action Test

`4.GitHub.pdf` 66~79쪽 실습입니다. 두 실습을 `githubaction-sample` 저장소에서 진행합니다.

## 66~72쪽: 기본 Actions

`.github/workflows/basic-ci.yml`은 main push/PR 시 다음 작업을 수행합니다.

1. `actions/checkout@v4`로 코드 가져오기
2. `Hello, GitHub Actions! 환경 설정이 완료되었습니다.` 출력
3. `actions/setup-python@v5`로 Python 3.10 설정
4. `python --version` 실행

## 73~79쪽: Node 테스트

Node 20 환경에서 다음 명령을 실행합니다.

```sh
npm install
./node_modules/.bin/mocha test.spec.js
npm test
```

Windows PowerShell에서 직접 실행할 때는 `./node_modules/.bin/mocha.cmd test.spec.js`를 사용합니다.
테스트 2개가 로그를 출력하고 `2 passing`으로 종료됩니다. 강의 예제에는 assertion이 없습니다.

`.github/workflows/node.js.yml`은 Node 20.x, checkout v4, setup-node v4를 사용합니다.
`npm install` → `npm run build --if-present` → `npm test` 순으로 실행합니다.
빌드 스크립트가 없으므로 빌드는 건너뜁니다.

강의 그대로 `start` 스크립트도 포함했지만 `bin/www`는 제공되지 않아 `npm start`는 실행할 수 없습니다.
이번 실습에서는 `npm test`만 사용합니다.

## 결과 확인

GitHub의 Actions 탭에서 `Basic CI Example`과 `Node.js CI` 실행을 각각 확인합니다.
Node 실행의 `build (20.x)` → `Run npm test` 단계에서 `2 passing`을 확인합니다.
