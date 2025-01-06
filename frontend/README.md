# Heat wave Alert Application

## Overview
The Heatwave Alert app provides heatwave warnings and updates to users. The project has a backend built in WordPress (using the REST API) and a frontend developed in Flutter.

## Backend Setup (WordPress)
1. Set up a WordPress instance.
2. Install necessary plugins like the "JWT Authentication for WP REST API".
3. Create a custom post type for "alerts".
4. Set up the WordPress REST API to expose heatwave alerts data.

## Frontend Setup (Flutter)
1. Install Flutter SDK: [Flutter Install](https://flutter.dev/docs/get-started/install).
2. Clone the repository and navigate to the `heatwave_alert` folder.
3. Run `flutter pub get` to install dependencies.
4. Run `flutter run` to start the app.

## Project Structure
- `backend/` - WordPress site and API configuration
- `frontend/` - Flutter app for displaying alerts
- `README.md` - Project documentation

## License
This project is licensed under the MIT License.






To start a project named "Heatwave Alert" with a backend in WordPress and frontend in Flutter, and manage it in one GitHub repository, you can follow these steps:

### 1. **Create the GitHub Repository**
   - Go to GitHub and create a new repository named `heatwave-alert`.
   - Initialize it with a `README.md` file.

### 2. **Set up the Backend (WordPress)**
   WordPress can be used as a headless CMS for your project.
   
   - **Install WordPress locally (using XAMPP/WAMP or Docker) or on a web hosting server.**
   - Set up the WordPress API to serve content (use the **REST API**).
   
   **Steps for setting up WordPress REST API:**
   - Install WordPress plugins if needed, like **JWT Authentication for WP REST API** to secure the API.
   - Create custom post types for heatwave alerts and necessary content types (alerts, locations, etc.).
   - Ensure that the API is enabled by visiting the URL for your WordPress site's REST API (e.g., `https://your-wordpress-site/wp-json/`).
   
   **Example structure for the backend API:**
   - Custom Post Type: `alerts`
   - API endpoint: `GET /wp-json/wp/v2/alerts` to fetch all alerts.
   
### 3. **Set up the Frontend (Flutter)**
   - **Install Flutter** if you haven't already. Follow the official documentation [here](https://flutter.dev/docs/get-started/install).
   - Create a new Flutter project:
     ```bash
     flutter create heatwave_alert
     cd heatwave_alert
     ```
   - **Add Dependencies:**
     - For HTTP requests, use the `http` package:
       ```yaml
       dependencies:
         flutter:
           sdk: flutter
         http: ^0.13.3
       ```
     - Install the dependencies by running `flutter pub get`.

   - **Connect to the Backend:**
     - Create a `service.dart` file in the Flutter project to handle API requests.
     ```dart
     import 'dart:convert';
     import 'package:http/http.dart' as http;

     class AlertService {
       final String apiUrl = 'https://your-wordpress-site/wp-json/wp/v2/alerts';

       Future<List<Alert>> fetchAlerts() async {
         final response = await http.get(Uri.parse(apiUrl));

         if (response.statusCode == 200) {
           List jsonResponse = json.decode(response.body);
           return jsonResponse.map((alert) => Alert.fromJson(alert)).toList();
         } else {
           throw Exception('Failed to load alerts');
         }
       }
     }

     class Alert {
       final String title;
       final String description;

       Alert({required this.title, required this.description});

       factory Alert.fromJson(Map<String, dynamic> json) {
         return Alert(
           title: json['title']['rendered'],
           description: json['content']['rendered'],
         );
       }
     }
     ```

   - **Display Alerts in Flutter:**
     - Use `FutureBuilder` to fetch and display the alerts:
     ```dart
     import 'package:flutter/material.dart';

     void main() {
       runApp(MyApp());
     }

     class MyApp extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         return MaterialApp(
           title: 'Heatwave Alert',
           home: AlertList(),
         );
       }
     }

     class AlertList extends StatefulWidget {
       @override
       _AlertListState createState() => _AlertListState();
     }

     class _AlertListState extends State<AlertList> {
       late Future<List<Alert>> futureAlerts;

       @override
       void initState() {
         super.initState();
         futureAlerts = AlertService().fetchAlerts();
       }

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(title: Text('Heatwave Alerts')),
           body: FutureBuilder<List<Alert>>(
             future: futureAlerts,
             builder: (context, snapshot) {
               if (snapshot.connectionState == ConnectionState.waiting) {
                 return CircularProgressIndicator();
               } else if (snapshot.hasError) {
                 return Text('Error: ${snapshot.error}');
               } else if (snapshot.hasData) {
                 return ListView.builder(
                   itemCount: snapshot.data!.length,
                   itemBuilder: (context, index) {
                     return ListTile(
                       title: Text(snapshot.data![index].title),
                       subtitle: Text(snapshot.data![index].description),
                     );
                   },
                 );
               }
               return Text('No Alerts');
             },
           ),
         );
       }
     }
     ```

### 4. **Create the `README.md` File**
   The `README.md` file will include the basic setup for both the backend and frontend.

   Example `README.md` content:
   ```markdown
   # Heatwave Alert

   ## Overview
   The Heatwave Alert app provides heatwave warnings and updates to users. The project has a backend built in WordPress (using the REST API) and a frontend developed in Flutter.

   ## Backend Setup (WordPress)
   1. Set up a WordPress instance.
   2. Install necessary plugins like the "JWT Authentication for WP REST API".
   3. Create a custom post type for "alerts".
   4. Set up the WordPress REST API to expose heatwave alerts data.

   ## Frontend Setup (Flutter)
   1. Install Flutter SDK: [Flutter Install](https://flutter.dev/docs/get-started/install).
   2. Clone the repository and navigate to the `heatwave_alert` folder.
   3. Run `flutter pub get` to install dependencies.
   4. Run `flutter run` to start the app.

   ## Project Structure
   - `backend/` - WordPress site and API configuration
   - `frontend/` - Flutter app for displaying alerts
   - `README.md` - Project documentation

   ## License
   This project is licensed under the MIT License.
   ```

### 5. **Organize the Repository**
   - Structure your project like this:
     ```
     heatwave-alert/
     ├── backend/              # WordPress files (if needed)
     ├── frontend/             # Flutter app
     ├── .gitignore            # Ignore files like `build/`, `*.log`, etc.
     ├── README.md             # Project documentation
     └── LICENSE               # License file
     ```