PZ PULSE - ENGLISH EXAMPLE
==========================

This folder is a complete, ready-to-publish Project Zomboid mod that contains nothing but
text. Fill in the text and it is a PZ Pulse translation. There is no code to write, no build
step, and nothing in PZ Pulse itself has to change to accept your work.

It is also the only copy of the ENGLISH in the PZ Pulse Language Pack repository, and that is
deliberate. The pack ships all 27 translations but never ships English, because an English file
sitting beside PZ Pulse's own would collide with it. So this is the file you read to find out
what a string is supposed to say - useful even if you never publish anything.

Everything you need is here. If you only read one thing, read THE FOUR STEPS.


THE FOUR STEPS
--------------

1. Rename the folder

       42/media/lua/shared/Translate/XX/

   from XX to your language's code, from the list at the bottom of this file. Uppercase,
   exactly as written there. This one rename is what turns the pack on: XX is not a code
   the game recognizes, so as shipped this pack does nothing at all.

2. Open UI.json in that folder and translate THE RIGHT-HAND SIDE ONLY.

       "UI_PZ_Pulse_Panel_skills": "Skills"     <- before
       "UI_PZ_Pulse_Panel_skills": "Competences" <- after

   Never change the part left of the colon. That is how the game finds the string. Save the
   file as UTF-8.

3. Fill in the placeholders in 42/mod.info and workshop.txt. Both contain the word LANGUAGE
   and one contains YOURNAME; replace those, and change the mod id at the same time:

       id=PZ_Pulse_Lang_XX   ->   id=PZ_Pulse_Lang_FR

   Leave "id=" in workshop.txt empty. Steam fills that in the first time you upload.

4. Rename this whole folder to match that id, then test and publish (see below).


THE THREE RULES
---------------

1. NEVER CHANGE A KEY. Only the text on the right. If a key is missing from your file that
   one string simply stays English, so a partial translation is safe to ship at any point.
   You do not have to finish before you publish.

2. NO PERCENT SIGN. ANYWHERE. Since build 42.20.1, a literal "%" in a translated string
   makes Project Zomboid delete the whole string, leaving a blank label - and the error log
   blames an unrelated mod, so it is nearly impossible to trace. Write the word out
   ("percent", "pour cent", "prozent") or rephrase. This is a Project Zomboid bug that
   affects every mod, not a PZ Pulse one.

   Related: {1} and {2} are values the game fills in. Keep them, and put them wherever your
   language wants them - that is the whole point of them being placeholders.

       "{1} holes"        ->  "{1} trous"
       "Repaired x{1}"    ->  "Repare x{1}"

   Drop a {1} and that number vanishes from the display. (Project Zomboid's own files use
   %1 for this. PZ Pulse uses {1} because a % is unsafe, see above.)

3. KEEP IT SHORT. PZ Pulse is a column layout with fixed-width panels. Many of these strings
   are panel titles sitting in a title bar next to three buttons, or row labels in a narrow
   left column. A translation much longer than the English will be cramped or clipped. Prefer
   a short synonym over an accurate-but-long phrase, and if a title genuinely cannot fit, say
   so - that is worth knowing about and worth fixing properly.

Accented characters, Cyrillic, Greek and CJK are all fine. The dashboard renders in a browser
using the reader's own system fonts, not a fixed bitmap font.

Right-to-left languages: Project Zomboid ships no right-to-left locale today (AR is Español
(Argentina), not Arabic - see the code list at the bottom), so this can only come up via a
language the game itself adds later. The characters would render, but the layout has never
been tested RTL and does not mirror itself. If that is you, please say so first.


WHAT YOU DO NOT HAVE TO TRANSLATE
---------------------------------

Anything the game itself supplies is ALREADY in your language and is not in this file: skill
and perk names, body parts, wound descriptions, item and weapon names, moodle names. PZ Pulse
asks Project Zomboid for those. That is why this file is a couple of hundred short strings
instead of thousands.

Deliberately left English by PZ Pulse, so do not be surprised by them:

  - The Shift+Z support dump. A player pastes it into a bug report for the mod author to read,
    who may not speak the reporter's language.
  - The name "PZ Pulse" on the options screen, and the menu route "Options -> Mods". Support
    instructions have to match what is actually on a stuck player's screen in every language.


TESTING IT
----------

1. Put this folder in your Project Zomboid mods folder:

       Windows:  C:\Users\<you>\Zomboid\mods\
       Linux:    ~/Zomboid/mods/

2. Start the game, enable both PZ Pulse and your pack in the Mods screen.
3. Options -> Language -> your language.
4. RESTART PROJECT ZOMBOID. Translations load only at startup, so switching language
   mid-session changes nothing.
5. LOAD A SAVE. Not the main menu - see the warning below.
6. Open the dashboard.

