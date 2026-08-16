# PZ Pulse Language Pack

**[PZ Pulse](https://steamcommunity.com/sharedfiles/filedetails/?id=3753700423) in all 27
languages Project Zomboid speaks.** One Workshop subscription; your in-game language is the one
the dashboard uses.

**It is machine-generated, and this repo is where you tell us what it got wrong.**

## Found a bad string? That's what this repo is for

**One wrong word is a perfectly good bug report.** You don't need to speak developer, finish a
language, or know anything about modding.

**[Open an issue](https://github.com/PZ-Pulse/PZ_Pulse_Language_Pack/issues/new)** and say:

- the **language**,
- the **label you saw** - a screenshot is easiest,
- **what it should say instead**.

That's it. It goes into the next update and reaches everyone playing in that language.

**Prefer to fix it directly?** The files are right here:
[`42/media/lua/shared/Translate/<CODE>/UI.json`](42/media/lua/shared/Translate). A PR against your
language is very welcome - just be aware these files are **generated**, so we hand-apply your fix
into the source rather than merging the diff straight in. Nothing is lost; it just means an issue
is no less useful than a PR here.

Corrections are credited in this repo's commit history - nothing to maintain, and it doesn't
disappear.

## Where the words come from

**About a third of the pack isn't generated at all.** Where Project Zomboid already has its own
word for *Hunger*, *Fracture*, *Endurance* or *Traits*, the pack uses **the game's word** rather
than inventing a second one - those are the developers' own translations, already on screen in the
character window this dashboard mirrors. Two words for one thing, three inches apart, is worse
than either word alone.

The rest is machine-generated and has been read only for obvious breakage. It is meant as a floor
that beats English, not as a finished translation. That's the honest description, and it's why
this repo exists.

## Want to translate a language properly?

**Do - I'm hoping this is good enough for now, and that better ones take over.** You may use this
as a template. One thing to know first: two mods translating the same language into the same table
means one silently wins, and *which* one depends on mod load order rather than on which is better.
Players pick one or the other rather than running both.

[`english-example/`](english-example) is **the English**, packaged as a complete, ready-to-publish
mod. Worth knowing why it's here rather than being a convenience: it is the **only English file in
this repo**, and it's what you translate *from*. The pack itself ships the 27 translations and
deliberately never ships English - an English file alongside PZ Pulse's own would collide with it -
and `reference/STREW` has every value replaced already. So if you want to see what a string is
supposed to say, this is the copy that tells you.

Rename its `Translate/XX` folder to your language code and it becomes a working mod; leave it and
it does nothing, because `XX` isn't a code the game recognizes.
[`english-example/README.txt`](english-example/README.txt) is its short guide, and
[`TRANSLATING.md`](TRANSLATING.md) is the full one - the language codes and their traps (`AR` is
Español (Argentina), not Arabic; `CH` is Traditional and `CN` Simplified), the `%` rule, and how
to test your work.

[`reference/STREW/UI.json`](reference/STREW/UI.json) is the base game's own joke locale, where
every word is "Strewberrie" - a finished file to compare against, and a way to watch the whole
pipeline work before writing a word.

## The one rule that will bite you

**No `%` character, in any value, ever.** Since build 42.20.1 a literal `%` makes Project Zomboid
**delete the whole string**, leaving a blank label - and the error log blames an unrelated mod, so
it's nearly untraceable. Write the word out ("percent", "por ciento", "Prozent") or rephrase. This
is a Project Zomboid bug that hits every mod, not a PZ Pulse one.

`{1}` and `{2}` are values the game fills in. Keep them, and put them wherever your language wants
them - that's the point of them being placeholders.

## Licence

[0BSD](LICENSE) - no attribution required. Your corrections are your own work and stay yours.

**Not the PZ Pulse name or the EKG logo though. Those I'm keeping** - which is why `poster.png`
and `preview.png` here are plain placeholders rather than the real card art. If you publish a pack
of your own, it wants its own image anyway. Can be EKG themed or EKG in a corner as long
as it's not confusing.