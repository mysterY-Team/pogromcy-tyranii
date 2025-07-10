# Pogromcy tyranii

Githubowe API stanowiące "blacklistę" do Discorda.

## Użycie

Użycie jest darmowe, jak i zarazem proste. Metodą `GET` pobiera się z linku ze schematu:

```
https://raw.githubusercontent.com/mysterY-Team/pogromcy-tyranii/main/<guilds | bots | users>/<id>.json
```

-   `guilds` oznaczają serwery
-   `bots` oznaczają boty
-   `users` oznaczają użytkowników

...a wszystkie kategorie można pobrać z tąd:

```
https://raw.githubusercontent.com/mysterY-Team/pogromcy-tyranii/main/categories.json
```

### Odczytywanie oraz kategorie

Tak wygląda zwrócony obliekt przy `bots` oraz `guilds`:

```json
{
    "api_version": "0.0", //ciąg znaków
    "report_ids": ["dc0t", "gh#0", "s.0", "odc#0"], //tablica ciągów znaków; dc- oznacza zgłoszenie w Discordzie (odc- w czasach przed rajdem), gh- oznacza zgłoszenie w GitHubie. s- oznacza specjalne zgłoszenie, które (w rzadkich wypadkach) nie mogło być utworzone, lub wymagało natychmiastowego działania.
    "reasons": {
        "main": "Powód główny", //ciąg znaków
        "others": ["Powód poboczny nr. 1", "Powód poboczny nr. 2"] // tablica ciągów znaków
    },
    "proofs": [""], //tablica ciągów znaków; $report:id oznacza sprawozdanie jednego z przypisanych id zgłoszeń, brak dolara na początku oznacza czysty tekst.
    "levels": {
        //obiekt zawierający (niecałe) kategorie, liczba od 1 do 7
        "_sum_": //liczba; suma
    }
}
```

Przy `users` jest nieco inaczej - zwraca górne wraz z `"mult": false`, gdy dotyczy to głównego konta.
Natomiast zwróci to, gdy jest multikontem lub "wtykiem":

```json
{
    "api_version": "0.0", //ciąg znaków
    "mult": true, //wartość logiczna
    "reference": "" //ciąg znaków; Snowflake (ID)
}
```

> [!NOTE]
> **Wszystkie** zgłoszenia posiadające ID w stylu `odc#0`, pozostaną na wersji API 1.2 **aż do wypuszczenia 2.0** - to dlatego, że wszystkie dowody, które były, zniknęły wraz ze starymi kanałami Discord...

Na stan 6.01.2025 mamy 8 kategorii:

-   `scam` (scam/oszukiwanie)
-   `harassment_or_bullying` (prześladowanie lub znęcanie się)
-   `sexual_behaviour` (zachowanie seksualne \[m.in. gwałt, pedofilstwo])
-   `illegal_content` (nielegalny kontent)
-   `violent_content` (treści przemocowe)
-   `acting_against_smth` (działania na szkodę kogoś/czegoś)
-   `hate_speech` (mowa nienawiści)
-   `exposing_private_identifying_info` (upublicznianie cudzych danych)
-   `theft` (kradzież \[tj. serwera, prac - każdy typ posiadający prawa autorskie])
-   `misinformation` (dezinformacja, szerzenie informacji wprowadzających w błąd)
-   `evasion_of_restrictions` (omijanie ograniczeń [np. poprzez multikonta czy VPN/VPS])

Główny poziom zalecamy, aby wyliczyć za pomocą "średniej" sumę liczb z `levels` (dajemy także do poziomów `_sum_`, aby ułatwić niektórym pobieranie) przez ilość owych kategorii.

## Nadawanie zgłoszeń

Zgłoszenia można pisać albo z GitHuba przez "Issues", lub na [serwerze Discord](https://discord.gg/jrmMNFtkZU) w oddzielnej do tego kategorii (możliwe **tylko** po odebranej roli).
