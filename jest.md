# jest, cross-env, @jest/globals 모듈 설치
```
# DevDependencies로 jest, cross-env 를 설치합니다.
yarn add -D jest cross-env @jest/globals
```

# Jest Configs 설정하기
Jest 설정하기: jest.config.js
* 특정 경로의 테스트 파일을 무시하도록 설정하고, 모든 Test Case (expect)의 결과값 출력을 설정하였습니다.
  ```
  // jest.config.js

export default {
  // 해당 패턴에 일치하는 경로가 존재할 경우 테스트를 하지 않고 넘어갑니다.
  testPathIgnorePatterns: ['/node_modules/'],
  // 테스트 실행 시 각 TestCase에 대한 출력을 해줍니다.
  verbose: true,
};
```
[Configuring Jest](https://jestjs.io/docs/configuration)

# Jest Scripts 설정하기
 Jest CLI Script 설정하기: package.json
테스트 코드의 실시간 모니터링을 진행하거나, 결과값을 별도의 파일로 생성하거나, 테스트 코드의 커버리지를 확인하는 등 다양한 옵션을 설정
```
// package.json

{
  ...

  "scripts": {
    ...

    "test": "cross-env NODE_ENV=test NODE_OPTIONS=--experimental-vm-modules jest --forceExit",
    "test:silent": "cross-env NODE_ENV=test NODE_OPTIONS=--experimental-vm-modules jest --silent --forceExit",
    "test:coverage": "cross-env NODE_ENV=test NODE_OPTIONS=--experimental-vm-modules jest --coverage --forceExit",
    "test:unit": "cross-env NODE_ENV=test NODE_OPTIONS=--experimental-vm-modules jest __tests__/unit --forceExit"
  },

  ...
}
```

# cross-env 모듈이란?
```
cross-env는 OS마다 다른 환경 변수 설정 방식을 일괄적으로 통일해주는 모듈입니다.
```
macOS는 NODE_ENV=test 형식으로 환경 변수를 설정하지만, Windows에서는 set NODE_ENV=test 로 설정해야합니다.
cross-env는 이러한 OS 종속적인 부분을 일관된 문법으로 사용할 수 있게 해줍니다.

# Jest CLI Options
- `--forceExit`
    - 테스트 코드 검사가 완료되었을 때, 강제로 **Jest**를 종료합니다.
    - **express**의 `app` 객체와 **Prisma** 연결이 `Connect`상태로 남아있어 테스트 코드가 종료되지 않을 때 사용합니다.
- `--silent`
    - 테스트 코드를 실행했을 때, `console.log`와 같은 메시지를 출력하지 않습니다.
- `--coverage`
    - 테스트 코드 검사가 완료된 후 현재 프로젝트의 **테스트 코드 커버리지**를 출력해줍니다.
    - `--coverage` 옵션 이미지
        - `**--coverage` 설정을 하지 않은 경우**
            - 테스트 파일을 기준으로 결과가 출력됩니다.
            
            ![스크린샷 2023-08-09 오후 11.33.32.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/300b3a50-91d3-41b5-bf81-f4a9f789039e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.33.32.png)
            
        - `**--coverage` 설정을 한 경우**
            - 전체 프로젝트의 커버리지가 출력됩니다.
            
            ![스크린샷 2023-08-09 오후 11.34.11.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04eaab34-c2d5-47b3-8d82-756d43e4e0a2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.34.11.png)
            
        
- `--verbose`
    - 테스트 코드의 **개별 테스트 결과**를 표시해줍니다.
    - `--verbose` 옵션 이미지
        - `**--verbose` 옵션 설정을 하지 않은 경우**
            - 테스트 파일을 기준으로 결과가 출력됩니다.
            
            ![스크린샷 2023-08-09 오후 11.33.32.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/300b3a50-91d3-41b5-bf81-f4a9f789039e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.33.32.png)
            
        - `**--verbose` 옵션 설정을 한 경우**
            - 테스트 파일의 `test()`를 기준으로 결과값이 출력됩니다.
            - 테스트 결과를 명확하게 볼 수 있어 **디버깅할 때 유용**하게 사용할 수 있습니다.
            
            ![스크린샷 2023-08-09 오후 11.34.56.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a50c8fda-5c7c-498c-b319-af903fb89b16/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-08-09_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.34.56.png)

[Jest CLI Options](https://jestjs.io/docs/cli

# 자주 사용하는 Jest 문법 정리
- **expect 결과값 검증하기**
    - **`.mockReturnValue(value)`**
        - Mock 함수의 **반환값**을 지정합니다.
    - `**.toBe(value)**`
        - 입력받은 예상값과 결과값이 일치하는지 비교합니다.
        - 만약 **객체 인스턴스**를 비교하려 한다면, **인스턴스** **ID**까지 비교하므로 **엄격하게** 동일한지 검증합니다.
    - **`.toEqual(value)`**
        - 입력받은 예상값과 결과값이 일치하는지 비교합니다.
    - **`.toMatch(regexp | string)`[](https://jestjs.io/docs/expect#tomatchregexp--string)**
        - 입력받은 문자열이 결과값과 같은지 검증합니다.
        - **String** 또는 **정규표현식**으로 검증할 수 있습니다.
    - **`.toBeTruthy()`[](https://jestjs.io/docs/expect#tobetruthy)**
        - 결과값이 `true`인지 검증합니다.
    - **`.toBeInstanceOf(Class)`[](https://jestjs.io/docs/expect#tobeinstanceofclass)**
        - 입력받은 예상값과 **Class**가 동일한 **Instance**인지 검증합니다.
        - **Error**를 검증할 때 주로 사용합니다.
    - **`.toHaveProperty(keyPath, value?)`[](https://jestjs.io/docs/expect#tohavepropertykeypath-value)[](https://jestjs.io/docs/expect#tobetruthy)**
        - 입력받은 객체의 **Key**와 **Value**가 일치하는지 검증합니다.
    - **`.toMatchObject(object)`[](https://jestjs.io/docs/expect#tomatchobjectobject)[](https://jestjs.io/docs/expect#tobetruthy)**
        - 입력받은 객체와 결과 객체가 일치하는지 검증합니다.
        - 만약, 입력받은 객체에는 없지만, 결과 객체에 있는 속성이 있다면 **이를 무시**하고 일치 여부를 확인합니다.

- **Global Jest 문법**
    - `**afterAll(fn, timeout)**`
        - **모든** `test()`가 **완료된 이후**에 수행됩니다.
        - 테스트가 완료된 이후 DB에 변경된 데이터를 삭제하거나 Mock을 초기화 하기 위해 사용됩니다.
    - `**afterEach(fn, timeout)**`
        - **각** `test()`가 **완료된 이후**에 수행됩니다.
        - 테스트코드가 완료된 이후 Mock 또는 변경된 전역 변수를 초기화할 때 사용됩니다.
    - `**beforeAll(fn, timeout)**`
        - **테스트 코드**가 **실행되기 전** **최초로** 수행됩니다.
        - DB의 데이터를 초기화하거나 전역 Mock을 초기화할 때 사용됩니다.
    - `**beforeEach(fn, timeout)**`
        - **각** `test()`가 **실행되기 전**에 수행됩니다.
        - 테스트가 실행되기 전, 동일한 설정을 반복해야할 때 사용됩니다.

# Global Jest 문법의 실행 순서
before after가 실행되는 순서 정리
```
// before-after-grammars.spec.js

beforeAll(() => console.log('1 - beforeAll'));
afterAll(() => console.log('1 - afterAll'));
beforeEach(() => console.log('1 - beforeEach'));
afterEach(() => console.log('1 - afterEach'));

test('', () => console.log('1 - test'));

describe('Scoped / Nested block', () => {
  beforeAll(() => console.log('2 - beforeAll'));
  afterAll(() => console.log('2 - afterAll'));
  beforeEach(() => console.log('2 - beforeEach'));
  afterEach(() => console.log('2 - afterEach'));

  test('', () => console.log('2.1 - test'));

  test('', () => console.log('2.2 - test'));
});

/** Print
 *
 *     1 - beforeAll
 *       at Object.<anonymous> (test/jest-grammars/before-after.spec.test.js:1:45)
 *
 *     1 - beforeEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:3:26)
 *
 *     1 - test
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:6:24)
 *
 *     1 - afterEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:4:25)
 *
 *     2 - beforeAll
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:9:27)
 *
 *     1 - beforeEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:3:26)
 *
 *     2 - beforeEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:11:28)
 *
 *     2.1 - test
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:14:26)
 *
 *     2 - afterEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:12:27)
 *
 *     1 - afterEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:4:25)
 *
 *     1 - beforeEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:3:26)
 *
 *     2 - beforeEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:11:28)
 *
 *     2.2 - test
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:16:26)
 *
 *     2 - afterEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:12:27)
 *
 *     1 - afterEach
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:4:25)
 *
 *     2 - afterAll
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:10:26)
 *
 *     1 - afterAll
 *       at Object.log (test/jest-grammars/before-after.spec.test.js:2:24)
 * **/
```
[Globals](https://jestjs.io/docs/api)

# Mock Functions
```
<aside>
**[Mock](https://jestjs.io/docs/mock-functions)**은 **특정 메서드나 함수를 Mocking**하기 위해 사용됩니다.

즉, 테스트에서 **시간** 또는 **비용**이 많이들거나, **의존성이 높은 코드**를 **직접 실행하지 않고** 호출 여부, 입력한 값의 일치 여부와 같은 정보를 확인하기 위해 사용하는 **가짜 객체**입니다.

</aside>
```
코드를 실행했을 때 **문제가 발생**하거나 로직을 검사하는데 방해가 되는 코드를 **실제로 실행한 것처럼** 만들기 위해 **Mock**이라는 **가짜 객체**를 사용하게 됩니다.

**Mock 객체**는 테스트 코드에서 **특정 코드를 실행하지 않고, 원하는 부분만을 테스트하고 싶을 때** 실제로 존재하는 값처럼 사용할 수 있도록 만들어놓은 **가짜 객체**입니다.

예를 들어, **Repository Layer**에서 테스트 코드를 실행할 때 마다 DB에 접근하여 매번 새로운 데이터를 **생성**하거나, **삭제**한다면 좋지 않은 방법일것입니다.

**Repository**가 사용하는 **DB를 Mocking**하게 된다면, **실제 DB에 접근하지 않고도** 특정한 값이 입력되었을 때 어떤 결과가 나오는지 임의로 설정하여 **DB에 접근했을 때와 동일한 상황을 예상**하여 코드를 작성할 수 있게 됩니다. 

또한 **Mock 객체**의 특정 메서드가 **몇번 호출**되었는지, **어떤 값을 전달**받았는지, **전달받은 데이터의 형식**은 내가 생각한것이 맞는지 등 다양한 조건을 검사할 수 있습니다. 😊

![Mocking된 경우 외부 환경을 배제하고 독립적인 환경에서 테스트를 진행할 수 있습니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2f2d4dba-1f1f-41a3-805f-82d4df29f10c/Mocking_Object.png)

Mocking된 경우 외부 환경을 배제하고 독립적인 환경에서 테스트를 진행할 수 있습니다.

**자주 사용하는 Mock expect 문법**

- **`.toHaveBeenCalledTimes(number)`[](https://jestjs.io/docs/expect#tohavebeencalledtimesnumber)**
    - **Mock**이 몇번 호출되었는지 검증합니다.
- **`.toHaveBeenCalledWith(arg1, arg2, ...)`[](https://jestjs.io/docs/expect#tohavebeencalledwitharg1-arg2-)**
    - 어떤 인자를 이용해 **Mock**이 호출되었는지 검사합니다.
[Mock Functions](https://jestjs.io/docs/mock-function-api)
