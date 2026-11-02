# User Interface Design Using Flutter Lab

---

# Experiment 1

## 1(a) Install Flutter and Dart SDK

### Aim
To install the Flutter and Dart SDK and set up the development environment.

### Description
- **Flutter** is an open-source UI toolkit by Google used to build Android, iOS, web and desktop apps from a single codebase.
- **Dart** is the object-oriented programming language used to write Flutter apps. The Dart SDK comes bundled with Flutter, so it need not be installed separately.

### Procedure
1. **System requirements (Windows):** Windows 10/11 (64-bit), at least 1.64 GB disk space, Git and Chrome installed.
2. **Download** the latest stable Flutter SDK zip from https://flutter.dev/docs/get-started/install.
3. **Extract** the zip to a permanent location such as `C:\src\flutter` (not `C:\Program Files`).
4. **Set the PATH:** Environment Variables → System variables → Path → Edit → add `C:\src\flutter\bin`.
5. **Verify:** open Command Prompt and run
   ```
   flutter doctor
   ```
6. **Install Android Studio** (for the Android SDK and emulator) and optionally VS Code.
7. **Install IDE plugins:** install the Flutter plugin (Dart is installed automatically) in VS Code or Android Studio.
8. **Create an emulator:** Android Studio → AVD Manager → create a virtual device (e.g., Pixel 5) → start it.
9. **Run the first app:**
   ```
   flutter create my_app
   cd my_app
   flutter run
   ```

### Output
`flutter doctor` shows green checkmarks, and the default counter app runs on the emulator.

*(Paste screenshot here)*

### Result
Flutter and Dart SDK were installed and verified successfully.

---

## 1(b) Simple Dart Program to Understand the Language Basics

### Aim
To write a simple Dart program covering variables, conditions, loops and functions.

### Description
Dart programs start execution from `main()`. The basics used here are variables with types (`String`, `int`), the `if-else` statement, the `for` loop and a user-defined function.

### Program
```dart
void main() {
  String name = 'John';
  int age = 20;
  print('Name: $name, Age: $age');

  if (age >= 18) {
    print('$name is an adult.');
  } else {
    print('$name is a minor.');
  }

  for (int i = 1; i <= 3; i++) {
    print('Count: $i');
  }

  greet(name);
}

void greet(String name) {
  print('Hello, $name!');
}
```

### Output
```
Name: John, Age: 20
John is an adult.
Count: 1
Count: 2
Count: 3
Hello, John!
```

### Result
The Dart program was executed successfully.

---

# Experiment 2

## 2(a) Explore Various Flutter Widgets (Text, Image, Container, etc.)

### Aim
To explore basic Flutter widgets such as Text, Image, Container and Icon.

