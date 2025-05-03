# 복잡한 UI 작성
## 과제1 값(데이터)와 값을 화면에 표현하는 로직을 구분하여 구현하는 것이 중요한 이유
### 유지보수성	
- UI와 로직을 따로 수정 가능
### 재사용성	
- 로직을 다른 UI에서도 재사용 가능
### 확장성
- 앱 규모가 커져도 안정적으로 관리
### 협업 용이	
- 디자이너와 개발자 또는 백엔드와 프론트 분업 가능
### 테스트 용이	
- 비즈니스 로직 단독 테스트 가능

## 과제2 7장의 코드에 값과 화면 구성을 구분해서 화면 구성을 좀 더 효과적으로 전개
### data.dart에 데이터 분리
#### Page1.dart
```
import 'package:flutter/material.dart';
import 'package:carousel_slider/carousel_slider.dart';
import 'data.dart';

class Page1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ListView(
      children: [
        _buildTop(),
        _buildMiddle(),
        _buildBottom(),
      ],
    );
  }

  Widget _buildTop() {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 20),
      child: Column(
        children: [
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: menuItems.map((title) => _buildCar(title)).toList(),
          ),
          const SizedBox(height: 20),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              ...menuItems.take(3).map((title) => _buildCar(title)).toList(),
              _buildCar('대리', isInvisible: true),
            ],
          ),
        ],
      ),
    );
  }

  Widget _buildCar(String title, {bool isInvisible = false}) {
    return Opacity(
      opacity: isInvisible ? 0.0 : 1.0,
      child: GestureDetector(
        onTap: () => print('클릭: $title'),
        child: Column(
          children: [
            const Icon(Icons.local_taxi, size: 40),
            Text(title),
          ],
        ),
      ),
    );
  }

  Widget _buildMiddle() {
    return CarouselSlider(
      options: CarouselOptions(height: 150, autoPlay: true),
      items: dummyItems.map((url) {
        return Builder(
          builder: (context) => Container(
            width: MediaQuery.of(context).size.width,
            margin: const EdgeInsets.symmetric(horizontal: 5),
            child: ClipRRect(
              borderRadius: BorderRadius.circular(8),
              child: Image.network(url, fit: BoxFit.cover),
            ),
          ),
        );
      }).toList(),
    );
  }

  Widget _buildBottom() {
    return ListView(
      physics: const NeverScrollableScrollPhysics(),
      shrinkWrap: true,
      children: noticeItems.asMap().entries.map((entry) {
        final index = entry.key;
        final title = entry.value;
        return ListTile(
          leading: const Icon(Icons.notifications_none),
          title: Text(title),
          onTap: () => print('클릭한 인덱스: $index'),
        );
      }).toList(),
    );
  }
}

```
#### data.dart
```
// data.dart
final List<String> dummyItems = [
  'https://cdn.pixabay.com/photo/2018/11/12/18/44/thanksgiving-3811492_1280.jpg',
  'https://cdn.pixabay.com/photo/2019/10/30/15/33/tajikistan-4589831_1280.jpg',
  'https://cdn.pixabay.com/photo/2019/11/25/16/15/safari-4652364_1280.jpg',
];

final List<String> menuItems = [
  '택시',
  '블랙',
  '바이크',
  '대리',
];

final List<String> noticeItems = List.generate(
  10,
  (i) => '[이벤트] 이것은 공지사항 $i번입니다',
);

```
