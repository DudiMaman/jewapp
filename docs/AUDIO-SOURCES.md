# Reading audio — existing libraries & integration

Goal: authentic **cantillated / melodic** Hebrew reading (ta'amim for Tanakh; nusach melody
for prayers), by **tradition (Ashkenaz / Sepharad)** and **voice (male / female)**. These are
human recordings — no TTS produces ta'amim. Below are real, reusable sources.

## Candidate libraries

| Source | Coverage | Tradition | Voice | Ta'amim? | License | Hosting |
|---|---|---|---|---|---|---|
| **PocketTorah** | Torah + Haftarah (no Tehillim) | Ashkenaz | male | yes (chanted) | **CC BY-SA** (code LGPL) | Internet Archive |
| **Rabbi Dan Be'eri Tanakh** | Most of Tanakh incl. **Tehillim** (missing ~⅓; Psalms 50–112 absent); some narrated, some sung | **Sepharad** (Aleppo/Attiya) | male | partial (cantillated + narrated) | **CC BY-SA 3.0** | Internet Archive |
| **Sefaria** | Tanakh **text** + API; embeds PocketTorah audio | — | — | text has marks | text: CC (mixed) | api.sefaria.org |
| **National Library of Israel — "הזמנה לפיוט" / Piyut** | Piyutim & prayers across **many edot** (Ashkenaz/Sepharad/Mizrah/Teiman) | multi | male/female | melody (nusach) | **per-item** (varies) | nli.org.il |
| **Chabad.org Tehillim Audio** | All 150 Psalms, chanted | (Chabad) | male | chanted | proprietary (personal use) | chabad.org |
| **dafyomireview.com/torahreading** | Torah leining + Tehillim MP3 | Ashkenaz **and** Sephardi | male | yes | check/attribute | site |

## Recommended stack

1. **Tanakh / Torah reader (with ta'amim), free & licensable now:**
   - **Ashkenaz →** PocketTorah (Torah/Haftarah).
   - **Sepharad →** Rabbi Dan Be'eri Tanakh (incl. partial Tehillim).
   - Both are **CC BY-SA** — usable commercially **with attribution**, and derivative audio
     stays under the same license (share-alike). Pull the MP3s from the Internet Archive
     items and store the source + attribution alongside each file.
   - Use **Sefaria's API** for the synchronized text layer (it already links PocketTorah audio).

2. **Gaps that these don't cover (need commissioning or per-item licensing):**
   - **Female voice** (none of the free CC sets provide it).
   - **Complete Tehillim** (Be'eri is missing ~a third).
   - **Prayers / Siddur nusach melodies** (Modeh Ani, Shacharit/Mincha/Maariv, Kabbalat
     Shabbat…) — best from **NLI Piyut** (license per recording) or **commissioned**.

3. **Robust long-term path:** commission a **ba'al-korei / chazzan (male)** and a **female
   reader** to record the fixed texts per nusach. It's a bounded, one-time content effort
   (the texts never change) and yields a fully-owned, consistent library.

## How it plugs into the app

The player already selects by **prayer × voice** (and the model keys on **nusach**), so
integration is only a matter of filenames:

```
audio/<text>-<ashkenaz|sepharad>-<male|female>.mp3     # or stream from Internet Archive
```

- Drop CC BY-SA files into the matching slots (keep each file's LICENSE/attribution).
- For streamed sources, store URLs + attribution in a small `audio/manifest.json`.
- Note distinction: **ta'amim** apply to **Tanakh** (Torah/Megillot/Tehillim); **prayers**
  use **nusach melody**, not ta'amim.

## Legal note
CC BY-SA permits commercial use **with attribution** and **share-alike** on the audio (the
recordings keep their license; your app code is unaffected). Confirm each Internet-Archive
item's stated license before shipping, and add a credits screen listing the readers/sources.

## Sources
- PocketTorah — https://www.pockettorah.com/
- Rabbi Dan Be'eri Tanakh (CC BY-SA 3.0) — https://archive.org/details/TanakhAudioRecordingByRabbiDanBeeri-BookByBook
- Sefaria API — https://developers.sefaria.org/ · audio topic: https://www.sefaria.org/topics/audio-recordings
- Hebcal leyning audio (PocketTorah-based) — https://www.hebcal.com/home/498/torah-trope-chanting-audio-leyning
- Chabad Tehillim Audio — https://www.chabad.org/multimedia/music_cdo/aid/3995914/
- Ashkenazi/Sephardi Torah + Tehillim MP3 — https://dafyomireview.com/torahreading/
- Open Siddur cantillation — https://opensiddur.org/readings-and-sourcetexts/cantillation/cantillation-tables-for-torah-readings/
