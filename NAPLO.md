# Mérési napló

Minden sor egy ténylegesen elvégzett mozgás ebben a repóban, nem elméleti
példa. A repó publikus, a fiók `Voody2324`.

## Kiinduló állapot

A profilon három kitüntetés volt: **Pull Shark (x2)**, **Pair Extraordinaire**,
**YOLO**. Az összevont pull requestek száma 22.

A gépi ellenőrzés parancsa:

```bash
curl -sL "https://github.com/Voody2324?tab=achievements" | grep -o 'data-achievement-slug="[a-z-]*"'
```

## 1. Quickdraw

**Feltétel:** issue vagy PR lezárása a nyitástól számított 5 percen belül.

Az [1-es issue](https://github.com/Voody2324/gh-achievements/issues/1) nyitása
és lezárása között **2 másodperc** telt el:

| Esemény | Időbélyeg (UTC) |
| --- | --- |
| nyitás | 13:10:00 |
| zárás | 13:10:02 |

A lezárás módja (`completed` vagy `not planned`) nem számít, csak az eltelt idő.

## 2. Galaxy Brain

**Feltétel:** 2 elfogadott válasz. Nem elég egy.

Ehhez előbb be kellett kapcsolni a Discussions funkciót, mert alapból ki van
kapcsolva:

```bash
gh repo edit --enable-discussions
```

Majd a **Q&A** kategóriába — ez az egyetlen, aminél `isAnswerable: true` —
két kérdés került, mindkettőre válasszal, a válasz elfogadva:

- [#2 — Naponta vonok össze PR-t, mégsem kapom meg a Pull Sharkot](https://github.com/Voody2324/gh-achievements/discussions/2)
- [#3 — Mennyi idő alatt jelenik meg egy frissen megszerzett jelvény](https://github.com/Voody2324/gh-achievements/discussions/3)

A válasz elfogadása a felületen egy pipa, gépből a `markDiscussionCommentAsAnswer`
GraphQL-mutáció.

**Fontos korlát:** a GitHub 2024 februárjában kivonta a saját Community
Discussions felületét a kitüntetés alól, spam elleni védelemként. Saját repó
Discussions rovata nem esett ebbe.

## 3. Pull Shark, YOLO, Pair Extraordinaire

Mindhárom megvolt már, de ez a pull request mind a hármat eteti egyszerre:

- **Pull Shark** — összevont PR, a 23. a fiókon. A következő fokozat (x3) 128-nál van.
- **YOLO** — összevonás kódellenőrzés nélkül.
- **Pair Extraordinaire** — `Co-authored-by` sor a commitban. A következő fokozat (x2) 10 társszerzős összevont PR-nál van.

## Amit nem lehetett elvégezni

**Starstruck** — 16 csillag kell egy repóra. Ebből egy saját csillagozással
megvan, a maradék 15 másik emberen múlik. Nem kerülhető meg.

**Public Sponsor** — GitHub Sponsors előfizetés kell hozzá, a legolcsóbb
szinten is bankkártyás terheléssel. Pénzügyi döntés, nem technikai.

**Pull Shark x3** — 128 összevont PR. A jelenlegi 22-ről ide eljutni valódi
munkával megy, nem egy munkamenetben.
