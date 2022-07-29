# 09. enum, Interface, Library, Import

## enum

enum은 상수 세트로, 각 상수에 이름을 붙여줄 수 있다.

```
// enum 선언
enum CarStaus {
    TurnOff,
    TurnOn,
    Drive,
    Stop
}

// enum 생성
Carstatus public = carstatus; // carstatus 라는 enum 생성

// 접근
carstatus = Carstatus.TurnOn; // 선언했던 enum의 요소를 . 으로 접근
carstatus = Carstatus(2); // 요소를 0,1,2... 순서로 숫자로도 접근 가능하다. 이 코드는 carstatus = Carstatus.Drive; 와 같음.
carstatus는 (리턴, 이벤트 기록 시 등) 정수 값을 가지나 Carstatus 자료형이므로 uint로 사용하려면 타입을 명시적 변경을 해 주어야 한다.
```

## interface

interface는 컨트랙트 내에서 정의되어야 할 것들을 규정한다.

- 다른 컨트랙트에서 interface의 함수를 참고해야 하므로 external로 작성함.
- enum, struct 사용 가능
- 변수, 생성자 **사용 불가**

```
interface A {
    struct item {
        string name;
        uint256 price;
    }
    function add(string _name, uint256 _price) external;
}

contract B is A { // is 로 인터페이스를 적용한다.

    item[] public itemList; // 인터페이스에 적용된 item을 바로 가져다 쓸 수 있다.

    function add (string memory _name, uinty256 _price) override public {
        itemList.push(item(_name,_price));
    }
    // 인터페이스에서 정의했던 함수는 인터페이스를 사용하는 컨트랙트에서도 반드시 같은 모양으로 정의가 되어 있어야 한다. 그러지 않는다면 에러 발생
}
```

## Library

여러 스마트컨트랙트에서 공통으로 사용되는 함수들을 하나의 컨트랙트에 넣어 두고 사용하는 방식

- 재사용성이 좋음
- 가스 소비 줄임 (반복되는 부분을 라이브러리로 해결할 수 있으므로 컨트랙트 길이가 줄어듦)
- 데이터 타입 적용 가능

특징은 다음과 같다.

- fallback 사용 불가
- payable 사용 불가
- 상속 불가

오버플로우 방지하는 라이브러리 예시를 보자.

```
// 라이브러리 정의
library safeMath {
    function add(uint8 a, uint8 b) internal pure returns (uint8) {
        require(a+b >= a, "safeMath addiction overflow");
        return a + b;
    }
}

// 사용
contract A {
    using safeMath for uint8; // 사용하는 법;
    uint public a;

    function overFlow(uint8 _num1, uint8 _num2) public { // _num1, _num2 는 safeMath가 적용되었음.
        a = _num1.add(_num2); // _num1에 바로 safeMath의 함수를 사용할 수 있음
        a = safeMath.add(_num1, _num2) // 또는 이렇게도 사용 가능
    }
}

```

- **0.8.0부터는 오버플로우 방지를 솔리디티에서 기본적으로 지원함.**

## import

파일 간 서로 내용을 사용할 수 있도록 하는 것임. 세미콜론 붙여야 함

```
import './example.sol'; // 가져올 파일의 주소를 넣어줌
./ 같은 폴더
../ 상위 폴더
```