### Description
Everything in Flutter is a widget.
- **Text:** displays styled text.
- **Image:** displays images from network, assets or files.
- **Container:** a box that supports padding, margin, color and decoration.
- **Icon:** displays built-in material icons.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter Widgets Demo')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              // Text widget
              Text(
                'Welcome to Flutter!',
                style: TextStyle(
                  fontSize: 24,
                  color: Colors.deepPurple,
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(height: 20),

              // Image widget
              Image.network(
                'https://upload.wikimedia.org/wikipedia/commons/1/17/Google-flutter-logo.png',
                width: 200,
                errorBuilder: (c, e, s) => Text('Failed to load image'),
              ),
              SizedBox(height: 20),

              // Container widget
              Container(
                padding: EdgeInsets.all(16),
                decoration: BoxDecoration(
                  color: Colors.amber[200],
                  borderRadius: BorderRadius.circular(8),
                ),
                child: Text('This is a Container'),
              ),
              SizedBox(height: 20),

              // Icon widgets
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(Icons.favorite, color: Colors.red, size: 30),
                  SizedBox(width: 10),
                  Icon(Icons.star, color: Colors.orange, size: 30),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Output
The screen shows the styled heading, the Flutter logo, an amber container with text, and two icons.

*(Paste screenshot here)*

### Result
Basic Flutter widgets were explored successfully.

---

## 2(b) Layout Structures using Row, Column and Stack

### Aim
To implement different layouts using Row, Column and Stack widgets.

### Description
- **Row:** arranges children horizontally.
- **Column:** arranges children vertically.
- **Stack:** places children on top of each other (layered).

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  Widget box(String label, Color color) {
    return Container(
      margin: EdgeInsets.all(4),
      padding: EdgeInsets.all(16),
      color: color,
      child: Text(label, style: TextStyle(color: Colors.white)),
    );
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Row, Column & Stack')),
        body: ListView(
          padding: EdgeInsets.all(16),
          children: [
            Text('Column Layout'),
            Column(children: [
              box('Box 1', Colors.red),
              box('Box 2', Colors.green),
            ]),
            SizedBox(height: 20),

            Text('Row Layout'),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                box('A', Colors.purple),
                box('B', Colors.teal),
                box('C', Colors.indigo),
              ],
            ),
            SizedBox(height: 20),

            Text('Stack Layout'),
            Container(
              height: 200,
              color: Colors.grey[300],
              child: Stack(
                alignment: Alignment.center,
                children: [
                  Container(width: 180, height: 180, color: Colors.yellow),
                  Container(width: 120, height: 120, color: Colors.blue),
                  Container(width: 60, height: 60, color: Colors.red),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Output
Boxes stacked vertically (Column), boxes side by side (Row), and three overlapping squares (Stack).

*(Paste screenshot here)*

### Result
Row, Column and Stack layouts were implemented successfully.

---

# Experiment 3

## 3(a) Responsive UI that Adapts to Different Screen Sizes

### Aim
To design a responsive UI that adapts to different screen sizes.

### Description
A responsive UI changes its layout based on the available screen size. `LayoutBuilder` gives the available width (`constraints.maxWidth`), and the layout is chosen using that width. Here, one box is shown on mobile, two on tablet and three on desktop.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Responsive UI')),
        body: LayoutBuilder(
          builder: (context, constraints) {
            if (constraints.maxWidth < 600) {
              return layout('Mobile', 1);
            } else if (constraints.maxWidth < 900) {
              return layout('Tablet', 2);
            } else {
              return layout('Desktop', 3);
            }
          },
        ),
      ),
    );
  }

  Widget layout(String title, int count) {
    return Center(
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          Text('$title Layout',
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
          SizedBox(height: 20),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: List.generate(
              count,
              (i) => Container(
                margin: EdgeInsets.all(8),
                width: 100,
                height: 100,
                color: Colors.primaries[i],
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

### Output
The layout changes between Mobile (1 box), Tablet (2 boxes) and Desktop (3 boxes) as the window width changes.

*(Paste screenshots here)*

### Result
A responsive UI was designed and executed successfully.

---

## 3(b) Media Queries and Breakpoints

### Aim
To implement MediaQuery and breakpoints for responsiveness.

### Description
`MediaQuery.of(context).size` gives the screen width and height. **Breakpoints** are width limits (for example 600 and 900) at which the UI changes.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('MediaQuery & Breakpoints')),
        body: ResponsiveWidget(),
      ),
    );
  }
}

class ResponsiveWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double width = MediaQuery.of(context).size.width;

    if (width < 600) {
      return box('Mobile Layout', Colors.blue, 150);
    } else if (width < 900) {
      return box('Tablet Layout', Colors.green, 300);
    } else {
      return box('Desktop Layout', Colors.orange, 450);
    }
  }

  Widget box(String text, Color color, double size) {
    return Center(
      child: Container(
        width: size,
        height: size,
        color: color,
        child: Center(
          child: Text(text, style: TextStyle(color: Colors.white, fontSize: 20)),
        ),
      ),
    );
  }
}
```

### Output
A blue box (width < 600), a green box (600 to 900) or an orange box (width > 900) is shown, with its size growing accordingly.

*(Paste screenshots here)*

### Result
MediaQuery and breakpoints were implemented successfully.

---

# Experiment 4

## 4(a) Navigation between Screens using Navigator

### Aim
To set up navigation between different screens using Navigator.

### Description
Flutter manages screens as a stack of routes. `Navigator.push()` opens a new screen and `Navigator.pop()` returns to the previous one.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: FirstScreen());
  }
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('First Screen')),
      body: Center(
        child: ElevatedButton(
          child: Text('Go to Second Screen'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondScreen()),
            );
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: ElevatedButton(
          child: Text('Go Back'),
          onPressed: () => Navigator.pop(context),
        ),
      ),
    );
  }
}
```

### Output
Tapping the button on the First Screen opens the Second Screen, and tapping "Go Back" returns to the First Screen.

*(Paste screenshots here)*

### Result
Navigation between screens using Navigator was implemented successfully.

---

## 4(b) Navigation with Named Routes

### Aim
To implement navigation using named routes.

### Description
Named routes use string names (such as `'/second'`) defined in a `routes` map in `MaterialApp`. Navigation is done with `Navigator.pushNamed()`, which keeps the code clean and organized.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => FirstScreen(),
        '/second': (context) => SecondScreen(),
      },
    );
  }
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('First Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pushNamed(context, '/second'),
          child: Text('Go to Second Screen'),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Second Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => Navigator.pop(context),
          child: Text('Go Back'),
        ),
      ),
    );
  }
}
```

### Output
The button opens the Second Screen using the route `/second`, and "Go Back" returns to `/`.

*(Paste screenshots here)*

### Result
Navigation with named routes was implemented successfully.

---

# Experiment 5

## 5(a) Stateful and Stateless Widgets

### Aim
To learn about stateless and stateful widgets in Flutter.

### Description
- **Stateless widget:** immutable, cannot change after it is built. Used for static content such as `Text` and `Icon`.
- **Stateful widget:** mutable, can change at runtime using `setState()`. Used for dynamic content such as counters and forms.

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
"I am Stateless" never changes. "I am Stateful" shows `Counter: 0`, and each tap on **Add Count** increases it by 1.

*(Paste screenshot here)*

### Result
The difference between stateless and stateful widgets was understood and implemented successfully.

---

## 5(b) State Management using setState and Provider

### Aim
To implement state management in Flutter using `setState` and `Provider`.

### Description
- **setState:** manages local state inside one widget. Best for small things such as counters and toggles.
- **Provider:** manages global state shared across many widgets. The state is kept in a class extending `ChangeNotifier`, and `notifyListeners()` rebuilds all listening widgets. Best for a cart, login or theme.

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
Two tabs, **setState** and **Provider**. Each button tap increases the apple count or the cart item count respectively.

*(Paste screenshot here)*

### Result
State management using `setState` and `Provider` was implemented successfully.

---

# Experiment 6

## 6(a) Create Custom Widgets for Specific UI Elements

### Aim
To create reusable custom widgets in Flutter.

### Description
A custom widget is a reusable UI component defined once and used many times with different data. It reduces code duplication and keeps the app organized. Here `ProfileCard` and `ActionButton` are custom widgets.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text("Profile App")),
        body: Center(
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              ProfileCard(name: "John Doe", email: "john.doe@example.com"),
              SizedBox(height: 20),
              ActionButton(
                text: "Follow",
                color: Colors.green,
                onPressed: () => print("Follow button clicked"),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

// Custom Profile Card Widget
class ProfileCard extends StatelessWidget {
  final String name;
  final String email;

  ProfileCard({required this.name, required this.email});

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      margin: EdgeInsets.all(12),
      child: ListTile(
        leading: CircleAvatar(child: Icon(Icons.person)),
        title: Text(name, style: TextStyle(fontWeight: FontWeight.bold)),
        subtitle: Text(email),
      ),
    );
  }
}

// Custom Button Widget
class ActionButton extends StatelessWidget {
  final String text;
  final Color color;
  final VoidCallback onPressed;

  ActionButton({required this.text, required this.color, required this.onPressed});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      style: ElevatedButton.styleFrom(backgroundColor: color),
      onPressed: onPressed,
      child: Text(text),
    );
  }
}
```

