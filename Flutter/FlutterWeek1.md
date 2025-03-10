# Flutter 환경 구성 및 'Hello World' 앱 실행하기
## Flutter 환경 구성하기
안드로이드 스튜디오는 저번 학기 수업으로 인해 설치되어 있음.
- Flutter 플러그인을 안드로이드 스튜디오에서 설치.
- Flutter 공식 홈페이지에서 **Flutter SDK**를 3.29.0 버전으로 다운로드
- Flutter SDK path에 다운로드 받은 Flutter SDK 폴더 연결
## 'Hello World' 앱 실행하기
- New Flutter Project 클릭
- hello_world라는 이름으로 프로젝트 생성
- 다음 코드를 **main.dart**에 작성한 후 브라우저로 실행
```
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(// 최상단 그릇
      home: Scaffold(// home: 필수적으로 필요한 요소 Scaffold: 발판, 앱을 구성하기 위한 뼈대
        appBar: AppBar(
          title: Text('Hello World'),
        ),
        backgroundColor: Colors.black,
          body: Center( // 몸통, 중간
            child: Text( // child: 자식, Text: 글자 위젯
              'Hello World', // Text에 들어갈 글자
              style: TextStyle( // 글자 스타일
                fontSize: 40.0, // 글자 크기
                color: Colors.yellow, // 글자 색
              ),
              ),
          ),
      ),
    ),
  );
}
```

