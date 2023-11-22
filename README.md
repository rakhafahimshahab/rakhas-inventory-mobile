# rakhas_inventory_mobile

# Assignment 7
## Questions
### 1. What are the main differences between stateless and stateful widget in Flutter?
Stateless widgets in Flutter are immutable and do not hold any state that changes over time. They are simple and efficient, perfect for static elements in your UI, re-rendering only when external factors, such as parent widgets, trigger a change. On the other hand, stateful widgets are dynamic and maintain state that can change during the widget's lifetime. They have a more complex lifecycle, involving a separate State object that persists over time and allows for interactive elements, like toggles or text inputs, to update and rebuild the UI when internal state changes, typically triggered by user actions or data responses. The choice between them hinges on whether the UI component needs to update dynamically or remain static throughout its presence on the screen.
### 2. Explain all widgets that you used in this assignment.
- `MaterialApp`: This is the top-level widget for a Flutter app using Material Design.
- `ThemeData`: This defines the color and typographic values for your application's theme.
- `Scaffold`: Scaffold provides the basic visual layout structure of the material design.
- `AppBar`: It is a material design app bar that appears at the top of the application.
- `Padding`: A widget that adds padding around its child.
- `Column`: This layout widget arranges its children vertically. 
- `Text`: Displays a string of text with the given style.
- `GridView.count`: A grid layout widget that creates a fixed number of tiles in the cross-axis.
- `MenuCard`: This is a custom StatelessWidget that you've defined to represent each menu item.
- `InkWell`: A rectangular area of a Material that responds to touch.
- `Container`: A widget that combines common painting, positioning, and sizing of its child.
- `Center`: This widget centers its child within itself.
- `Icon`: A graphic representation of a material icon.
- `SnackBar`: A message widget that appears at the bottom of the screen to provide feedback about an operation.
## Steps
### 1. create new flutter project
    ```
    flutter create inventaris_mobile
    cd inventaris_mobile
    flutter run
    ```
### 2. Modify main.dart and create menu.dart
1. main.dart
    ```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/menu.dart';

    void main() {
    runApp(const MyApp());
    }

    class MyApp extends StatelessWidget {
    const MyApp({super.key});

    // This widget is the root of your application.
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
        title: 'Inventory',
        theme: ThemeData(
            // This is the theme of your application.
            //
            // TRY THIS: Try running your application with "flutter run". You'll see
            // the application has a blue toolbar. Then, without quitting the app,
            // try changing the seedColor in the colorScheme below to Colors.green
            // and then invoke "hot reload" (save your changes or press the "hot
            // reload" button in a Flutter-supported IDE, or press "r" if you used
            // the command line to start the app).
            //
            // Notice that the counter didn't reset back to zero; the application
            // state is not lost during the reload. To reset the state, use hot
            // restart instead.
            //
            // This works for code too, not just values: Most code changes can be
            // tested with just a hot reload.
            colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
            useMaterial3: true,
        ),
        home: MyHomePage(),
        );
    }
    }
    ```
2. menu.dart
    ```
    import 'package:flutter/material.dart';

    class MenuItem {
    final String name;
    final IconData icon;

    MenuItem(this.name, this.icon);
    }

    class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    final List<MenuItem> items = [
        MenuItem("View Item", Icons.checklist),
        MenuItem("Add Item", Icons.add),
        MenuItem("Logout", Icons.logout),
    ];

    // This widget is the home page of your application. It is stateful, meaning
    // that it has a State object (defined below) that contains fields that affect
    // how it looks.

    // This class is the configuration for the state. It holds the values (in this
    // case the title) provided by the parent (in this case the App widget) and
    // used by the build method of the State. Fields in a Widget subclass are
    // always marked "final".

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: const Text(
            'Inventory',
            ),
        ),
        body: SingleChildScrollView(
            // Scrolling wrapper widget
            child: Padding(
            padding: const EdgeInsets.all(10.0), // Set padding for the page
            child: Column(
                // Widget to display children vertically
                children: <Widget>[
                const Padding(
                    padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                    // Text widget to display text with center alignment and appropriate style
                    child: Text(
                    "Rakha's Inventory", // Text indicating the shop name
                    textAlign: TextAlign.center,
                    style: TextStyle(
                        fontSize: 30,
                        fontWeight: FontWeight.bold,
                    ),
                    ),
                ),
                // Grid layout
                GridView.count(
                    // Container for our cards.
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    shrinkWrap: true,
                    children: items.map((MenuItem item) {
                    // Iteration for each item
                    return MenuCard(item);
                    }).toList(),
                ),
                ],
            ),
            ),
        ),
        );
    }
    }

    class MenuCard extends StatelessWidget {
    final MenuItem item;

    const MenuCard(this.item, {Key? key}); // Constructor

    @override
    Widget build(BuildContext context) {
        return Material(
        color: Colors.indigo,
        child: InkWell(
            // Responsive touch area
            onTap: () {
            // Show a SnackBar when clicked
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("You pressed the ${item.name} button!")));
            },
            child: Container(
            // Container to hold Icon and Text
            padding: const EdgeInsets.all(8),
            child: Center(
                child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                    Icon(
                    item.icon,
                    color: Colors.white,
                    size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                    item.name,
                    textAlign: TextAlign.center,
                    style: const TextStyle(color: Colors.white),
                    ),
                ],
                ),
            ),
            ),
        ),
        );
    }
    }
    ```
