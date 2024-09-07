# SQL Injection

## Basic Overview 
QL injection is a common web vulnerability that occurs when an attacker can inject malicious SQL queries into input fields of a website, potentially gaining unauthorized access to databases.This is a basic scanner that primarily checks for error-based SQL injection vulnerabilities. It does not handle more advanced cases like blind or time-based SQL injection.

## Code Breakdown 

Imports:

- requests: Allows sending HTTP requests to websites.
- BeautifulSoup: A library for parsing HTML and extracting data.
- sys: Provides access to system-specific parameters (though unused here).
- urljoin: Used to combine URLs in a consistent way.

 get_forms(url) Function - This function fetches all forms from a given webpage.
 - It sends a GET request to the specified URL, parses the content with BeautifulSoup, and returns all the form elements (<form> tags) on that page.

 form_details(form) Function - This extracts detailed information about the form.
 - The form’s action (where the form data is sent) and method (either "GET" or "POST") are extracted.
 - All input fields (<input> tags) within the form are collected with their type (e.g., text, hidden, submit), name, and value.

  vulnerable(response) Function - Checks if the response contains specific error messages that might indicate a SQL injection vulnerability.
  - It looks for common SQL-related errors in the response from the server, like "you have an error in your SQL syntax.

  sql_injection_scan(url) Function - This is the main function that scans the page for SQL injection vulnerabilities.
  - It calls get_forms() to retrieve all forms from the page and prints how many forms were found.
  - form_details(form) is called to get form-specific details.
  - A loop iterates over the form's input fields, injecting a single quote (') and double quote (") to test for potential SQL injection.
  - Based on the form method (GET or POST), it sends the appropriate request (either s.get or s.post) to submit the form data.
  - After the form submission, vulnerable(response) checks if the response contains SQL error messages that suggest a vulnerability.

  Main Execution Block - If the script is executed as the main program, it calls the sql_injection_scan() function on the specified URL (in this case, cnn.com).

  ## SQL Injection Check Logic:
  The code checks whether injecting a single or double quote into the input fields of a form leads to an SQL-related error in the server's response. If such an error is detected, it indicates the presence of a vulnerability that could allow an attacker to perform an SQL injection attack.
  
  Example Process:
  The code detects forms on a webpage.
  For each form, it fills input fields with SQL injection payloads (like test' or test").
  It submits the form and checks the response for SQL-related error messages.
  If such messages are found, the website may be vulnerable to SQL injection.
