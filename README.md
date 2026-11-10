# SAML & SSO Troubleshooting

## 🎫 The Ticket

It's been over a month since I joined the security team at Northwind Health. Now in my fifth week, the work has moved to a new challenge: the Billing application's SSO launch is tomorrow, but testing has uncovered three problems.

My manager writes:

> We launch single sign-on for the billing app tomorrow. In testing today, nothing works the way it should. Three things are going wrong. Work out what's causing each one, tell me the order to fix them, and flag anything that's a security problem, not just an annoyance.

<BR>

**Supporting information:** [SSO configuration and testing details](Document/01.%20Source%20Data.md)

<BR>


## What's the Risk?

Looking at the supporting information, three things concern me.

Employees who need access might be unable to do their jobs, potentially disrupting Billing operations. Meanwhile, someone else might receive more access than their responsibilities allow, creating a security risk.

But there's another concern: **the pressure to launch tomorrow.** A temporary workaround is already in place to keep testing moving. What happens when getting the application working feels more important than making sure it’s secure?

The challenge isn’t just getting people signed in with the right access. It’s making that happen without easing up on security checks along the way.

<BR>


## The Investigation

Three questions guided my investigation:

### 1. Where and why does the sign-in process break?

I looked at what worked, where the errors appeared and what each system expected.

### 2. Which problems affect access, and which create security risks?

I considered the impact of the failures and whether any users were receiving permissions beyond their roles.

### 3. How do we meet the launch deadline without compromising security?

I considered the impact on users, business operations and security, including the temporary workaround, before deciding what needed attention first.

<br>


## What I Found

The three SSO problems had different causes.

| Problem | Root Cause | Impact |
|---|---|---|
| Invalid audience | A trailing slash caused the SAML audience identifiers to differ. | Users were blocked from accessing the Billing application. |
| No matching account | Entra ID sent UPNs, while the application expected email addresses. | Sam and six colleagues couldn't access their accounts. |
| Incorrect Admin access | The application assigned Admin based on group names containing `Billing`. | Lena could see the Admin menu despite being a Billing Clerk. |

The first two problems prevented legitimate access. **Lena's case raised a different concern: someone might have more access than their role allows.**

[Explore the findings and root causes](Document/02.%20Findings%20%26%20Root%20Causes.md).


