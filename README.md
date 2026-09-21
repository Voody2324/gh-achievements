# GitHub Achievements — magyar terepnapló

Ez a repó egy **mért** leltár arról, hogy a GitHub profilon látható kitüntetések
(Achievements) miből járnak, melyik szerezhető meg saját erőből, és melyikhez
kell rajtad kívül más is.

Nem elmélet: minden állítás mögött egy tényleges, ebben a repóban elvégzett
mozgás áll.

## Mi az az Achievement

A profilod bal oldalán, a követők alatt megjelenő kis jelvénysor. A GitHub
2021 áprilisában vezette be, 2022 júniusában bővítette ki. **Hivatalos,
naprakész lista nincs** — a GitHub kivette a dokumentációból, azóta a közösség
tartja karban.

## A teljes lista

### Megszerezhető, egyedül

| Kitüntetés | Miből jár | Egyedül megy? |
| --- | --- | --- |
| **Pull Shark** | 2 összevont pull request | igen |
| **YOLO** | saját PR összevonása kódellenőrzés nélkül | igen |
| **Quickdraw** | issue vagy PR lezárása a nyitástól számított 5 percen belül | igen |
| **Pair Extraordinaire** | társszerzős (`Co-authored-by`) commit egy összevont PR-ban | igen, ha van kivel |
| **Galaxy Brain** | 2 elfogadott válasz Discussions alatt | saját repóban kipróbálható |

### Megszerezhető, de kell hozzá más

| Kitüntetés | Miből jár | Mi kell hozzá |
| --- | --- | --- |
| **Starstruck** | 16 csillag egy általad létrehozott repón | 16 másik ember |
| **Public Sponsor** | nyílt forrású munka támogatása GitHub Sponsorson | bankkártya |

### Már nem szerezhető meg

| Kitüntetés | Miért |
| --- | --- |
| **Arctic Code Vault Contributor** | a 2020-as archiválási programhoz kötött, lezárult |
| **Mars 2020 Contributor** | az Ingenuity helikopter kódjához kötött, lezárult |
| **Heart On Your Sleeve** | kikapcsolva |
| **Open Sourcerer** | kikapcsolva |
| **Proxima Pioneer / Staffshipper / Staffuser** | belsős, GitHub-alkalmazottaknak |

## Highlights — a másik jelvénysor, amiről kevés szó esik

A profilon az Achievements alatt van egy második sáv, **Highlights** néven.
Ezek nem tevékenységből járnak, hanem tagságból vagy elismerésből. Könnyű
átsiklani felettük, pedig az egyik ingyen megszerezhető.

| Highlight | Miből jár | Pénzbe kerül? |
| --- | --- | --- |
| **Developer Program Member** | regisztráció a GitHub Developer Programba | nem |
| **Pro** | GitHub Pro előfizetés | igen |
| **Security Bug Bounty Hunter** | biztonsági hiba bejelentése a GitHub bug bounty programjában | nem, de nehéz |
| **Security advisory credit** | elfogadott bejelentés a GitHub Advisory Database-be | nem, de nehéz |
| **GitHub Campus Expert** | részvétel a GitHub Campus programban | nem, de egyetemi kötöttség |

A **Developer Program Member** a leggyorsabb ezek közül. A feltétel két dolog:

1. Legyen egy integrációd, ami a GitHub API-t használja, éles vagy fejlesztés
   alatt álló állapotban.
2. Legyen egy e-mail-cím, amin a GitHub felhasználói elérnek támogatásért.

A regisztráció a <https://github.com/developer/register> címen megy, és ingyenes.
Saját döntés, mert a nevedet és egy elérhetőségedet adod meg egy űrlapon.

## A jelvény kinézete a bőrszín-beállítástól függ

Két jelvény, a **Starstruck** és a **Quickdraw**, integető kezet ábrázol, és a
kéz színe az emoji bőrszín-beállításodat követi. A beállítás az
[appearance settings](https://github.com/settings/appearance) alatt van. Nem
befolyásolja, hogy megkapod-e, csak azt, hogyan néz ki.

## Fokozatok

Öt kitüntetésnek van fokozata. A jelvényre kerülő `x2`, `x3`, `x4` címke
bronz, ezüst, arany.

| Kitüntetés | x2 (bronz) | x3 (ezüst) | x4 (arany) |
| --- | --- | --- | --- |
| Pull Shark | 16 PR | 128 PR | 1024 PR |
| Pair Extraordinaire | 10 PR | 24 PR | 48 PR |
| Galaxy Brain | 8 válasz | 16 válasz | 32 válasz |
| Starstruck | 128 csillag | 512 csillag | 4096 csillag |

A fokozat-ugrások nem lineárisak: a Pull Shark x2 még egy hétvége alatt
összejön, az x3-hoz 128 összevont PR kell.

## Két csapda, ami időbe kerül

**A privát repó igenis számít — a közhiedelem itt téved.** A legtöbb útmutató
azt írja, hogy csak a publikus tevékenység számít. Ezen a fiókon mérve ez nem
igaz: **23 összevont pull requestből 22 privát repóban van**, és a Pull Shark
mégis a **x2** fokozaton áll, ami 16 összevont PR-t kér. A privát PR-ok tehát
beleszámoltak.

```bash
gh api graphql -f query='{ viewer { pullRequests(states:MERGED, first:100){ nodes {
  repository{ nameWithOwner isPrivate } } } } }'
```

Amit viszont érdemes bekapcsolni: a profilbeállításokban a privát hozzájárulások
megjelenítése. E nélkül a privát munka nem látszik a profilodon.

**A megjelenés késik, de nem egyformán.** A Quickdraw ezen a repón egy percen
belül kikerült a profilra. A Galaxy Brain ennél lassabb. Ha közvetlenül a
művelet után nézed és nincs ott, ne kezdj hibát keresni.

## Mérési napló

A repó tényleges mozgásai, amikkel a fenti állításokat ellenőriztük:
lásd [NAPLO.md](NAPLO.md).
