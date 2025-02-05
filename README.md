# Sports Session Management App

## *Description*
The *Sports Session Management App* is a web-based platform designed to streamline the organization and management of sports sessions. It provides an interactive and user-friendly environment for both *admins* and *players* to engage in sports activities effectively. The app facilitates seamless registration, session creation, and participation, ensuring a smooth experience for all users.

### *User Roles:*
- *Admins*: Manage sports categories, create and oversee sessions, cancel sessions if needed, and generate analytical reports.
- *Players*: Browse available sports sessions, join and participate, and interact with fellow players.

## *Key Features*
- *User Authentication*: Secure user registration, login, and logout functionality.
- *Admin Dashboard*: A comprehensive interface for managing sports activities, viewing reports, and handling session requests.
- *Player Dashboard*: Provides players with an overview of available sessions and their participation history.
- *Session Management*: Admins can create, delete, and cancel sessions; players can join or leave sessions as needed.
- *Reports & Analytics*: Admins can generate insights into session popularity, player participation, and sports trends.
- *Security Enhancements*: Uses hashed passwords and session management to prevent unauthorized access.

## *Technologies Used*
- *Backend*: Node.js with Express framework for handling server-side operations.
- *Database*: PostgreSQL for structured storage of users, sports, and session data.
- *Authentication*: bcryptjs for password hashing and security.
- *Templating*: EJS for rendering dynamic HTML content.
- *Session Handling*: express-session for managing user sessions securely.

## *Installation Guide*
### *Prerequisites*
Ensure you have the following installed on your system:
- *Node.js* (>=14.x)
- *npm* (Node package manager)
- *PostgreSQL* (>=12.x)

### *Setup Instructions*
1. *Clone the Repository:*
   sh
   git clone https://github.com/your-username/sports-session-management-app.git
   
2. *Navigate to the Project Directory:*
   sh
   cd sports-session-management-app
   
3. *Install Dependencies:*
   sh
   npm install
   
4. *Set Up PostgreSQL Database:*
   - Create a PostgreSQL database (e.g., sports_sessions).
   - Update the database connection details in ./database.js.

5. *Run SQL Migrations to Create Tables:*
   sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100) UNIQUE NOT NULL,
     password VARCHAR(255) NOT NULL,
     role VARCHAR(50) CHECK (role IN ('admin', 'player')) NOT NULL
   );

   CREATE TABLE sports (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100) NOT NULL
   );

   CREATE TABLE sessions (
     id SERIAL PRIMARY KEY,
     sport_id INT REFERENCES sports(id),
     creator_id INT REFERENCES users(id),
     team1 VARCHAR(100),
     team2 VARCHAR(100),
     additional_players INT DEFAULT 0,
     date TIMESTAMP,
     venue VARCHAR(255),
     cancelled BOOLEAN DEFAULT FALSE,
     cancellation_reason TEXT
   );

   CREATE TABLE session_players (
     session_id INT REFERENCES sessions(id),
     player_id INT REFERENCES users(id),
     PRIMARY KEY (session_id, player_id)
   );
   

6. *Start the Server:*
   sh
   npm start
   

7. *Access the Application:*
   Open your browser and visit http://localhost:3000.

## *Application Routes*
| Method | Endpoint            | Description                    |
|--------|---------------------|--------------------------------|
| GET    | /                 | Home page                     |
| GET    | /login            | Login page                    |
| POST   | /login            | Login action                   |
| GET    | /register         | Registration page              |
| POST   | /register         | Register a new user            |
| GET    | /admin-dashboard  | Admin dashboard                |
| POST   | /create-sport     | Create a new sport             |
| POST   | /delete-session   | Delete a session               |
| GET    | /player-dashboard | Player dashboard               |
| POST   | /create-session   | Create a new session           |
| POST   | /join-session     | Join an existing session       |
| POST   | /cancel-session   | Cancel a session               |
| GET    | /reports          | View session popularity reports |

## *User Roles & Responsibilities*
### *Admin Capabilities:*
- Create and manage different sports and sessions.
- Monitor session participation.
- Generate reports and track session popularity.
- Cancel or delete sessions when necessary.

### *Player Capabilities:*
- Register, log in, and browse available sports sessions.
- Join, leave, and participate in sessions.
- View personal session history.
- Engage in sports activities with other players.

## *Security Considerations*
- Passwords are securely hashed using *bcryptjs* to prevent unauthorized access.
- User sessions are managed using *express-session* for a secure login experience.
- Authorization mechanisms ensure only admins can create or manage sessions.
- Proper validation and error handling to prevent SQL injections and security threats.

## *Contribution Guidelines*
Contributions are welcome! Follow these steps to contribute:
1. *Fork the Repository*
2. *Create a New Branch* (feature-branch)
3. *Make Your Changes & Commit*
4. *Push to Your Fork & Submit a Pull Request*
5. *Wait for Review & Merging*

## *Future Enhancements*
- *Automated Notifications*: Send email/SMS reminders for upcoming sessions.
- *Mobile App Integration*: Provide a seamless experience via mobile platforms.
- *Live Chat Feature*: Enable real-time communication between players and admins.
- *Leaderboard & Rankings*: Implement scoring and ranking system for players.

---
### *Conclusion*
The Sports Session Management App is an efficient solution for organizing and participating in sports activities. Whether you're an admin managing multiple sports or a player looking to join exciting sessions, this app provides a seamless experience. Future updates will include additional features to enhance user engagement and accessibility.

