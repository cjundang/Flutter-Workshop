# Flutter-Workshop

Got it ✅
Let me extract and organize the **commands from Section 1** of your uploaded PDF **“Mobile Application Development with Flutter”** by Asst. Prof. Dr. Chanankorn Jandaeng, so you can **self-learn Flutter setup and basic operations** effectively.

---

# **Section 1: Introduction to Flutter & Toolchain Setup**

This section focuses on setting up Flutter, verifying installation, creating projects, running apps, and building for different platforms.

---

## **1. Download & Install Flutter**

**Steps:**

1. Download Flutter SDK → [https://docs.flutter.dev/get-started/install](https://docs.flutter.dev/get-started/install)
2. Extract the downloaded file.
3. Set the Flutter SDK path in your environment variables.

**Command Example (Linux / macOS):**

```bash
export PATH="$PATH:/path-to-flutter/bin"
```

**Command Example (Windows PowerShell):**

```powershell
setx PATH "%PATH%;C:\path-to-flutter\bin"
```

---

## **2. Verify Flutter Installation**

Use the following command to check if Flutter is installed properly and if your environment is ready:

```bash
flutter doctor
```

* It scans your environment and shows the status.
* If there are missing dependencies, follow the recommendations displayed.

---

## **3. Create a New Flutter Project**

You can create a **new Flutter project** in two different ways:

### **a. Default Project Structure**

```bash
flutter create my_app
```

* This creates a standard Flutter app with demo code and assets.

### **b. Empty Project**

```bash
flutter create project_name --empty
```

* This creates a **clean project** with minimal boilerplate code.

---

## **4. Open the Project in VS Code**

1. Create a new folder:

   ```bash
   mkdir starter
   ```
2. Drag and drop the folder into **Visual Studio Code**.
3. Open the terminal in VS Code:
   **Menu → Terminal → New Terminal**

---

## **5. Run the Flutter Application**

Once the project is created, navigate to the project folder and run:

```bash
cd my_app
flutter run
```

* By default, it runs on the **connected emulator** or **physical device**.
* Make sure to start your Android Emulator or connect a physical device.

---

## **6. Run the App on Android Emulator**

First, start your Android Virtual Device (AVD):

```bash
flutter emulators
flutter emulators --launch <emulator_id>
```

Then run your project:

```bash
flutter run
```

---

## **7. Build a Web Application**

Flutter also supports building apps for the **Web**.

### **a. Build for Web**

```bash
flutter build web --release
```

* Generates a production-ready web app.

### **b. Locate the Build Files**

```
/my_app/build/web
```

### **c. Run a Local Web Server**

```bash
cd my_app/build/web
python3 -m http.server 8888
```

Then, open:
[http://localhost:8888](http://localhost:8888)

---

## **8. Additional Useful Commands**

| **Command**         | **Description**                                   |
| ------------------- | ------------------------------------------------- |
| `flutter upgrade`   | Updates Flutter SDK to the latest stable version  |
| `flutter pub get`   | Installs dependencies listed in **pubspec.yaml**  |
| `flutter devices`   | Lists all available connected devices & emulators |
| `flutter clean`     | Clears the build cache to fix dependency issues   |
| `flutter doctor -v` | Shows detailed Flutter environment information    |

---

## **Self-Learning Practice Workflow**

Here’s the **recommended order** to practice commands from this section:

1. **Set up Flutter SDK** → `flutter doctor`
2. **Create a new project** → `flutter create my_app`
3. **Run the project** → `flutter run`
4. **Enable Android Emulator** → `flutter emulators --launch`
5. **Build for Web** → `flutter build web --release`
6. **Serve Web App** → `python3 -m http.server 8888`
7. **Update SDK & Fix Issues** → `flutter upgrade` & `flutter clean`

---

Below is a compact, self-learning “lab” for **Section 2 – Widgets & Layouts**. It includes (A) the minimal commands you’ll use while practicing, and (B) concise, runnable example code that exercises the core widgets discussed in the slides—**MaterialApp, Scaffold, AppBar, Text, Container, Center, Column, Row, ListView, ListTile**—with pointers to where these are introduced in the PDF.

---

# A) Practice commands (terminal)

```bash
# 1) Create a clean sandbox project
flutter create --empty widgets_lab
cd widgets_lab

# 2) Run on a connected device/emulator (hot reload with `r`)
flutter run

# 3) (Optional) Run as a web app for quick iteration
flutter run -d chrome

# 4) If cache issues arise during iteration
flutter clean && flutter pub get
```

Why these? Section 2 introduces the widget system—**Stateless vs. Stateful**, **Scaffold**, **AppBar**, and the canonical **layout widgets** (Text, Container, Center, Column, Row, ListView/ListTile). Practicing them in a fresh project with hot-reload is the shortest path to mastery.

---

# B) Example code (paste into `lib/main.dart`)

## 1) “Hello, Scaffold”: Material shell + text

Demonstrates **MaterialApp → Scaffold → AppBar → Body** and a centered **Text** with styling and alignment controls discussed in the slides.

```dart
import 'package:flutter/material.dart';

void main() => runApp(const WidgetsLabApp());

class WidgetsLabApp extends StatelessWidget {
  const WidgetsLabApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Widgets Lab',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        useMaterial3: true,
      ),
      home: const HelloScaffold(),
    );
  }
}

class HelloScaffold extends StatelessWidget {
  const HelloScaffold({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Hello, Scaffold')),
      body: const Center(
        child: Text(
          'Everything is a widget',
          textAlign: TextAlign.center,
          maxLines: 2,
          overflow: TextOverflow.ellipsis,
          style: TextStyle(fontSize: 24, fontWeight: FontWeight.w600),
        ),
      ),
    );
  }
}
```

---

## 2) Layout essentials: Container • Center • Column • Row

Exercises **Container** (size, padding, decoration), **Center**, **Column**, **Row**—the core layout bloc introduced in Section 2.

Replace the `home:` in `MaterialApp` with `const LayoutEssentials()` to run this screen.

```dart
class LayoutEssentials extends StatelessWidget {
  const LayoutEssentials({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Layout Essentials')),
      body: Center(
        child: Container(
          width: 320,
          padding: const EdgeInsets.all(16),
          margin: const EdgeInsets.all(12),
          decoration: BoxDecoration(
            color: Colors.indigo.withOpacity(0.08),
            borderRadius: BorderRadius.circular(12),
            border: Border.all(color: Colors.indigo),
          ),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              const Text('Column + Row demo', style: TextStyle(fontSize: 18)),
              const SizedBox(height: 12),
              Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: const [
                  Icon(Icons.star),
                  Text('Left'),
                  Text('Right'),
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

---

## 3) Lists two ways: `ListView` + `ListTile`, then `ListView.builder`

Demonstrates a fixed **ListView** and the scalable **ListView\.builder** pattern highlighted in the slides.

Replace the `home:` with `const ListsDemo()` to run this screen.

```dart
class ListsDemo extends StatelessWidget {
  const ListsDemo({super.key});

  @override
  Widget build(BuildContext context) {
    final items = List<String>.generate(100, (i) => 'Item #$i');

    return Scaffold(
      appBar: AppBar(title: const Text('Lists Demo')),
      body: ListView(
        children: const [
          ListTile(
            leading: Icon(Icons.person),
            title: Text('Alice'),
            subtitle: Text('Fixed ListTile'),
            trailing: Icon(Icons.chevron_right),
          ),
          Divider(),
          ListTile(
            leading: Icon(Icons.person_outline),
            title: Text('Bob'),
            subtitle: Text('Another fixed ListTile'),
            trailing: Icon(Icons.chevron_right),
          ),
          Divider(),
        ],
      ),
      bottomNavigationBar: SizedBox(
        height: 240,
        child: _BuilderPane(items: items),
      ),
    );
  }
}

class _BuilderPane extends StatelessWidget {
  const _BuilderPane({required this.items});
  final List<String> items;

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length,
      itemBuilder: (context, index) => ListTile(
        leading: const Icon(Icons.label),
        title: Text(items[index]),
        subtitle: Text('Index $index'),
        onTap: () => ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(content: Text('Tapped ${items[index]}')),
        ),
      ),
    );
  }
}
```

---

## 4) Theming scaffold components

A brief illustration of **Theme** customization as noted in the section (color, typography). Use this as `home:` to see themed surfaces.

```dart
class ThemedScaffold extends StatelessWidget {
  const ThemedScaffold({super.key});

