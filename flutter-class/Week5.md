# 기본 위젯
## 과제1 주어진 화면 만들기
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

## 과제2 계산기 만들기
```
import 'package:flutter/material.dart';

void main() => runApp(CalculatorUI());

class CalculatorUI extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.black,
        body: SafeArea(
          child: Column(
            children: [
              // 디스플레이 영역
              Expanded(
                flex: 2,
                child: Container(
                  alignment: Alignment.bottomRight,
                  padding: EdgeInsets.all(20),
                  child: Text(
                    '0',
                    style: TextStyle(
                      fontSize: 48,
                      color: Colors.white,
                    ),
                  ),
                ),
              ),

              // 버튼 영역
              Expanded(
                flex: 5,
                child: Column(
                  children: [
                    _buildButtonRow(['%', 'CE', 'C', '⌫']),
                    _buildButtonRow(['1/x', 'x²', '√x', '÷']),
                    _buildButtonRow(['7', '8', '9', '×']),
                    _buildButtonRow(['4', '5', '6', '−']),
                    _buildButtonRow(['1', '2', '3', '+']),
                    _buildButtonRow(['±', '0', '.', '=']),
                  ],
                ),
              ),
            ],
          ),
        ),
      ),
      debugShowCheckedModeBanner: false,
    );
  }

  // 버튼 행 생성기
  Widget _buildButtonRow(List<String> labels) {
    return Expanded(
      child: Row(
        children: labels.map((label) {
          final isEqualButton = label == '=';
          return Expanded(
            child: Padding(
              padding: const EdgeInsets.all(1.5),
              child: Container(
                decoration: BoxDecoration(
                  color: isEqualButton ? Colors.lightBlue : Colors.grey[850],
                  borderRadius: BorderRadius.circular(4),
                ),
                child: Center(
                  child: Text(
                    label,
                    style: TextStyle(
                      color: Colors.white,
                      fontSize: 22,
                    ),
                  ),
                ),
              ),
            ),
          );
        }).toList(),
      ),
    );
  }
}
```
