# Burp Suite Community Edition

**Category:** Web Application Security Testing  
**Difficulty:** Intermediate  

## Description

Burp Suite is the leading toolkit for web application penetration testing. The Community edition is completely free and extremely powerful.

## Core Tools Used
- Proxy (intercept and modify requests)
- Repeater
- Intruder
- Site map / Target scope

## Common Workflow

1. Configure browser proxy (127.0.0.1:8080)
2. Turn Intercept On/Off
3. Send requests to Repeater for manual testing
4. Use Intruder for fuzzing and brute forcing

## Example Usage

**Example 1: Intercepting and Modifying Requests**  
Intercepted a login request and modified parameters.

*(Insert screenshot: Burp Proxy intercepting a request)*

**Example 2: SQL Injection Testing**  
Used Repeater to test different payloads.

**Example 3: Brute Force Attack**  
Used Intruder with a wordlist against a login form (in lab only).

## What I Learned
- How modern web apps communicate behind the scenes
- The impact of improper input validation
- Difference between manual and automated testing

## Resources
- PortSwigger Web Security Academy (Free training)
- Burp Suite Documentation
