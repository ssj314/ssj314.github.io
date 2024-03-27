---
title: 비동기 프로그래밍
posted: YYYY-MM-DD hh:mm:ss +09:00
category: ["개발", "Flutter"]
---

## 목차
1. Future 클래스
2. Async와 Await 키워드
3. Stream 클래스

---
네트워크를 통해 데이터를 가져오거나, 파일로 부터 데이터를 읽는 등 일정 시간이 소요되는 작업은 비동기로 처리해야 한다. 그렇지 않으면 다음 코드는 이전 작업이 완료될 때까지 기다려야하는 문제가 발생한다. Dart는 async, await 키워드를 통해 비동기 작업을 지원한다.

## Future
---
Dart는 모든 비동기 작업의 결과를 **Future** 인스턴스를 통해 나타낸다. **Future**는 미완료 또는 완료 상태를 가지지만, 작업이 완료되더라도 값으로 바뀌지는 않는다.
```dart
Future<String> fetchMsg() {
	final duration = Duration(seconds: 2);
	final message = "Hello World";
	return Future.delayed(duraction, message);
}
```
`fetchMsg` 함수는 지연이 발생하는 비동기 작업이다. 따라서, 함수 결과가 Future 클래스에 포장되어서 주어진다.

### then 메서드
Future 클래스로 포장된 결과에 접근하기 위해선 **then** 메서드를 이용해야 한다. 이 키워드는 비동기 작업이 끝났을 때 코드를 실행할 수 있게 해 준다.
```dart
final result = fetchMsg();    // Future<String>
result.then((value) {
	print(value);             // "Hello World"
});
```

## Async와 Await
---
**async**와 **await** 키워드는 비동기 작업을 명시적으로 정의하는 방법이다. 두 키워드를 사용하려면 반드시 두 가지 규칙을 지켜야 한다.

1. 비동기 함수를 정의하려면, async 키워드를 추가하라
2. await 키워드를 사용하려면 async 함수로 선언하라



**await** 키워드는 작업이 끝날 때까지 코드를 중단시켜준다. **await**을 이용하면 비동기 함수가 되므로 리턴 타입을 **Future**로 표시한다.
```dart
Future<String> delayedFn() async {
	Future.delayed(Duration(seconds: 2));
	return "Hello World";
}
```

## Stream
---
만약, 어떤 데이터가 꾸준히 로딩될 필요가 있다면 어떻게 처리해야 할까? 실시간 교통 정보같이 불특정 시간에 데이터가 계속 업데이트된다면 분명 위에서 배운 것만으로는 해결할 수 없을 것이다. 이럴 때 스트림을 이용하면 된다.

### 작동 방식
스트림은 기본적으로 비동기 이벤트에 가깝다. 스트림은 Iterable 타입으로 데이터를 반환하기 때문에 프로그램에 변화를 알릴 수 있다. 아래 코드를 살펴보자.
```dart
Stream<int> generateInt(int n) async* {
	final duration = Duration(seconds: 1);
	for(int i = 0; i < n; ++i) {
		await Future.delayed(duration);
		yield i;
	}
}
```
이 함수는 1부터 n까지 수를 1초마다 생성한다. 이와 같은 비동기 이벤트에 접근하려면 await for-loop를 이용해야 한다.
```dart
final stream = generateInt(10);
await for(var event in stream) {
	print(event);                  // 1, 2, ... , 10
}
```
비동기 이벤트는 Future와 달리 접근 시작하는 순간부터 실행된다.

### listen 메서드
Future의 then과 마찬가지로 Stream도 데이터에 접근할 수 있는 **listen** 메서드가 존재한다.
```dart
final result = generateInt(10);    // Future<String>
result.listen((value) {
	print(value);                  // 1, 2, ..., 10
});
```
