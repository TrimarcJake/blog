---
title: Using the Protected Users Group - Credential Caching (Part 2 of…
creation_date: April 9, 2024
modification_date: April 22, 2024
---
In today's episode, we’ll be getting into credential caching and why membership in the Protected Users Group (PUG) eliminates it.

In Active Directory-based environments, there are credentials *everywhere*:
* AD attributes: unicodePwd, dbcsPwd, ntPwdHistory, lmPwdHistory, SupplementalCredentials
* Local Security Account Manager (SAM) databases
* Local Security Authority Subsystem Service (LSASS) memory
* “Passwords.xlsx” 🥲

In most situations (except Passwords.xlsx  🥲), credentials are stored as a "one-way function" (OWF) which converts the password you type into a bunch of gobbledygook that can’t be easily converted back into its original value. This conversion process is called “hashing” and helps protect the confidentiality of the password in cases of casual discovery of hashes. 

Unfortunately, Active Directory considers this hashed password information functionally identical to the original password. If an attacker can find a hashed password, they can use it to gain access to other systems as if they were the original owner of that password. There’s no need to find the actual cleartext password.

However, using a hash as your credential is not super flexible; a cleartext password is more valuable. Thankfully (for attackers), it’s now technically feasible to crack some types of hashed passwords in reasonable periods of time using consumer-level password cracking rigs. After cracking, the attacker gains knowledge of the actual password, not just its hash.

An actual password is more useful for an attacker because it can be used anywhere there’s a password field instead only services that accept hashes as authentication. For example, Entra ID… and everything that uses Entra ID as an Identity Provider. 

Speaking of actual passwords, did you notice how I said “most situations” above? Some password caching methods (eg. WDigest) forgo hashing and store the password in cleartext. If an attacker gets control of a computer with WDigest authentication enabled, they don’t need to crack the password; it’s cached in memory as cleartext already. A simple memory dump reveals the password to the attacker. 

Adding users to the Protected Users group eliminates this caching completely. Hashed, cleartext, whatever, wherever - it ain’t happening. When an attacker gets access to a computer that *should* contain cached information, they’ll find nothing. 

But don’t worry about those poor attackers, there are plenty of other ways for them to get access to credentials without cache abuse. In the next episode, we’ll talk about how membership in the Protected Users group helps eliminate the authentication methods that are most susceptible to other types of credential abuse. 
