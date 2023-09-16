# AMIZONE Bot

This is a Python script for interacting with the AMIZONE website using the `requests` library. It provides a set of methods to perform various actions such as logging in, retrieving attendance information, accessing exam schedules, fetching faculty information, and retrieving results.

## Prerequisites
- Python 3.x
- `requests` library
- `bs4` (Beautiful Soup) library
- `telegram` library
- `firebase`

## Installation
1. Clone the repository or download the script file.
2. Install the required libraries using pip:
   ```shell
   pip install requests bs4 telegram
   ```

## Firebase Integration

The Telegram bot requires Firebase integration to store and retrieve user credentials. Follow the steps below to set up Firebase integration:

1. Create a Firebase project: Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.

2. Generate Firebase Admin SDK credentials: In the Firebase Console, go to "Project settings" and navigate to the "Service Accounts" tab. Click on "Generate new private key" to download the JSON key file.

3. Save the JSON key file: Save the downloaded JSON key file securely on your system.

4. Update the AMIZONE class: In the `__init__` method of the `AMIZONE` class, update the path to the JSON key file in the `credentials.Certificate()` call.

```python
cred = credentials.Certificate('/path/to/your/firebase-adminsdk-key.json')
```

5. Initialize the Firebase Admin SDK: In the `__init__` method of the `AMIZONE` class, update the `databaseURL` parameter in the `firebase_admin.initialize_app()` call with your Firebase project's database URL.

```python
firebase_admin.initialize_app(cred, {
    'databaseURL': 'https://your-project-id.firebaseio.com/'
})
```

## Usage
1. Import the necessary classes and exceptions:
   ```python
   from http.client import HTTPException
   import requests
   import bs4
   import json
   import telegram
   from telegram import Update, Bot, replymarkup
   from telegram.ext import Updater, CommandHandler, CallbackContext
   from requests.exceptions import HTTPError
   ```
2. Create an instance of the `AMIZONE` class:
   ```python
   amizone = AMIZONE()
   ```
3. Login to AMIZONE using your credentials:
   ```python
   amizone.login(username, password)
   ```
4. Perform the desired actions by calling the appropriate methods of the `AMIZONE` class. For example, to retrieve attendance information:
   ```python
   attendance_data = amizone.my_courses()
   ```
5. Handle exceptions appropriately to deal with any errors that may occur during the process.

## Available Methods
- `login(username, password)`: Logs in to AMIZONE using the specified username and password.
- `my_courses(sem=None)`: Retrieves the list of courses along with attendance information. Optionally, you can provide a semester to filter the results.
- `faculty()`: Retrieves faculty information.
- `exam_schedule()`: Retrieves the exam schedule.
- `my_profile()`: Retrieves the user's profile information.
- `results(sem=None)`: Retrieves the results. Optionally, you can provide a semester to filter the results.
- `start_telegram_bot()`: Starts a Telegram bot for interacting with AMIZONE. This method uses the `telegram` library and requires a valid Telegram token.

Please note that some methods may raise exceptions in case of invalid or expired cookies, HTTP errors, or other issues. Make sure to handle these exceptions appropriately in your code.

## Credits
This script was developed by Vaibhav Srivastava and is provided under the [MIT License](LICENSE). Feel free to modify and use it according to your needs.