# Assignment 8
## Questions
### 1. Explain the difference between `Navigator.push()` and `Navigator.pushReplacement()`, accompanied by examples of the correct usage of both methods!
push() maintains the current screen in the stack, whereas pushReplacement() removes it.With push(), the back button takes you to the previous screen. With pushReplacement(), the back button does not take you to the replaced screen.push() is for temporary navigation where returning is expected. pushReplacement() is for permanent navigation transitions, like logging in or completing a workflow.
Example `Navigator.push()`:
```
    Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => NewScreen()),
    );
```
Example `Navigator.pushReplacement()`:
```
    Navigator.pushReplacement(
    context,
    MaterialPageRoute(builder: (context) => HomeScreen()),
    );

```
### 2. Explain each layout widget in Flutter and their respective usage contexts!
In Flutter, layout widgets are essential for structuring and styling user interfaces. The Container widget is a multi-purpose tool used for creating a customizable rectangular area, ideal for adding decorations like colors, borders, or shadows, and for applying margins, padding, and constraints. Row and Column are linear layout widgets; the former arranges children horizontally and the latter vertically, perfect for aligning items like text and buttons in a single line. The Stack widget allows overlapping of elements, enabling designs where components like text overlay images. For grid-based layouts, like photo galleries or item grids, GridView organizes widgets in a two-dimensional array, adjusting neatly to varying screen sizes.

For displaying scrollable lists, ListView is the go-to widget, efficiently handling long lists by rendering only visible items, thus saving memory. Padding is a straightforward widget, crucial for creating readable and aesthetically pleasing layouts by adding space around elements. In complex layouts, especially within Rows or Columns, Expanded and Flexible widgets are vital; they manage space distribution, with Expanded dividing space evenly and Flexible offering more nuanced control. Each of these widgets plays a distinct role in creating intuitive, responsive, and visually appealing interfaces in Flutter applications.

### 3. List the form input elements you used in this assignment and explain why you used these input elements!
- `Text Field`: Used for single-line text input, such as names or email addresses. It's the most basic form of input for collecting short text responses.
- `Textarea`: Ideal for multi-line text input, like comments or messages. It allows users to enter longer, free-form text.
- `Checkbox`: Suitable for options that can be selected independently of others, like agreeing to terms and conditions. Checkboxes are used when multiple choices are allowed.
- `Radio Buttons`: Used for mutually exclusive selections, where only one option can be chosen out of a set, such as selecting a gender or a payment method.
- `Dropdown Menu` (Select Box): Efficient for saving space when there's a list of multiple options, and only one selection is allowed, like choosing a country from a list.
- `Date Picker`: Facilitates the entry of dates, providing a calendar interface to select a specific day, month, and year. It ensures the user inputs a valid date format.
- `File Input`: Allows users to upload files, like images or documents. It's crucial for forms that require document attachments or image uploads.
- `Submit Button`: Essential for form submission. It signals the form completion and triggers the process to send data to the server or handle it in some other predefined manner.
- `Reset Button`: Clears all the inputs in a form. It's less commonly used nowadays, as it can lead to accidental data loss, but it might be included for convenience in long forms.