  @override
  Widget build(BuildContext context) {
    final scheme = Theme.of(context).colorScheme;
    return Scaffold(
      appBar: AppBar(title: const Text('Themed Scaffold')),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: const Icon(Icons.add),
      ),
      body: Center(
        child: Container(
          padding: const EdgeInsets.all(20),
          decoration: BoxDecoration(
            color: scheme.secondaryContainer,
            borderRadius: BorderRadius.circular(16),
          ),
          child: const Text(
            'ThemeData · ColorScheme · Material 3',
            textAlign: TextAlign.center,
          ),
        ),
      ),
    );
  }
}
```

---

## Study map to slides

* **Everything is a widget; Stateless vs. Stateful (overview & use cases)**
* **Scaffold & AppBar structure**
* **Text widget: style, align, overflow, maxLines**
* **Core layout widgets (Container, Center, Column, Row)**
* **Lists: ListView, ListTile, customization & builder pattern**

---

## Suggested self-learning drills

1. **Text drill:** Recreate the “Hello, Scaffold” screen; vary `TextAlign`, `maxLines`, and `overflow`.
2. **Layout drill:** Build a profile card using **Container** with padding/margin/decoration; arrange fields with **Column** and a stats row with **Row**.
3. **List drill:** Convert a fixed `ListView` to `ListView.builder`; attach a `SnackBar` on tap; add `leading`/`trailing` icons with `ListTile`.

Below is a concise self-learning “lab” for **Section 3 – State Management**. It focuses on (A) the commands you’ll use while practicing and (B) minimal, runnable examples for **`setState`**, **`TextField` + `TextEditingController`**, and a lightweight **Provider** pattern.

---

# A) Practice commands (terminal)

```bash
# 1) Start a fresh sandbox
flutter create --empty state_lab
cd state_lab

