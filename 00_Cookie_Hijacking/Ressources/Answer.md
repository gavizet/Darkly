# 00_Cookie Hijacking

## Risk

If we look into the Cookies used for the site, we can see an ```I_am_admin``` entry with ```68934a3e9455fa72420237eb05902327``` as it's value.\
Using an [MD5 encrypt/decrypt site](https://www.cryptage-md5.com), we can easily see this translates to ```false ```.\
Just change the value of ```I_am_admin``` to ```true``` in MD5 (```b326b5062b2f0e69046810717534cb09```) in order to be considered an admin on the site.\
For this specific cookie, both the HttpOnly (readable from front-end Javascript code by simply typing ```document.cookie``` in the console) and Secure (cookie can be returned over non encryted connections aka HTTP) properties are blank, meaning they are not enabled, meaning it has even less protection.\
Attacker can easily hijack an admin session with all its privileges.

**Flag :** ```df2eb4ba34ed059a1e3e89ff4dfc13445f104a1a52295214def1c4fb1693a5c3```

## Prevention

The session cookie does not ever need to be readable by the client and is only needed for the server.\
**There are multiple easy ways to prevent this specific security risk :**
- Set ```HttpOnly``` flag on all cookies
- Set ```Secure``` flag on all cookies
- Use randomly generated and encoded data for the cookie value
- Uh... just don't stock admin status in a cookie !
