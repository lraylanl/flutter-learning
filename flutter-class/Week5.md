# 기본 위젯
## 과제1
```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: SafeArea(
          child: Column(
            children: [
              Expanded(
                flex: 1,
                child: Row(
                  children: [
                    // 빨강
                    Expanded(
                      flex: 2,
                      child: Container(color: Colors.red),
                    ),
                    // 파랑 + 검정 + 주황
                    Expanded(
                      flex: 2,
                      child: Column(
                        children: [
                          // 파랑
                          Expanded(
                            flex: 1,
                            child: Container(color: Colors.blue),
                          ),
                          // 검정 + 주황
                          Expanded(
                            flex: 1,
                            child: Row(
                              children: [
                                // 검정
                                Expanded(
                                  flex: 1,
                                  child: Container(color: Colors.black),
                                ),
                                // 주황
                                Expanded(
                                  flex: 1,
                                  child: Container(color: Colors.orange),
                                ),
                              ],
                            ),
                          ),
                        ],
                      ),
                    ),
                  ],
                ),
              ),
              // 노랑
              Expanded(
                flex: 1,
                child: Container(color: Colors.yellow),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
