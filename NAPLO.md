# Mérési napló

Minden sor egy ténylegesen elvégzett mozgás ebben a repóban, nem elméleti
példa. A repó publikus, a fiók `Voody2324`.

## Kiinduló állapot

A profilon három kitüntetés volt: **Pull Shark (x2)**, **Pair Extraordinaire**,
**YOLO**. Az összevont pull requestek száma 22 — és ebből **mind a 22 privát
repóban**. Publikus összevont PR a mérés kezdetén nulla volt.

Ez a mondat a legfontosabb lelet az egész naplóban, mert megdönt egy széles
körben ismételt állítást. Lásd a 4. pontot.

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

### Az eredmény: nem jött meg

A hivatalos feltétel teljesült — két elfogadott válasz, válaszolható
kategóriában, publikus repóban —, a jelvény mégsem jelent meg.

| Ellenőrzés | Eredmény |
| --- | --- |
| elfogadott válasz | 2 |
| kategória `isAnswerable` | igen |
| repó publikus | igen |
| jelvény 20 perc után | nincs |
| jelvény 82 perc után | nincs |

Az összehasonlítás miatt fontos, hogy a **Quickdraw ugyanezen a repón egy
percen belül kikerült**. A két mérés között nyolcvankétszeres a különbség,
ami nem magyarázható a feldolgozási sorral.

A legvalószínűbb magyarázat, hogy a **saját kérdésre adott saját válasz nem
számít**. Mindkét válasz szerzője ugyanaz a fiók, aki a kérdést feltette:

```bash
gh api graphql -f query='{ repository(owner:"Voody2324",name:"gh-achievements"){
  discussions(first:10){ nodes{ number isAnswered answer{ author{ login } } } } } }'
```

Ez illeszkedik ahhoz, amit a GitHub 2024-ben tett: a Community Discussions
kivonása is spam elleni lépés volt. Az önválasz kizárása ugyanennek a logikának
a folytatása lenne.

A mérés két lehetséges mechanizmust hagy nyitva, és egyedül nem lehet
szétválasztani őket:

1. A saját kérdésre adott saját válasz nem számít.
2. A saját tulajdonú repóban adott válasz nem számít, akkor sem, ha más kérdez.

Mindkettőből ugyanaz következik a gyakorlatban: **más ember kérdése kell**.

**Amit ez nem bizonyít:** hogy a jelvény soha nem jön meg. Csak azt, hogy
nyolcvankét perc alatt nem jött. A kérdést nem hagytuk nyitva: a repóba került
egy [munkafolyamat](.github/workflows/jelveny-figyelo.yml), ami naponta ránéz
a profilra, és issue-t nyit, ha a jelvény mégis megjelenik. Ha nincs változás,
nem csinál semmit.

**Amit viszont jelent a gyakorlatban:** a Galaxy Brain az egyetlen olyan
kitüntetés az „egyedül megszerezhető" listán, amihez mérhetően **más ember
kérdése** kell. Ezzel átkerül a Starstruck mellé.

## 3. Pull Shark, YOLO, Pair Extraordinaire

Mindhárom megvolt már, de ez a pull request mind a hármat eteti egyszerre:

- **Pull Shark** — összevont PR, a 23. a fiókon. A következő fokozat (x3) 128-nál van.
- **YOLO** — összevonás kódellenőrzés nélkül.
- **Pair Extraordinaire** — `Co-authored-by` sor a commitban. A következő fokozat (x2) 10 társszerzős összevont PR-nál van.

## 4. A privát repók lelete — a közhiedelem cáfolata

A mérés közben kiderült, hogy a repó README-je és a saját Discussions-válaszom
is hibás állítást tartalmazott. Mindkettő azt mondta, hogy a kitüntetésekhez
publikus tevékenység kell. Ez ezen a fiókon mérve nem igaz.

| Repó | Privát | Összevont PR | Társszerzős |
| --- | --- | --- | --- |
| `Voody2324/veylan` | igen | 14 | 14 |
| `Voody2324/zoralva` | igen | 7 | 7 |
| `Voody2324/vhdesk` | igen | 1 | 1 |
| `Voody2324/gh-achievements` | nem | 1 | 1 |

A Pull Shark **x2** fokozata 16 összevont PR-t kér. A mérés kezdetén 22 PR
volt, mind privát repóban, és a fokozat megvolt. Ugyanez a Pair Extraordinaire-re
és a YOLO-ra: mindkettő privát repóban végzett mozgásból származik.