### 4. How is clean architecture implemented in a Flutter application?
Clean Architecture in Flutter involves structuring the app into three main layers: the Presentation Layer, which handles UI and state management using Flutter widgets; the Domain Layer, serving as the core of the application with business logic, use cases, and entity definitions; and the Data Layer, responsible for data retrieval, storage, and conversion. This architecture emphasizes separation of concerns, where each layer operates independently but communicates with others through well-defined interfaces. It ensures scalability and maintainability by keeping the business logic central and independent of UI and external data sources. The implementation typically includes a clear directory structure, dependency injection for managing dependencies between layers, and a focus on making each layer independently testable. This approach not only enhances the testability and maintainability of the application but also aligns with best practices in software development for creating robust, scalable Flutter applications.

## Steps
### 1. Create Screens folder with item_form.dart and alocate menu.dart
1. item_form.dart
```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/widget/left_drawer.dart';

    class ItemFormPage extends StatefulWidget {
    const ItemFormPage({super.key});

    @override
    State<ItemFormPage> createState() => _ItemFormPageState();
    }

    class _ItemFormPageState extends State<ItemFormPage> {
    final _formKey = GlobalKey<FormState>();
    String _name = "";
    int _amount = 0;
    String _category = "";
    String _description = "";

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: const Center(
            child: Text(
                'Add Item Form',
            ),
            ),
            backgroundColor: Colors.teal,
            foregroundColor: Colors.white,
        ),
        // Adding the previously created drawer here
        drawer: const LeftDrawer(),
        body: Form(
            key: _formKey,
            child: SingleChildScrollView(
            child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Item Name",
                        labelText: "Item Name",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _name = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _name = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Name cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Amount",
                        labelText: "Amount",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _amount = int.tryParse(value!) ?? _amount;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _amount = int.tryParse(value!) ?? _amount;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Amount cannot be empty!";
                        }
                        if (int.tryParse(value) == null) {
                            return "Amount must be a number!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Category",
                        labelText: "Category",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _category = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _category = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Category cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Description",
                        labelText: "Description",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _description = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _description = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Description cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Align(
                    alignment: Alignment.bottomCenter,
                    child: Padding(
                        padding: const EdgeInsets.all(8.0),
                        child: ElevatedButton(
                        style: ButtonStyle(
                            backgroundColor:
                            MaterialStateProperty.all(Colors.teal),
                        ),
                        onPressed: () {
                            if (_formKey.currentState!.validate()) {
                            showDialog(
                                context: context,
                                builder: (context) {
                                return AlertDialog(
                                    title: const Text('Item successfully saved'),
                                    content: SingleChildScrollView(
                                    child: Column(
                                        crossAxisAlignment:
                                        CrossAxisAlignment.start,
                                        children: [
                                        // Display other values here
                                        Text('Name: $_name'),
                                        Text('Amount: $_amount'),
                                        Text('Category: $_category'),
                                        Text('Description: $_description')
                                        ],
                                    ),
                                    ),
                                    actions: [
                                    TextButton(
                                        child: const Text('OK'),
                                        onPressed: () {
                                        Navigator.pop(context);
                                        },
                                    ),
                                    ],
                                );
                                },
                            );
                            // Reset the form after the dialog is displayed
                            _formKey.currentState!.reset();
                            }
                        },
                        child: const Text(
                            "Save",
                            style: TextStyle(color: Colors.white),
                        ),
                        ),
                    ),
                    ),
                ]
            ),
            ),
        ),
        );
    }
    }
```

