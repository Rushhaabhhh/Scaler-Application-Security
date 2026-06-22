# Lab: High-Level Business Logic Flaw

## Introduction

This lab illustrates a business logic flaw resulting from inadequate validation of input controlled by the client. The application permits users to update item quantities in the shopping cart to negative numbers. By taking advantage of this vulnerability, attackers can alter the final cart balance, enabling them to obtain costly items for a fraction of their actual price.

## Objective

Complete the purchase of the **Lightweight l33t leather jacket** even though the account lacks the required store credit.

---

## Vulnerability Details

The server accepts the client-side `quantity` parameter directly without verifying that it represents a positive integer. 

An attacker can exploit this by:

1. Putting a low-cost item into the shopping cart.
2. Editing the item quantity to a negative integer.
3. Reducing the overall cart total below zero.
4. Adding a high-value item to the cart.
5. Balancing out the cost using the negative offset.
6. Completing checkout using standard store credit.

---

## Exploitation Steps

### 1. Authentication

Log in to the application using the following credentials:

```text
Username: wiener
Password: peter
```

**Screenshot:** `images/login_success.png`

---

### 2. Selecting a Low-Cost Item

Add the lowest-priced product available in the store catalog to the shopping cart.

**Screenshot:** `images/cheap_item_added.png`

---

### 3. Intercepting the Cart Update

Turn on interception in Burp Suite and add another unit of the low-cost item.

Examine the captured request:

```http
POST /cart
```

Expected body content:

```http
productId=2&quantity=1
```

**Screenshot:** `images/original_quantity_request.png`

---

### 4. Injecting a Negative Value

Forward the intercepted request to Burp Repeater and modify the quantity parameter to a negative integer:

```http
quantity=-10
```

(or another appropriate negative number).

The application processes this negative quantity and updates the cart contents accordingly.

---

### 5. Generating Negative Cart Balance

Repeat this step until the shopping cart displays a negative balance.

For example:

```text
Quantity: -99
Total: -$X.XX
```

This effectively acts as artificial store credit to offset future purchases.

**Screenshot:** `images/negative_cart_total.png`

---

### 6. Adding the Target Product

Add the target item to your shopping cart:

```text
Lightweight l33t leather jacket
```

The positive price of the leather jacket is balanced out by the negative total already present in the cart.

**Screenshot:** `images/jacket_added.png`

---

### 7. Checking Out

Navigate to the checkout page and finalize the transaction.

The manipulated cart total allows the purchase to be completed successfully.

**Screenshot:** `images/lab_solved.png`

---

## Impact Assessment

This business logic vulnerability allows unauthorized users to:

- Acquire goods at prices far below their retail value.
- Generate artificial transaction balances.
- Bypass established business constraints.
- Inflict direct financial loss on the business entity.
- Manipulate shopping cart workflows.

---

## Root Cause Analysis

The system fails to enforce business constraints on user-supplied product quantities at the server level.

Specifically:

- The system permits negative values in quantity fields.
- Total cart costs are calculated directly using these unvalidated values.
- There is no backend check to ensure that the item quantity is greater than zero.

---

## Mitigation Strategies

1. Validate item quantities on the server side prior to processing.
2. Reject any negative quantity values outright.
3. Enforce strict minimum quantity limits.
4. Calculate pricing on the server side rather than relying on client input.
5. Implement integrity validations on shopping cart contents before checkout.

---

## Key Takeaway

Business logic flaws typically occur when web applications trust client-supplied input without enforcing business rules on the backend. In this case, accepting negative quantities allowed for the manipulation of pricing calculations, making unauthorized purchases possible.