You should see your text in the panel title bars and throughout the panels, in the settings
drawer, in each panel's gear menu, and in Options -> Mods -> PZ Pulse.

  !! THE DASHBOARD STAYS ENGLISH UNTIL YOU LOAD A SAVE, AND THAT LOOKS EXACTLY LIKE A BROKEN
     FILE. PZ Pulse hands your strings to the web page by writing them out when a save loads.
     At the main menu that has not happened yet, so the page shows the English it ships with.
     Sitting at the menu with the dashboard open and seeing English proves nothing.

     The options screen is the exception, and it is a useful early check: Options -> Mods ->
     PZ Pulse is resolved inside the game rather than in the browser, so it translates from
     the main menu with no save loaded. If that screen is in your language and the dashboard
     is not, load a save. Your file is fine.

If a string is still English, the usual causes in order:

  - you have not loaded a save yet (above). By far the most common, and the least obvious;
  - the folder name is not an exact language code from the list below;
  - the folder is in the wrong place (it must be under lua/shared/Translate/, not media/Translate/);
  - a key was altered;
  - the JSON has a syntax error. A trailing comma is the classic one. Paste the file into any
    online JSON validator.

A quick way to see the machinery working before you have translated anything: PZ Pulse ships a
complete translation into STREW, the base game's own joke language where every word is
"Strewberrie". Set Options -> Language -> Strewberrie and restart, and the dashboard turns into
Strewberrie along with the rest of the game.


KEEP 42/media/ PURE - IT BUYS YOU MULTIPLAYER
---------------------------------------------

Project Zomboid recognizes "translation mod" as a real status, and this pack has it. The rule
is simple: inside 42/, anything under media/ must be under media/lua/shared/Translate/ and must
be a .json or .txt file. Files outside media/ (mod.info, poster.png) do not count.

So do not put a readme, a texture, a screenshot or anything else under 42/media/. Keep extras at
the top level of the folder, next to this file.

Why it matters: a translation mod is the ONE kind of mod a multiplayer client may load on its
own. Normally a server dictates the entire client mod list, and a mod the server does not list
simply does not load, no matter what the player enabled. Translation mods are exempt, so your
pack works for a player on someone else's server even if that server has never heard of it.

Break the rule and nothing warns you. The pack keeps working perfectly in singleplayer and
silently stops loading in multiplayer.


PUBLISHING IT
-------------

A language pack is an ordinary mod, so the normal route works: launch Project Zomboid, choose
Workshop, and your item appears ready to upload. The poster.png and preview.png here are neutral
placeholders - put your own image in before you publish.

You do not need permission, a code change, or any cooperation from PZ Pulse for this to work.
The game merges every installed mod's translations into one table, filling English first and the
player's chosen language second, so your entries win regardless of which mod loaded first.

One thing to know: the PZ Pulse Language Pack bundles all 27 languages, so a player who has both
it and your pack installed gets a collision - one silently wins, and which one depends on mod
load order rather than on which is better. Players pick one or the other rather than running both.

If you would rather send corrections to that pack instead of publishing your own, they are
credited in its commit history.


LANGUAGE CODES
--------------

The folder name must be exactly one of these, uppercase. Any other name is silently ignored.

The game's Language menu shows only the NAME, never the code, so this is the mapping between
the two. The right-hand column is the exact text on that menu.

LANGUAGE-CODES:BEGIN

  AR      Español (Argentina)
  CA      Català
  CH      Chinese (Traditional)
  CN      Chinese (Simplified)
  CS      Čeština
  DA      Dansk
  DE      Deutsch
  EN      English
  ES      Español (España)
  ES_CL   Español (Chile)
  ES_MX   Español (México)
  FI      Suomi
  FR      Français
  HU      Magyar
  ID      Bahasa Indonesia
  IT      Italiano
  JP      Japanese
  KO      Korean
  NL      Nederlands
  NO      Norsk
  PL      Polski
  PT      Português (Portugal)
  PTBR    Português Brasileiro
  RO      Română
  RU      Russian
  STREW   Strewberrie
  TH      Thai
  TR      Türkçe
  UA      Ukrainian

LANGUAGE-CODES:END

Four of these are worth calling out, because guessing wrong costs you the whole pack:

  - AR is ARGENTINA, not Arabic. Project Zomboid ships no Arabic locale at all. Spanish has
    four separate regional tables - ES (Spain), ES_MX, ES_CL and AR - and the game never
    falls back between them, so a translation in ES does nothing for a player set to
    Español (México). To cover several, copy the same file into each folder.

  - CH is TRADITIONAL Chinese and CN is SIMPLIFIED, the opposite of what the country codes
    suggest.

  - PTBR has no underscore, while ES_MX and ES_CL do. Copy the code exactly as written.

  - JP, not JA, for Japanese.

STREW is the developers' own joke locale, not a real language, and PZ Pulse already ships a
complete one. You do not need to touch it.


Thank you.