2. menu.dart cut the menucard class and paste it on menu_card.dart later on
```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/widget/left_drawer.dart';
    import 'package:rakhas_inventory/widget/menu_card.dart';


    class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    final List<MenuItem> items = [
        MenuItem("View Item", Icons.checklist, Colors.cyan),
        MenuItem("Add Item", Icons.add,Colors.blueAccent),
        MenuItem("Logout", Icons.logout,Colors.cyanAccent),
    ];

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: const Text(
            'Inventory',
            ),
            backgroundColor: Colors.teal,
            foregroundColor: Colors.white,
        ),
        drawer: const LeftDrawer(),
        body: SingleChildScrollView(
            // Scrolling wrapper widget
            child: Padding(
            padding: const EdgeInsets.all(10.0), // Set padding for the page
            child: Column(
                // Widget to display children vertically
                children: <Widget>[
                const Padding(
                    padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                    child: Text(
                    "Rakha's Inventory", // Text indicating the shop name
                    textAlign: TextAlign.center,
                    style: TextStyle(
                        fontSize: 30,
                        fontWeight: FontWeight.bold,
                    ),
                    ),
                ),
                // Grid layout
                GridView.count(
                    // Container for our cards.
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    shrinkWrap: true,
                    children: items.map((MenuItem item) {
                    // Iteration for each item
                    return MenuCard(item);
                    }).toList(),
                ),
                ],
            ),
            ),
        ),
        );
    }
    }
```
### 2. Create widget folder with left_drawer.dart and menu_card.dart
1. left_drawer.dart
```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/screens/menu.dart';
    import 'package:rakhas_inventory/screens/item_form.dart';

    class LeftDrawer extends StatelessWidget {
    const LeftDrawer({super.key});

    @override
    Widget build(BuildContext context) {
        return Drawer(
        child: ListView(
            children: [
            const DrawerHeader(
                decoration: BoxDecoration(
                color: Colors.teal,
                ),
                child: Column(
                children: [
                    Text(
                    'Item List',
                    textAlign: TextAlign.center,
                    style: TextStyle(
                        fontSize: 30,
                        fontWeight: FontWeight.bold,
                        color: Colors.white,
                    ),
                    ),
                    Padding(padding: EdgeInsets.all(10)),
                    Text("Write all your item needs here!",
                    style: TextStyle(
                        fontSize: 15,
                        color: Colors.white,
                        fontWeight: FontWeight.w100,
                    ),
                    textAlign: TextAlign.center,
                    ),
                ],
                ),
            ),
            ListTile(
                leading: const Icon(Icons.home_outlined),
                title: const Text('Home Page'),
                // redirect to MyHomePage
                onTap: () {
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(
                        builder: (context) => MyHomePage(),
                    ));
                },
            ),
            ListTile(
                leading: const Icon(Icons.add),
                title: const Text('Add Item'),
                // redirect to ShopFormPage
                onTap: () {
                /*
        TODO: Create routing to ShopFormPage here
        */
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => ItemFormPage())
                );
                },
            ),
            ],
        ),
        );
    }
    }
```
2. menu_card.dart
```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/screens/item_form.dart';


    class MenuItem {
    final String name;
    final IconData icon;
    final Color color;

    MenuItem(this.name, this.icon,this.color);
    }

    class MenuCard extends StatelessWidget {
    final MenuItem item;

    const MenuCard(this.item, {Key? key}); // Constructor

    @override
    Widget build(BuildContext context) {
        return Material(
        color: item.color,
        child: InkWell(
            // Responsive touch area
            onTap: () {
            // Show a SnackBar when clicked
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("You pressed the ${item.name} button!")));
            if (item.name == "Add Item") {
                Navigator.push(
                context,
                MaterialPageRoute(
                    builder: (context) => ItemFormPage(),
                ),
                );
            }
            },
            child: Container(
            // Container to hold Icon and Text
            padding: const EdgeInsets.all(8),
            child: Center(
                child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                    Icon(
                    item.icon,
                    color: Colors.white,
                    size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                    item.name,
                    textAlign: TextAlign.center,
                    style: const TextStyle(color: Colors.white),
                    ),
                ],
                ),
            ),
            ),
        ),
        );
    }
    }
```

