# Node 테스트 프로젝트를 GitHub Actions로 실행

강의자료 `4.GitHub.pdf` 73~79쪽 실습입니다.
저장소: https://github.com/jiwon28/githubaction-sample

## 로컬 실행

Node.js 24를 설치한 터미널에서 실행합니다.

```sh
npm ci
npm test
```

`Default Test Set`의 테스트 2개가 실행되어 `2 passing`이 표시됩니다.
강의 예제 그대로 로그를 출력하는 테스트이며, 실제 비즈니스 로직을 검증하는 assertion은 없습니다.

## GitHub Actions 확인

1. 코드를 수정한 뒤 `main` 브랜치에 commit/push합니다.
2. 저장소의 **Actions → Node.js CI → 실행 항목 → build (24.x)**를 엽니다.
3. **Run Mocha tests** 단계에서 `2 passing`과 전체 작업의 초록색 성공 표시를 확인합니다.

`main` 대상 pull request에서도 실행됩니다. **Actions → Node.js CI → Run workflow**로 수동 실행할 수도 있습니다.

## 강의 예제에서 조정한 부분

- 저장소 이름은 사용자가 지정한 `githubaction-sample`을 사용합니다.
- Node 20 대신 Node 24, checkout/setup-node는 v6를 사용합니다.
- Mocha는 개발 의존성으로 설치하고 `package-lock.json`을 커밋합니다.
- Actions에서 `npm install` 대신 `npm ci`로 잠금 파일의 버전을 설치합니다.
- npm scripts에서는 `mocha test.spec.js`로 실행하여 Windows에서도 동일하게 사용합니다.
- 강의의 `start` 명령은 대상 파일 `bin/www`가 이 테스트 프로젝트에 없으므로 넣지 않습니다.
- 빌드 스크립트가 없으므로 `npm run build --if-present`는 정상적으로 건너뜁니다.

워크플로 파일: `.github/workflows/node.js.yml`

공식 참고: https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs
