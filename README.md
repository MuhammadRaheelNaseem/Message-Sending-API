# Message Sending API

## Introduction
In this repository, you'll find Python scripts showcasing different approaches to sending SMS messages using the Sinch SMS API. Sinch offers a robust platform for communication services, including SMS, voice, and video. These scripts provide practical examples of integrating SMS functionality into your Python applications, catering to various use cases and preferences.

## Prerequisites
Before utilizing these scripts, ensure you have the following prerequisites:
- **Sinch Account**: Sign up for a Sinch account and obtain your API credentials (API key and API secret).
- **Python Environment**: Ensure Python is installed on your system.
- **Dependencies**: Install necessary Python libraries using pip:
  ```
  pip install sinch
  ```

## Code 1: Using Requests Library (urequests)
```python
import requests as urequests

def send_sms(token, recipient, message):
    url = "https://sms.api.sinch.com/xms/v1/your_batch_id/batches"
    headers = {
        "Authorization": token,
        "Content-Type": "application/json"
    }
    data = {
        "from": "your_sender_id",
        "to": [recipient],
        "body": message
    }
    response = urequests.post(url, headers=headers, json=data)
    print(response.text)
    response.close()

# Replace token, recipient, and message with your values
token = "Bearer your_api_token"
recipient = "recipient_phone_number"
message = "Your test message here"

# Send SMS
send_sms(token, recipient, message)
```
**Explanation:**
- This script demonstrates sending SMS messages using the `urequests` library, suitable for MicroPython environments or environments with limited resources.
- It constructs a POST request to the Sinch API endpoint with necessary parameters, including API token, recipient number, and message.
- The `send_sms` function sends the request and prints the response received from the API.

## Code 2: Using SinchClient Library
```python
from sinch import SinchClient

sinch_client = SinchClient(
    key_id="your_key_id",
    key_secret="your_key_secret",
    project_id="your_project_id"
)

send_batch_response = sinch_client.sms.batches.send(
    body="Hello from Sinch!",
    to=["recipient_phone_number"],
    from_="sender_phone_number",
    delivery_report="none"
)

print(send_batch_response)
```
**Explanation:**
- This script utilizes the Sinch Python SDK (`sinch` library) to interact with the Sinch API in a more structured way.
- It initializes a Sinch client with your API credentials and project ID.
- Then it sends an SMS batch with specified parameters, including the message body, recipient number, and sender number.

## Code 3: Using Requests Library (with Base64 Encoding)
```python
import requests as urequests
import base64

def send_sms(app_key, app_secret, recipient, message):
    url = "https://sms.api.sinch.com/xms/v1/your_batch_id/batches"
    auth_str = "{}:{}".format(app_key, app_secret)
    headers = {
        "Authorization": "Bearer your_api_token",
        "Content-Type": "application/json"
    }
    data = {
        "from": "sender_phone_number",
        "to": [recipient],
        "body": message
    }
    response = urequests.post(url, headers=headers, json=data)
    print(response.text)
    response.close()

# Replace app_key, app_secret, recipient, and message with your values
APP_KEY = "your_app_key"
APP_SECRET = "your_app_secret"
recipient = "recipient_phone_number"
message = "Your test message here"

# Send SMS
send_sms(APP_KEY, APP_SECRET, recipient, message)
```
**Explanation:**
- This script also uses the `urequests` library for making HTTP requests.
- It constructs a POST request to the Sinch API endpoint with necessary parameters, including app key, app secret, recipient number, and message.
- Basic authentication is encoded in Base64 format before sending the request to the API.

## Usage
To use these scripts:
1. Replace the placeholder variables with your actual Sinch API credentials, recipient number, and message.
2. Run the desired script using Python.

## Conclusion
These scripts provide comprehensive examples of integrating SMS functionality into your Python applications using the `Sinch SMS API`. Whether you're working in a resource-constrained environment, prefer a structured SDK approach, or need to handle authentication manually, there's a suitable method for your needs. Feel free to customize and extend these scripts to fit your specific requirements.