# Assignment 9
## Questions
### 1. Can we retrieve JSON data without creating a model first? If yes, is it better than creating a model before retrieving JSON data?
Yes, it is possible to retrieve JSON data in Flutter without creating a model first. This can be done by directly parsing the JSON data into a dynamic type or a map in Dart. However, creating a model before retrieving JSON data offers several advantages. It enhances code readability, makes the data easier to manage, and helps in maintaining type safety, which is crucial for large and complex applications. Models act as a blueprint for the data, ensuring that only valid data is processed and helping in catching errors early in the development process.
### 2. Explain the function of CookieRequest and explain why a CookieRequest instance needs to be shared with all components in a Flutter application.
CookieRequest is not a standard class or function in Flutter. However, if we consider a hypothetical CookieRequest in the context of web and network programming, it would likely be a class or function designed to handle HTTP cookies in network requests. In a Flutter application, sharing a CookieRequest instance across different components would be important to maintain session consistency. This ensures that all components of the app use the same session data, like authentication tokens or user preferences, leading to a seamless user experience and consistent data handling across the application.
### 3. Explain the mechanism of fetching data from JSON until it can be displayed on Flutter.
- *Making a Network Request*: Using packages like http to send a network request to a server.
- *Receiving the JSON Response*: The server responds with JSON-formatted data.
- *Parsing the JSON Data*: The received JSON data is parsed. This can be done directly into a map or by using a model class that represents the JSON structure.
- *Using the Data in the App*: The parsed data is then used to update the application's state, which can be displayed in the UI. Flutter's widgets rebuild themselves when their state changes, allowing the new data to be displayed.
### 4. Explain the authentication mechanism from entering account data on Flutter to Django authentication completion and the display of menus on Flutter.
- *Entering Account Data*: The user enters account data (like username and password) in the Flutter app.
- *Sending Authentication Request*: The app sends these credentials to the Django backend, usually as a POST request.
- *Django Authentication Process*: Django processes the request. This involves verifying the credentials against the database.
- *Response and Token Generation*: If authenticated, Django sends back a response, often including a token (like a JWT) for session management.
- *Token Storage in Flutter*: The Flutter app stores this token securely (possibly using a package like flutter_secure_storage).
- *Accessing Secured Resources*: The app uses this token in subsequent requests to access protected resources.
- *Display of Menus*: Once authenticated, the Flutter app updates its state and UI to display menus and features available to the authenticated user.
### 5. List all the widgets you used in this assignment and explain their respective functions.
- `ListView`:  is a scrollable list widget used in Flutter to display a list of items.
-  `FutureBuilder`:  It is used to perform asynchronous tasks and display the results once the task is complete.
- `TextFormField`:  is a form field widget that allows users to enter text. 
- `ElevatedButton`: is a Material Design button widget that appears to be raised (or elevated) above the UI.
- `InkWell`:  is a rectangular area of a Material that responds to touch actions.
## Steps
### 1. Creating Authentication
1. make login.dart in screens folder
```
    import 'package:rakhas_inventory/screens/menu.dart';
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';

    void main() {
    runApp(const LoginApp());
    }

    class LoginApp extends StatelessWidget {
    const LoginApp({super.key});

    @override
    Widget build(BuildContext context) {
        return MaterialApp(
        title: 'Login',
        theme: ThemeData(
            primarySwatch: Colors.teal,
        ),
        home: const LoginPage(),
        );
    }
    }

    class LoginPage extends StatefulWidget {
    const LoginPage({super.key});

    @override
    _LoginPageState createState() => _LoginPageState();
    }

    class _LoginPageState extends State<LoginPage> {
    final TextEditingController _usernameController = TextEditingController();
    final TextEditingController _passwordController = TextEditingController();

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
        appBar: AppBar(
            title: const Text('Login'),
        ),
        body: Container(
            padding: const EdgeInsets.all(16.0),
            child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
                TextField(
                controller: _usernameController,
                decoration: const InputDecoration(
                    labelText: 'Username',
                ),
                ),
                const SizedBox(height: 12.0),
                TextField(
                controller: _passwordController,
                decoration: const InputDecoration(
                    labelText: 'Password',
                ),
                obscureText: true,
                ),
                const SizedBox(height: 24.0),
                ElevatedButton(
                onPressed: () async {
                    String username = _usernameController.text;
                    String password = _passwordController.text;

                    // Check credentials
                    // TODO: Change the URL and don't forget to add a trailing slash (/) at the end of the URL!
                    // To connect the Android emulator to Django on localhost,
                    // use the URL http://10.0.2.2/
                    final response = await request.login("http://localhost:8000/auth/login/", {
                    'username': username,
                    'password': password,
                    });

                    if (request.loggedIn) {
                    String message = response['message'];
                    String uname = response['username'];
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(builder: (context) => MyHomePage()),
                    );
                    ScaffoldMessenger.of(context)
                        ..hideCurrentSnackBar()
                        ..showSnackBar(
                            SnackBar(content: Text("$message Welcome, $uname.")));
                    } else {
                    showDialog(
                        context: context,
                        builder: (context) => AlertDialog(
                        title: const Text('Login Failed'),
                        content:
                        Text(response['message']),
                        actions: [
                            TextButton(
                            child: const Text('OK'),
                            onPressed: () {
                                Navigator.pop(context);
                            },
                            ),
                        ],
                        ),
                    );
                    }
                },
                child: const Text('Login'),
                ),
            ],
            ),
        ),
        );
    }
    }
```
2. Make authentication app in django project
views.py:
```
    from django.shortcuts import render
    from django.contrib.auth import authenticate, login as auth_login
    from django.http import JsonResponse
    from django.views.decorators.csrf import csrf_exempt
    from django.contrib.auth import logout as auth_logout

    @csrf_exempt
    def login(request):
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(username=username, password=password)
        if user is not None:
            if user.is_active:
                auth_login(request, user)
                # Successful login status.
                return JsonResponse({
                    "username": user.username,
                    "status": True,
                    "message": "Login successful!"
                    # Add other data if you want to send data to Flutter.
                }, status=200)
            else:
                return JsonResponse({
                    "status": False,
                    "message": "Login failed, account disabled."
                }, status=401)

        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, check email or password again."
            }, status=401)
        
    @csrf_exempt
    def logout(request):
        username = request.user.username

        try:
            auth_logout(request)
            return JsonResponse({
                "username": username,
                "status": True,
                "message": "Logged out successfully!"
            }, status=200)
        except:
            return JsonResponse({
            "status": False,
            "message": "Logout failed."
            }, status=401)

```
urls.py:
```
    from django.urls import path
    from authentication.views import login,logout

    app_name = 'authentication'

    urlpatterns = [
        path('login/', login, name='login'),
        path('logout/', logout, name='logout'),
    ]
```
also add the routing to the new app in the project folder