# 2) Run with hot reload
flutter run

# 3) (Optional) Add Provider for app-level state
flutter pub add provider
```

Rationale: This section contrasts **stateless** vs **stateful** widgets and introduces **interactive updates** via `setState`, plus **text input** with `TextField`/`TextEditingController`. A Provider add-on enables scalable state beyond a single widget. These are the exact themes highlighted in the slides.

---

# B) Example code (paste into `lib/main.dart`)

## 1) Counter with `setState` (fundamental stateful pattern)

Demonstrates a canonical **StatefulWidget**, **FAB**, and `setState`—the interactive pattern emphasized in the slides.

```dart
import 'package:flutter/material.dart';

void main() => runApp(const StateLabApp());

class StateLabApp extends StatelessWidget {
  const StateLabApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'State Lab',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.indigo),
      home: const CounterScreen(),
    );
  }
}

class CounterScreen extends StatefulWidget {
  const CounterScreen({super.key});
  @override
  State<CounterScreen> createState() => _CounterScreenState();
}

class _CounterScreenState extends State<CounterScreen> {
  int _count = 0;

  void _inc() => setState(() => _count++);
  void _dec() => setState(() => _count--);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Counter (setState)')),
      body: Center(
        child: Text('Count: $_count', style: const TextStyle(fontSize: 28)),
      ),
      floatingActionButton: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          FloatingActionButton(onPressed: _inc, child: const Icon(Icons.add)),
          const SizedBox(height: 12),
          FloatingActionButton(onPressed: _dec, child: const Icon(Icons.remove)),
        ],
      ),
    );
  }
}
```

> The slides explicitly frame **stateful widgets** as those that “can change their state over time” and showcase an interactive counter area and `setState()` update cycle.

---

## 2) Text input: `TextField` + `TextEditingController`

Illustrates **controlled input**, mirroring the “TextField” and “TextEditingController” emphasis.

```dart
class TextEchoScreen extends StatefulWidget {
  const TextEchoScreen({super.key});
  @override
  State<TextEchoScreen> createState() => _TextEchoScreenState();
}

class _TextEchoScreenState extends State<TextEchoScreen> {
  final _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose(); // always dispose controllers
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('TextField + Controller')),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: const InputDecoration(
                labelText: 'Type something',
                border: OutlineInputBorder(),
              ),
              onChanged: (_) => setState(() {}),
            ),
            const SizedBox(height: 16),
            Text('Echo: ${_controller.text}', style: const TextStyle(fontSize: 18)),
          ],
        ),
      ),
    );
  }
}
```

To try this screen, temporarily set `home: const TextEchoScreen(),` in `StateLabApp`.

---

## 3) App-level state with **Provider** (scales beyond one widget)

Slides later introduce **Provider/Consumer** for structured state sharing; here’s a minimal pattern using `ChangeNotifier` and `Consumer`.

```dart
// Add at top with other imports:
// import 'package:provider/provider.dart';

class CounterModel extends ChangeNotifier {
  int value = 0;
  void inc() { value++; notifyListeners(); }
  void dec() { value--; notifyListeners(); }
}

class ProviderApp extends StatelessWidget {
  const ProviderApp({super.key});
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => CounterModel(),
      child: MaterialApp(
        title: 'Provider Demo',
        theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.teal),
        home: const ProviderCounterScreen(),
      ),
    );
  }
}

