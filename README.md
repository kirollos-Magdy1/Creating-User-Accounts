# Project Overview

⚙️ **Configurigation Initialization**: The automation process begins by reading the configuration file to set up the required automation settings.

📧 **Email Reception and Validation**: The system waits until an email with a specified subject is received. Upon reception, it downloads the attached Excel file and validates its format to ensure correct attachment data.

🔒 **VPN Activation and Account Creation**:

- The "Hide Me" Desktop VPN Application is activated to access the [Hide Me website](https://hide.me/en/).
- Depending on the provided email:
    - If the email is not associated with a "Hide Me" account, an activation email is received to create a new account by inserting a username and password.
    - If the email is already linked to a "Hide Me" account, an email is received requesting a password change.
    - Upon successful account activation or password reset within 30 seconds, the robot logs out. Otherwise proceed with the next step

🔑 **Login and Captcha Handling**: The robot logs into the "Hide Me" account and attempts to solve the captcha three times.

📊 **Excel Data Extraction**: Extracting User records to a user info Data table from the downloaded Excel file.

👤 **User Profile Generation**:

- For each record in the data table:
    - Information such as name, password, birthday, address, phone, country code, company, and occupation is generated using the [Fake Name Generator](https://www.fakenamegenerator.com/).
    - Extracted data is saved in the "result.xlsx" file.
    - Valid given user data trigger account creation on the [Automation Exercise website](https://automationexercise.com/).
    - The API endpoint "https://reqres.in/api/users" is called to add user information, to get the ID retrieved from the response. To be the transition item ID

💾 **Data Storage and Reporting**:

- Extracted data is stored in "result.xlsx", while transaction results are logged in "summary.csv", including start and end dates, user ID, username, status, error message (if any), and screenshot path.

📧 **Email Notification**: The generated "result.xlsx" and "summary.csv" files are sent via email to the recipients.

⏳ **Email Monitoring**: The system waits for new emails. If no emails are received within 5 minutes, the process stops.

# Core Components

## Main State Machine

![Main State Machine](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/f7455e0a-d79e-42e7-8e65-b0d0741b18ba)

- Start by "Initialize Settings" state to load the config file
- If it is loaded successfully with no system exception, transition to the "Waiting For Email" State to receive the first email
- While a new valid email is being received, transition to the "process transaction" state
- While no system exceptions occur during the Process Transaction State, transition back to the Waiting For Email State to receive and handle subsequent emails.


## Receive Email

![Receive Email](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/bf3f4508-e608-40c8-a5bc-fd7582dfdb6f)
A Workflow that is responsible for receiving the client/stackholder email to process its items or receiving emails containing action links from Hide Me website


## Initialize All Applications
![Initialize All Applications](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/0a55fd73-4453-48be-a4ee-f07dd690b7f7)
<aside>
💡 exceptions are handled, not letting them rethrow, so that the transaction process not interrupted

</aside>

## Process Overview
![Process Overview](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/c448793e-cf7e-4cde-bc7b-908e9d67a8ad)



### Preparing Process Transactions
![Preparing Process Transactions](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/1243cf12-cf87-43bb-8ca0-4ca0d889d60b)

### Process Invocation
![Process Invocation](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/d41fe1d7-b7ec-4b6f-9543-08a08109a9ad)



### Proces Transaction Item
![Process Each Transaction Item](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/1202e641-3acf-41c0-8857-8e7f3b6e3bdc)


### Process Transaction Item Exception Handling
![Process Transaction Item Exception Handling](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/425f4d7a-9e75-474e-8a5a-fd7ff973fbf2)

