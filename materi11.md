# [Back to Readme](./README.md)

## buat project

tentukan folder yang ingin di jadikan project \
lalu klik kanan dan _"open with terminal"_ \
lalu ketik perintah berikut

```bash
flutter create materi11
```

ketik lagi

```bash
cd materi11
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

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: BelajarNavBar(),
    );
  }
}

class BelajarNavBar extends StatefulWidget {
  const BelajarNavBar({super.key});
  @override
  State<BelajarNavBar> createState() => _BelajarNavBarState();
}

class _BelajarNavBarState extends State<BelajarNavBar> {
  int _selectedNavbar = 0;
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
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Beranda',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.assignment),
            label: 'Pesanan',
          ),
          BottomNavigationBarItem(icon: Icon(Icons.mail), label: 'Inbox'),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Akun',
          ),
        ],
        currentIndex: _selectedNavbar,
        selectedItemColor: Colors.green,
        unselectedItemColor: Colors.grey,
        showUnselectedLabels: true,
        onTap: _changeSelectedNavBar,
      ),
    );
  }
}
```

lalu 
```bash
flutter run
```
ketik 2 untuk jalankan di chrome
```bash
2
```
