

<div align="left"><img src="https://github.com/user-attachments/assets/62f72f75-840c-47ed-875f-ad0bb3cfeb8d" width=25% height=25%></div>

# Back-To-The-Last-Password
DateTime Password Generator

# Overview

_"Back To The Last Password"_ is a multilingual password generator based on the last time a user changed their password. It uses information from that date, such as the season, month, day of the week, and year, to generate passwords.
This application supports 155 languages, although not all languages have been fully tested, as I only read and understand 4 languages :-]

# Why?

When performing International Red Teaming, you might find yourself working with languages that you do not understand. This tool will assist in generating low-level passwords in the required language. However, it is important to remember that users within a specific domain may not always use datetime as their passwords, even though it is a possibility.

# How It Works

## Input Data
- **No Data to Upload**: Select Country, Language and Date and you can  generate passwords and wordlist

https://github.com/user-attachments/assets/7613c29f-233f-4d4f-a884-95f135208412


- **Ldapdomaindump**: `domain_users.json` [https://github.com/dirkjanm/ldapdomaindump](https://github.com/dirkjanm/ldapdomaindump)



https://github.com/user-attachments/assets/6d1d0bbe-e145-48d3-9948-db76b774cd09



- **Roadrecon**: `roadrecon.db` [https://github.com/dirkjanm/ROADtools](https://github.com/dirkjanm/ROADtools)

https://github.com/user-attachments/assets/190012d2-134b-465b-b7a7-2a28216f5a38


- **Azure AD Password Checker**: `js script` [https://github.com/quahac/Azure-AD-Password-Checker](https://github.com/quahac/Azure-AD-Password-Checker)

   #### Steps to Use the "Azure AD Password Checker" js script 

   1. **Download Script:**
      - Access the Azure AD Password Checker script from the following GitHub repository: [Azure AD Password Checker](https://github.com/quahac/Azure-AD-Password-Checker/blob/main/userslist%20web%20browser%20console.js).

  1. **Copy the Script:**
     - Open the script in your web browser.
     - Select all the code and copy it to your clipboard.

  2. **Open Azure Portal, if you have access:**
     - Navigate to the Azure Portal: [Azure Portal](https://portal.azure.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers).
     - Alternatively, you can use this link: [Microsoft Entra](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers/).

  3. **Open Developer Console:**
     - Press `F12` to open the Developer Tools in your browser.
     - Navigate to the "Console" tab.

  4. **Paste the Script:**
     - Paste the copied script into the console and press `Enter`.

  5. **Wait for Execution:**
     - Wait a few seconds for the script to execute and display the results.

     **Notes** 
     - Ensure you have the necessary permissions to run scripts in your Azure environment.


## Password Generation

When you select a user, the application looks at the last password change date and creates a password using:
- Year
- Season
- Month
- Day of the week
- Day of the month
- Special characters

For example, if a user changed their password on January 1, 2025, the generated password might look like this:

```2025 > Winter > January > Wednesday > 01 > SpecialChars: !@#...```

### Special Character Options

You can customize the special characters used in the passwords with a slider that has four options:

- **Min:** Uses a few characters like `!@#$%^` (good for quick checks).
- **Norm:** Uses more characters like `!@#$%^&*()-_` (recommended for regular use).
- **Max:** Uses many characters like `!@#$%^&*()-_=+{}[]:;"'<>,.?/~`` (you can change this in the code).
- **Custom:** You can enter any characters you want. (Red Team option)

## Features

- **Offline Use:** You can use this application without an internet connection.
- **Multilingual:** You can generate passwords in almost every language (that JavaScript datetime language handles).
- **MFA Anomaly:** List of users that could not have enabled Multi Factor Authentication, see for more information [Azure AD Password Checker](https://github.com/quahac/Azure-AD-Password-Checker) 

## Download Options

- **Download User Passwords:** Generate passwords for the selected user.
- **Download All Passwords:** Generate passwords for all users.
- **Download Language Words:** Generate words in selected languages, to use as banning list or for Hashcat or John.

## Embedded Sources

- **Countries Data:** The application includes `countries` data from [https://restcountries.com/](https://restcountries.com/v3.1/all), which has useful information about countries, credits to them.
  - [https://restcountries.com/v3.1/all](https://restcountries.com/v3.1/all)
- **SQLite Support:** It uses `sql.js`, `sql-wasm.min.js` and `sql_wasm_dataURL.js` for database functions without needing the internet. Check + credits to them:
  - [https://github.com/incubated-geek-cc/SQLiteBrowserUtility](https://github.com/incubated-geek-cc/SQLiteBrowserUtility)
  - [https://github.com/sql-js/sql.js](https://github.com/sql-js/sql.js)
- **Wasm Loading:** The application can load Wasm files without a server, based on this article. Check + credits to them: [How to Load & Run Local Wasm Modules Without a Server Using Client-Side JavaScript](https://javascript.plainenglish.io/how-to-load-run-local-wasm-modules-without-a-server-using-client-side-javascript-692f7b89da7d).

## Development and Testing

The application has been tested on the following systems and browsers:

### Operating Systems:
- Windows 10, 11 (en-us)
- Kali Linux 2024+ 

### Browsers:
- Firefox (version 131 and above) (en-us)
- Edge (version 130 and above) (en-us)
- Chrome (version 130 and above; some languages may not work) (en-us)

### Limitations

- **Apple IOS**: Running HTML and JavaScript files directly from the file system without a web server is restricted on iOS. This limitation is primarily due to security measures that prevent unauthorized access to local files.
- **Workaround**: To work around this limitation
   - **Use a Local Web Server**: Set up a local web server within the app using libraries like [GCDWebServer](https://github.com/swisspol/GCDWebServer). This allows you to serve HTML and JavaScript files from the app's bundle, enabling them to be accessed via `http://localhost`.
   - **Embed HTML in the App**: Instead of loading HTML files from the file system, you can embed the HTML content directly in your app's code and load it into a WebView. This approach eliminates the need for file system access.
 
## Acknowledgments

The HTML, JavaScript coding scripting information, and seasonal data were collected using GPT-4o mini via Duck.ai and ChatGPT (note: there may be translation errors).


# How to Fix This

Experienced hackers probably use this techniques to compromise users accounts ( and I admit, I use this too :-] ). One effective solution is to implement a banning list for certain words. You can generate these words using the `Download Language Words` button. Here’s how to apply this in different environments:

- **Azure:** Refer to Microsoft’s [Global Banned Password List](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-password-ban-bad#global-banned-password-list) for guidance on implementing a banned password list.
  
- **Normal Active Directory (AD):** Unfortunately, I don't have a specific solution for this. However, you may want to explore third-party tools or consult documentation for AD password policies.

Ultimately, the best solution is to promote **Security Awareness** among users. Educating them about the importance of strong passwords and the risks associated with weak ones can significantly enhance security.

# Another thing!

Just a heads up: I'm not a pro at HTML or JavaScript. I’ve done my best to figure things out and make this project work. Thanks for checking it out, and I’m open to any tips or feedback!


>**DISCLAIMER:**
>
>This code is for educational and research purposes only. The author does not support its use for illegal or unethical activities and is not liable for any harm or damage resulting from its use.
>
>By using this code, you agree to comply with all applicable laws and take full responsibility for your actions. This code is provided "as-is," without any warranties.
>
>Using this code for illegal or unethical purposes is strictly prohibited. You use it at your own risk and may face legal consequences. 