class ProviderCounterScreen extends StatelessWidget {
  const ProviderCounterScreen({super.key});
  @override
  Widget build(BuildContext context) {
    final counter = context.watch<CounterModel>();
    return Scaffold(
      appBar: AppBar(title: const Text('Counter (Provider)')),
      body: Center(child: Text('Count: ${counter.value}', style: const TextStyle(fontSize: 28))),
      floatingActionButton: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          FloatingActionButton(onPressed: () => context.read<CounterModel>().inc(), child: const Icon(Icons.add)),
          const SizedBox(height: 12),
          FloatingActionButton(onPressed: () => context.read<CounterModel>().dec(), child: const Icon(Icons.remove)),
        ],
      ),
    );
  }
}
```

To run the Provider demo:

1. Ensure `provider` is added (`flutter pub add provider`).
2. Change your `main()` to:

```dart
void main() => runApp(const ProviderApp());
```

> This mirrors the slides’ framing of a **producer** (a `ChangeNotifier` that holds and updates state) and **consumers** (widgets that rebuild on change).

---

## Suggested drills (quick, verifiable)

1. **Counter variants:** Add a “Reset” button; disable “−” when the count is 0. (Tests `setState` logic.)
2. **Text input UX:** Add input validation (e.g., non-empty), and show a `SnackBar` on submit. (Extends TextField practice.)
3. **Provider extension:** Track both counter and a timestamp of last change; show only the affected `Text` rebuilding (separate Consumer). (Reinforces Provider principles.)

---

Alright, CJ 🙂
Let’s break down **Section 4 (Web API & Asynchronous Programming)** and **Section 5 (Routing & Navigation)** from your Flutter PDF into a **self-learning guide**.
This will include:

1. **Required commands**
2. **Example code** (runnable in a fresh Flutter project)
3. **Hands-on drills** aligned with your slides.

---

# **SECTION 4 — Web API & Asynchronous Programming**

This section introduces **fetching data from APIs**, working with **JSON**, and handling **async/await**.

---

## **A) Practice Commands**

```bash
# 1) Create a new project for API learning
flutter create --empty api_lab
cd api_lab

# 2) Add the HTTP package for API calls
flutter pub add http

# 3) Run the project with hot reload
flutter run
```

Optional: Use [randomuser.me](https://randomuser.me/) or [fakestoreapi.com](https://fakestoreapi.com/products) as shown in the PDF.

---

## **B) Basic Web API Fetch + JSON Parse Example**

**Goal:** Fetch and display product data from **fakestoreapi.com**.

> Paste this in `lib/main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(const ApiLabApp());

class ApiLabApp extends StatelessWidget {
  const ApiLabApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'API Lab',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.deepPurple),
      home: const ProductListScreen(),
    );
  }
}

class ProductListScreen extends StatefulWidget {
  const ProductListScreen({super.key});
  @override
  State<ProductListScreen> createState() => _ProductListScreenState();
}

class _ProductListScreenState extends State<ProductListScreen> {
  List<dynamic> _products = [];
  bool _loading = true;

  @override
  void initState() {
    super.initState();
    fetchProducts();
  }

  Future<void> fetchProducts() async {
    try {
      final url = Uri.parse('https://fakestoreapi.com/products');
      final response = await http.get(url);

      if (response.statusCode == 200) {
        setState(() {
          _products = json.decode(response.body);
          _loading = false;
        });
      } else {
        throw Exception('Failed to load products');
      }
    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Error: $e')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Products')),
      body: _loading
          ? const Center(child: CircularProgressIndicator())
          : ListView.builder(
              itemCount: _products.length,
              itemBuilder: (context, index) {
                final product = _products[index];
                return ListTile(
                  leading: Image.network(product['image'], width: 50),
                  title: Text(product['title']),
                  subtitle: Text('\$${product['price']}'),
                );
              },
            ),
    );
  }
}
```

---

## **C) Async/Await Best Practices**

* Use `Future<void>` for asynchronous calls.
* Always wrap network calls in `try/catch` blocks.
* Show a **loading indicator** until the data arrives.
* Decode JSON using `json.decode()` from `dart:convert`.

---

## **D) Hands-on Drills**

| **Exercise**                           | **Goal**                                                         |
| -------------------------------------- | ---------------------------------------------------------------- |
| Fetch random users via `randomuser.me` | Display first/last names + profile pictures                      |
| Add a **Refresh** button               | Re-fetch API data on-demand                                      |
| Display network errors                 | Show SnackBars when the server fails                             |
| Convert response into Dart models      | Use [quicktype.io](https://app.quicktype.io/) to generate models |

---

# **SECTION 5 — Routing & Navigation**

This section covers **screen transitions**, **Navigator API**, **MaterialPageRoute**, and **data passing** between pages.

---

## **A) Practice Commands**

```bash
# Continue in the same project OR start fresh:
flutter create --empty nav_lab
cd nav_lab
flutter run
```

---

## **B) Navigator Push & Pop Example**

> Paste this into `lib/main.dart`:

```dart
import 'package:flutter/material.dart';

void main() => runApp(const NavLabApp());

