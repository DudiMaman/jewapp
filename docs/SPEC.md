# Neshama (נשמה) — Product Specification

> **נשמה** — a daily Jewish-life companion for prayer, Tehillim (Psalms), and mitzvot,
> with an AI guide and gentle, time-aware reminders.
> Subscription mobile app for **iOS + Android**, Hebrew-first (RTL).

---

## Table of contents

1. [Overview & Vision](#1-overview--vision)
2. [Target Users & Value Proposition](#2-target-users--value-proposition)
3. [Platforms & Technical Assumptions](#3-platforms--technical-assumptions)
4. [Information Architecture](#4-information-architecture)
5. [Onboarding Flow](#5-onboarding-flow)
6. [Core Feature Areas](#6-core-feature-areas)
7. [Notifications](#7-notifications)
8. [Personalization & Content Model](#8-personalization--content-model)
9. [Monetization](#9-monetization)
10. [Data Model](#10-data-model)
11. [Non-Functional Requirements](#11-non-functional-requirements)
12. [Design System](#12-design-system)
13. [Appendix A — Screen-by-Screen Reference](#appendix-a--screen-by-screen-reference)
14. [Appendix B — Notification Copy Library](#appendix-b--notification-copy-library)
15. [Appendix C — Open Questions](#appendix-c--open-questions)

---

## 1. Overview & Vision

**Neshama** ("Soul") is a subscription mobile app that makes everyday Jewish practice feel
*simple, personal, and close again*. It combines the spiritual content a person needs —
the Siddur, Tehillim, the Tanakh, prayer guides, and daily mitzvot — with three things a
plain text app does not provide:

- **Personalization** — content is tuned to the user's nusach, gender, age, Hebrew name,
  and Hebrew reading level.
- **A guide ("the companion")** — an AI chat that explains any prayer or verse in plain
  language and recommends the right chapter for the moment.
- **Gentle structure** — a daily "journey," streaks, commitments (קבלות), and time-aware
  push reminders that respect Shabbat.

The product tone is calm, warm, and non-judgmental ("אין שיפוט. רק נקודת התחלה" — *no
judgment, just a starting point*). The closest analogues are wellness apps such as Calm and
Headspace, reimagined for Jewish daily life.

### Product pillars

| Pillar | What it means |
|---|---|
| **Daily rhythm** | A single "Today" screen that tells the user exactly what to do now. |
| **Understanding** | Every word is approachable — translation/explanation on demand, AI guide. |
| **Personal** | Built around *this* user's name, age, nusach, and goals. |
| **Consistency without guilt** | Streaks that survive Shabbat, make-up days, soft reminders. |
| **Beautiful & calm** | Premium visual design (see §12), watercolor warmth, quiet typography. |

---

## 2. Target Users & Value Proposition

**Primary user:** a Jewish adult (traditional → observant, or returning/strengthening) who
wants daily Jewish life — prayer, Tehillim, small mitzvot — to feel approachable and
consistent, in Hebrew, on their phone.

**Jobs to be done (captured directly from onboarding "מה מביא אותך לכאן?"):**
- Strength to cope (כוח להתמודדות)
- A daily moment of gratitude (רגע יומי של הודיה)
- Healing for myself or loved ones (רפואה לי או ליקירים)
- Protection and inner peace (שמירה ושקט נפשי)
- Connection to something greater (חיבור למשהו גדול יותר)
- Building a daily habit (לבנות הרגל יומי)

**Core promise (paywall headline):** *"הדרך הפשוטה לחיבור יומי"* — the simple path to a
daily connection. Tehillim, Siddur, and prayer, all in one place, every day.

---

## 3. Platforms & Technical Assumptions

- **Native mobile**, iOS and Android. (Recording is iOS; parity expected on Android.)
- **Hebrew-first, full RTL** layout. English/other languages are out of scope for v1 UI,
  though the content layer should not hard-code Hebrew-only assumptions.
- **Offline-capable reading**: Tehillim, Siddur, and Tanakh text are bundled/cached so the
  user can read without connectivity. AI chat requires network.
- **Push notifications** with local scheduling (prayer-time and daily reminders) plus the
  ability to send server-driven messages.
- **Widgets**: Home-screen and Lock-screen widgets (premium).
- **In-app purchases / subscriptions**: Apple StoreKit 2 and Google Play Billing, with a
  7-day free trial, weekly and annual plans, and restore-purchases.
- **AI backend**: an LLM-backed chat service with Jewish-text grounding (citations to
  chapters/verses). Responses must be warm, accurate, and link to in-app sources.
- **Hebrew typography with nikud (vowels)** and ta'amim where relevant; adjustable font size.
- **Zmanim engine**: halachic times by geolocation to drive prayer reminders and the daily
  Hebrew date. Requires location (or manual city) permission.
- **Hebrew calendar**: full Hebrew date, parashat ha-shavua, and Shabbat/Yom Tov detection
  (drives the "Shabbat-silent" notification rule and streak protection).

---

## 4. Information Architecture

The app uses a **5-tab bottom navigation** (RTL order, right → left):

| Tab | Hebrew | Purpose |
|---|---|---|
| **Tanakh** | תנ"ך | Full Bible reader with nikud, AI-explain, highlighting. |
| **Tehillim** | תהילים | Psalms reader: personal daily chapters, full book, highlighting. |
| **Today** | היום | Home / daily journey dashboard (default tab). |
| **Siddur** | סידור | Prayer book for the user's nusach. |
| **Chat** | צ'אט | AI companion ("נשמה"). |

`היום` (Today) is the default/center tab and is marked with the brand flame icon.

Above the tabs sit the full-screen flows that are **not** tabs: onboarding, paywall,
settings, and individual reader/prayer detail screens (pushed modally or via navigation).

---

## 5. Onboarding Flow

Onboarding is a personalization funnel that both configures the app and sells the value of
the subscription. It is linear with a top progress indicator; most steps have a "המשך"
(Continue) pill CTA that is disabled until a valid selection is made. A back/forward
chevron is available.

### 5.1 Splash
- App icon (gold flame/leaf with a sparkle on a white rounded tile), wordmark **נשמה**.
- Verse: *"ה' שְׂפָתַי תִּפְתָּח וּפִי יַגִּיד תְּהִלָּתֶךָ"* with caption *"פתיחת העמידה"*.

### 5.2 Value carousel (4 slides)
Watercolor illustration + headline + CTA. Slide order:
1. Doorway opening — *"צעד אחד פנימה, והדרך נפתחת."* — CTA **"בואו נתחיל"**.
2. Dove over the Old City of Jerusalem — *"מותאם לגיל שלך, ללב שלך, וליום הזה."*
3. Couple praying by a window — *"הימים שלך מלאים. הנשמה שלך מחכה לך."*
4. Open Tehillim with candle & olive branch — *"כמה דקות שקטות ביום. תהילים, תפילה
   ומעשים קטנים של אמונה."*

### 5.3 Profile & personalization questions
In order:

| Step | Prompt | Input | Drives |
|---|---|---|---|
| Gender | "נעים להכיר" | אישה / גבר (single) | prayers & customs shown |
| Goals | "מה מביא אותך לכאן?" | 6 options (multi) | content emphasis, copy |
| Age | "כמה אתה?" | number wheel | **personal daily Tehillim chapter by age** |
| Hebrew name | "מה השם העברי שלך?" | text | **personal Psalm 119 name-verses** |
| Nusach | "מהו נוסח התפילה שלך?" | אשכנז / ספרד / עדות המזרח | which siddur loads |
| Tehillim frequency | "באיזו תדירות אתה אומר תהילים היום?" | 3 options | starting cadence |
| Commitment cadence | "מה יהיה משמעותי עבורך?" | כל יום / כמה פעמים בשבוע | reminder plan |
| Hebrew reading level | "איך הולך לך עם העברית?" | 3 options | translation/explanation depth |

**Notes**
- *Age → daily psalm*: reflects the custom of reciting the psalm corresponding to one's age
  (e.g. age 20 → Psalm 21). Stored and surfaced as a personal daily chapter.
- *Hebrew name → Psalm 119*: the letters of the user's name map to the eight-verse
  acrostic sections of Psalm 119 (קי"ט). Example shown: דויד → verses כ"ה-ל"ב, מ"א-מ"ח, …
  The UI previews the mapped verses live as the user types.
- *Reading level* options: "אני מבין את רוב מה שאני קורא" / "קולט חלק, מפספס הרבה" /
  "אני קורא את המילים בלי להבין" → controls how much translation/explanation/nikud is shown
  by default.

### 5.4 Plan build (loading)
"מכינים את המסע שלך" with an animated checklist: *matching your nusach → finding your
name's verses → choosing your daily chapters → setting your daily pace.*

### 5.5 Personalized value screen
"דויד, זה נבנה בשבילך" ("your plan is ready"). A "החיבור היומי שלך" line chart compares
**עם נשמה** vs **לבד** (with Neshama vs alone) over היום / שבוע 1 / חודש 1. Social-proof
stat: *"87% מהמתפללים מדווחים שהם מתמידים יותר…"*. Teases reminders, tefillin guidance, and
the AI chat.

### 5.6 Feature preview — AI chat
"שאל את נשמה כל דבר" ("המלווה שלך"). Demonstrates a real exchange:
*"איזה פרק תהילים עוזר לחרדה?"* → a warm answer recommending **תהילים כ"ג** and **צ"א**,
explaining each and linking to the chapters.

### 5.7 Streak intro
"היום הראשון שלך מתחיל עכשיו" — flame with day **1**. **"שבת מטופלת"**: the streak
continues through Friday night and Shabbat; the user rests "בלי דאגות" and the streak
resumes Sunday. (Shabbat never breaks a streak.)

### 5.8 Social proof
"יחד נבנה את החזון" — testimonials and a 5-star App Store rating ask.

### 5.9 Permissions
- **Notifications priming** "נזכיר לך כשמגיע הזמן": reminders for prayer times, daily
  Tehillim, and the user's commitments — at convenient times. **"בשבת אנחנו שותקים"**
  (silent on Shabbat). Then the iOS system permission dialog.
- **Privacy / App Tracking Transparency priming**: *"התפילות והפרטים האישיים שלך תמיד
  נשארים פרטיים. אנחנו לעולם לא מוכרים את המידע שלך."*

### 5.10 Trial & paywall
- Trial intro: *"אנחנו נותנים 7 ימים חינם כדי שכולם יוכלו להתקרב לה'."*
- Trial reminder promise: *"תקבל תזכורת יומיים לפני סיום הניסיון."*
- **Paywall** — see §9.

---

## 6. Core Feature Areas

### 6.1 Today / Daily Journey (היום)
The home and default screen — *"המסע של היום"*.

**Header**
- Settings gear; **streak badge** (flame + count).
- Full **Hebrew date** line: e.g. *"ט"ו בתמוז תשפ"ו · יום שלישי, 30 ביוני"* (Hebrew +
  Gregorian).

**Daily-Tehillim journey strip**
- A horizontal row of **day-circles** labelled with Hebrew-letter day numbers (… יג, יד,
  **טו**, טז, יז …). Today is highlighted; future days are **locked**; completed days are
  marked done. Represents progression through the user's daily Tehillim plan.

**Action cards (vertical, each expandable / actionable):**
- **Commitments (קבלות)** — a featured dark card *"אני לוקח על עצמי / להתחיל קבלה חדשה"*
  with a **+** to add a new personal commitment.
- **Halacha / mitzvah of the day** — e.g. *"המתנה בין בשר לחלב"* with a **"התחילי"** CTA
  that opens a short guide.
- **Parashat ha-shavua** — *"פרשת השבוע · פינחס"* (expandable).
- **Prayer cards**, each expandable into a guided reader: **מודה אני** (morning gratitude),
  **תפילין** (tefillin guide, with illustration), **שחרית** (Shacharit), and additional
  prayers below the fold (Mincha, Maariv, Kriat Shema al ha-mita, etc.).

Each card uses a calm full-bleed watercolor background tinted to its time of day.

### 6.2 Tehillim (תהילים)
- Read the full book of Psalms and the user's **personal daily chapters** (by age and by
  name, see §8).
- **Highlighting** verses in any color (premium: unlimited; see §9).
- Per-verse AI-explain and translation toggle based on reading level.
- Progress feeds the day-circle journey and the streak.

### 6.3 Siddur (סידור)
- Full prayer book rendered in the user's chosen **nusach** (Ashkenaz / Sefard /
  Edot HaMizrach).
- Context-aware: surfaces the right tefillah for the current time (Shacharit / Mincha /
  Maariv) and links from the Today prayer cards.
- Same reader affordances (nikud, font size, highlight, AI-explain).

### 6.4 Tanakh (תנ"ך)
- Full Bible reader. Verses rendered with **full nikud** and verse-letter markers
  (e.g. בראשית א: א, ב, ג …).
- Chapter picker (e.g. "בראשית א" dropdown).
- **Selection toolbar** on long-press: **AI-explain (sparkle)**, **color highlight**
  (palette), **copy**, **font-size (אא)**.

### 6.5 AI Chat — "the companion" (צ'אט)
- Conversational assistant branded as **נשמה**.
- Capabilities: explain any prayer/verse in plain Hebrew; recommend Psalms by emotion or
  situation (anxiety, healing, gratitude…); answer practical halacha/"how do I…" questions;
  link directly to the relevant in-app chapter/verse.
- Tone: warm, encouraging, non-judgmental; cites sources; ends supportively.
- Message styling: user bubble = brand navy; assistant bubble = white card; typing
  indicator while generating.

### 6.6 Cross-cutting reader engine
A shared reader powers Tehillim, Siddur, and Tanakh:
- Hebrew text with nikud; adjustable font size (אא).
- Translation / transliteration / explanation layers, default depth from reading level.
- Verse selection → AI-explain, highlight (color), copy.
- Highlights persist per user and sync.

### 6.7 Streaks & commitments
- **Streak**: daily completion of the user's plan increments a flame count.
- **Shabbat-aware**: Friday night + Shabbat never break the streak.
- **Streak repair / make-up days** (premium): retroactively complete missed days to keep
  the streak.
- **Commitments (קבלות)**: user-defined personal undertakings tracked on the Today screen.

### 6.8 Widgets (premium)
- **Home-screen** and **Lock-screen** widgets showing the daily Tehillim chapter / next
  prayer / streak.

---

## 7. Notifications

Reminders are **time-based, name-personalized, and Shabbat-silent**. Times follow the
user's commitment cadence and (for prayers) local **zmanim**. On Shabbat and Yom Tov the
app sends **no** notifications ("בשבת אנחנו שותקים").

**Observed daily schedule (from the notification screen):**

| Time | Title | Body |
|---|---|---|
| 09:00 | תהילים יומי 📖 | "התהילים שלך להיום: ע"ז – ע"ח. כמה פסוקים עושים הרבה 🌿" |
| 13:30 | דויד, זמן מנחה 🕐 | "עצור, נשום, התפלל. מנחה כאן ☀️" |
| evening | תפילת ערבית 🌙 | "אור רך, שעה שקטה. זמן מעריב ✨" |
| bedtime | קריאת שמע על המיטה ✨🌙 | "המילים האחרונות של היום, שיהיו שמע" |

**Rules**
- Personalize with the user's name where natural ("דויד, זמן מנחה").
- Prayer reminders anchor to zmanim; daily-Tehillim and commitment reminders anchor to
  user-chosen times.
- All reminder times are editable, and notifications can be turned off per-type, in
  Settings ("אפשר לשנות זמנים או לכבות בכל רגע בהגדרות").
- A trial-ending reminder fires **2 days before** the free trial ends.

---

## 8. Personalization & Content Model

| Input | Source | Effect |
|---|---|---|
| **Nusach** | onboarding | Which Siddur text/version is loaded. |
| **Gender** | onboarding | Which prayers/customs and gendered wording appear. |
| **Age** | onboarding | Personal **daily psalm by age** (age N → Psalm N+1). |
| **Hebrew name** | onboarding | Personal **Psalm 119 name-verses** (acrostic sections). |
| **Reading level** | onboarding | Default depth of translation/explanation/nikud. |
| **Goals** | onboarding | Emphasis of content, recommendations, and copy. |
| **Commitment cadence** | onboarding | Reminder frequency and plan pacing. |
| **Location** | zmanim permission | Halachic times, Hebrew date, Shabbat detection. |

**Content library required:** Tehillim (all 150), Siddur in three nusachim, full Tanakh
with nikud, prayer guides (Modeh Ani, Shacharit, Mincha, Maariv, Kriat Shema al ha-mita,
tefillin), weekly parasha summaries, and a halacha/mitzvah card library.

---

## 9. Monetization

**Model:** subscription with a 7-day free trial.

| Plan | Price | Notes |
|---|---|---|
| Weekly | ₪17.90 / week | recurring weekly |
| Annual | ₪149.90 / year | **7-day free trial**, "84% הנחה" vs weekly, no charge now |

**Premium-gated features (from the paywall):**
- AI companion ("הבינו כל פרק ופסוק בעזרת העוזר של נשמה").
- **Home-screen + lock-screen widgets**.
- **Unlimited verse highlighting in any color**.
- **Streak repair / make-up missed days**.

**Paywall screen** — "הדרך הפשוטה לחיבור יומי" / "תהילים, סידור, ותפילה. הכל במקום אחד, בכל
יום." Feature checklist, two plan rows (annual pre-selected, discount badge), "המשך" CTA,
and footer links: **פרטיות · תנאים · שחזר רכישות**. Standard StoreKit/Play purchase, restore,
and a trial-ending reminder 2 days out.

---

## 10. Data Model

Core entities (indicative, not a schema):

- **User** — auth identity, locale, created date, subscription state.
- **Profile** — gender, ageAtSignup (+ birth handling), hebrewName, nusach, readingLevel,
  goals[], commitmentCadence, location/city.
- **Plan** — derived: dailyPsalmByAge, namePsalm119Verses[], dailyChapters[], pacing.
- **DayProgress** — date (Hebrew + Gregorian), completed items, isShabbat, isMakeup.
- **Commitment (קבלה)** — title, cadence, createdAt, history.
- **Highlight** — ref (book/chapter/verse), color, createdAt. (Unlimited only if premium.)
- **Streak** — current, longest, lastCompletedDate, shabbatProtected.
- **Subscription** — plan, status (trial/active/expired), trialEndsAt, store, receipts.
- **ChatThread / ChatMessage** — role, content, cited refs[], createdAt.
- **NotificationSchedule** — type, time/zman anchor, enabled, shabbatSilent=true.

---

## 11. Non-Functional Requirements

- **Privacy**: prayers and personal details stay private; **data is never sold**; ATT
  handled transparently. Clear privacy policy + terms; restore purchases.
- **Shabbat/Yom Tov awareness**: no notifications; streak protection; (consider an optional
  Shabbat mode that limits interaction).
- **RTL & Hebrew typography**: correct bidi, nikud rendering, verse-letter numerals,
  adjustable font size, high legibility.
- **Accessibility**: dynamic type, sufficient contrast (mind the light-gold accents),
  VoiceOver/TalkBack labels in Hebrew.
- **Performance & offline**: instant reader open; bundled/cached texts; graceful offline
  for everything except AI chat.
- **Internationalization-ready** content layer even though v1 UI is Hebrew-only.

---

## 12. Design System

The current cream/peach + terracotta-orange theme is **replaced** by a **Jewish
blue-and-white palette with very delicate, light gold accents**, while keeping the calm,
premium, watercolor feel and rounded-card layout. The full component library is delivered
as a **Claude Design system** (claude.ai/design); see that project for living previews.

**Palette (summary)**
- **Primary blue** (deep tekhelet / navy): `#102A43` / `#1E3A5F`; **accent blue** `#2C5F8A`;
  soft sky-blue tints for backgrounds.
- **Surfaces**: white `#FFFFFF` / off-white `#F7FAFC`.
- **Gold (light, sparing)**: `#C8A24B` and soft `#E3CB86` — thin dividers, small icon
  strokes, active states, and delicate ornament flourishes only (no heavy gold fills).
- **Neutrals/semantics**: locked/disabled grays; success; the streak flame restyled toward
  gold/blue.

**Typography** — Hebrew-first, RTL. Refined serif for verse/prayer text (with nikud) and a
clean sans for UI; clear type scale.

**Ornamentation** — very subtle gold filigree / corner flourishes and a light arch or
Magen-David motif; delicate, never loud.

**Component inventory** (built as preview cards): color & type foundations, buttons & pill
CTA, prayer/halacha/commitment/parasha cards, option rows & multi-select chips, onboarding
progress bar, day-circle journey, streak badge, 5-tab bottom bar, chat bubbles + typing
indicator, reader view with selection toolbar, paywall + plan rows + discount badge,
onboarding slide template, notification card, and a recolored app-icon concept.

---

## Appendix A — Screen-by-Screen Reference

Each entry: **purpose · key elements · states**.

**Onboarding**
1. **Splash** — brand + Amida verse · icon, wordmark, verse, caption · transient.
2. **Carousel 1–4** — sell value · illustration, headline, dots, CTA · swipe; last → profile.
3. **Gender** — segment user · two option rows (אישה/גבר), Continue · disabled until choose.
4. **Goals** — capture motivation · 6 multi-select rows w/ icons, Continue · ≥1 required.
5. **Age** — set daily psalm · number wheel, Continue.
6. **Hebrew name** — set name-verses · text field, live verse preview, Continue · validates Hebrew.
7. **Nusach** — choose rite · 3 option rows w/ descriptions, Continue.
8. **Tehillim frequency** — baseline · 3 rows w/ icons, Continue.
9. **Commitment cadence** — reminder plan · 2 rows (כל יום / כמה פעמים בשבוע), Continue.
10. **Reading level** — content depth · 3 rows w/ icons, Continue.
11. **Plan build (loading)** — reassurance · animated checklist · auto-advances.
12. **Personalized value** — justify subscribe · chart (עם נשמה vs לבד), 87% stat, feature teasers.
13. **AI chat preview** — show the companion · sample Q&A bubbles, Continue.
14. **Streak intro** — habit hook · flame "1", "שבת מטופלת" copy, Continue.
15. **Social proof** — trust · testimonials, 5-star ask.
16. **Notification priming + dialog** — opt-in · "בשבת אנחנו שותקים", enable CTA, iOS dialog.
17. **Privacy / ATT priming** — trust · lantern illustration, "we never sell your data", Continue.
18. **Trial intro** — "7 ימים חינם" · Continue.
19. **Trial reminder** — "תזכורת יומיים לפני…" · Continue.
20. **Paywall** — convert · features, plan rows, badge, Continue, footer links · annual pre-selected.

**Main app**
21. **Today (היום)** — daily hub · header (gear, streak, Hebrew date), day-circle strip,
    commitment card, halacha card, parasha, prayer cards (Modeh Ani/Tefillin/Shacharit/…),
    bottom tabs · cards expand; future days locked.
22. **Tehillim** — psalms reader · chapter nav, verses w/ nikud, highlight, AI-explain,
    personal daily chapters · highlight-unlimited gated.
23. **Siddur** — nusach prayer book · time-aware tefillah, reader affordances.
24. **Tanakh** — bible reader · chapter dropdown, verses w/ nikud + letters, selection
    toolbar (AI-explain, color highlight, copy, font-size).
25. **Chat (צ'אט)** — AI companion · message list, user/assistant bubbles, typing indicator,
    cited links · network required.
26. **Settings** — manage · reminder times/toggles, nusach, reading level, subscription,
    privacy/terms, restore. *(Inferred from "ניתן לשנות בהגדרות"; confirm details.)*

---

## Appendix B — Notification Copy Library

Tone: short, warm, sensory, never nagging. Personalize with name when natural. Silent on
Shabbat/Yom Tov.

- **Daily Tehillim (09:00)** — "תהילים יומי 📖 — התהילים שלך להיום: {range}. כמה פסוקים עושים
  הרבה 🌿"
- **Mincha (13:30 / zman)** — "{name}, זמן מנחה 🕐 — עצור, נשום, התפלל. מנחה כאן ☀️"
- **Maariv (evening / zman)** — "תפילת ערבית 🌙 — אור רך, שעה שקטה. זמן מעריב ✨"
- **Kriat Shema al ha-mita (bedtime)** — "קריאת שמע על המיטה ✨🌙 — המילים האחרונות של היום,
  שיהיו שמע"
- **Trial ending (T-2 days)** — reminder that the free trial ends in two days.

---

## Appendix C — Open Questions

These were not fully visible in the recording and should be confirmed before build:

1. **Settings** screen contents and layout (reminder editing, account, subscription mgmt).
2. **Auth**: is there account creation/login, or is it device-local + store entitlement?
3. **Account across devices / sync** of highlights, streak, commitments.
4. **Tefillin guide** depth (step-by-step, audio, illustrations?).
5. **Commitments (קבלות)** library — preset suggestions vs. free text; tracking/streaks.
6. **Halacha card** source/breadth and whether it is a daily rotation.
7. **Birthday handling** for the age→psalm mapping (does the daily psalm advance each Hebrew
   birthday?).
8. **AI guardrails** for halachic questions (when to defer to a rav).
9. **Localization** beyond Hebrew (future).
10. Exact **zman provider** and location/manual-city UX.

---

*Source: this specification was reconstructed from a 32-screen product walkthrough and the
push-notification screen of the existing build. UI strings are quoted in Hebrew as they
appear in-product.*
