# popups

Sbírka popupů.

## Plinko Discount Popup

`index.html` — samostatná stránka (HTML + CSS + JS v jednom souboru, bez závislostí)
s popupem, kde návštěvník zadá e-mail a shodí kuličku po plinko desce. Podle toho,
do kterého slotu spadne, dostane slevový kód (10 / 15 / 20 / 25 %).

### Lokální spuštění

```bash
python3 -m http.server 8000
```

Pak otevřít http://localhost:8000

### Napojení na backend

V `index.html` ve funkci `drop()` je zakomentovaný `fetch('/api/subscribe', …)` —
tam patří odeslání leadu do vlastního backendu / ESP.
