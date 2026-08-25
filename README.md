# popups

Sbírka popupů.

## Plinko Discount Popup

`index.html` — samostatná stránka (HTML + CSS + JS v jednom souboru, bez build stepu
a bez závislostí) s popupem, kde návštěvník zadá e-mail a shodí kuličku po plinko
desce. Podle toho, do kterého slotu spadne, dostane slevový kód (10 / 15 / 20 / 25 %).

### Lokální spuštění

```bash
python3 -m http.server 8000
```

Pak otevřít http://localhost:8000

### Typografie

Headliny a čísla na desce: **Outfit**, UI text: **Inter** — obojí z Google Fonts,
s fallbackem na systémové písmo, takže stránka funguje i bez připojení.

### Zvuk

Všechny efekty jsou syntetizované přes Web Audio API — žádné audio soubory, nic
se nehostuje. `AudioContext` se vytváří až při prvním kliknutí (jinak ho prohlížeč
zablokuje). Kulička hraje pentatonickou stupnici, jak padá po řadách; výherní
fanfára je delší a jasnější pro vyšší slevu.

Přepínač zvuku je vlevo nahoře v popupu, volba se pamatuje v `localStorage`
(`pk-sound`). Stránka respektuje i `prefers-reduced-motion` — animace se zrychlí
a vypnou se poskoky.

### Konfigurace

Nahoře v `<script>`:

| konstanta  | význam |
|------------|--------|
| `PRIZES`   | popisky slotů |
| `CODES`    | slevové kódy pro jednotlivé sloty |
| `WEIGHTS`  | pravděpodobnost jednotlivých slotů zleva doprava (`[40,30,20,10]`) |
| `SLOT_KS`  | dráhy vedoucí do každého slotu — měnit jen při změně `ROWS` |

Výsledek se losuje předem podle `WEIGHTS` a dráha kuličky se k němu dopočítá,
takže animace vždy sedí na skutečnou výhru.

### Napojení na backend

V `index.html` ve funkci `drop()` je zakomentovaný `fetch('/api/subscribe', …)` —
tam patří odeslání leadu do vlastního backendu / ESP. Pozor: sloty se losují
v prohlížeči, takže pro reálné nasazení má o výhře rozhodovat server a kód
vydávat až on.
