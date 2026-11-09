
## 🎫 The Ticket

It's been over a month since I joined the security team at Northwind Health. Now in my fifth week, the work has moved to a new challenge: the Billing application's SSO launch is tomorrow, but testing has uncovered three problems.

My manager writes:

> We launch single sign-on for the billing app tomorrow. In testing today, nothing works the way it should. Three things are going wrong. Work out what's causing each one, tell me the order to fix them, and flag anything that's a security problem, not just an annoyance.

<BR>

**Supporting information:** [SSO configuration and testing details](Document/01.%20Source%20Data.md)

<BR>

## What's the Risk?

Looking at the supporting information, two things concern me: employees who need access might be unable to do their jobs, while someone else might receive more access than they should.

The first could disrupt Billing operations. The second is a security concern, particularly if someone can perform administrative actions beyond their responsibilities.

There's also a temporary workaround in place to keep testing moving, which needs to be reviewed before launch.

**Getting people signed in isn't enough. They also need to have the right level of access.**

<BR>

## The Investigation

The supporting information showed three different problems, so I needed to understand where each one occurred before deciding what to fix.

Three questions guided my investigation:

### 1. Where does the sign-in process break?

I looked at what worked, where the error appeared and what each system expected.

### 2. Is this an authentication problem or an access problem?

I wanted to separate problems that prevent someone from signing in from those that could give someone the wrong permissions.

### 3. What needs attention first?

With the launch scheduled for tomorrow, I needed to consider the impact on users, business operations and security risks before recommending a fix order.


