<div align="center">

# 🐺🌕 Beast Aware 🌕🦇

### *They see the beast. They hear the change.*

**A SkyrimNet add-on: NPCs notice when you become a werewolf, werebear or Vampire Lord.**

`v1.1` · Skyrim SE 1.5.97 · ESL-flagged · by **That Guy (Coronerra)**

</div>

---

## 🩸 What it does

When you transform, SkyrimNet NPCs **know**. When you shift into or out of beast form, Beast Aware sends a SkyrimNet event, and while you are transformed it keeps the beast in scene context.

### 1. Transformation event (werewolf, werebear, Vampire Lord)
> *&lt;Name&gt; tore free of their clothes as their body swelled and twisted, stripping them off before they could rip, and grew into a massive, hairy werewolf.*

The ending changes by form: "...a massive, shaggy, bear-like werebear" or "...a towering, leathery-winged Vampire Lord, a grey-skinned monster with claws and fangs".

### 2. "Too large for clothing" state, while transformed
A short-lived event (`beastaware_player_form`, 45 s, refreshed every 30 s):
> *&lt;Name&gt; is in werewolf form: a towering, fur-covered beast far too large for any clothing or armor to fit. Being unclothed is natural for this form, and their body is fully exposed. Anyone nearby sees a huge, hairy werewolf and reacts to that (fear, awe, desire, or whatever fits them), and would not scold them for lacking clothes the way they would a naked human.*

A SkyrimNet prompt submodule (`character_bio/0405_beastaware_form.prompt`) also adds a **"Current Form"** section to the profile of **any** actor (not only the player) whose race is Werewolf, Werebear or Vampire Lord. It is additive and does not replace any SkyrimNet file.

### 3. Revert
> *&lt;Name&gt; shrank back into human form, left standing naked and exhausted among the remains of the change.*

For a Vampire Lord, the revert text says "mortal form" instead of "human form".

**"NPCs react out loud" on** (the default): the event is narrated (`DirectNarration`), so nearby NPCs can respond. **Off**: it is stored silently as a persistent memory.

Detection: a player alias catches `OnRaceSwitchComplete`, re-checks after a game load, and re-checks every 30 s while you are transformed. Loading a save doesn't trigger an announcement.

## 📋 Requirements

| Requirement | Why |
|---|---|
| Skyrim SE 1.5.97 (tested). Other versions are untested. | `Skyrim.esm` is the only master. |
| [SKSE64](https://skse.silverlock.org/) | The scripts use SKSE functions (`StringUtil`, `GetDisplayName`, `OnPlayerLoadGame`). |
| [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444) | Required by SkyrimNet |
| [SkyrimNet](https://github.com/MinLL/SkyrimNet-GamePlugin) | Tested on **beta28**; built against the beta28 `SkyrimNetApi`. The manifest asks for SkyrimNet 0.25.0 or newer. |
| [SkyUI](https://www.nexusmods.com/skyrimspecialedition/mods/12604) | MCM (`SKI_ConfigBase`, `SKI_PlayerLoadGameAlias`) |
| Dawnguard (part of SE) | Vampire Lord detection. It is read at runtime, so it isn't a master. |

**Optional and compatible:** Growl (werebear), [OStim Beast Form](https://github.com/Coronerra/OStim-Beast-Form), ABC and any werewolf body mod. Beast Aware **touches no vanilla records**: it adds one quest and one prompt file.

## 📦 Install

Download **`BeastAware_v1.1.zip`** from [Releases](../../releases/latest). It has a Data-root layout.

**Mod Organizer 2:** *Install a new mod from archive* → choose the zip → make sure `BeastAware.esp` is ticked in the right pane. Load order doesn't matter.

**Vortex:** drag the zip into *Mods* → *Install* → *Enable* → *Deploy*. Make sure `BeastAware.esp` is enabled in *Plugins*.

**Manual:** extract the zip into `Skyrim Special Edition\Data`.

Load a save and give SkyUI a minute to register the menu.

## ⚙️ MCM: "Beast Aware"

| Option | Default |
|---|---|
| Enabled | ✔️ |
| Announce transforming | ✔️ |
| Announce changing back | ✔️ |
| NPCs react out loud | ✔️ (off = remembered silently) |
| Keep beast form in scene context | ✔️ |
| Debug notifications | ❌ |

The menu also shows your current form.

## 🧪 Tested on

Tested only on my modified **Nolvus 6.0.21** setup (Skyrim SE 1.5.97) with SkyrimNet beta28. It should work on other setups, but that hasn't been confirmed.

## 🔗 Also included in the Werewolf Overhaul

Beast Aware is also bundled in the [Werewolf-Overhaul-Proof-of-Concept](https://github.com/Coronerra/Werewolf-Overhaul-Proof-of-Concept) repo. **It works fully standalone**, so you don't need anything from that repo.

## 🔗 Related / recommended
- 💦 [GT - Softbody](https://www.nexusmods.com/skyrimspecialedition/mods/152103): affects ABC's creature bodies and physics. Recommended with the werewolf setup.
- 💦 [OCum-Tull-Liquid-Softbody-Patch](https://github.com/Coronerra/OCum-Tull-Liquid-Softbody-Patch): a merged OCum script for OCum Ascended 4.1.1, the Tull/Liquid Pack and GT Softbody.

## 🛠️ Source

- `src/Scripts/`: Papyrus sources (`BA_Main`, `BA_MCM`, `BA_PlayerAlias`). Compile them with Caprica or the Creation Kit compiler against the vanilla, SKSE, SkyUI SDK and SkyrimNet API headers. The sources are also shipped in `Data/Scripts/Source`.
- `src/SkyrimNet/`: the SkyrimNet bundle (manifest and prompt).
- `src/mkesp.py`: writes `BeastAware.esp` (`python mkesp.py`).

## 🙏 Credits

- **That Guy (Coronerra)**: Beast Aware
- Huge thanks to **MinLL and the SkyrimNet team** for SkyrimNet and its open API and prompt system 🌕
- The SKSE team, Address Library (meh321) and SkyUI (schlangster and team)

## 📜 License

[MIT](LICENSE) © coronerra

*Have fun and Happy Modding!* 🐺
