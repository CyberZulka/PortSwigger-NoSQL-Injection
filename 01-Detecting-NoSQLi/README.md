# Lab 01: Detecting NoSQL Injection-- SOLVED ✅
# Lab 01: Detecting NoSQL Injection — SOLVED ✅

**Platform:** PortSwigger Web Security Academy  
**Category:** NoSQL Injection  
**Level:** Apprentice  
**Tool:** Burp Suite Community Edition (Repeater)  
**Status:** Solved ✅

---

## Objective

The product category filter is powered by MongoDB. Perform a NoSQL injection attack that causes the application to display unreleased products.

## Vulnerability Type

**JavaScript / Syntax Injection** (Not Operator Injection)

The `category` parameter is concatenated directly into a server-side JavaScript query without sanitization or type validation.

## Detection

Intercepted the request in Burp:
