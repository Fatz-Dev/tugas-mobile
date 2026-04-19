# [Back to Readme](./README.md)


## buat project

tentukan folder yang ingin di jadikan project \
lalu klik kanan dan _"open with terminal"_ \
lalu ketik perintah berikut

```bash
flutter create materiapiquran
```

ketik lagi

```bash
cd materiapiquran
```

ketik lagi

```bash
flutter pub add http
```

ketik lagi

```bash
code .
```

---

### 1. Buat file lib/surat.dart

Salin code dibawah ini dan paste kan di surat.dart

```dart
class Surat {
  final int nomor;
  final String nama;
  final String latin;
  final int jumlahAyat;
  
  Surat({
    required this.nomor,
    required this.nama,
    required this.latin,
    required this.jumlahAyat,
  });

  factory Surat.fromJson(Map<String, dynamic> json) {
    // perbaikan nya ada pada bagian nomor dan jumlahAyat harus parse dari int ke string
    // pada dan penamaan data tidak sesuai dengan api
    return Surat(
      nomor: int.tryParse(json['number'].toString()) ?? 0,
      nama: json['name_id'],
      latin: json['name_en'],
      jumlahAyat: int.tryParse(json['number_of_verses'].toString()) ?? 0,
    );
  }
}
```

---

### 2. Buat file lib/api_service.dart

Salin code dibawah ini dan paste kan di api_service.dart

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import 'surat.dart';

class ApiService {
  final String baseUrl = 'https://api.myquran.com/v2/quran/surat/all';
  Future<List<Surat>> fetchSurat() async {
    final response = await http.get(Uri.parse(baseUrl));
    if (response.statusCode == 200) {
      List<dynamic> data = jsonDecode(response.body)['data'];
      return data.map((item) => Surat.fromJson(item)).toList();
    } else {
      throw Exception('Failed to load surat');
    }
  }
}
```

---

### 3. Buat file lib/detil.dart

Salin code dibawah ini dan paste kan di detil.dart

```dart
import 'package:flutter/material.dart';
import 'surat.dart';

class DetailPage extends StatelessWidget {
  final Surat surat;

  DetailPage({required this.surat});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(surat.nama),
        leading: IconButton(
          icon: Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Nomor Surat: ${surat.nomor}',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10),
            Text(
              'Nama Surat: ${surat.nama}',
              style: TextStyle(fontSize: 18),
            ),
            SizedBox(height: 10),
            Text(
              'Nama Latin: ${surat.latin}',
              style: TextStyle(fontSize: 18),
            ),
            SizedBox(height: 10),
            Text(
              'Jumlah Ayat: ${surat.jumlahAyat}',
              style: TextStyle(fontSize: 18),
            ),
            SizedBox(height: 20),
            Text(
              'Detail tentang surat ini akan ditampilkan di sini.',
              style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

### 4. Pergi ke folder lib/main.dart

Salin code dibawah ini dan paste kan di main.dart \
_ctrl+a lalu ctrl+v_

```dart
import 'package:flutter/material.dart';
import 'package:meterihttpcomplete/detil.dart';
import 'api_service.dart';
import 'surat.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Aplikasi Quran',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  late Future<List<Surat>> futureSurat;

  @override
  void initState() {
    super.initState();
    futureSurat = ApiService().fetchSurat();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Daftar Surat')
      ),
      body: FutureBuilder<List<Surat>>(
        future: futureSurat,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(child: Text('Error: ${snapshot.error}'));
          }
          List<Surat> suratList = snapshot.data!;
          return ListView.builder(
            itemCount: suratList.length,
            itemBuilder: (context, index) {
              Surat surat = suratList[index];
              return ListTile(
                title: Text(surat.nama),
                subtitle: Text(surat.latin),
                trailing: Row(
                  mainAxisSize: MainAxisSize.min,
                  children: [
                    Text('${surat.jumlahAyat} Ayat'),
                    SizedBox(width: 10),
                    TextButton(
                      onPressed: () {
                        Navigator.push(
                          context,
                          MaterialPageRoute(
                            builder: (context) => DetailPage(surat: surat),
                          ),
                        );
                      },
                      child: Text('Detail', style: TextStyle(color: Colors.blue)),
                    ),
                  ],
                ),
              );
            },
          );
        },
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
