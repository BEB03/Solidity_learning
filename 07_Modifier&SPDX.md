# 07. Modifier & SPDX

## 함수 값 리턴 방법

함수 값 리턴시 리턴값의 명칭을 적을 수 있음

```
function add (uint256 x, uint256 y) public pure returns (uint256 total) {
    total = x + y;
    return total;
}
```

## modifier (수정자)

함수에 적용해 함수보다 먼저 실행되는 것. 유효성 검증등을 깔끔하게 할 수 있다. **코드의 재사용 관점에서 유용**하다.

```
modifier onlyBy(parameter) {
    if (msg.sender == personIdentifier) {
        _; // 수정자가 적용된 해당 함수를 의미한다. 따라서 다른 코드가 있으면 순서에 영향을 받는다.
    }
}
```

```
function getAge(address _personIdentifier) **onlyBy()** payalbe external returns (uint) {

}
```

- **payable은 수정자이다.**

## 라이센스

- **0.6.8부터 라이센스가 도입되었다. 이떄부터는 이것을 쓰지 않으면 경고가 뜸.**

```
// SPDX-License-Identifier: MIT

```

## 주석

```
// 단일행
/* 여러
줄
주석 */
```
