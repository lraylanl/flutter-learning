
# 프로젝트 구조와 앱 구조

## 과제: 현재 시각을 표시하는 앱

```dart
import 'dart:async';
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '현재 시각 앱',
      home: TimeDisplayScreen(),
    );
  }
}

class TimeDisplayScreen extends StatefulWidget {
  @override
  _TimeDisplayScreenState createState() => _TimeDisplayScreenState();
}

class _TimeDisplayScreenState extends State<TimeDisplayScreen> {
  late Timer _timer;
  late DateTime _now;

  @override
  void initState() {
    super.initState();
    _now = DateTime.now();
    _timer = Timer.periodic(Duration(seconds: 1), (Timer timer) {
      setState(() {
        _now = DateTime.now();
      });
    });
  }

  @override
  void dispose() {
    _timer.cancel();
    super.dispose();
  }

  String formatDate(DateTime dt) {
    return '${dt.year}-${_twoDigits(dt.month)}-${_twoDigits(dt.day)}';
  }

  String formatTime(DateTime dt) {
    String period = dt.hour < 12 ? '오전' : '오후';
    int hour12 = dt.hour % 12 == 0 ? 12 : dt.hour % 12;
    return '$period ${_twoDigits(hour12)}:${_twoDigits(dt.minute)}:${_twoDigits(dt.second)}';
  }

  String _twoDigits(int n) => n.toString().padLeft(2, '0');

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('현재 시각'),
        centerTitle: true,
      ),
      backgroundColor: Colors.white,
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              formatDate(_now),
              style: TextStyle(fontSize: 32, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10),
            Text(
              formatTime(_now),
              style: TextStyle(fontSize: 48, fontWeight: FontWeight.w500),
            ),
          ],
        ),
      ),
    );
  }
}
```

## 코드 설명
### MyApp 클래스

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp( // 전체 앱을 감싸는 위젯
      title: '현재 시각 앱', // 앱 이름
      home: TimeDisplayScreen(), // 앱이 시작되면 TimeDisplayScreen 위젯을 보여줌
    );
  }
}
```

#### MaterialApp: build() 메서드에서 반환하는 인스턴스로  Flutter 애플리케이션의 기본적인 설정과 구조를 제공하는 데 사용  
- **UI의 기본 구조를 제공**  
- **테마 설정**  
- **내비게이션 관리**  
- **지역화 지원**  
- **디버깅 도구 제공**  

#### StatelessWidget: 클래스 상태가 없는(상태가 변하지 않는) 위젯을 정의하는데 사용  
- **불변 UI 구성**  
- **재사용 가능 (불변이므로)**  
- **렌더링 효율성이 좋음**  

### TimeDisplayScreen 클래스

```dart
class TimeDisplayScreen extends StatefulWidget {
  @override
  _TimeDisplayScreenState createState() => _TimeDisplayScreenState();
}
```

#### StatefulWidget: 동적인 상태(state)를 관리해야 하는 UI 요소를 표현할 때 사용  
- **상태 관리**  
- **UI 재구성**  
- **동적인 데이터 처리**  

#### createState(): 실제 상태를 관리하는 _TimeDisplayScreenState를 생성  

### _TimeDisplayScreenState 클래스

```dart
class _TimeDisplayScreenState extends State<TimeDisplayScreen> {
  late Timer _timer; // 1초마다 시간 갱신을 위한 타이머
  late DateTime _now; // 현재 시각을 저장하는 변수
```

#### initState(): 최초 1회 실행(시간 관련 로직 실행)

```dart
  @override
  void initState() {
    super.initState();
    _now = DateTime.now(); // 현재 시각을 가져옴
    _timer = Timer.periodic(Duration(seconds: 1), (Timer timer) {
      setState(() {
        _now = DateTime.now(); // 1초마다 현재 시각을 갱신하고 화면 새로고침
      });
    });
  }
```

#### Timer.periodic: 주기적으로 동작하는 타이머 (1초 간격)  
#### setState(): UI를 다시 그리게 함  

### 날짜/시간 포맷 함수

```dart
  String formatDate(DateTime dt) {
    return '${dt.year}-${_twoDigits(dt.month)}-${_twoDigits(dt.day)}';
  }

  String formatTime(DateTime dt) {
    String period = dt.hour < 12 ? '오전' : '오후';
    int hour12 = dt.hour % 12 == 0 ? 12 : dt.hour % 12;
    return '$period ${_twoDigits(hour12)}:${_twoDigits(dt.minute)}:${_twoDigits(dt.second)}';
  }

  String _twoDigits(int n) => n.toString().padLeft(2, '0'); // 한 자리 숫자 앞에 0을 붙여 두 자리로 만듦
```

#### formatDate: 날짜를 YYYY-MM-DD 형태로 변환  
#### formatTime: 시간을 오전/오후 HH:MM:SS 형태로 변환  
#### _twoDigits: 항상 두 자리 숫자 형태로 출력  

### 화면 그리기 (build())

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold( // 앱의 뼈대 역할
      appBar: AppBar(
        title: Text('현재 시각'),
        centerTitle: true, // 타이틀을 가운데 정렬
      ),
      backgroundColor: Colors.white,
      body: Center( // 화면 중앙에 배치
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center, // 수직 중앙 정렬
          children: [
            Text(
              formatDate(_now), // 날짜 표시
              style: TextStyle(fontSize: 32, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10), // 날짜와 시간 사이 여백
            Text(
              formatTime(_now), // 시간 표시
              style: TextStyle(fontSize: 48, fontWeight: FontWeight.w500),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### Scaffold: 앱 기본 구조 (앱바 + 바디 등)  
#### AppBar: 화면 상단에 나타나는 제목 영역 (상단에 "현재 시각" 표시)  
#### Center + Column: 중앙 정렬 + 수직 배치  
#### Text: 날짜 및 시간 텍스트 출력  
