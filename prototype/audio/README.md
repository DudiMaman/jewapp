# Audio — reading recordings

Files are selected by the user's preference: **prayer × voice (male/female)**.
Naming: `audio/<prayer>-<male|female>.mp3` (e.g. `modeh-ani-male.mp3`).

Current files are **neural TTS** (Microsoft Edge `he-IL-AvriNeural` = male,
`he-IL-HilaNeural` = female) — natural voices, and a big step up from device TTS.
They are **plain reading, without ta'amim/melody**.

## For production (authentic cantillation & nusach)
Ta'amim (cantillation) and nusach melodies (chazzanut) are **human performances** and
cannot be synthesized. Replace these files with recorded ba'al-korei / chazzan / female
reader tracks, organized by tradition and voice:

```
audio/<prayer>-<ashkenaz|sepharad>-<male|female>.mp3
```

Note: ta'amim apply to **Tanakh** (Torah, Megillot, and the ta'amim of Tehillim);
prayers such as Modeh Ani use **nusach melody**, not ta'amim. The player already keys on
nusach and voice, so dropping in the correctly-named files is all that's needed.