### Output
A profile card showing the name and email with an avatar, and a green **Follow** button below it.

*(Paste screenshot here)*

### Result
Custom widgets were created and used successfully.

---

## 6(b) Styling using Themes and Custom Styles

### Aim
To apply styling using themes and custom styles.

### Description
`ThemeData` defines colors, fonts and widget styles once, and all widgets follow it automatically, so the design stays consistent. This program defines a light theme and a dark theme and switches between them.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool isDark = false;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(brightness: Brightness.light, primarySwatch: Colors.blue),
      darkTheme: ThemeData(brightness: Brightness.dark, primarySwatch: Colors.deepPurple),
      themeMode: isDark ? ThemeMode.dark : ThemeMode.light,
      home: Scaffold(
        appBar: AppBar(title: Text("Theme Demo")),
        body: Center(
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Text("Hello Flutter!", style: TextStyle(fontSize: 24)),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: () => setState(() => isDark = !isDark),
                child: Text(isDark ? "Switch to Light" : "Switch to Dark"),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Output
The button toggles the whole app between the light (blue) theme and the dark (purple) theme.

*(Paste screenshots here)*

### Result
Styling using themes was implemented successfully.

---

# Experiment 7

## 7(a) Design a Form with Various Input Fields

### Aim
To design a form with various input fields.

### Description
A `Form` widget groups input fields. `TextFormField` takes text input, `Radio` buttons select one option, and a `GlobalKey<FormState>` is used to access the form's state.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: StudentForm());
  }
}

