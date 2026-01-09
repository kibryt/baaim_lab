# Przygotowanie do laboratorium

Do wykonania laboratorium będziesz potrzebował konta na [PortSwigger](https://portswigger.net) oraz narzędzia [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload).

Dodatkowo do tworzenia szablonu CSRF PoC (fragmentu kodu pokazującego, że podatność istnieje) będzie potrzeba skorzystania z narzędzia, który taki kod generuje na podstawie zapytania HTTP/HTTPS (tylko w niektórych ćwiczeniach). Można skorzystać z [csrfshark](https://csrfshark.github.io/app).

Aby przechwycić zapytania, należy włączyć przeglądarkę Burp'a i znaleźć je w 
Proxy -> HTTP History

Z wygenerowanego kodu, na potrzeby ćwiczeń trzeba wyodrębnić jedynie formularz (bez kodu HTML). Będzie też potrzeba napisać odpowiednie rzeczy z podanych:

```javascript
<script>
	document.forms[0].submit();
</script>
```

```javascript
<script>
	document.location="";
</script>
```

```HTML
<meta name="referrer" content="no-referrer">
```

```javascript
history.pushState("", "", "/?")
```

# Ćwiczenia

#### [Lab 1](https://portswigger.net/web-security/csrf/lab-no-defenses)

#### [Lab 2](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)

#### [Lab 3](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override)

#### [Lab 4](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-depends-on-header-being-present)

#### [Lab 5](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-broken)
