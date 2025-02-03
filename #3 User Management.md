# User Management

## Server access types:

### OS Access: Performed by admins and developer for administration and development.
### Application Access: Performed by end users for accessing application.

## User types:

1. Local user: End user with limited privileges.
2. Super user: Admin user with full privileges. [root]
3. System user: Inbuilt user used by the OS and Applications internally [we cannot login with this user]

## AAA Proccess:

A -> Authentication - Kaun hai.
A -> Authorization - Kya yah kar sakta hai.
A -> Accounting - kya kya kiya.

* Credential or token user for AAA is called user.
* To secure the access of a usser, We must define a password.
* When we create a user in linux: it gets created in locked state.
* To unlock a user: it is mandotory to either seta password or disable password.

## Commands for basic user management.
```
# useradd jane - Adda user account.
```
