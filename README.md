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
`
    flutter create inventaris_mobile
    cd inventaris_mobile
    flutter run
`
### 2. Modify main.dart and create menu.dart
1. main.dart
`
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
`
2. menu.dart
`
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
`
