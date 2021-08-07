# Take care of your trailing slashs

When calling a Django server, you must be aware of how you call it given your different params (for example: the URL). Django doesn't add trailing slashs at the end of the URL except that you use the [Common.middleware](https://docs.djangoproject.com/en/1.8/ref/middleware/#module-django.middleware.common). The `class CommonMiddleware` performs URL rewriting based on the `APPEND_SLASH` and `PREPEND_WWW` settings. Both `APPEND_SLASH` and `PREPEND_WWW` are `True` by default.


### When it could be start causing issues

If you make a request to a Django server and you send an URL like this `www.example.com/append_slash`, Django will perform this call internally as `www.example.com/append_slash/` but if the server doesn't reply with a OK status, the call will be performed again (by nginx) with the URL with the slash. If you're changing something in the DB or performing some non-idempotent actions, it's possible to start receiving 4xx status from the server.
