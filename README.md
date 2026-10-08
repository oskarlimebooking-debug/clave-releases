# Clave — macOS izdaje

Podpisane (Developer ID) in notarizirane universal izdaje Clave (Intel + Apple Silicon).
Ta repo je hkrati **feed za samodejne posodobitve** — nameščen Clave ga preverja sam.

**Prenos:** [Latest release](https://github.com/oskarlimebooking-debug/clave-releases/releases/latest) → `clave-<verzija>.dmg`

## Prva namestitev (samo enkrat)

1. Prenesi `clave-<verzija>.dmg` iz [zadnje izdaje](https://github.com/oskarlimebooking-debug/clave-releases/releases/latest).
2. Zapri Clave, če teče (⌘Q).
3. Odpri DMG in povleci **Clave** v **Applications** (če vpraša, izberi *Replace*).
4. Zaženi Clave iz Applications. Ker je aplikacija notarizirana, se odpre brez opozorila
   »unidentified developer«.

> Starejše verzije (do 1.51.5-fork.18) niso bile podpisane in se ne morejo posodobiti same —
> zato je ta korak potreben samo enkrat. Od 1.51.5-fork.19 naprej gre samo.

Preveri verzijo: **Clave → About Clave** (ali v Terminalu
`defaults read /Applications/Clave.app/Contents/Info.plist CFBundleShortVersionString`).

## Kako delujejo posodobitve

- Clave preveri novo verzijo **5 s po zagonu** in nato **vsakih 30 min**.
- Ko je na voljo, se v stranski vrstici prikaže pasica **»vX · Update«**.
- Klik **Update** → prenos (z napredkom) → Clave se sam zapre, zamenja in ponovno zažene.
- Če pasico zapreš, se posodobitev vseeno namesti ob naslednjem izhodu iz Clave (⌘Q).

## Preverjanje, da auto-update deluje

1. Namesti trenutno zadnjo verzijo (zgoraj) in jo pusti teči.
2. Ko je objavljena novejša izdaja, **ponovno zaženi Clave** (ali počakaj do 30 min).
3. Pričakovano: pasica »v<nova> · Update« → klik → po ponovnem zagonu *About* kaže novo verzijo.

Če se nič ne zgodi, zaženi Clave iz Terminala in spremljaj izpis updaterja:

```sh
/Applications/Clave.app/Contents/MacOS/Clave 2>&1 | grep -i updater
```

`[updater] App is up to date` = feed dosegljiv, novejše verzije ni.
`[updater] Update available: …` = posodobitev najdena.

## Za vzdrževalca

Izdajo naredi `npm run release` v zasebnem repu (bump `-fork.N` → universal build →
podpis + notarizacija → objava sem). Vsaka izdaja mora vsebovati `latest-mac.yml`,
`fork-mac.yml` in `Clave-<v>-universal-mac.zip` — iz njih bere updater.
