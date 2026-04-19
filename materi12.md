# [Back To Readme](./README.md)

## buat project

tentukan folder yang ingin di jadikan project \
lalu klik kanan dan _"open with terminal"_ \
lalu ketik perintah berikut

```bash
flutter create materi12
```

ketik lagi

```bash
cd materi12
```

ketik lagi

```bash
flutter pub add convex_bottom_bar
```

ketik lagi

```bash
code .
```

---

### Pergi ke folfer lib/main.dart

Salin code dibawah ini dan paste kan di main.dart \
_ctrl+a lalu ctrl+v_

```dart
import 'package:flutter/material.dart';
import 'package:convex_bottom_bar/convex_bottom_bar.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: BelajarNavBar(),
    );
  }
}

class BelajarNavBar extends StatefulWidget {
  @override
  _BelajarNavBarState createState() => _BelajarNavBarState();
}

class _BelajarNavBarState extends State<BelajarNavBar> {
  int _selectedNavbar = 2;
  void _changeSelectedNavBar(int index) {
    setState(() {
      _selectedNavbar = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("belajarFlutter.com")),
      body: Center(
        child: Text(
          "Tab Index yang aktif : $_selectedNavbar",
          style: TextStyle(fontSize: 16),
        ),
      ),
      bottomNavigationBar: ConvexAppBar(
        items: [
          TabItem(icon: Icons.home, title: 'Home'),
          TabItem(icon: Icons.map, title: 'Discovery'),
          TabItem(icon: Icons.add, title: 'Add'),
          TabItem(icon: Icons.message, title: 'Message'),
          TabItem(icon: Icons.people, title: 'Profile'),
        ],
        initialActiveIndex: _selectedNavbar,
        onTap: _changeSelectedNavBar,
      ),
    );
  }
}
```


lalu buka terminal (ctrl+`) dan ketik perintah berikut
```bash
flutter run
```
ketik 2 untuk jalankan di chrome
```bash
2
```
