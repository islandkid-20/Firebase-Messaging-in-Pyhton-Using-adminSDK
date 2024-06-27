# Firebase-Messaging-in-Pyhton-Using-adminSDK
To send Firebase Cloud Messaging (FCM) messages to mobile devices using the Firebase Admin SDK, follow these steps:

## 1. Set up Firebase Admin SDK:
  - First, you need to set up a Firebase project and download the service account key file (.json file).
  - Install the Firebase Admin SDK in your project. You can do this using `pip`:

  ```python
  pip install firebase-admin
  ```
## 2. Initialize the Firebase Admin SDK:
- Initialize the SDK in your Python script using the service account key file you downloaded.
```python
import firebase_admin
from firebase_admin import credentials, messaging

# Path to the service account key file
cred = credentials.Certificate("path/to/serviceAccountKey.json")

# Initialize the app with a service account, granting admin privileges
firebase_admin.initialize_app(cred)
```

## 3. Send a Message
- Use the `messaging` module to send a message. You can send different types of messages, such as notification messages or data messages. Here’s an example of sending a notification message to a specific device:
```python
def send_fcm_message(token):
    # Define the message payload
    message = messaging.Message(
        notification=messaging.Notification(
            title='Hello!',
            body='This is an FCM notification message!',
        ),
        token=token,
    )

    # Send the message
    response = messaging.send(message)
    print('Successfully sent message:', response)

# Replace with your device registration token
registration_token = 'YOUR_DEVICE_REGISTRATION_TOKEN'
send_fcm_message(registration_token)
```

# Example Breakdown:
## 1. Initialization:
- The `credentials.Certificate` method is used to load the service account key file.
- `firebase_admin.initialize_app` initializes the Firebase app with these credentials.

## 2. Creating a Message:
- `messaging.Message` constructs the message to be sent. This example includes a notification with a title and body.
- `token` is the recipient’s device token. Replace `YOUR_DEVICE_REGISTRATION_TOKEN` with the actual token of the device you want to send the message to.

## 3. Sending the Message:
- `messaging.send` sends the message. The response contains the message ID if the message was successfully sent.

# Additional Features:
- Data Messages:
  If you want to send data messages, you can `add` a data field:

  ```python
  message = messaging.Message(
    data={
        'key1': 'value1',
        'key2': 'value2',
    },
    token=token,
  )
  ```
- Topic Messaging:
If you want to send a message to all devices subscribed to a topic:

```python
def send_topic_message(topic):
    message = messaging.Message(
        notification=messaging.Notification(
            title='Topic Message',
            body='This is a message to a topic!',
        ),
        topic=topic,
    )

    response = messaging.send(message)
    print('Successfully sent topic message:', response)

send_topic_message('news')
```
Replace `news` with your topic name. Devices need to subscribe to the topic to receive messages.

These steps will enable you to send FCM messages using Firebase Admin SDK in Python. Make sure to handle exceptions and errors as needed to ensure your implementation is robust.
    