class NavLabApp extends StatelessWidget {
  const NavLabApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Navigation Demo',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.blue),
      home: const HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Home Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => const DetailsScreen(name: "CJ")),
            );
          },
          child: const Text('Go to Details'),
        ),
      ),
    );
  }
}

class DetailsScreen extends StatelessWidget {
  final String name;
  const DetailsScreen({super.key, required this.name});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Details Screen')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Welcome, $name!', style: const TextStyle(fontSize: 20)),
            const SizedBox(height: 16),
            ElevatedButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Back to Home'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## **C) Data Passing Between Screens**

### **Send data → Next screen**

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailsScreen(name: 'Flutter Dev'),
  ),
);
```

### **Return data → Previous screen**

```dart
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const InputScreen()),
);
print('Returned: $result');
```

---

## **D) Hands-on Drills**

| **Exercise**               | **Goal**                                                |
| -------------------------- | ------------------------------------------------------- |
| Add a **Profile Screen**   | Pass username & email from home screen                  |
| Create a **Todo List**     | Add, view, and delete tasks across screens              |
| Combine with Section 4 API | Navigate to a “Product Details” page using fetched data |
| Use **Named Routes**       | Define routes in `MaterialApp` for clean navigation     |

---

# **Quick Summary**

| **Aspect**     | **Section 4: Web API & Async**           | **Section 5: Routing & Navigation** |
| -------------- | ---------------------------------------- | ----------------------------------- |
| Package needed | `http`                                   | Built-in                            |
| Core topic     | Fetching APIs, parsing JSON, async/await | Moving between screens              |
| Example API    | fakestoreapi.com, randomuser.me          | Passing/receiving data              |
| Main classes   | `http`, `Future`, `ListView`             | `Navigator`, `MaterialPageRoute`    |
| Output         | Dynamic data-driven UI                   | Interactive, multi-screen app       |

---

Alright, CJ 🙂
Let's dive into **Section 6 — Form Handling & Validation** from your Flutter PDF.
This section focuses on **creating forms, validating inputs, handling authentication, and integrating with APIs or local servers**.

I’ll give you:

1. **Required commands**
2. **Full runnable example code**
3. **Form validation techniques**
4. **Hands-on self-learning drills**

---

# **SECTION 6 — Form Handling & Validation**

This section teaches you how to build **interactive forms** in Flutter, manage **user input**, **validate data**, and connect the form to **APIs or local servers**.

---

## **A) Practice Commands**

```bash
# 1) Create a fresh project for form handling
flutter create --empty form_lab
cd form_lab

# 2) Add required packages (for APIs or state management if needed)
flutter pub add http
flutter pub add provider   # optional, if managing login state

# 3) Run the project
flutter run
```

If you want to simulate backend APIs locally, you can use `json-server` as suggested in the PDF:

```bash
npm install -g json-server
json-server --watch data.json --port 3000
```

---

## **B) Basic Login Form with Validation**

This example matches the slides’ focus on using `Form`, `TextFormField`, and **form validation**.

> Paste this into `lib/main.dart`:

```dart
import 'package:flutter/material.dart';

void main() => runApp(const FormLabApp());

class FormLabApp extends StatelessWidget {
  const FormLabApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Form Validation Lab',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.teal),
      home: const LoginScreen(),
    );
  }
}

class LoginScreen extends StatefulWidget {
  const LoginScreen({super.key});
  @override
  State<LoginScreen> createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();
  bool _loading = false;

  void _login() {
    if (_formKey.currentState!.validate()) {
      setState(() => _loading = true);

      // Simulate async API call
      Future.delayed(const Duration(seconds: 2), () {
        setState(() => _loading = false);

        ScaffoldMessenger.of(context).showSnackBar(
          SnackBar(
            content: Text(
                'Welcome, ${_emailController.text}! Password length: ${_passwordController.text.length}'),
          ),
        );
      });
    }
  }

  @override
  void dispose() {
    _emailController.dispose();
    _passwordController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Login Page")),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                controller: _emailController,
                keyboardType: TextInputType.emailAddress,
                decoration: const InputDecoration(
                  labelText: 'Email',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Email is required';
                  }
                  if (!RegExp(r'^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(value)) {
                    return 'Enter a valid email';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 16),
              TextFormField(
                controller: _passwordController,
                obscureText: true,
                decoration: const InputDecoration(
                  labelText: 'Password',
                  border: OutlineInputBorder(),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Password is required';
                  }
                  if (value.length < 6) {
                    return 'Password must be at least 6 characters';
                  }
                  return null;
                },
              ),
              const SizedBox(height: 24),
              _loading
                  ? const CircularProgressIndicator()
                  : ElevatedButton(
                      onPressed: _login,
                      child: const Text('Login'),
                    ),
            ],
          ),
        ),
      ),
    );
  }
}
```

---

## **C) Adding API Authentication (Optional)**

The PDF also references connecting login forms to **Web APIs**.
Here's how you integrate API calls:

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

Future<bool> loginUser(String email, String password) async {
  final response = await http.post(
    Uri.parse('http://localhost:3000/login'),
    headers: {'Content-Type': 'application/json'},
    body: json.encode({'email': email, 'password': password}),
  );

  if (response.statusCode == 200) {
    return true; // success
  } else {
    return false; // failed
  }
}
```

