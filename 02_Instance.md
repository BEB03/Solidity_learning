# 02. 인스턴스

## instance

같은 파일 내의 다른 컨트랙트에 접근할 수 있는 방법

```
contract A {
    uint public a = 5;
}

contract B {
    // 컨트랙트이름 변수명(직접 정함) = new 컨트랙트이름();
    A instance = new A();
    // 접근은 . 으로
    function () {
        instance.a // = 5임
    }
}
```

인스턴스는 복사해서 가져오는 것이다. 따라서 가져온 인스턴스의 내용을 바꾸어도 원래 컨트랙트 (A) 에는 영향이 없음. 그 반대도 마찬가지. A의 값을 변경해도 B의 instance 에는 영향 없음

## constructor

컨트랙트의 state variable을 초기화 하는 기능을 가지고 있음, 배포나 인스턴스 생성 시 해당 컨스트럭터에 알맞게 인수를 넣어줘야 함.

```
contract A {
    uint public value;
    constructor (uint _value) {
        value = _value;
    }
}

contract B {
    A instance = new A(10000);
}
```
