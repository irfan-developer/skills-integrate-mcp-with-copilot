# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities as a teacher
- Remove student registrations as a teacher

## Getting Started

1. Install the dependencies:

   ```
   pip install -r ../requirements.txt
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                     | Start a teacher session                                             |
| POST   | `/auth/logout`                                                    | End the current teacher session                                     |
| GET    | `/auth/me`                                                        | Check the current teacher session                                   |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity as a teacher                                |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Remove a registration as a teacher                              |

The demo teacher account is `teacher` with password `teacher123`. Credentials are stored as a salted password hash in `teachers.json`; replace this file and use a secret-management solution before deploying beyond local development. Activity viewing remains public, while signup and unregister require a teacher session.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

Activity and session data is stored in memory, which means it will be reset when the server restarts. Teacher credentials are loaded from `teachers.json` at startup.
