# 03. 상속 & event

## event

EVM 로깅 환경을 계약의 현재 상태에 대한 정보를 알리는데 사용된다.  
다른 언어의 print 역할을 한다고 보면 될 듯. 이벤트 값은 블록 내부에 저장하므로 계속 꺼내쓸 수 있다.

```
// 선언
event 이름(파라미터);
event ageRead(address, int); 이름을 제외하고 자료형만 지정할 수 있다.
```

```
function () {
    // 코드
    emit ageRead(personIdentifier, stateIntVariable); // 이벤트 호출, 자료형 순서에 맞게 작성 즉 personIdentifier는 address 여야한다.
}
```

- indexed : 특정한 이벤트의 값을 가져올 때 사용한다. 잘 이해는 못했는데 이벤트 값에 index를 붙여서 이벤트 값을 가져올 때 (js에서라든가) 조건을 지정할 수 있도록 쓰이는 것 같다. 나중에 실습 한 번 해봐야 할 듯.

```
event Add(uint indexed tx);
```
