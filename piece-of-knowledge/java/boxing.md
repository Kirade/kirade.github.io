---
description: https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html
---

# Boxing

_Autoboxing_ 은 자바 컴파일러에 의해 원시 타입과 원시 타입에 대응하는 래퍼 클래스 사이에서 발생하는 자동 변환이다. 예를 들어 원시타입 `int`는 `Integer` 로, `double` 은 `Double` 로 대응해서 변환된다. 만약 변환이 반대로 이루어지면 이것을 _unboxing 이라고 한다._

이런 기능을 제공하는 이유는 개발자들이 더 깔끔한 코드를 작성할 수 있게 하기 위함이다.

### Autoboxing

```
Character ch = 'a';
```

원시 타입인 'a' 가 대응하는 래퍼 클래스인 `Character` 로 자동 변환 되었다.

```
List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(i);
```

`List` 타입인 li 는 `Integer` 타입을 원소로 받지만 원시타입이 추가가 정상적으로 이뤄진다. 런타임에는 다음과 같은 형변환이 자동으로 이루어진다.

```
List<Integer> li = new ArrayList<>();
for (int i = 1; i < 50; i += 2)
    li.add(Integer.valueOf(i));
```

Autoboxing 이 일어나는 조건은 다음과 같다.

* 원시 타입에 대응하는 래퍼 클래스를 매개변수로 받는 함수에 원시 타입이 전달되는 경우
* 대응하는 래퍼 클래스의 변수로 원시 타입이 할당되는 경우

```
public static int sumEven(List<Integer> li) {
    int sum = 0;
    for (Integer i: li)
        if (i % 2 == 0)
            sum += i;
        return sum;
}
```

`Integer` 타입에 대해서 % 혹은 += 등의 연산은 지원하지 않음에도 불구하고 위의 코드가 작성하는 이유는 런타임에 아래와 같이 적절하게 형변환이 되기 때문이다.

```
public static int sumEven(List<Integer> li) {
    int sum = 0;
    for (Integer i : li)
        if (i.intValue() % 2 == 0)
            sum += i.intValue();
        return sum;
}
```

### Unboxing

반대로 원시 타입에 대응하는 래퍼 클래스가 원시타입으로 변환되는 것을 Unboxing 이라고 한다. Unboxing 이 일어나는 조건은 다음과 같다.

* 원시 타입을 매개변수로 받는 함수에 대응하는 래퍼 클래스가 전달되는 경우
* 대응하는 원시 타입의 변수로 래퍼 클래스가 할당되는 경우

```
import java.util.ArrayList;
import java.util.List;

public class Unboxing {

    public static void main(String[] args) {
        Integer i = new Integer(-8);

        // 1. Unboxing through method invocation
        int absVal = absoluteValue(i);
        System.out.println("absolute value of " + i + " = " + absVal);

        List<Double> ld = new ArrayList<>();
        ld.add(3.1416);    // Π is autoboxed through method invocation.

        // 2. Unboxing through assignment
        double pi = ld.get(0);
        System.out.println("pi = " + pi);
    }

    public static int absoluteValue(int i) {
        return (i < 0) ? -i : i;
    }
}
```

위 코드의 실행 결과는 다음과 같다.

```
absolute value of -8 = 8
pi = 3.1416
```

### 원시 타입과 래퍼 클래스

| Primitive type | Wrapper class |
| -------------- | ------------- |
| boolean        | Boolean       |
| byte           | Byte          |
| char           | Character     |
| float          | Float         |
| int            | Integer       |
| long           | Long          |
| short          | Short         |
| double         | Double        |

