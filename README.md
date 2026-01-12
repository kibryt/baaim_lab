# Przygotowanie do laboratorium

Do wykonania laboratorium będziesz potrzebował konta na [PortSwigger](https://portswigger.net) oraz narzędzia [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload).

##  Instrukcja instalacji i użycia Burp Suite Community Edition

1. Pobierz i zainstaluj [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload).

2. Otwórz Burp Suite Community Edition > Temporary Project in Memory > Use Burp Defaults.

3. Kliknij "Open Browser" w sekcji Proxy.

4. Do labów używaj przeglądarki Burpa (chromium) i stworzonego konta na PortSwiggerze.

## Szablony

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

#### [Lab 1 - no defenses](https://portswigger.net/web-security/csrf/lab-no-defenses)
<details>
<summary>Podpowiedź</summary>
	Przechwyć wysłane żądanie zmiany adresu email i na jego podstawie skonstruuj payload
</details>

#### [Lab 2 - bypassing token validation](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)
<details>
<summary>Podpowiedź 1</summary>
	Tak samo jak w poprzednim ćwiczeniu, przechwyć to samo żądanie, znajdź różnice i przeanalizuj zachowanie aplikacji przy zmianie zawartości żądania w Repeater
</details>

<details>
<summary>Podpowiedź 2</summary>
	Skoro aplikacja weryfikuje token csrf przy żądaniu POST, może trzeba zmienić metodę? Burp oferuje taką opcję
</details>

#### [Lab 3 - bypassing samesite restrictions](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override)
<details>
<summary>Podpowiedź 1</summary>
	Przechwyć żądanie /login i sprawdź, jakiego zabezpieczenia SameSite używa aplikacja i czy ma ono jakieś metody obejścia?
</details>

<details>
<summary>Podpowiedź 2</summary>
	Ponownie przechwyć żądanie POST /change-email i spróbuj zmienić metodę żądania 
</details>

<details>
<summary>Podpowiedź 3</summary>
	Skoro aplikacja nie akceptuje żądań GET, to spróbuj nadpisać metodę
</details>

#### [Lab 4 - bypassing referer based defenses](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-depends-on-header-being-present)
<details>
<summary>Podpowiedź 1</summary>
	Przechwyć żądanie ze zmiany adresu email i przeanalizuj zachowanie aplikacji przy zmianie nagłówka Referer
</details>

<details>
<summary>Podpowiedź 2</summary>
	Zauważ, że przy całkowitym usunięciu nagłówka, żądanie jest akceptowane
</details>

#### [Lab 5 - bypassing referer based defenses](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-broken)

W nagłówku payload'u trzeba umieścić `Referrer-Policy: unsafe-url`

<details>
<summary>Podpowiedź 1</summary>
	Tak samo przechwyć żądanie ze zmiany adresu email i przeanalizuj zachowanie aplikacji przy zmianie nagłówka Referer, zauważ, że dodając adres oryginalnej strony jako parametr żądanie jest w naiwny sposób akceptowane
</details>

<details>
<summary>Podpowiedź 2</summary>
	Użyj funkcji history.pushState("", "", "/?"), aby wepchnąć parametr zaakceptowany przez Referer
</details>