Then call this inside `_login()` and handle success/failure accordingly.

---

## **D) Important Form Widgets (From the Slides)**

| **Widget**                    | **Purpose**                           |
| ----------------------------- | ------------------------------------- |
| **`Form`**                    | Groups fields and manages validation  |
| **`TextFormField`**           | Input fields with built-in validation |
| **`InputDecoration`**         | Adds labels, hints, and styles        |
| **`DropdownButtonFormField`** | Dropdown inside forms                 |
| **`TextEditingController`**   | Controls and retrieves field data     |
| **`GlobalKey<FormState>`**    | Tracks form state for validation      |

---

## **E) Hands-on Drills**

| **Exercise**                     | **Goal**                                |
| -------------------------------- | --------------------------------------- |
| **Email & Password Validation**  | Test invalid inputs, empty fields, etc. |
| **Add a Confirm Password Field** | Validate matching passwords             |
| **Integrate API Authentication** | Use `json-server` or real APIs          |
| **Add “Remember Me” Checkbox**   | Manage additional form state            |
| **Use Provider for Auth State**  | Store login status globally             |

---

## **Summary for Section 6**

| **Aspect**      | **Details**                                                           |
| --------------- | --------------------------------------------------------------------- |
| **Topic**       | Forms, validation, authentication                                     |
| **Key Widgets** | `Form`, `TextFormField`, `InputDecoration`, `DropdownButtonFormField` |
| **Integration** | Local `json-server` or live Web API                                   |
| **Goal**        | Build a login/register form with full validation                      |

---

Alright, CJ 🙂
Let's work on **Section 7 — Building a Frontend Application with Flutter** from your PDF.
This section focuses on combining concepts from earlier sections (**widgets, forms, state management, API integration, routing**) into a **complete multi-screen Flutter application** that manages **user data** (add, edit, delete, display).

From the slides, this section demonstrates:

* **Frontend app structure**
* **Side Menu navigation**
* **Login page implementation**
* **User data handling** with **ListView, JSON, APIs**
* **Add/Edit/Delete user features**.

I’ll give you:

1. **Project setup & required commands**
2. **Application architecture**
3. **Complete runnable example**
4. **Self-learning drills**

---

# **SECTION 7 — Frontend Application with Flutter**

---

## **A) Practice Commands**

```bash
# 1) Create a new project for the full app
flutter create frontend_lab
cd frontend_lab

# 2) Add dependencies (for API, state, and JSON)
flutter pub add http
flutter pub add provider

# 3) Run the app with hot reload
flutter run
```

---

## **B) App Architecture Overview**

This section builds a **user management app** based on the PDF content:

```
lib/
 ├── main.dart            → App entry point & routes
 ├── models/
 │    └── user.dart       → User model class
 ├── services/
 │    └── api_service.dart → API calls (GET, POST, PUT, DELETE)
 ├── providers/
 │    └── user_provider.dart → State management using Provider
 ├── screens/
 │    ├── home_screen.dart    → List of users
 │    ├── add_user_screen.dart → Add new user form
 │    ├── edit_user_screen.dart → Edit existing user form
 │    └── user_detail_screen.dart → Show user info
```

---

## **C) Step 1 — Define the User Model (`models/user.dart`)**

```dart
class User {
  final int id;
  final String name;
  final String email;

  User({required this.id, required this.name, required this.email});

  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
    };
  }
}
```

---

## **D) Step 2 — API Service (`services/api_service.dart`)**

Handles data fetching from a REST API (or local JSON server).

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';
import '../models/user.dart';

class ApiService {
  static const String baseUrl = 'http://localhost:3000/users';

  Future<List<User>> fetchUsers() async {
    final response = await http.get(Uri.parse(baseUrl));
    if (response.statusCode == 200) {
      final List<dynamic> data = json.decode(response.body);
      return data.map((e) => User.fromJson(e)).toList();
    } else {
      throw Exception('Failed to fetch users');
    }
  }