A lekérdezés, amivel ez ellenőrizhető:

```bash
gh api graphql -f query='{ viewer { pullRequests(states:MERGED, first:100){ nodes {
  repository{ nameWithOwner isPrivate } } } } }'
```

A README és a két Discussions-válasz ennek alapján javítva lett. A hibás
állítást nem töröltük, hanem a javítás mellé odaírtuk, mi volt az eredeti.

## 5. Mennyit késik a jelvény

| Kitüntetés | Mozgás ideje (UTC) | Megjelenés |
| --- | --- | --- |
| Quickdraw | 13:10:02 | egy percen belül |
| Galaxy Brain | 13:10:40 | 82 perc után sem |

A késés tehát nem egyforma. Aki rögtön a művelet után nézi a profilt és nem
látja, jó eséllyel nem rontott el semmit.

De van egy határ, ahol a „csak késik" magyarázat elfogy. Ha az egyik jelvény
egy percen belül kint van, a másik pedig nyolcvankét perc után sincs, akkor a
különbség már nem a feldolgozási sorban van, hanem a feltételben.

## Amit nem lehetett elvégezni

**Galaxy Brain** — a feltétel teljesült, a jelvény nem jött meg. A mérés
szerint más ember kérdése kell hozzá, nem elég a saját kérdésre adott saját
válasz. Lásd a 2. pontot.

**Starstruck** — 16 csillag kell egy repóra. Ebből egy saját csillagozással
megvan, a maradék 15 másik emberen múlik. Nem kerülhető meg.

**Public Sponsor** — GitHub Sponsors előfizetés kell hozzá, a legolcsóbb
szinten is bankkártyás terheléssel. Pénzügyi döntés, nem technikai.

**Pull Shark x3** — 128 összevont PR. A jelenlegi 22-ről ide eljutni valódi
munkával megy, nem egy munkamenetben.

## 6. Nyitott kérdés: a Pair Extraordinaire nem lép fokozatot

Ezt mértük, és nem tudjuk megmagyarázni.

A fiók **24 összevont pull requestje mind társszerzős**, és a társszerző egy
létező GitHub-fiók, nem ismeretlen e-mail-cím:

| E-mail | Név | GitHub-fiók |
| --- | --- | --- |
| `jodzsi@gmail.com` | Jozsef Arvai | `Voody2324` |
| `noreply@anthropic.com` | Claude | `claude` |

A Pair Extraordinaire **x2** fokozata 10 társszerzős összevont PR-nál jár,
az **x3** 24-nél. A profil mégis az alap fokozatot mutatja. A profiloldal
HTML-je egyértelmű: a fokozatcímke csak a Pull Sharkhoz tartozik.

```bash
curl -sL "https://github.com/Voody2324?tab=achievements" \
  | grep -n 'data-achievement-slug\|>x[0-9]<'
```

Három lehetséges magyarázat, egyiket sem sikerült bizonyítani:

1. A fokozatszámláló kihagyja a bot- és alkalmazásfiókokat társszerzőként.
2. A fokozat kiértékelése lassabb, mint az alap jelvényé, és napokat késik.
3. A társszerzőnek a PR-on kívül is kell tevékenységnek lennie a repóban.

A küszöbértékeket két egymástól független közösségi lista is ugyanígy adja meg
(`Schweinepriester/github-profile-achievements` és `drknzz/GitHub-Achievements`),
tehát a 24-es ezüstküszöb nem elírás az egyik forrásban. Az anomália marad.

**Egy magyarázat időközben elfogyott.** 2026. szeptember 11-én a GitHub
[bejelentette](https://github.blog/changelog/2026-09-11-profiles-now-show-your-highest-achievement-badge-tier/),
hogy a profil ezentúl a legmagasabb elért fokozatot mutatja a többszintű
kitüntetéseknél. Eddig lehetett azzal érvelni, hogy a fokozat megvan, csak a
megjelenítés nem követi. Ez az érv megszűnt. A mérés tíz nappal a változás
után készült, és a profil továbbra is fokozat nélkül mutatja a jelvényt.

Marad a legvalószínűbb ok: a társszerző egy **alkalmazásfiók** (`claude`), és a
fokozatszámláló vélhetően nem veszi figyelembe. Az alap jelvényhez elég volt,
a fokozathoz nem. Ez továbbra sem bizonyított.

Aki ezt olvassa és tudja a választ, nyisson egy Discussions-kérdést.
