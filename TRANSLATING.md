# Translating PZ Pulse

PZ Pulse can speak any language Project Zomboid does, and **translating it takes one JSON file.**
No code, no build step, and nothing in the mod has to change to accept your work.

If you want to translate it, you are in the right place and this is the whole job.

---

## The short version

**Every language already has a baseline translation** - the
[PZ Pulse Language Pack](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack) covers all 27, and
it is machine-generated, so most of what's useful now is **fixing what's wrong** rather than
starting from blank.

1. Look at your language's file in the pack:
   [`42/media/lua/shared/Translate/<CODE>/UI.json`](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/tree/main/42/media/lua/shared/Translate),
   with your code from [Language codes](#language-codes).
2. Fix **the values on the right**. Never touch the keys on the left.
3. Send it in - one word or the whole file, both are welcome. See
   [How to contribute](#how-to-contribute--and-what-changed).

Prefer to start from the English rather than from generated text? The
[**English example**](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/tree/main/english-example)
is the same file with the English still in it, packaged as a ready-to-publish mod; its `README.txt`
is this page's short form and travels with the folder.

**It is also the only English in that repo, which is why it's worth knowing about even if you never
publish anything.** The pack ships the 27 translations and never ships English - an English file
sitting beside PZ Pulse's own would collide with it - so when you need to check what a string is
meant to say, that folder is where the answer is.

If you'd rather assemble the mod folder yourself, the file inside that example is
[`english-example/42/media/lua/shared/Translate/XX/UI.json`](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/blob/main/english-example/42/media/lua/shared/Translate/XX/UI.json)
- the English, every string in one place, page and options screen alike - and the packaging is
written out under [Packaging it as a Workshop mod](#packaging-it-as-a-workshop-mod).

```json
{
    "UI_PZ_Pulse_Panel_skills": "Skills",          ←  EN
    "UI_PZ_Pulse_Panel_health": "Health"
}
```
```json
{
    "UI_PZ_Pulse_Panel_skills": "Compétences",     ←  your FR
    "UI_PZ_Pulse_Panel_health": "Santé"
}
```

That's it. The game resolves the strings and hands them to the dashboard page automatically.

### See it working first

PZ Pulse ships one complete translation you can try right now: **STREW**, the base game's own
joke language where every word is "Strewberrie". Set **Options > Language > Strewberrie** and
restart, and the dashboard's panel titles turn into Strewberrie along with the rest of the game.

That's the whole pipeline running end to end, and
[`reference/STREW/UI.json`](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/blob/main/reference/STREW/UI.json)
ships beside the pack so you can see the shape of a finished file.

**Don't start from STREW, though** - it's a demonstration, not a template. Every value in it is
already replaced, so there's nothing left to read and no way to see how far you've got. Start
from the [English example](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/tree/main/english-example),
which is the same file with the English still in it.

---

## How to contribute - and what changed

**Read this bit even if you've done this before, because the answer changed.**

Every one of the game's 27 non-English languages is now covered by the
**[PZ Pulse Language Pack](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack)** - a single
Workshop mod that gives all of them a baseline translation. It is machine-generated and openly
says so. It exists because waiting for 27 volunteers wasn't working, not because the job is
considered done.

**So the useful thing to send is a correction, and it does not have to be a big one.** One wrong
word, in one language, is a perfectly good contribution. The pack ships to everyone playing in
that language, so a single fix lands everywhere at once.

|  | **Correct the pack** | **Publish your own pack** |
|---|---|---|
| What you do | Open an issue or PR on the pack repo - one word, or a whole file | Publish a Workshop mod containing only your JSON |
| Size that makes sense | Anything from one string upward | A complete language |
| Reaches | Everyone already subscribed | People who find and subscribe to yours |
| Who updates it when PZ Pulse adds strings | We do, and the build refuses to ship a language that's behind | You, and nothing will tell you |
| Your name on it | The pack repo's commit history | It's your Workshop item |

### If you'd rather publish your own pack

**Go ahead.** You don't need permission, and `english-example/` is there to be used as a template. A
hand-made translation should beat a generated one; the pack is a floor, not a claim.

One thing to know rather than a reason not to: two mods translating the same language into the
same table means one silently wins, and *which* one depends on mod load order rather than on which
is better. So players pick one or the other rather than running both.

---

## The three rules

**1. Never change a key.** The part left of the colon (`UI_PZ_Pulse_Panel_skills`) is how the game
finds the string. Translate only the text on the right. If a key is missing from your file, that
one string just stays English - a partial translation is fine and safe to ship.

**2. No `%` character. Anywhere.** Since build 42.20.1, a literal `%` in a translated string makes
the game **delete the entire string**, leaving a blank label - and the error log blames a completely
unrelated mod, so it is nearly impossible to trace. Write out the word ("percent", "pour cent",
"процент") or rephrase. This is a Project Zomboid bug, not a PZ Pulse one, and it affects every mod.

**2b. `{1}`, `{2}` are values that get filled in.** Keep them, and move them wherever your language
needs them - that's the whole point of them being placeholders rather than glued-on text.

```json
"UI_PZ_Pulse_Clo_Holes": "{1} holes"        >  "{1} trous"
"UI_PZ_Pulse_Wpn_Repaired": "Repaired x{1}" >  "Réparé x{1}"
```

Dropping a `{1}` loses that number from the display. (PZ's own files use `%1` for this; PZ Pulse
uses `{1}` because a `%` is unsafe - see rule 2.)

**3. Keep it short.** PZ Pulse is a column layout with fixed-width panels. Many of these strings
are **panel titles** in a title bar next to three buttons, or row labels in a narrow left column,
so a translation much longer than the English will be cramped or clipped. If your language needs more room than the English
allows, prefer a shorter synonym over an accurate-but-long phrase - and tell us, because a title
that can't fit is worth knowing about.

Everything else is up to you. Accented characters, Cyrillic, Greek and CJK are all fine on the
dashboard - it renders in a browser, using the reader's system fonts rather than a fixed bitmap
font.

> **Right-to-left languages:** Project Zomboid ships no RTL locale today (`AR` is Español
> (Argentina), not Arabic - see [Language codes](#language-codes)), so this can only come up via a
> language the game itself adds later. The characters would render, but the dashboard's layout has
> never been tested RTL and does not mirror itself. If that's you, please say so - it's worth
> fixing properly rather than guessing.

---

## Where the file goes

```
PZ_Pulse/
  42/
    media/
      lua/
        shared/
          Translate/
            EN/UI.json      ← the source you're translating
            FR/UI.json      ← yours
```

Note the path: **`lua/shared/Translate/`**. This mirrors the base game's own layout. A folder at
`media/Translate/` is silently never read - no error, the strings just stay English.

### Language codes

The folder name must be **exactly** one of the codes below, uppercase. A folder with any other
name is ignored - silently, with no error.

The game's own Language menu shows only the **name**, never the code, so this is the mapping
between the two. The right-hand column is the exact text on that menu.

<!-- LANGUAGE-CODES:BEGIN - generated from the installed game by `make_locale.py --codes`; edits here are overwritten -->

| Code | The language menu calls it |
|---|---|
| `AR` | Español (Argentina) |
| `CA` | Català |
| `CH` | Chinese (Traditional) |
| `CN` | Chinese (Simplified) |
| `CS` | Čeština |
| `DA` | Dansk |
| `DE` | Deutsch |
| `EN` | English |
| `ES` | Español (España) |
| `ES_CL` | Español (Chile) |
| `ES_MX` | Español (México) |
| `FI` | Suomi |
| `FR` | Français |
| `HU` | Magyar |
| `ID` | Bahasa Indonesia |
| `IT` | Italiano |
| `JP` | Japanese |
| `KO` | Korean |
| `NL` | Nederlands |
| `NO` | Norsk |
| `PL` | Polski |
| `PT` | Português (Portugal) |
| `PTBR` | Português Brasileiro |
| `RO` | Română |
| `RU` | Russian |
| `STREW` | Strewberrie |
| `TH` | Thai |
| `TR` | Türkçe |
| `UA` | Ukrainian |

<!-- LANGUAGE-CODES:END -->

Four of those are worth calling out, because guessing wrong costs you the whole pack:

- **`AR` is Argentina, not Arabic.** Project Zomboid ships **no Arabic locale at all**. Spanish has
  four separate regional tables - `ES` (Spain), `ES_MX`, `ES_CL` and `AR` - and PZ never falls back
  between them, so a translation in `ES` does nothing for a player set to Español (México). If you
  want to cover several, copy the same file into each folder.
- **`CH` is Traditional Chinese and `CN` is Simplified**, which is the opposite of what the country
  codes suggest.
- **`PTBR` has no underscore** while `ES_MX` and `ES_CL` do. Copy the code exactly as written above.
- **`JP`, not `JA`**, for Japanese.

`STREW` is the developers' own joke locale, not a real language, and PZ Pulse already ships a
complete one (see [above](#see-it-working-first)). You don't need to touch it.

---

## Packaging it as a Workshop mod

A language pack is an ordinary Project Zomboid mod that happens to contain only text.
**The [English example](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/tree/main/english-example)
is already exactly this**, with placeholders to fill in - so this section is here to explain it, not
because you have to build it by hand.

```
PZ_Pulse_French/
  workshop.txt
  preview.png
  42/
    mod.info
    poster.png
    media/lua/shared/Translate/FR/UI.json
```

`42/mod.info`:

```ini
name=PZ Pulse - French
id=PZ_Pulse_French
description=French translation for PZ Pulse.
poster=poster.png
icon=poster.png
author=yourname
category=features
require=PZ_Pulse
modversion=1.0.0
versionMin=42.0.0
```

Three notes:

- **The `42/` folder is required.** A B42 mod without one is silently skipped from the Mods menu
  entirely - no error, it simply never appears.
- **`require=PZ_Pulse` is a courtesy, not a mechanism.** Your JSON is inert without PZ Pulse
  installed, so nothing breaks either way; the line just makes the dependency visible to players.
- `category` is a free-text label for the mod menu, not a fixed list - `features` is what
  everything here uses. The Steam Workshop's own tags are set separately, in `workshop.txt`.

---

## Testing your translation

1. Put your `UI.json` in place (either in PZ Pulse's folder, or in your own pack with the pack
   enabled).
2. In game: **Options > Language >** your language.
3. **Restart Project Zomboid.** Translations load only at startup, so an in-session language
   switch changes nothing.
4. **Load a save.** Not the main menu - see below.
5. Open the dashboard.

You should see your text in the **panel title bars and throughout the panels**, in the settings
drawer and each panel's gear menu, and in **Options > Mods > PZ Pulse**.

> **The dashboard stays English until you load a save, and this looks exactly like a broken
> file.** PZ Pulse hands your strings to the page by writing them out when a save loads - at the
> main menu that has not happened yet, so the page renders the English it ships with. Sitting at
> the menu with the dashboard open and seeing English proves nothing at all.
>
> The options screen is the exception and it is a useful early check: **Options > Mods > PZ Pulse**
> is resolved inside the game rather than in the browser, so it translates from the main menu, with
> no save loaded. If that screen is in your language and the dashboard is not, **load a save** -
> your file is fine.

If a string is still English, the usual causes in order:

1. **You haven't loaded a save yet** (above) - by far the most common, and the least obvious.
2. The folder name isn't an exact [language code](#language-codes).
3. The file is at `media/Translate/` instead of `media/lua/shared/Translate/`.
4. A key was altered.
5. The JSON has a syntax error - a trailing comma is the classic one; paste it into any JSON
   validator.

---

## Extension panels are translated separately

Other mods can add their own panels to the PZ Pulse dashboard. **Those panels' text belongs to
those mods**, not to this one - each ships its own `Translate/EN/UI.json` with its own keys, and
you translate it the same way, by putting a file in that mod's language folder or publishing a pack
for it.

If a panel's title and labels stay English while PZ Pulse's own go French, that panel is a
third-party extension and its author is who to talk to. You can tell which panels are extensions:
press **Shift+A** on the dashboard and it lists each one with the mod it came from.

Extension authors: the API side of this is documented in
[`API.md`](https://github.com/PZ-Pulse/API/blob/main/API.md) §4.

---

## What is deliberately not translated

- **The Shift+Z support dump.** It's a diagnostic report a player copies into a bug report for the
  mod author to read, so it stays English on purpose - a translated dump is harder for the person
  receiving it, who may not speak the reporter's language.
- **The name "PZ Pulse"** in the options screen. Support instructions tell stuck players to go to
  `Options > Mods > PZ Pulse`, and that has to match what's on their screen in every language.
- **Data that comes from the game itself** - skill names, body parts, wound descriptions, item and
  weapon names, moodle names. PZ Pulse asks Project Zomboid for those, so they are **already in
  your language** with no work from you. That's why this file is a couple of hundred short
  strings instead of thousands.

---

## Credit

Corrections are credited in the pack repo's commit history - nothing to maintain, and it doesn't
disappear.

Thank you.
