# want


# Experiment 5

## 5(a) Stateful and Stateless Widgets

### Aim
To learn about stateless and stateful widgets in Flutter.

### Description
Widgets are the basic building blocks of a Flutter UI. They are of two types:

- **Stateless widget:** It is immutable, so once built it cannot change. It is used for static content such as `Text`, `Icon` and `Image`.
- **Stateful widget:** It is mutable and can change at runtime using `setState()`. It is used for dynamic content such as counters, forms and checkboxes.

| Stateless Widget | Stateful Widget |
|---|---|
| Does not change after it is built | Can change during runtime |
| No internal state | Has internal state |
| Overrides only `build()` | Has a `State` class with `build()` |
| Does not use `setState()` | Uses `setState()` to refresh the UI |

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("Stateless vs Stateful")),
        body: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            MyStatelessWidget(),
            SizedBox(height: 30),
            MyStatefulWidget(),
          ],
        ),
      ),
    );
  }
}

// Stateless Widget
class MyStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text("I am Stateless", style: TextStyle(fontSize: 20));
  }
}

// Stateful Widget
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int counter = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text("I am Stateful\nCounter: $counter", style: TextStyle(fontSize: 18)),
        ElevatedButton(
          onPressed: () => setState(() => counter++),
          child: Text("Add Count"),
        ),
      ],
    );
  }
}
```

### Output
- The screen shows the text "I am Stateless", which never changes.
- Below it, "I am Stateful" shows `Counter: 0`.
- Each tap on the **Add Count** button increases the counter by 1.

*(Paste your output screenshot here)*

### Result
The difference between stateless and stateful widgets was understood and implemented successfully.

---

## 5(b) State Management using setState and Provider

### Aim
To implement state management in Flutter using `setState` and `Provider`.

### Description
State management controls how data is stored and updated in an app.

- **setState:** It manages local state inside a single widget. Calling `setState()` rebuilds that widget. It is best for small things such as counters and toggles.
- **Provider:** It manages global state shared across many widgets. The state is kept in a separate class that extends `ChangeNotifier`. When `notifyListeners()` is called, all widgets listening to it rebuild. It is best for things such as a cart, login or theme.

### Add the dependency in `pubspec.yaml`
```yaml
dependencies:
  provider: ^6.0.5
```
Then run `flutter pub get`.

### Program
```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => CartProvider(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: DefaultTabController(
        length: 2,
        child: Scaffold(
          appBar: AppBar(
            title: Text("Cart Demo"),
            bottom: TabBar(tabs: [
              Tab(text: "setState"),
              Tab(text: "Provider"),
            ]),
          ),
          body: TabBarView(children: [LocalCart(), GlobalCart()]),
        ),
      ),
    );
  }
}

// 1. setState (Local state)
class LocalCart extends StatefulWidget {
  @override
  _LocalCartState createState() => _LocalCartState();
}

class _LocalCartState extends State<LocalCart> {
  int apples = 0;

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(mainAxisSize: MainAxisSize.min, children: [
        Text("Apples: $apples", style: TextStyle(fontSize: 24)),
        ElevatedButton(
          onPressed: () => setState(() => apples++),
          child: Text("Add Apple"),
        ),
      ]),
    );
  }
}

// 2. Provider (Global state)
class CartProvider extends ChangeNotifier {
  int items = 0;

  void add() {
    items++;
    notifyListeners();
  }
}

class GlobalCart extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final cart = Provider.of<CartProvider>(context);
    return Center(
      child: Column(mainAxisSize: MainAxisSize.min, children: [
        Text("Cart Items: ${cart.items}", style: TextStyle(fontSize: 24)),
        ElevatedButton(
          onPressed: cart.add,
          child: Text("Add Item"),
        ),
      ]),
    );
  }
}
```

### Output
- The app has two tabs: **setState** and **Provider**.
- In the **setState** tab, each tap on *Add Apple* increases the apple count.
- In the **Provider** tab, each tap on *Add Item* increases the cart item count.

*(Paste your output screenshot here)*

### Result
State management using `setState` and `Provider` was implemented successfully.
