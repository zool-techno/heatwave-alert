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
