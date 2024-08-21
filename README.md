# Pogromcy tyranii

Githubowe API stanowiące "blacklist" do Discorda.

## Użycie

Użycie jest darmowe, jak i zarazem proste. Metodą `GET` pobiera się z linku ze schematu:

```
https://raw.githubusercontent.com/mysterY-Team/pogromcy-tyranii/main/<guilds | bots | users>/<id>.json
```

-   `guilds` oznaczają serwery
-   `bots` oznaczają boty
-   `users` oznaczają użytkowników

### Odczytywanie

Kod JSON powinien zwrócić coś takiego (oznaczone co i jak):

```json
{
    "report_ids": ["dc0t", "gh#0"], // tablica ciągów znaków; dc- oznacza zgłoszenie w Discordzie, gh- oznacza zgłoszenie w GitHubie
    "reasons": {
        "main": "Powód głowny", // ciąg znaków
        "others": ["Powód poboczny nr. 1", "Powód poboczny nr. 2"] // tablica ciągów znaków
    },
    "main_level": 1, // liczba od 1 do 7
    "level_by_category": {
        /*
        Liczby od 1 do 7
        Tutaj kategorie to: "sexual_content", "hate_speech", "scam", "harassment_or_bullying", "exposing_private_identifying_info", "illegal_content" oraz "acting_against_smth"
        np:
        {
            "scam": 5,
            "harassment_or_bullying": 2
        }
        */
    }
}
```

Powinno się stosować poziomy w stylu `max(data.main_level, data.level_by_category[typ1] ?? 0, data.level_by_category[typ2] ?? 0, ...)` w zależności od potrzebnych dodatkowych typów do sprawdzenia (Znaki zapytania skorzystane z JavaScript; [znaczenie](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing))

## Nadawanie zgłoszeń

Zgłoszenia można pisać albo z GitHuba przez "Issues", lub na [serwerze Discord](https://discord.gg/jrmMNFtkZU) w oddzielnej do tego kategorii (możliwe **tylko** po odebranej roli)
