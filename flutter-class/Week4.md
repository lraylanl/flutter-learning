# 프로젝트 구조와 앱 구조

## 과제

```
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

