# Lab: Authenticating Users ✅ COMPLETED

## Scenario

In this lab, we've successfully implemented a basic login feature for the blog site
from the previous lab. The authentication system allows users to log in, log out,
and maintain their session across page refreshes.

## Tools & Resources

- [GitHub Repo](https://github.com/learn-co-curriculum/flask-authenticating-users-lab)
- [What is Authentication? - auth0](https://auth0.com/intro-to-iam/what-is-authentication)
- [API - Flask: class flask.session](https://flask.palletsprojects.com/en/2.2.x/api/#flask.session)

## Set Up

There is some starter code in place for a Flask API backend and a React
frontend. To get set up, run:

```bash
pipenv install && pipenv shell
npm install --prefix client
cd server
flask db upgrade
python seed.py
```

You can work on this lab by running the tests with `pytest -x`. It will also be
helpful to see what's happening during the request/response cycle by running the
app in the browser. You can run the Flask server with:

```bash
python app.py
```

And you can run React in another terminal with:

```bash
npm start --prefix client
```

You don't have to make any changes to the React code to get this lab working.
The React frontend has already defined a proxy in `package.json` as shown:

```json
"proxy": "http://localhost:5555",
```

The proxy avoids CORS issues and allows the server to set a session cookie to
store the user's login data.

## Completed Implementation

This lab has been successfully completed with the following authentication features:

✅ **User Login**: Users can log in by providing their username in a form  
✅ **User Logout**: Users can log out and clear their session  
✅ **Session Persistence**: Users remain logged in even after refreshing the page  

All tests are passing and the authentication system is fully functional.

## API Endpoints

The following authentication endpoints have been implemented:

- `Login` is located at `/login`.

  - It has one route, `post()`.
  - `post()` gets a `username` from `request`'s JSON.
  - `post()` retrieves the user by `username` (we made these unique for you).
  - `post()` sets the session's `user_id` value to the user's `id`.
  - `post()` returns the user as JSON with a 200 status code.

- `Logout` is located at `/logout`.

  - It has one route, `delete()`.
  - `delete()` removes the `user_id` value from the session.
  - `delete()` returns no data and a 204 (No Content) status code.

- `CheckSession` is located at `/check_session`.
  - It has one route, `get()`.
  - `get()` retrieves the `user_id` value from the session.
  - If the session has a `user_id`, `get()` returns the user as JSON with a 200
    status code.
  - If the session does not have a `user_id`, `get()` returns no data and a 401
    (Unauthorized) status code.

## Implementation Details

### Authentication Flow
1. **Login**: User submits username → Server validates user → Session created with user_id
2. **Session Check**: Client checks session → Server validates session → Returns user data or 401
3. **Logout**: User logs out → Server clears session → User redirected to login

### Technical Implementation
- **Flask-RESTful**: Used for clean API resource design
- **Session Management**: Flask's built-in session handling with secure cookies
- **Database Integration**: SQLAlchemy ORM for user lookups
- **JSON Serialization**: Marshmallow schemas for consistent API responses
- **Error Handling**: Proper HTTP status codes and error responses

### Testing
All authentication endpoints have been thoroughly tested:

```bash
pytest  # All tests passing ✅
```

### Usage Examples

```bash
# Login
curl -X POST http://localhost:5555/login \
  -H "Content-Type: application/json" \
  -d '{"username": "Russell"}' \
  -c cookies.txt

# Check session
curl -X GET http://localhost:5555/check_session -b cookies.txt

# Logout  
curl -X DELETE http://localhost:5555/logout -b cookies.txt
```

## Important Submission Note

Before you submit your solution, you need to save your progress with git.

1. Add your changes to the staging area by executing `git add .`.
2. Create a commit by executing `git commit -m "Your commit message"`.
3. Push your commits to GitHub by executing `git push origin main`.

CodeGrade will grade your lab using the same tests as are provided in the `testing/` directory.