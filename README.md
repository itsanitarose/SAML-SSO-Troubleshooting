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

I identified three configuration problems affecting the Billing application's SSO launch.

| Problem | Finding |
|---|---|
| **Audience validation failure** | A trailing slash caused the audience identifiers to differ, preventing users from accessing the application. |
| **Identity mapping failure** | Entra ID sent UPNs that didn't match the email addresses expected by the application, affecting Sam and six colleagues. |
| **Incorrect Admin role assignment** | A broad group-matching rule included `Billing-Readers`, allowing Lena to see the Admin menu. |

The first two problems blocked legitimate access. The third raised a security concern: Lena appeared to have access beyond her role, although her ability to perform administrative actions still needed verification.

[Explore the findings and root causes](Document/02.%20Findings%20%26%20Root%20Causes.md).

<BR>




## Decisions & Recommendations

My first security priority was Lena's potential Admin access. I recommended verifying her permissions, reviewing privileged activity and containing any excessive access identified.

The audience mismatch was the first technical fix because it affected everyone and needed correcting to allow proper testing. The identity-mapping issue would follow.

With launch approaching, I recommended delaying it until the fixes were verified. If the issues couldn't be resolved before launch, I'd present the unresolved risks, their potential impact on Billing operations and my recommendation to delay, leaving the final go-live decision to the responsible decision maker.

[Explore the fix order and verification plan](Document/03.%20Fix%20Order%20%26%20Verification%20Plan.md)

<BR>


## Reflection & Next Steps

This investigation reinforced the difference between authentication and authorization, and why both must be checked separately. Authentication confirms who a user is: Sam authenticates successfully at Entra ID, but the application cannot match his identity to an account. Authorization determines what an authenticated user may do: Lena signs in successfully, but the application may give her access beyond her role.

Both problems looked like "SSO is broken," but they required completely different fixes: one in identity mapping, the other in role assignment. Neither could be safely solved by simply making sign-in work.

I also learned to distinguish **security urgency from technical dependency**. The most serious concern isn't always the first configuration change needed to make testing possible.

Next, I want to reproduce the SAML configuration in my Entra ID lab and test the behaviour myself.

<BR>

---

## Explore the Investigation

| Document | What's Inside |
| :--- | :--- |
| [01. Source Data](https://github.com/itsanitarose/SAML-SSO-Troubleshooting/blob/main/Document/01.%20Source%20Data.md) | The ticket, SSO configuration and testing details |
| [02. Findings & Root Causes](https://github.com/itsanitarose/SAML-SSO-Troubleshooting/blob/main/Document/02.%20Findings%20%26%20Root%20Causes.md) | What doesn't match, between which settings, and which side to change |
| [03. Fix Order & Verification Plan](https://github.com/itsanitarose/SAML-SSO-Troubleshooting/blob/main/Document/03.%20Fix%20Order%20%26%20Verification%20Plan.md) | Fix order, how each fix is tested, security assessment and launch recommendation |
| [04. Digging Deeper](https://github.com/itsanitarose/SAML-SSO-Troubleshooting/blob/main/Document/04.%20Digging%20Deeper.md) | Why one trailing slash breaks sign-in |


[← Week 4: MFA Recovery & Identity Verification](https://github.com/itsanitarose/IAM-Social-Engineering-MFA-Recovery) · [All Case Studies](https://github.com/itsanitarose/IAM-Case-Studies)

*Northwind Health is fictional. This is independent work; no production systems were changed.*
