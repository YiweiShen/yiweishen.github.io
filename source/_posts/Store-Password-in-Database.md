---
title: Store Password in Database
date: 2021-07-14 22:59:48
tags:
---
I have been thinking about how to store customer's login details into the database.

I mean, how to arrange the tables to store the passwords securely enough so that even if one day the database is leaked (and it will), no actual passwords are exposed.

On seond thoughts, managing the passwords by myself could be a bad idea.

Hand it over to Google or Facebook.

OK.

Let's say, for some unknown reasons, I have to do it.

The million-dollar question is, HOW.

- If I store the plain text password anywhere in the database, the company probably would just fire the guy who designed the database, that's me, for good.
- If I store the hashed password with username, just like that, it is vulnerable to dictionary or rainbow table attacks. But maybe I can keep my job, for now.
- If I use SHA512, instead of MD5, as the hash function, the computational power required to crack the passwords is signaficantly different.

## Solution (perhaps) 

Add random salt to each individual password, and then calculate the SHA512 hash values. Remember to generate salt again, once the customer changes the password. Also, I need a cryptographically secure random function to generate salt.

| LoginID |  LoginName  |  Salt |  HashedPasswordWithSalt |
|:-------:|:-----------:|:-----:|:-----------------------:|
| 0000001 |     Alice   | T7#jd | RncFuVDvUtVxXUFrvOHPfiF |
| 0000002 |      Bob    | $1Yo2 | UZ0CkHkEccFErZujyAl3wys |
| 0000003 |    Charlie  | UWp*1 | Pt4a1176FY2zcewmbcvEuAN |

In practice, use longer salt, I guess.

Ref:

Password Cracking
https://www.youtube.com/watch?v=7U-RbOKanYs

How NOT to Store Passwords!
https://www.youtube.com/watch?v=8ZtInClXe1Q

Rainbow table
https://en.wikipedia.org/wiki/Rainbow_table