class StudentForm extends StatefulWidget {
  @override
  _StudentFormState createState() => _StudentFormState();
}

class _StudentFormState extends State<StudentForm> {
  final _formKey = GlobalKey<FormState>();
  String _name = '';
  String _rollNo = '';
  String _gender = 'Male';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Student Details Form')),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: ListView(
            children: [
              TextFormField(
                decoration: InputDecoration(labelText: 'Name'),
                onSaved: (v) => _name = v ?? '',
              ),
              TextFormField(
                decoration: InputDecoration(labelText: 'Roll No'),
                keyboardType: TextInputType.number,
                onSaved: (v) => _rollNo = v ?? '',
              ),
              SizedBox(height: 20),
              Text('Gender:'),
              RadioListTile<String>(
                title: Text('Male'),
                value: 'Male',
                groupValue: _gender,
                onChanged: (v) => setState(() => _gender = v!),
              ),
              RadioListTile<String>(
                title: Text('Female'),
                value: 'Female',
                groupValue: _gender,
                onChanged: (v) => setState(() => _gender = v!),
              ),
              ElevatedButton(
                onPressed: () {
                  _formKey.currentState!.save();
                  showDialog(
                    context: context,
                    builder: (_) => AlertDialog(
                      title: Text('Submitted Info'),
                      content: Text('Name: $_name\nRoll No: $_rollNo\nGender: $_gender'),
                    ),
                  );
                },
                child: Text('Submit'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Output
A form with Name, Roll No and Gender fields. On **Submit**, a dialog shows the entered details.

*(Paste screenshot here)*

### Result
A form with various input fields was designed successfully.

---

## 7(b) Form Validation and Error Handling

### Aim
To implement form validation and error handling.

### Description
Each `TextFormField` has a `validator` function. It returns an error message if the input is invalid, or `null` if it is valid. Calling `_formKey.currentState!.validate()` checks all fields and shows the error messages.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: FormValidationPage());
  }
}

class FormValidationPage extends StatefulWidget {
  @override
  _FormValidationPageState createState() => _FormValidationPageState();
}

class _FormValidationPageState extends State<FormValidationPage> {
  final _formKey = GlobalKey<FormState>();

  String? validateName(String? value) {
    if (value == null || value.isEmpty) return 'Name is required';
    return null;
  }

  String? validateEmail(String? value) {
    if (value == null || value.isEmpty) return 'Email is required';
    if (!RegExp(r'^[^@]+@[^@]+\.[^@]+').hasMatch(value)) {
      return 'Enter a valid email';
    }
    return null;
  }

