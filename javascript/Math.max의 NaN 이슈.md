## Math.max에서 NaN이 발생하는 이유

```
/** 문제 상황 */
If at least one of arguments cannot be converted to a number, the result is NaN.
```

배열 중 하나라도 Number 타입이 아닌 경우 NaN이 발생하게 됩니다.
아래와 같은 경우는 혼란스럽습니다.

```javascript
Math.max([1, 2, 3]);
```

분명 배열을 부여하고 Math.max를 돌렸으니 최대 값을 찾아주지 않을까 라는 생각을 하지만, Java와 달리 JavaScript에서는 `[1,2,3]`을 `"1,2,3"`으로 컨버팅을 합니다. 그렇기 때문에 문자열에서 최대 값을 찾으라고 지시를 하니 NaN이 발생하게 됩니다.

```javascript
Math.max([23]); // return 23
```

위의 코드는 정상적으로 작동합니다.
그 이유는 `[23] > "23" > 23` 숫자로 제대로 변형이 되기 때문입니다.
Math.max()에서 배열을 원하는 결과로 배열을 만들고자 한다면 아래와 같이 사용을 할 수 있습니다.

```javascript
Math.max.apply(Math, [1, 2, 3]);
```

apply() 메서드는 주어진 this 값과 배열(또는 배열과 유사한 객체)로 제공된 인수로 지정된 함수를 호출합니다. 이 방법 이외에 쉬운 방법으로도 접근을 할 수 있습니다.

```javascript
Math.max(...[1, 2, 3]); // ...[1,2,3] > 1,2,3
```

위와 같이 spread operator(스프레드 연산자)를 이용하여 `...`을 사용하면 배열이 분해되어 각각의 숫자 배열에서 최대 값을 정상적으로 찾을 수 있습니다.