  Future<User> addUser(User user) async {
    final response = await http.post(
      Uri.parse(baseUrl),
      headers: {'Content-Type': 'application/json'},
      body: json.encode(user.toJson()),
    );
    if (response.statusCode == 201) {
      return User.fromJson(json.decode(response.body));
    } else {
      throw Exception('Failed to add user');
    }
  }

  Future<void> deleteUser(int id) async {
    final response = await http.delete(Uri.parse('$baseUrl/$id'));
    if (response.statusCode != 200) {
      throw Exception('Failed to delete user');
    }
  }
}
```

---

## **E) Step 3 — State Management (`providers/user_provider.dart`)**

```dart
import 'package:flutter/material.dart';
import '../models/user.dart';
import '../services/api_service.dart';

class UserProvider extends ChangeNotifier {
  final ApiService _api = ApiService();
  List<User> _users = [];

  List<User> get users => _users;

  Future<void> loadUsers() async {
    _users = await _api.fetchUsers();
    notifyListeners();
  }

  Future<void> addUser(User user) async {
    final newUser = await _api.addUser(user);
    _users.add(newUser);
    notifyListeners();
  }

  Future<void> deleteUser(int id) async {
    await _api.deleteUser(id);
    _users.removeWhere((user) => user.id == id);
    notifyListeners();
  }
}
```

---

## **F) Step 4 — App Entry Point & Routes (`main.dart`)**

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'providers/user_provider.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => UserProvider(),
      child: const FrontendApp(),
    ),
  );
}

class FrontendApp extends StatelessWidget {
  const FrontendApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Frontend App',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.teal),
      home: const HomeScreen(),
    );
  }
}
```

---

## **G) Step 5 — Home Screen (`screens/home_screen.dart`)**

