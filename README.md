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






