# Accessing Hidden Admin Panels via Client-Side Source Code Exposure

## Lab Information

* **Classification:** Access Control
* **Skill Level:** Apprentice
* **Challenge Name:** Unprotected Admin Functionality with Unpredictable URL
* **Status:** Resolved

---

## Objective

Discover a hidden administrative route exposed within client-side scripts and use it to delete the user account:

```text
carlos
```

---

## Vulnerability Analysis

The application attempts to secure its administrative interface by placing it at an obfuscated, unpredictable URL path. However, this route is exposed within the application's client-side source code, allowing any visitor to find it. Because the administration endpoint does not enforce access control verification on the backend, once discovered, it can be accessed by anyone.

---

## Exploitation Steps

### 1. Inspecting the Client-Side Code

View the homepage source code of the application:

```text
Ctrl + U
```

Within the client-side JavaScript code, we locate the reference to the administrative endpoint:

```javascript
adminPanelTag.setAttribute('href', '/admin-z691va');
```

This reveals the path to the administrative interface.

### Screenshot

![Source Code Disclosure](images/admin_url_source_code.png)

---

### 2. Navigating to the Admin Endpoint

Use the discovered path to access the administrator panel directly:

```text
/admin-z691va
```

The application grants full access to the administrative dashboard without asking for authentication.

---

### 3. Deleting the Target User

The administrator console provides user management controls. Locate the account entry for:

```text
carlos
```

and delete it.

---

## Result

The target user account was deleted and the challenge was successfully completed.

### Screenshot

![Lab Solved](images/solved_evidence.png)

---

## Severity and Impact

An attacker can:

* Discover obscured administrative pathways.
* Bypass client-side security measures.
* Execute administrative actions.
* Modify, edit, or delete sensitive user databases.

---

## Mitigation and Prevention

* Enforce strict role-based access validation on the server side for all routes.
* Never use obfuscated URLs or hidden paths as a primary security control.
* Restrict access to administrative functionality using backend session checks.
* Avoid exposing administrative paths or credentials in client-side code.

---

## Key Takeaways

* Obfuscating paths is not a replacement for access controls.
* Client-side code should never expose backend administration routes.
* Session checks must be processed on the server on every request.
* Security through obscurity leaves systems vulnerable to disclosure.