Displays all users from the API.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../providers/user_provider.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});
  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  @override
  void initState() {
    super.initState();
    Future.microtask(() =>
        Provider.of<UserProvider>(context, listen: false).loadUsers());
  }

  @override
  Widget build(BuildContext context) {
    final userProvider = Provider.of<UserProvider>(context);

    return Scaffold(
      appBar: AppBar(title: const Text('Users')),
      body: userProvider.users.isEmpty
          ? const Center(child: CircularProgressIndicator())
          : ListView.builder(
              itemCount: userProvider.users.length,
              itemBuilder: (context, index) {
                final user = userProvider.users[index];
                return ListTile(
                  leading: const Icon(Icons.person),
                  title: Text(user.name),
                  subtitle: Text(user.email),
                  trailing: IconButton(
                    icon: const Icon(Icons.delete, color: Colors.red),
                    onPressed: () => userProvider.deleteUser(user.id),
                  ),
                );
              },
            ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Implement Add User Screen
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

## **H) Optional — Add/Edit User Screens**

Using **TextFormField**, similar to **Section 6**, you can create forms to add or update users.
The process mirrors login form validation but sends the data to your API.

---

## **I) Hands-on Drills**

| **Exercise**                 | **Goal**                                |
| ---------------------------- | --------------------------------------- |
| **Create Login Screen**      | Secure the app before showing user list |
| **Implement Add User**       | Form with validation + POST to API      |
| **Implement Edit User**      | Pre-fill fields + PUT to API            |
| **Add Pagination**           | Load more users on scroll               |
| **Improve UI**               | Add `Drawer` for side menu navigation   |
| **Integrate Authentication** | Use API tokens + secure storage         |

---

## **J) Summary of Section 7**

| **Aspect**       | **Details**                                          |
| ---------------- | ---------------------------------------------------- |
| **Topic**        | Build a complete **Frontend Flutter App**            |
| **Key Focus**    | Multi-screen navigation, CRUD with API               |
| **Main Widgets** | `Scaffold`, `ListView`, `ListTile`, `Form`, `Drawer` |
| **Packages**     | `http`, `provider`                                   |
| **Outcome**      | A fully functional, data-driven Flutter app          |

---
Alright CJ 🙂
Let's dive into **Section 8 — Web API & Asynchronous Programming (Advanced)** from your Flutter PDF.
This section extends what you learned in Section 4 by **integrating RESTful APIs**, working with **JSON data**, using **async/await**, and building **dynamic Flutter UIs** based on server responses.
It also references using APIs like **randomuser.me** and **fakestoreapi.com**.

I’ll give you:

1. **Setup & required commands**
2. **Core concepts explained**
3. **Full runnable example (API + JSON + ListView)**
4. **Asynchronous patterns**
5. **Self-learning drills**

---

# **SECTION 8 — Web API & Asynchronous Programming (Advanced)**

---

## **A) Practice Commands**

```bash
# 1) Create a new Flutter project
flutter create --empty api_advanced_lab
cd api_advanced_lab

# 2) Add the HTTP package for network requests
flutter pub add http

# 3) Run the project with hot reload
flutter run
```

**Optional (for local testing, as per PDF instructions):**

```bash
npm install -g json-server
json-server --watch data.json --port 3000
```

---

## **B) Core Concepts Covered in Section 8**

| **Concept**        | **Description**                                                      |
| ------------------ | -------------------------------------------------------------------- |
| **Web API**        | Interfaces that allow Flutter apps to interact with backend services |
| **HTTP Requests**  | Using **GET, POST, PUT, DELETE** methods via the `http` package      |
| **JSON**           | Fetching structured data and converting it into Dart models          |
| **Async/Await**    | Handling network requests without blocking the UI                    |
| **ListView**       | Displaying fetched data dynamically in a scrollable list             |
| **Error Handling** | Handling timeouts, network errors, and invalid responses             |

---

## **C) Example: Fetch Data from an API + Show in ListView**

This runnable example uses the **Fake Store API** to fetch and display product data, similar to the example from the slides.

> Paste into `lib/main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(const ApiAdvancedApp());

class ApiAdvancedApp extends StatelessWidget {
  const ApiAdvancedApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Web API & Async Demo',
      theme: ThemeData(useMaterial3: true, colorSchemeSeed: Colors.blue),
      home: const ProductListScreen(),
    );
  }
}

class ProductListScreen extends StatefulWidget {
  const ProductListScreen({super.key});

  @override
  State<ProductListScreen> createState() => _ProductListScreenState();
}

class _ProductListScreenState extends State<ProductListScreen> {
  late Future<List<dynamic>> _products;

  @override
  void initState() {
    super.initState();
    _products = fetchProducts();
  }

  Future<List<dynamic>> fetchProducts() async {
    try {
      final url = Uri.parse('https://fakestoreapi.com/products');
      final response = await http.get(url);

      if (response.statusCode == 200) {
        return json.decode(response.body);
      } else {
        throw Exception('Failed to fetch products');
      }
    } catch (e) {
      throw Exception('Network Error: $e');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Product List')),
      body: FutureBuilder<List<dynamic>>(
        future: _products,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return const Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(child: Text('Error: ${snapshot.error}'));
          } else if (!snapshot.hasData || snapshot.data!.isEmpty) {
            return const Center(child: Text('No products found.'));
          }

          final products = snapshot.data!;
          return ListView.builder(
            itemCount: products.length,
            itemBuilder: (context, index) {
              final product = products[index];
              return Card(
                elevation: 3,
                margin: const EdgeInsets.symmetric(vertical: 8, horizontal: 12),
                child: ListTile(
                  leading: Image.network(
                    product['image'],
                    width: 50,
                    height: 50,
                    fit: BoxFit.cover,
                  ),
                  title: Text(product['title']),
                  subtitle: Text("\$${product['price']}"),
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

---

## **D) Working with JSON in Flutter**

From the PDF, JSON is the **main data format** used in Web APIs.

**Steps:**

1. Fetch JSON response from the API.
2. Parse it using `json.decode()` from **dart\:convert**.
3. Convert it into **Dart model classes** (optional but recommended).
4. Use the models to build dynamic UIs.

**Tip:** Use [https://app.quicktype.io](https://app.quicktype.io) (as mentioned in the slides) to generate model classes automatically.

---

## **E) Asynchronous Patterns**

Section 8 highlights `async` and `await` usage.

**Basic pattern:**

```dart
Future<void> getData() async {
  try {
    final response = await http.get(Uri.parse("https://example.com/data"));
    if (response.statusCode == 200) {
      print(json.decode(response.body));
    } else {
      print("Error: ${response.statusCode}");
    }
  } catch (e) {
    print("Network Error: $e");
  }
}
```

---

## **F) Hands-on Self-Learning Drills**

| **Exercise**                 | **Goal**                                           |
| ---------------------------- | -------------------------------------------------- |
| Fetch random users           | Use **randomuser.me** API and show names & avatars |
| Add pull-to-refresh          | Use `RefreshIndicator` to reload API data          |
| Add a search bar             | Filter API results locally                         |
| Handle API errors gracefully | Show a Snackbar for failures                       |
| Cache API data               | Use `shared_preferences` for offline access        |
| Convert JSON → Dart models   | Practice using quicktype.io                        |

---

## **G) Summary of Section 8**

| **Aspect**       | **Details**                                     |
| ---------------- | ----------------------------------------------- |
| **Topic**        | Fetching & displaying API data                  |
| **Key Concepts** | Web APIs, JSON, async/await, error handling     |
| **Packages**     | `http`                                          |
| **Widgets**      | `FutureBuilder`, `ListView.builder`, `ListTile` |
| **Output**       | A data-driven, dynamic Flutter UI               |

---
