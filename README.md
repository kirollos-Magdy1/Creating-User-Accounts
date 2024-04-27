# Project Overview

A robot built with UI Path that listens to a specific email and reads the nationalities and genders data table from the received email, then generates additional information from the “[Fake Name Generator](https://www.fakenamegenerator.com/)” website, uses it to create a profile on the “[Automation Exercise](https://automationexercise.com/)” website,


The user data table is treated as transaction items, which are processed by assigning an ID for each transaction generated from the “[https://reqres.in”](https://reqres.xn--in-02t/) API using the user information, then processing the item and closing the transaction with a status either completed or failed with a message error and a screenshot.

Also, the process involves enabling the desktop VPN application to create an account on the “[Hide Me](https://hide.me/en/)” VPN website before starting work on the data table records.

Finally, gather all transactions within an excel file along with the user's information and send them back to the recipient email, and prepare to wait for another incoming email to begin processing its items.

# Automation Workflow Details

1️⃣ Read the configuration file to initialize automation settings.

2️⃣ Wait until you receive an email with a specified subject. Download the attached

Excel file validating if a file with the correct attachment data format was received,

3️⃣ Enable the “Hide Me” Desktop VPN Application to navigate to the https://hide.me/en/ website, create an account, insert your email, and click on register:

🔸 If the provided email is not associated with a “Hide Me” account an activation email is received, to activate it and create an account (insert username and password)

**🔹** If the provided email is already associated with a “Hide Me” account an email is received asking to change the account password.

♦ If an email is received within 30 seconds and successfully reset to activate the account, then the robot will logout.

4️⃣ log in to the “Hide Me” account and attempt to solve the captcha three times.

5️⃣ Read the data table from the downloaded Excel file.

6️⃣ For each record in the data table, do the following steps:

a. Go to https://www.fakenamegenerator.com/ select gender and country, and click on

generate button, then get the information:

- Name
- Password
- Birthday
- Address
- Phone
- Country code
- Company
- Occupation

b. Save the extracted data in the result Excel file (mentioned in step 6.e).

c. If the country and gender data are valid: Go to https://automationexercise.com/ and click on sign up, then insert the username.

and email and fill in the user information, click on Create Account (make sure that the account has been created), then click on Continue and delete it.

d. Call this API: https://reqres.in/api/users to add the user info, then get the ID from the

response:

i. End point: https://reqres.in/api/users

ii. Method: POST

iii. Body:

{

"name": "Ronald Beaman",

"birthday": "1980-12-11 ",

"address": "311 Burning Memory Lane",

"phone": "215-289-4533",

"countryCode": "1",

"company": "Red Robin Stores",

"occupation": "dredge operator"

}

e. Save data in the following files:

result.xlsx: contains the user-extracted date in step 7.b.

summary.csv: contains the transaction result

- Start Date: start date of the transaction
- End Date: The end date of the transaction
- User ID: the ID value that we get in step 7.
- Username: the username that we get in step 7.a
- Status: Completed or Failed
- Error Message: the error message If the status is failed and empty, it’s completed.
- Screenshot Path: screenshot of the error

7️⃣ Send the result.xlsx and summary.csv files via email to receiver emails.

8️⃣ Wait until you receive a new email. If you didn’t receive an email for 5 minutes, then stop the

process.



# Core Components

## Main State Machine

![Main State Machine](https://github.com/kirollos-Magdy1/Creating-User-Accounts/assets/61789409/732fddf9-541b-424f-a4f9-d5f0236096fe)
- Start by Initlializtion state to load the config file
- If it is loaded successfully with no system exception,. go to Waiting For Email State to receive the first email
- While a new email being received, the process will run through the following loop
    - “Waiting For Email’ =⇒ “Initialization”
    - “Initialization” =⇒ “Process Transaction”
    - “Process Transaction” =⇒ “Waiting For Email’


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

