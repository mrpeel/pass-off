# Open Sesame Password Manager
The Open Sesame Password Manager remembers your passwords without remembering your passwords.  Open Sesame implements a version of the Master Password App ([Lyndir/MasterPassword](https://github.com/Lyndir/MasterPassword)) algorithm (<http://masterpasswordapp.com/algorithm.html>).

It is a standalone web-app ([https://mrpeel.github.io/opensesame/]) and a chrome-extension which allows unique passwords to be generated for a website domain.  The generation is deterministic which means that the same set of values will always generate the same password.  This allows Open Sesame to 'remember' your passwords.

## What it does
Open Sesame generates passwords using the combination of fields and password type.  The same combination always generates the same password.  A change to any of the fields or password type will result in a different password being generated.  This means that using the same personal details and pass phrase for different websites will generate a different password for each site.

Open Sesame generates passwords using the following fields:
* First name
* Family name
* Open Sesame Pass phrase
* Web site domain
* Password type
* (Optional) User name
* (Only for security answer) Security question

Open Sesame generates the following types of passwords:
* Maximum password (20 characters)
* Long password (14 characters)
* Medium password (8 characters)
* Basic password (8 characters - only uses letters and numbers)
* Short password (4 characters - only uses letters and numbers)
* Four digit PIN
* Six digit PIN
* User name
* Security answer



## How it works
Open sesame uses PBKDF2 and HMAC256 crypto functions.  'window.crypto.subtle' it used when it is supported by the browser, otherwise CryptoJS is loaded.  

The steps to generate a password are:

1. Use PBKDF2 on the Pass phrase with full name (First name + Family Name) as the salt to generate a key
2. Join User name, Domain name and Security question together and use the key to generate a seed array using HMAC256
3. Use the seed to select a template of the correct type
4. Work through the template and select the appropriate type of character for each element in the template using the seed array
5. The Generated password is the resulting string


## Libraries used
* Material Design Lite


Polyfills:
* CryptoJS (aes.js)
* CryptoJS (pbkdf2.js)
* CryptoJS (hmac-sha256.js)
* Promise.js