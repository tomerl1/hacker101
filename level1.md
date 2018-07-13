# [Hacker101 Level 1](https://levels-a.hacker101.com/levels/1/)

It says there are 4 bugs but states only 3, I couldnt find anything else...

## 1 CSRF

The protection is flawed because the CSRF token that is generated is not randomized, it's always the same.  
So just like in Level 0 you can have a CSRF attack just add the CSRF input field.

## 2 Stored XSS

The posts table is vulnerable to stored XSS attack.  
For example:

```
http://"onmouseover="alert('hacked')
```

## 3 Forced Browsing

The permalink allows you to see any post by any user. It looks like the Id is incremental.
So just change the Id param and you will be exposed to other users posts and information.

Example:  
[https://levels-a.hacker101.com/levels/1/post?id=20]