  void submitForm() {
    if (_formKey.currentState!.validate()) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Form submitted successfully!')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Form Validation')),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                decoration: InputDecoration(labelText: 'Name'),
                validator: validateName,
              ),
              SizedBox(height: 16),
              TextFormField(
                decoration: InputDecoration(labelText: 'Email'),
                validator: validateEmail,
              ),
              SizedBox(height: 32),
              ElevatedButton(onPressed: submitForm, child: Text('Submit')),
            ],
          ),
        ),
      ),
    );
  }
}
```

### Output
- Empty fields show "Name is required" or "Email is required" in red.
- An invalid email shows "Enter a valid email".
- Valid input shows the snackbar "Form submitted successfully!".

*(Paste screenshots here)*

### Result
Form validation and error handling were implemented successfully.

---

# Experiment 8

## 8(a) Add Animations to UI Elements using Flutter's Animation Framework

### Aim
To add animations to UI elements using Flutter's animation framework.

### Description
Flutter provides implicit animation widgets such as `AnimatedContainer` and `AnimatedOpacity`. They automatically animate between old and new values over a given `duration` when the state changes through `setState()`.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: AnimationPage());
  }
}

class AnimationPage extends StatefulWidget {
  @override
  _AnimationPageState createState() => _AnimationPageState();
}

class _AnimationPageState extends State<AnimationPage> {
  bool _big = false;
  bool _visible = true;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Flutter Animations")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            GestureDetector(
              onTap: () => setState(() => _big = !_big),
              child: AnimatedContainer(
                duration: Duration(seconds: 1),
                width: _big ? 200 : 100,
                height: _big ? 200 : 100,
                color: _big ? Colors.blue : Colors.red,
                child: Center(
                  child: Text("Tap Me", style: TextStyle(color: Colors.white)),
                ),
              ),
            ),
            SizedBox(height: 30),
            ElevatedButton(
              onPressed: () => setState(() => _visible = !_visible),
              child: Text("Toggle Text"),
            ),
            AnimatedOpacity(
              opacity: _visible ? 1.0 : 0.0,
              duration: Duration(seconds: 1),
              child: Text("Hello Flutter!", style: TextStyle(fontSize: 22)),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Output
Tapping the box smoothly changes its size and color (red ↔ blue). The **Toggle Text** button fades the text in and out.

*(Paste screenshots here)*

### Result
Animations were added to UI elements successfully.

---

## 8(b) Different Types of Animations (Fade, Slide, etc.)

### Aim
To experiment with different types of animations such as fade, slide and scale.

### Description
- **Fade:** `AnimatedOpacity`
- **Slide:** `AnimatedPositioned` (inside a `Stack`)
- **Scale:** `AnimatedContainer` (changing the width and height)

All three animate together when the floating button is pressed.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: AnimationExample());
  }
}

class AnimationExample extends StatefulWidget {
  @override
  _AnimationExampleState createState() => _AnimationExampleState();
}

class _AnimationExampleState extends State<AnimationExample> {
  bool _visible = true;
  bool _moved = false;
  bool _scaled = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Fade, Slide & Scale')),
      body: Stack(
        children: [
          // Slide
          AnimatedPositioned(
            duration: Duration(seconds: 1),
            curve: Curves.easeInOut,
            top: _moved ? 300 : 100,
            left: 100,
            // Fade
            child: AnimatedOpacity(
              duration: Duration(seconds: 1),
              opacity: _visible ? 1.0 : 0.0,
              // Scale
              child: AnimatedContainer(
                duration: Duration(seconds: 1),
                width: _scaled ? 150 : 100,
                height: _scaled ? 150 : 100,
                color: Colors.teal,
                child: Center(
                  child: Text('Animate Me', style: TextStyle(color: Colors.white)),
                ),
              ),
            ),
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.play_arrow),
        onPressed: () {
          setState(() {
            _visible = !_visible; // fade
            _moved = !_moved;     // slide
            _scaled = !_scaled;   // scale
          });
        },
      ),
    );
  }
}
```

### Output
On pressing the play button, the teal box slides down, grows in size and fades. Pressing it again reverses the animation.

*(Paste screenshots here)*

### Result
Fade, slide and scale animations were implemented successfully.

---

# Experiment 9

## 9(a) Fetch Data from a REST API

### Aim
To fetch data from a REST API in Flutter.

### Description
The `http` package is used to send HTTP requests. `http.get()` fetches data, `json.decode()` converts the JSON response to Dart objects, and `FutureBuilder` shows a loading indicator, an error or the data based on the state of the Future.

### Add the dependency in `pubspec.yaml`
```yaml
dependencies:
  http: ^1.2.0
```
Then run `flutter pub get`.

### Program
```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: ApiDemoPage());
  }
}

class ApiDemoPage extends StatelessWidget {
  Future<String> fetchAdvice() async {
    final response =
        await http.get(Uri.parse("https://api.adviceslip.com/advice"));

    if (response.statusCode == 200) {
      final data = json.decode(response.body);
      return data["slip"]["advice"];
    } else {
      throw Exception("Failed to load advice");
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Fetch Data from REST API")),
      body: Center(
        child: FutureBuilder<String>(
          future: fetchAdvice(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return CircularProgressIndicator();
            } else if (snapshot.hasError) {
              return Text("Error: ${snapshot.error}");
            } else {
              return Padding(
                padding: EdgeInsets.all(16),
                child: Text(
                  snapshot.data!,
                  textAlign: TextAlign.center,
                  style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
                ),
              );
            }
          },
        ),
      ),
    );
  }
}
```

### Output
A loading spinner is shown first, followed by a random piece of advice fetched from the API.

*(Paste screenshot here)*

### Result
Data was fetched from a REST API successfully.

---

## 9(b) Display the Fetched Data in a Meaningful Way in the UI

### Aim
To display data fetched from a REST API as a list in the UI.

