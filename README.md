# Codeveda Task: ASP.NET MVC Authentication with Google Login

## Overview

This project demonstrates **authentication and authorization** in an ASP.NET MVC application using **Individual Accounts** with **external login via Google**.

It is designed to show **real-world secure practices**, including handling sensitive data properly and integrating third-party authentication providers.

The project includes:

* ASP.NET Identity (Individual Accounts)
* Google External Login (OAuth 2.0)
* Secure handling of secrets using User Secrets & Environment Variables
* Authorization using `[Authorize]` attribute
* Clean project structure following best practices

---

## Features

### 1. **ASP.NET Identity Authentication**

* Built-in authentication system (Login, Register, Logout)
* Cookie-based authentication
* Secure password handling

---

### 2. **Google External Login Integration**

```csharp
builder.Services.AddAuthentication()
    .AddGoogle(options =>
    {
        options.ClientId = builder.Configuration["Authentication:Google:ClientId"];
        options.ClientSecret = builder.Configuration["Authentication:Google:ClientSecret"];
    });
```

* Login using Google account
* OAuth 2.0 integration
* Secure redirection handling

---

### 3. **Secure Secret Management**

Sensitive data مثل:

* Google `ClientId`
* Google `ClientSecret`

❌ NOT stored in source code

✔ Instead, handled using:

* **User Secrets (Local Development)**
* **Environment Variables (Production)**

Example:

```bash
dotnet user-secrets set "Authentication:Google:ClientId" "YOUR_CLIENT_ID"
dotnet user-secrets set "Authentication:Google:ClientSecret" "YOUR_CLIENT_SECRET"
```

---

### 4. **Authorization حماية الصفحات**

```csharp
[Authorize]
public class HomeController : Controller
{
    public IActionResult Index()
    {
        return View();
    }
}
```

* Only authenticated users can access protected pages

---

### 5. **Git Best Practices**

The project uses `.gitignore` to exclude:

```text
bin/
obj/
.vs/
secrets.json
appsettings.Development.json
```

✔ Prevents uploading:

* Temporary files
* Sensitive data
* Local configuration

---

## Project Structure

```
Codeveda-auth/
│
├── Controllers/
├── Views/
├── Models/
├── wwwroot/
├── Program.cs
├── appsettings.json
├── .gitignore
└── Codeveda-auth.csproj
```

---

## How to Run

1. Clone the repository from GitHub
2. Navigate to project folder
3. Add your Google credentials using User Secrets:

```bash
dotnet user-secrets init
dotnet user-secrets set "Authentication:Google:ClientId" "YOUR_CLIENT_ID"
dotnet user-secrets set "Authentication:Google:ClientSecret" "YOUR_CLIENT_SECRET"
```

4. Run the project:

```bash
dotnet run
```

5. Open browser:

```
https://localhost:{port}/Identity/Account/Login
```

---

## Security Notes (Important)

* Never expose secrets in source code or GitHub
* Always regenerate credentials if leaked
* Use secure storage for sensitive data

---

## Learning Outcomes

* Understanding ASP.NET Identity
* Implementing external authentication (Google OAuth)
* Securing applications using best practices
* Managing secrets safely in development and production
* Working with authentication middleware

---

## Conclusion

This project demonstrates how to build a **secure, production-ready authentication system** using ASP.NET MVC with external login providers, following **industry best practices**.
