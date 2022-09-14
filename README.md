# flutter_check_internet

[Source](https://flutter-developer.medium.com/flutter-how-to-check-internet-connection-b6ce0ec00d5c)

```
connectivity: ^3.0.6
```

- main.dart
```dart
import 'dart:io';

import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;
  // bool isOnline = await hasNetwork();


  const MyHomePage({
    Key? key,
    required this.title,
  }) : super(key: key);

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  bool isOnline = false;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('MyHomePage'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            Text(isOnline == true? "Connected To Internet" : "Time Out"),
            ElevatedButton(
                child: const Text("Check Connection"),
                onPressed: () async {
                  bool isConnect = await hasNetwork();
                  setState(() {
                    isOnline = isConnect;
                  });
                },
            )
          ],
        ),
      ),
    );
  }

  Future<bool> hasNetwork() async {
    try {
      final result = await InternetAddress.lookup('www.google.com');
      return result.isNotEmpty && result[0].rawAddress.isNotEmpty;
    } on SocketException catch (_) {
      return false;
    }
  }
}
```

---

```
Copyright 2022 M. Fadli Zein
```