### 2. Custom Model
create items.dart in a new folder called model\
run django server and goto your json path in local server\
copy paste json code to [QuickType](https://app.quicktype.io)
```
    // To parse this JSON data, do
    //
    //     final item = itemFromJson(jsonString);

    import 'dart:convert';

    List<Item> itemFromJson(String str) => List<Item>.from(json.decode(str).map((x) => Item.fromJson(x)));

    String itemToJson(List<Item> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

    class Item {
    String model;
    int pk;
    Fields fields;

    Item({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory Item.fromJson(Map<String, dynamic> json) => Item(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
    }

    class Fields {
    int user;
    String name;
    String category;
    int amount;
    String description;

    Fields({
        required this.user,
        required this.name,
        required this.category,
        required this.amount,
        required this.description,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        category: json["category"],
        amount: json["amount"],
        description: json["description"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "category": category,
        "amount": amount,
        "description": description,
    };
    }

```
### 3. Creating View Item Screen
1. In django main app add this code to views.py
```
    @csrf_exempt
    def create_product_flutter(request):
        if request.method == 'POST':
            
            data = json.loads(request.body)

            new_product = Product.objects.create(
                user = request.user,
                name = data["name"],
                amount = int(data["amount"]),
                category = data["category"],
                description = data["description"]
            )

            new_product.save()

            return JsonResponse({"status": "success"}, status=200)
        else:
            return JsonResponse({"status": "error"}, status=401)
```
2. Create list_item.dart in screens folder
```
    import 'package:flutter/material.dart';
    import 'package:http/http.dart' as http;
    import 'dart:convert';
    import 'package:rakhas_inventory/models/items.dart';
    import 'package:rakhas_inventory/widget/left_drawer.dart';
    import 'package:rakhas_inventory/screens/item_detail.dart';

    class ItemPage extends StatefulWidget {
    const ItemPage({Key? key}) : super(key: key);

    @override
    _ItemPageState createState() => _ItemPageState();
    }

    class _ItemPageState extends State<ItemPage> {
    Future<List<Item>> fetchItem() async {
        var url = Uri.parse(
            'http://localhost:8000/json/');
        var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
        );

        // decode the response to JSON
        var data = jsonDecode(utf8.decode(response.bodyBytes));

        List<Item> list_item = [];
        for (var d in data) {
        if (d != null) {
            list_item.add(Item.fromJson(d));
        }
        }
        return list_item;
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
            title: const Text('Item'),
            backgroundColor: Colors.teal,
            foregroundColor: Colors.white,
            ),
            drawer: const LeftDrawer(),
            body: FutureBuilder(
                future: fetchItem(),
                builder: (context, AsyncSnapshot snapshot) {
                if (snapshot.data == null) {
                    return const Center(child: CircularProgressIndicator());
                } else {
                    if (!snapshot.hasData) {
                    return const Column(
                        children: [
                        Text(
                            "No item data available.",
                            style:
                            TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                        ),
                        SizedBox(height: 8),
                        ],
                    );
                    } else {
                    return ListView.builder(
                        itemCount: snapshot.data!.length,
                        itemBuilder: (_, index) =>InkWell(
                        onTap: () {
                            Navigator.push(
                                context,
                                MaterialPageRoute(
                                    builder: (context) => ItemDetailPage(
                                        item: snapshot.data![index])));
                        },
                        child: Container(
                            margin: const EdgeInsets.symmetric(
                                horizontal: 16, vertical: 12),
                            padding: const EdgeInsets.all(20.0),
                            child: Column(
                            mainAxisAlignment: MainAxisAlignment.start,
                            crossAxisAlignment: CrossAxisAlignment.start,
                            children: [
                                Text(
                                "${snapshot.data![index].fields.name}",
                                style: const TextStyle(
                                    fontSize: 18.0,
                                    fontWeight: FontWeight.bold,
                                ),
                                ),
                                const SizedBox(height: 10),
                                Text("${snapshot.data![index].fields.amount}"),
                                const SizedBox(height: 10),
                                Text(
                                    "${snapshot.data![index].fields.category}"),
                                const SizedBox(height: 10),
                                Text(
                                    "${snapshot.data![index].fields.description}")
                            ],
                            ),
                        )));
                    }
                }
                }));
    }
    }
```
### 4. Creating Detail Item Screen
make item_detail.dart in screens folder
```
    import 'package:flutter/material.dart';
    import 'package:rakhas_inventory/models/items.dart';
    import 'package:rakhas_inventory/widget/left_drawer.dart';

    class ItemDetailPage extends StatelessWidget {
    final Item item;

    const ItemDetailPage({Key? key, required this.item}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: const Text('Item Details'),
            backgroundColor: Colors.teal,
            foregroundColor: Colors.white,
        ),
        drawer: const LeftDrawer(),
        body: Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
                Text(
                item.fields.name,
                style: const TextStyle(
                    fontSize: 24.0,
                    fontWeight: FontWeight.bold,
                ),
                ),
                const SizedBox(height: 10),
                Text("Amount: ${item.fields.amount}"),
                const SizedBox(height: 10),
                Text("Description: ${item.fields.description}"),
                const SizedBox(height: 10),
                Text("Category: ${item.fields.category}"),
                const SizedBox(height: 10),
                Text("Damage: ${item.fields.name}"),
                const SizedBox(height: 20),
                ElevatedButton(
                onPressed: () {
                    Navigator.pop(context); // Navigate back to the item list page
                },
                child: const Text('Back to Item List'),
                ),
            ],
            ),
        ),
        );
    }
    }
```
### 5. Adjusting other file to connect to django
1. item_form.dart
```
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:rakhas_inventory/widget/left_drawer.dart';
    import 'package:rakhas_inventory/screens/menu.dart';
    import 'dart:convert';

    class ItemFormPage extends StatefulWidget {
    const ItemFormPage({super.key});

    @override
    State<ItemFormPage> createState() => _ItemFormPageState();
    }

    class _ItemFormPageState extends State<ItemFormPage> {
    final _formKey = GlobalKey<FormState>();
    String _name = "";
    int _amount = 0;
    String _category = "";
    String _description = "";

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
        appBar: AppBar(
            title: const Center(
            child: Text(
                'Add Item Form',
            ),
            ),
            backgroundColor: Colors.teal,
            foregroundColor: Colors.white,
        ),
        // Adding the previously created drawer here
        drawer: const LeftDrawer(),
        body: Form(
            key: _formKey,
            child: SingleChildScrollView(
            child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Item Name",
                        labelText: "Item Name",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _name = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _name = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Name cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Amount",
                        labelText: "Amount",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _amount = int.tryParse(value!) ?? _amount;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _amount = int.tryParse(value!) ?? _amount;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Amount cannot be empty!";
                        }
                        if (int.tryParse(value) == null) {
                            return "Amount must be a number!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Category",
                        labelText: "Category",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _category = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _category = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Category cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                        decoration: InputDecoration(
                        hintText: "Description",
                        labelText: "Description",
                        border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(5.0),
                        ),
                        ),
                        onChanged: (String? value) {
                        setState(() {
                            _description = value!;
                        });
                        },
                        onSaved: (String? value) {
                        setState(() {
                            _description = value!;
                        });
                        },
                        validator: (String? value) {
                        if (value == null || value.isEmpty) {
                            return "Description cannot be empty!";
                        }
                        return null;
                        },
                    ),
                    ),
                    Align(
                    alignment: Alignment.bottomCenter,
                    child: Padding(
                        padding: const EdgeInsets.all(8.0),
                        child: ElevatedButton(
                        style: ButtonStyle(
                            backgroundColor:
                            MaterialStateProperty.all(Colors.teal),
                        ),
                        onPressed: () async {
                            if (_formKey.currentState!.validate()) {
                            // Send request to Django and wait for the response
                            final response = await request.postJson(
                                "http://localhost:8000/create-flutter/",
                                jsonEncode(<String, String>{
                                    'name': _name,
                                    'amount': _amount.toString(),
                                    'category': _category,
                                    'description': _description,
                                }));
                            if (response['status'] == 'success') {
                                ScaffoldMessenger.of(context)
                                    .showSnackBar(const SnackBar(
                                content: Text("New item has saved successfully!"),
                                ));
                                Navigator.pushReplacement(
                                context,
                                MaterialPageRoute(builder: (context) => MyHomePage()),
                                );
                            } else {
                                ScaffoldMessenger.of(context)
                                    .showSnackBar(const SnackBar(
                                content:
                                Text("Something went wrong, please try again."),
                                ));
                            }
                            }
                        },
                        child: const Text(
                            "Save",
                            style: TextStyle(color: Colors.white),
                        ),
                        ),
                    ),
                    ),
                ]
            ),
            ),
        ),
        );
    }
    }
```
2. main.dart
```
    import 'package:flutter/material.dart';
    import 'package:provider/provider.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:rakhas_inventory/screens/login.dart';

    void main() {
    runApp(const MyApp());
    }

    class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Provider(
        create: (_) {
            CookieRequest request = CookieRequest();
            return request;
        },
        child: MaterialApp(
            title: 'Inventory',
            theme: ThemeData(
                colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
                useMaterial3: true,
            ),
            home: const LoginPage()),
        );
    }
    }
```
3. menu_card.dart
```
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:rakhas_inventory/screens/item_form.dart';
    import 'package:rakhas_inventory/screens/login.dart';
    import 'package:rakhas_inventory/screens/list_item.dart';


    class MenuItem {
    final String name;
    final IconData icon;
    final Color color;

    MenuItem(this.name, this.icon,this.color);
    }

    class MenuCard extends StatelessWidget {
    final MenuItem item;

    const MenuCard(this.item, {Key? key}); // Constructor

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Material(
        color: item.color,
        child: InkWell(
            // Responsive touch area
            onTap: () async {
            // Show a SnackBar when clicked
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("You pressed the ${item.name} button!")));
            if (item.name == "Add Item") {
                Navigator.push(
                context,
                MaterialPageRoute(
                    builder: (context) => ItemFormPage(),
                ),
                );
            }else if (item.name == "View Item") {
                Navigator.push(context,
                    MaterialPageRoute(builder: (context) => const ItemPage()));
            }else if (item.name == "Logout") {
                final response = await request.logout(
                    "http://localhost:8000/auth/logout/");
                String message = response["message"];
                if (response['status']) {
                String uname = response["username"];
                ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                    content: Text("$message Good bye, $uname."),
                ));
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => const LoginPage()),
                );
                } else {
                ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                    content: Text("$message"),
                ));
                }
            }
            },
            child: Container(
            // Container to hold Icon and Text
            padding: const EdgeInsets.all(8),
            child: Center(
                child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                    Icon(
                    item.icon,
                    color: Colors.white,
                    size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                    item.name,
                    textAlign: TextAlign.center,
                    style: const TextStyle(color: Colors.white),
                    ),
                ],
                ),
            ),
            ),
        ),
        );
    }
    }
```