### Description
A list of posts is fetched from the JSONPlaceholder API and displayed using `ListView.builder` with `Card` and `ListTile` widgets.

### Program
```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: PostsPage());
  }
}

class PostsPage extends StatelessWidget {
  Future<List<dynamic>> fetchPosts() async {
    final response = await http
        .get(Uri.parse("https://jsonplaceholder.typicode.com/posts"));

    if (response.statusCode == 200) {
      return json.decode(response.body);
    } else {
      throw Exception("Failed to load posts");
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Posts from API")),
      body: FutureBuilder<List<dynamic>>(
        future: fetchPosts(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(child: Text("Error: ${snapshot.error}"));
          } else {
            final posts = snapshot.data!;
            return ListView.builder(
              itemCount: posts.length,
              itemBuilder: (context, index) {
                final post = posts[index];
                return Card(
                  margin: EdgeInsets.all(10),
                  child: ListTile(
                    title: Text(post['title'],
                        style: TextStyle(fontWeight: FontWeight.bold)),
                    subtitle: Text(post['body']),
                  ),
                );
              },
            );
          }
        },
      ),
    );
  }
}
```

### Output
A scrollable list of cards, each showing a post title in bold and its body below.

*(Paste screenshot here)*

### Result
The fetched API data was displayed in the UI successfully.

---

# Experiment 10

## 10(a) Write Unit Tests for UI Components

### Aim
To write unit (widget) tests for UI components in Flutter.

### Description
Flutter provides the `flutter_test` package. `testWidgets()` builds a widget in a test environment, `find` locates widgets, `tester.tap()` simulates a tap, and `expect()` checks the result. Test files are placed in the `test/` folder and run with `flutter test`.

### Program

**lib/main.dart**
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: Scaffold(body: Center(child: CounterWidget())));
  }
}

class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text('$_counter', style: TextStyle(fontSize: 32)),
        ElevatedButton(
          onPressed: () => setState(() => _counter++),
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

**test/widget_test.dart**
```dart
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:my_app/main.dart'; // replace my_app with your project name

void main() {
  testWidgets('Counter starts at 0', (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());
    expect(find.text('0'), findsOneWidget);
  });

  testWidgets('Counter increments when button is pressed',
      (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());
    await tester.tap(find.text('Increment'));
    await tester.pump();
    expect(find.text('1'), findsOneWidget);
  });
}
```

Run the tests using:
```
flutter test
```

### Output
```
00:02 +2: All tests passed!
```

### Result
Unit tests for UI components were written and executed successfully.

---

## 10(b) Use Flutter's Debugging Tools to Identify and Fix Issues

### Aim
To use Flutter's debugging tools to identify and fix issues.

### Description
Flutter provides these debugging tools:
- **debugPrint():** prints messages to the console.
- **assert():** checks a condition in debug mode and throws an error if it fails.
- **Flutter DevTools** (Widget Inspector, Debug Console, Performance view).
- **Hot reload** to quickly test fixes.

In this program the counter can wrongly become negative. The `assert` catches this bug, and the fix is to stop decrementing at 0.

### Program
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Flutter Debug Demo')),
        body: DebugDemoWidget(),
      ),
    );
  }
}

class DebugDemoWidget extends StatefulWidget {
  @override
  _DebugDemoWidgetState createState() => _DebugDemoWidgetState();
}

class _DebugDemoWidgetState extends State<DebugDemoWidget> {
  int _counter = 0;

  void _increment() {
    setState(() => _counter++);
    debugPrint('Counter incremented: $_counter');
  }

  void _decrement() {
    // BUG: counter can become negative.
    // FIX: only decrement when counter > 0.
    if (_counter > 0) {
      setState(() => _counter--);
    }
    debugPrint('Counter decremented: $_counter');
    assert(_counter >= 0, 'Counter should not be negative!');
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text('Counter: $_counter', style: TextStyle(fontSize: 28)),
          SizedBox(height: 10),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(onPressed: _increment, child: Text('Increment')),
              SizedBox(width: 10),
              ElevatedButton(onPressed: _decrement, child: Text('Decrement')),
            ],
          ),
        ],
      ),
    );
  }
}
```

### Output
- The Debug Console shows messages such as `Counter incremented: 1`.
- Before the fix, pressing Decrement at 0 trips the assertion error "Counter should not be negative!".
- After the fix, the counter stays at 0.

*(Paste screenshot here)*

### Result
Flutter debugging tools were used to identify and fix the issue successfully.
