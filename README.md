# GSC (Bulk) Indexing Requesting By Mecky 🚀

## Overview

This project provides a script to perform bulk indexing requests using the Google Search Console (GSC) API. The script automates the process of submitting URLs for indexing, making it easier to manage large volumes of URLs.

## Prerequisites ✅

Before you begin, ensure you have the following:

- Python 3.x installed on your machine
- Access to the Google Search Console API
- Google Cloud project with the Search Console API enabled
- OAuth 2.0 credentials (client ID and client secret)

## Setup 🛠️

### Clone the Repository

```bash
git clone https://github.com/KuyaMecky/GSC-Bulk-Indexing-Requesting-By-Mecky.git
cd GSC-Bulk-Indexing-Requesting-By-Mecky
```

### Install Required Python Packages

```bash
pip install -r requirements.txt
```

### Set Up Google Cloud Credentials

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing project.
3. Enable the Search Console API for your project.
4. Create OAuth 2.0 credentials and download the JSON file.
5. Save the JSON file in the project directory and rename it to `credentials.json`.

## Usage 🚀

### Authenticate with Google

Run the script to authenticate with your Google account:

```bash
python authenticate.py
```

This will open a browser window for you to log in and authorize the application. The authentication tokens will be saved for future use.

### Prepare Your URLs

Create a text file named `urls.txt` in the project directory and list the URLs you want to submit for indexing, one per line.

### Run the Indexing Script

Execute the script to submit the URLs for indexing:

```bash
python index_urls.py
```

The script will read the URLs from `urls.txt` and submit them to the GSC API for indexing.

## Implementation Details 📝

### Authenticating with the GSC API

The `authenticate.py` script handles the OAuth 2.0 authentication process. It uses the `google-auth` and `google-auth-oauthlib` libraries to manage the authentication flow and save the tokens.

### Submitting URLs for Indexing

The `index_urls.py` script reads the URLs from `urls.txt` and submits them to the GSC API using the `google-api-python-client` library. The script handles the API requests and responses, ensuring that each URL is submitted correctly.

## Contributing 🤝

If you would like to contribute to this project, please fork the repository and submit a pull request. We welcome all contributions!

## License 📄

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact 📧

For any questions or support, please contact Mecky at mecky@example.com.

---

## Fancy Design and Code Preview 💻

### How to Implement

```python
# authenticate.py
from google.oauth2 import service_account
from google_auth_oauthlib.flow import InstalledAppFlow
import google.auth.transport.requests

def authenticate():
    flow = InstalledAppFlow.from_client_secrets_file(
        'credentials.json',
        scopes=['https://www.googleapis.com/auth/webmasters']
    )
    creds = flow.run_local_server(port=0)
    return creds

if __name__ == '__main__':
    creds = authenticate()
    print("Authenticated successfully!")
```

### How to Run

```bash
# Step 1: Authenticate
python authenticate.py

# Step 2: Prepare URLs
# Create a file named urls.txt and list your URLs

# Step 3: Run the indexing script
python index_urls.py
```

```python
# index_urls.py
from googleapiclient.discovery import build
import json

def index_urls(creds):
    service = build('searchconsole', 'v1', credentials=creds)
    with open('urls.txt') as f:
        urls = f.read().splitlines()
    for url in urls:
        request_body = {
            'url': url,
            'type': 'URL_UPDATED'
        }
        response = service.urlInspection().index().insert(body=request_body).execute()
        print(f"Submitted {url} for indexing: {response}")

if __name__ == '__main__':
    creds = authenticate()
    index_urls(creds)
```

This design ensures that you can easily authenticate and submit URLs for indexing using the GSC API.
