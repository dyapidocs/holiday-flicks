[Back to Overview](overview.md)

# Obtain API Key for Holiday Flicks API

To use the Holiday Flicks API, you'll need to obtain an API key for authentication. Follow these steps to register and receive your API key.

## 1. Navigated to the Holiday Flicks API registration page:

```shell
https://api.holidayflicks.com/register
```

## 2. Fill out the registration form and submit upon completion.

## 3. Confirm your email address:

* Check your email Inbox:
  * Look for an email from "Holiday Flicks API" or "no-reply@holidayflicks.com".
  * If you don't see it, check your spam or junk folder.
* Verify your email:
  * Open the email and click the verification link provided.
  * This will confirm your email address and activate your account.

## 4. Log in to your account:

* Return to the Holiday Flicks API website.
* Click on the "Log In" button or link.
* Enter your registered email address and password.
* Click "Log In" to access your account dashboard.

## 5. Access your API Key:

* Navigate to the API Keys Section:
  * In your account dashboard, find the "API Keys", "Developer", or "Settings" section.
* Generate an API Key (if necessary):
  * If an API key isn't already displayed, click on "Generate New API Key".
* Copy Your API Key:
  * Your API key will be displayed on the screen.
  * Select and copy the API key to a secure place.

**Important: Keep your API key confidential. Do not share it publicly or commit it to source control repositories.**

## 6. Start using the Holiday Flicks API.

* Include your API Key in requests. For each API request, include your API key in the Authorization header.
* Header Format:

    ```shell
    Authorization: Bearer YOUR_API_KEY
    ```
* Example API Request using cURL:
    ```shell
    curl -H "Authorization: Bearer YOUR_API_KEY" https://api.holidayflicks.com/v1/works
    ```

## 7. Getting Support

If you encounter issues with your APK Key, contact `support@holidayflicks.com`.