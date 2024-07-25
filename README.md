# Understanding Reflected and Stored Cross-Site Scripting (XSS)

## Introduction

Cross-Site Scripting (XSS) is a common security vulnerability found in web applications. XSS attacks allow attackers to inject malicious scripts into web pages viewed by other users. There are mainly two types of XSS: Reflected XSS and Stored XSS. In this guide, we’ll explore both types and demonstrate how to test them using Damn Vulnerable Web Application (DVWA).

## Prerequisites

1. DVWA installed and running on your server.
2. Basic knowledge of HTML and JavaScript.
3. Web browser (preferably with developer tools).

## Setting Up DVWA

1. **Download and Install DVWA**: You can download DVWA from its [official GitHub repository](https://github.com/digininja/DVWA).
2. **Access DVWA**: Navigate to `http://localhost/dvwa` in your web browser.
3. **Login**: Default credentials are `admin` for the username and `password` for the password.
   <img width="960" alt="d4" src="https://github.com/user-attachments/assets/a800d14b-c3d3-49ca-93b2-2e2f8f297d12">
   

5. **Set Security Level**: Set the security level to "Low" for easier testing.
   <img width="960" alt="d3" src="https://github.com/user-attachments/assets/5bef4677-7409-4064-a9b3-9e41cbd35634">


## Reflected XSS

Reflected XSS occurs when malicious scripts are reflected off a web server and executed in the victim’s browser. The script is usually embedded in a URL.

### Steps to Test Reflected XSS in DVWA

1. **Navigate to XSS (Reflected)**:
   - From the DVWA main menu, click on "XSS (Reflected)".
     <img width="960" alt="d2" src="https://github.com/user-attachments/assets/4e946f37-70c8-47c3-8388-89ef839a86a0">


2. **Test Input Field**:
   - You will see an input field labeled "Name". Enter a basic XSS payload and submit.

     ```html
     <script>alert('XSS');</script>
     ```
     ![Screenshot 2024-07-25 121645](https://github.com/user-attachments/assets/0780429a-41fc-4132-b8f2-d45d3ea32875)



   - If the application is vulnerable, an alert box with the message "XSS" will appear.
  
     <img width="960" alt="d5" src="https://github.com/user-attachments/assets/34d35445-318a-4557-9c80-7cb2e4cceb60">

     

3. **Test URL Parameter**:
   - Modify the URL parameter to include an XSS payload.

     ```html
     http://localhost/dvwa/vulnerabilities/xss_r/?name=<script>alert('XSS');</script>
     ```
     <img width="960" alt="image" src="https://github.com/user-attachments/assets/7eccff65-7a60-4e04-ba37-7f7df41d5b92">



   - If the application is vulnerable, an alert box with the message "XSS" will appear.
     <img width="960" alt="d8" src="https://github.com/user-attachments/assets/5eb73ab2-42fc-4795-b896-800d115029b7">


4. **Advanced Payloads**:
   - Try different payloads to bypass simple filtering mechanisms.

     ```html
     <img src=x onerror=alert('XSS')>
     ```
     <img width="960" alt="d9" src="https://github.com/user-attachments/assets/b3b701d3-b9d5-4dfe-8a51-fea18c7a7406">
     ![Screenshot 2024-07-25 123738](https://github.com/user-attachments/assets/10d3cc0e-3500-4363-ba21-5943adf2ca06)



## Stored XSS

Stored XSS occurs when malicious scripts are permanently stored on the target server, such as in a database, and executed when users visit the affected page.

### Steps to Test Stored XSS in DVWA

1. **Navigate to XSS (Stored)**:
   - From the DVWA main menu, click on "XSS (Stored)".
     <img width="960" alt="c2" src="https://github.com/user-attachments/assets/b96aa115-47a8-4ced-b146-3a18ba2da265">


2. **Test Input Field**:
   - You will see fields to enter a message and your name. Enter a basic XSS payload in the message field and submit.

     ```html
     <script>alert('Stored XSS');</script>
     ```
     ![Screenshot 2024-07-25 124459](https://github.com/user-attachments/assets/4a02f3d6-d027-411f-ba94-e361fb7f930f)


   - If the application is vulnerable, an alert box with the message "Stored XSS" will appear when the page reloads or when any user views the stored message.
     <img width="960" alt="c4" src="https://github.com/user-attachments/assets/5363a287-30ec-4ee3-9861-4dca6f58bc85">


## Mitigation Techniques

### For Reflected XSS:
1. **Input Validation**: Validate and sanitize user inputs to prevent malicious scripts.
2. **Output Encoding**: Encode outputs to prevent the execution of injected scripts.

### For Stored XSS:
1. **Input Validation**: Ensure all inputs are validated and sanitized before storage.
2. **Output Encoding**: Encode outputs when displaying stored data.

## Conclusion

Understanding and identifying XSS vulnerabilities is crucial for securing web applications. By following the steps outlined above, you can test for both Reflected and Stored XSS using DVWA. Always remember to apply proper input validation and output encoding to mitigate these vulnerabilities.

Happy testing!
