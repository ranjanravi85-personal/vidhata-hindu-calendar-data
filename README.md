# Hindu Calendar and Muhurat Data 2026-2028 (computed, Vidhata)

Festival dates, griha pravesh days, wedding days by city, planetary ingresses
and the Sun's sankranti instants for 2026 to 2028, computed by the panchang
engine behind [Vidhata](https://vidhata.app), a Vedic astrology service. Every
date in this dataset was produced by the engine and then published on
vidhata.app. None was typed in from another almanac.

The data is released under CC BY 4.0. You may use it for any purpose,
including commercial use, as long as you credit Vidhata (see "How to cite"
below).

Published pages built on this data:

- Hindu festival calendars: [2026](https://vidhata.app/hindu-festivals-2026-calendar), [2027](https://vidhata.app/hindu-festivals-2027-calendar), [2028](https://vidhata.app/hindu-festivals-2028-calendar)
- [Wedding Season Index](https://vidhata.app/wedding-season-index), November 2026 to June 2027, ten cities
- [Griha pravesh muhurat dates](https://vidhata.app/blog/griha-pravesh-muhurat-dates)
- [2026 Vivah Muhurat Report](https://vidhata.app/2026-vivah-muhurat-report)
- [Press and media](https://vidhata.app/press)

## What is in it

| File | Rows | Contents |
|---|---:|---|
| `data/hindu_festivals_2026_2028.csv` | 117 | 39 major Hindu festivals for each of 2026, 2027 and 2028, with the classical rule that dates each one |
| `data/griha_pravesh_2027_days.csv` | 33 | Clean griha pravesh (house-warming) days in 2027 at Ujjain (17) and New Delhi (16) |
| `data/griha_pravesh_2027_monthly_counts.csv` | 24 | Those days counted by month, per location |
| `data/griha_pravesh_2027_rule_tiers.csv` | 8 | How the 2027 count changes as each rule set is added |
| `data/griha_pravesh_2027_excluded_seasons.csv` | 12 | Seasons that bar griha pravesh around 2027 (Kharmas, Malmas, Chaturmas, Venus and Jupiter combustion) |
| `data/chaturmas_ekadashis_2027.csv` | 4 | Devshayani and Prabodhini Ekadashi 2027, which open and close Chaturmas |
| `data/planetary_ingresses_2027.csv` | 13 | Sidereal sign changes of Jupiter and Saturn during 2027, plus the previous and next sign change of Jupiter, Saturn, Rahu and Ketu |
| `data/planetary_stations_2027.csv` | 3 | Jupiter and Saturn retrograde and direct stations in 2027 |
| `data/planet_signs_2027_year_boundaries.csv` | 8 | Sign and degree of Jupiter, Saturn, Rahu and Ketu at the start and end of 2027 |
| `data/sun_sankrantis_dec2026_jan2028.csv` | 14 | Every sidereal solar ingress (sankranti) from December 2026 to January 2028 |
| `data/kharmas_malmas_instants_2026_2028.csv` | 6 | Start and end instants of Kharmas 2026-27, Malmas 2027 and Kharmas 2027-28 |
| `data/wedding_days_by_city_2026_11_to_2027_06.csv` | 188 | Wedding days for ten Indian cities, November 2026 to June 2027 |
| `data/wedding_days_monthly_counts_by_city.csv` | 80 | Those days counted by month, per city |
| `data/wedding_days_rule_tiers_by_city.csv` | 40 | How each city's count changes as each rule set is added |
| `data/wedding_season_pauses_2026_11_to_2027_07.csv` | 7 | Runs of days when no wedding is fixed, and why |
| `data/wedding_days_city_differences_vs_new_delhi.csv` | 2 | Days a city loses or gains against the New Delhi list |
| `data/vivah_muhurat_2026_days.csv` | 13 | The 13 marriage muhurat days of 2026 at Ujjain |
| `data/vivah_muhurat_2026_monthly_counts.csv` | 12 | 2026 marriage days by month, with a note on each month |
| `data/vivah_muhurat_2026_prohibited_windows.csv` | 6 | The 2026 seasons that bar weddings |

`data/source/` holds the original JSON the CSVs were exported from:
`year-2027-facts.json` and `wedding-season-index.data.json` are the engine's
own output files, unchanged; `festivals-2026-2028.json` and
`vivah-muhurat-2026.json` are the festival tables, festival rules and 2026
vivah report exported as JSON from the source modules.

## How it was computed

**Ephemeris.** Planet positions come from the Swiss Ephemeris through
Vidhata's own wrapper. The 2027 facts file records the SWIEPH data files
(`sepl_18.se1`, `semo_18.se1`, sweph 2.10.3); the festival and 2026 vivah
method notes name the library's Moshier mode. For calendar work at the
resolution of a day the two agree.

**Zodiac.** Sidereal, with the Lahiri (Chitrapaksha) ayanamsa, the one
adopted for India's national calendar. Rahu is the mean node; Ketu is Rahu
plus 180 degrees.

**Reference locations.** National tables use Ujjain (23.1765 N, 75.7885 E),
the classical reference meridian of Indian astronomy. Griha pravesh 2027 is
also computed for New Delhi (28.6139 N, 77.2090 E), because many published
almanac pages are drawn up for New Delhi. The Wedding Season Index uses ten
city-centre coordinates, listed in its CSV. All times are Indian Standard
Time (UTC+05:30), and every row carries `timezone = Asia/Kolkata`.

**Day rule.** A civil day is read at that location's sunrise, using the
centre of the Sun's disc, which is the panchang convention. The tithi,
nakshatra and yoga printed for a day are the ones running at local sunrise.
A seasonal pause excludes a day if any part of it, from sunrise to the next
sunrise, falls inside the pause.

**Instants are not local times.** A sankranti, ingress or station is a
single astronomical moment. It is shown in IST for convenience and is the
same moment in every city. Which civil days a panchang then marks as Kharmas
depends on its sunrise rule; the engine's day-level dates are in
`griha_pravesh_2027_excluded_seasons.csv`. Ingress and station instants were
found by sampling daily at 00:00 IST and bisecting to well under a minute,
and each crossing was verified one minute either side.

### Festivals

1. The engine computed the panchang for every day of the window at Ujjain:
   tithi, paksha, nakshatra and the Sun's sidereal sign.
2. A calendar layer named each lunar month by the amanta rule (the month is
   named by the sankranti that falls inside the lunation) and detected
   intercalary months. The scan from December 2025 to January 2029 finds one:
   Adhika Jyeshtha 2026, about 17 May to 15 June 2026. 2027 and 2028 have no
   adhik maas, which is why their festivals sit about eleven days earlier
   each year while 2026's summer and autumn festivals sit about a lunar month
   later than in a common year.
3. Each festival has a classical rule: a lunar month, paksha and tithi, plus
   the ritual hour (nirnaya) that decides which civil day carries it. Sunrise
   for most vratas, pratahkala for Hartalika Teej, madhyahna for Ganesh
   Chaturthi, aparahna for Vijayadashami, pradosh for Dhanteras, Diwali,
   Chhath and Datta Jayanti, nishita for Maha Shivaratri, moonrise for Karva
   Chauth, and the Sun's sidereal ingress for the sankranti festivals. The
   rule for every festival is in the CSV.
4. The rule set was calibrated against the 2026 table, which was checked
   against the mainstream all-India almanac. Every rule reproduces the
   published 2026 date, so 2027 and 2028 are the same method applied to new
   years. Vidhata's test suite re-derives every date from the engine and
   fails if any drifts.

**Amanta and purnimanta.** The engine names months amanta (new moon to new
moon). Most North Indian almanacs name dark-fortnight festivals by the
purnimanta month, which is one month later for Krishna paksha. So "Diwali is
Kartika Krishna Amavasya" (purnimanta) and "Diwali is Ashwin Amavasya"
(amanta) describe the same night. The CSV gives both names.

**Conventions and rulings worth knowing**

- **Govardhan Puja 2026 is 10 November**, not the day after Diwali. It is
  dated by the udaya rule: the day on whose sunrise Kartika Shukla Pratipada
  is running. That is a Vidhata ruling of 25 October 2026, matching the Drik
  Panchang convention. The pratipada begins about 12:31 IST on 9 November and
  first holds a sunrise on 10 November.
- **Dhanteras 2026 is 6 November.** It is pradosh-vyapini: the trayodashi has
  to be running at sunset. Taking the tithi at sunrise would give 7 November.
- **Makar Sankranti 2027 is 15 January.** The Sun enters sidereal Makara at
  21:10 IST on 14 January, after sunset, so the punya kaal moves to the next
  sunrise. In 2028 it is 15 January again, but because the ingress (03:24 IST)
  falls before that day's sunrise.
- **Diwali 2027 is 29 October.** The amavasya runs 20:48 IST on 28 October
  to 19:06 IST on 29 October, so it fills only the 29 October pradosh window.
- **Sharad Navaratri 2027** begins 30 September on a kshaya pratipada that
  touches no sunrise; the day is chosen by the madhyahna fallback.
- **Ritual hour against sunrise.** Several dates follow the ritual-hour rule
  where a sunrise-only almanac prints a different day: Maha Shivaratri 2027
  and 2028, Dussehra 2027 and 2028, Karva Chauth 2027, Diwali 2028 and
  Baisakhi 2028. The `year_note` column says so on each row.
- **Vishu is pinned, not derived.** Kerala's Medam 1 reckoning has no rule
  that has been ruled on, so the Vishu dates follow the day-after-sankranti
  pattern of the checked 2026 entry (`derivation_status =
  pinned_not_derived`). For 2028 every candidate rule gives 14 April.
- **Hartalika Teej 2028 has no date.** Bhadrapada Shukla Tritiya 2028 runs
  08:44 IST on 22 August to 05:10 IST on 23 August at Ujjain, so it touches
  neither a pratahkala nor a sunrise. Which day carries a tithi of this shape
  is a nirnaya question that has not been ruled on, so the row is present
  with an empty date (`derivation_status = no_date_published`) rather than a
  guessed one.
- **Dhanteras 2028** (16 October) is the one row where the engine's single
  pradosh sample decides the day. A strict pradosh-vyapini almanac could
  argue for 15 October. Check it against your almanac.

### Griha pravesh 2027

A day is listed only when all of these hold at local sunrise:

- the Moon is in a griha pravesh nakshatra: Rohini, Mrigashira, Pushya,
  Hasta, Anuradha, Revati, Uttara Phalguni, Uttara Ashadha or Uttara
  Bhadrapada;
- no avoided nakshatra (Bharani, Krittika, Ashlesha, Magha, Vishakha), no
  avoided tithi (Chaturthi, Ashtami, Navami, Chaturdashi of either paksha,
  or Amavasya), no inauspicious yoga, no Vishti (Bhadra) karana;
- not a Sunday, Tuesday or Saturday;
- outside every seasonal exclusion: Kharmas (Sun in Dhanu), Malmas (Sun in
  Meena), Chaturmas, adhik and kshaya maas, and Shukra or Guru asta (Venus or
  Jupiter combust) with three days of margin either side.

Some almanacs also restrict griha pravesh to six lunar months. This dataset
does not, so on that axis it lists more days than they do.

### Wedding days (Wedding Season Index and the 2026 report)

The same filter, with the marriage rules, which are the classical vivaha
rules of the Muhurta Chintamani:

- the Moon in one of eleven vivaha nakshatras: Rohini, Mrigashira, Magha,
  Uttara Phalguni, Hasta, Swati, Anuradha, Mula, Uttara Ashadha, Uttara
  Bhadrapada and Revati;
- no avoided nakshatra (Bharani, Krittika, Ashlesha, Vishakha, Jyeshtha), no
  avoided tithi (Chaturthi, Shashthi, Ashtami, Navami, Dwadashi, Chaturdashi,
  Purnima, Amavasya), no inauspicious yoga, no Vishti karana;
- not a Tuesday or Saturday;
- outside Chaturmas, Kharmas, Malmas, adhik maas, Venus or Jupiter
  combustion, and outside the solar months that bar weddings (Sun in Karka,
  Simha or Kanya).

When the seasonal layer was built, its boundaries were checked against the
published 2026 and 2027 New Delhi vivah pages of Drik Panchang, and every
Kharmas, Malmas, Chaturmas and adhik maas boundary day matched.

**Why published lists disagree.** Online wedding date lists for the same
season differ by a factor of about three. Most of that is not error: each
list applies a different subset of the same rules. The `rule_tiers` files
show it with numbers. For New Delhi, November 2026 to June 2027: 96 days have
the Moon in a wedding nakshatra; 64 remain once the seasonal pauses are
applied; 25 once tithi, yoga and karana are checked; 19 once Tuesday and
Saturday are removed. A list near 96 has probably checked the nakshatra
alone. None of these is the one true answer. A family that follows a
particular pandit should follow that pandit's rules.

**Why cities differ.** Each city is read at its own sunrise. Kolkata sees
sunrise between half an hour and an hour before Delhi, so on 31 January 2027
the Navami tithi is still running at Kolkata sunrise, and on 21 June 2027 the
Moon is still in Purva Ashadha. Kolkata has 17 days; the other nine cities
have 19.

## Caveats

- **Venus combustion orb.** The engine uses a fixed angular distance from
  the Sun for asta: 10 degrees for Venus direct, 8 degrees for Venus
  retrograde, 11 degrees for Jupiter (BPHS and Phaladeepika). Around a
  superior conjunction this runs wider than the visibility dates some
  almanacs use, including Drik Panchang. The engine drops 6 and 20 February
  2026 for Venus; the almanac's Venus had already risen and lists both. The
  2026 vivah report keeps those two days, so it publishes 13 days where the
  strict engine filter gives 11. They are flagged with
  `engine_strict_pass = false` in `vivah_muhurat_2026_days.csv`.
- **Combustion in 2027.** By the fixed orb the next Venus combustion window,
  margin included, opens on 4 July 2027. Almanacs that go by visibility start
  it later in July.
- **Regional rules not applied.** Holashtak in North India, Guru in Simha
  and similar regional bars are not used.
- **A tithi festival can be kept a day apart by longitude.** The tithi at the
  ritual hour shifts with location, so Chennai and Delhi can observe the same
  festival a day apart. The festival table is a national reference; a local
  panchang is the authority for its own city.
- **Strict counts.** The wedding and griha pravesh lists are the
  conservative, all-rules-agree count. Lists that relax one limb, such as
  accepting Dwadashi or not keeping Chaturmas, run higher.
- **A day is a candidate, not a muhurat.** No lagna (exact ceremony time) is
  fixed, and no birth chart is consulted. The final muhurat depends on the
  people involved. Vidhata's [muhurat tools](https://vidhata.app/muhurat/marriage)
  compute windows for a given city and chart.
- The 2026 prohibited-window ranges in
  `vivah_muhurat_2026_prohibited_windows.csv` are given as text, as
  published, because several span two separate stretches.

## Column dictionary

Common columns: `latitude` and `longitude` are decimal degrees (north and
east positive). `timezone` is always `Asia/Kolkata` (IST, UTC+05:30). Dates
are ISO 8601 (`YYYY-MM-DD`) civil dates at that location. `ist_date` and
`ist_time` give an instant in IST; `utc_instant` gives the same instant in
UTC (`YYYY-MM-DDTHH:MMZ`), rounded to the minute. Booleans are `true` or
`false`. Empty cells mean "not applicable".

### hindu_festivals_2026_2028.csv

| Column | Meaning |
|---|---|
| `year` | Calendar year |
| `date` | Date of observance; empty only for Hartalika Teej 2028 |
| `weekday` | Day of the week for `date` |
| `festival_slug` | Stable identifier, same across years |
| `festival_name` | English name |
| `also_known_as` | Regional names, where they differ |
| `rule_type` | `lunar` (month, paksha, tithi), `sankranti` (solar ingress), `nakshatra`, `offset` (days from another festival) or `pinned` |
| `lunar_month_amanta` | Lunar month in the amanta convention, as the engine names it (Ashwin, Kartik, Margashira and so on) |
| `lunar_month_purnimanta` | The same month in the purnimanta convention (differs only for Krishna paksha) |
| `paksha` | Shukla or Krishna |
| `tithi_in_paksha` | 1 to 15 within the paksha; 15 is Purnima (Shukla) or Amavasya (Krishna) |
| `tithi_name` | Name of that tithi |
| `ritual_hour` | The moment at which the tithi must be running for the day to carry the festival |
| `fallback_hour` | Moment used when the tithi is absent at `ritual_hour` on every candidate day |
| `solar_sign` | Sidereal sign of the Sun for sankranti and nakshatra rules |
| `nakshatra` | Moon's nakshatra for nakshatra rules (Onam) |
| `offset_from_slug`, `offset_days` | For offset rules: the anchor festival and the day offset |
| `rule_basis` | The rule in words |
| `year_note` | What decided the day in this particular year, where it is not routine |
| `derivation_status` | `engine_derived`, `pinned_not_derived` (Vishu) or `no_date_published` |
| `reference_location` | Ujjain |
| `significance` | One-sentence description of the festival |

### griha_pravesh_2027_days.csv

`location_slug`, `location_name`, `latitude`, `longitude`, `timezone`;
`date`; `weekday`; `tithi` (paksha and tithi at local sunrise, for example
"Shukla Saptami"); `paksha`; `nakshatra` (Moon's nakshatra at local sunrise);
`read_at` (always "local sunrise").

### griha_pravesh_2027_monthly_counts.csv

Location columns; `month` (`YYYY-MM`); `clean_day_count` (days in that month
that pass every rule; months with none are listed with 0).

### griha_pravesh_2027_rule_tiers.csv and wedding_days_rule_tiers_by_city.csv

Location or city columns; `tier_order` (1 to 4); `tier_code`
(`nakshatraOnly`, `plusSeasons`, `plusTithiYogaKarana`, `strict`);
`tier_rule` (what the tier adds); `day_count` (days passing every rule up to
and including this tier); `period_start`, `period_end` (the range scanned).
Each tier includes all the rules of the tiers before it, so `strict` equals
the number of listed days.

### griha_pravesh_2027_excluded_seasons.csv

Location columns; `season_code` (`kharmas`, `malmas`, `shukra_asta`,
`guru_asta`, `chaturmas`); `from_date`, `to_date` (first and last civil day
excluded, inclusive); `reason`. The scan runs from November 2026 to January
2028, so seasons that straddle a year boundary show their true ends.

### chaturmas_ekadashis_2027.csv

Location columns; `ekadashi` (`devshayani` opens Chaturmas, `prabodhini`
closes it); `date`; `lunar_month_amanta`; `kshaya` (whether the ekadashi
touches no sunrise).

### planetary_ingresses_2027.csv

`planet`; `from_sign`, `to_sign` (sidereal, Sanskrit and English name);
`from_sign_number`, `to_sign_number` (1 = Mesha to 12 = Meena); `retrograde`
(planet's motion at the crossing; Rahu and Ketu are always retrograde);
`ist_date`, `ist_time`, `utc_instant`; `context` (`previous_before_2027`,
`during_2027`, `next_after_2027`).

### planetary_stations_2027.csv

`planet`; `station` (`retrograde` or `direct`); `sign`; `degree_in_sign`
(sidereal degrees within the sign); `ist_date`, `ist_time`, `utc_instant`.

### planet_signs_2027_year_boundaries.csv

`boundary` (`start_of_2027` or `end_of_2027`); `planet`; `at_ist` (sample
instant); `sign`; `degree_in_sign`; `retrograde`.

### sun_sankrantis_dec2026_jan2028.csv

`sign` (sidereal sign the Sun enters); `sign_number`; `ist_date`, `ist_time`,
`utc_instant`.

### kharmas_malmas_instants_2026_2028.csv

`period` (`kharmas_2026_27`, `malmas_2027`, `kharmas_2027_28`); `kind`
(`kharmas` or `malmas`); `event` (`sunEntersDhanu`, `sunEntersMakara`,
`sunEntersMeena`, `sunEntersMesha`); `ist_date`, `ist_time`, `utc_instant`.

### wedding_days_by_city_2026_11_to_2027_06.csv

`city_slug`, `city_name`, `latitude`, `longitude`, `timezone`; `date`;
`weekday`; `tithi`; `paksha`; `nakshatra`; `read_at` (always "local sunrise").

### wedding_days_monthly_counts_by_city.csv

City columns; `month` (`YYYY-MM`); `wedding_day_count`.

### wedding_season_pauses_2026_11_to_2027_07.csv

`pause_code` (`chaturmas`, `shukra_asta`, `kharmas`, `malmas`,
`vivah_solar_month`); `from_date`, `to_date` (inclusive); `days_inclusive`;
`reason`; `scan_start`, `scan_end` (2026-11-01 to 2027-07-31);
`clipped_by_scan` (true when the pause continues beyond the scan, so its
true start or end lies outside the shown range).

### wedding_days_city_differences_vs_new_delhi.csv

City columns; `difference` (`lost_vs_new_delhi` or `gained_vs_new_delhi`);
`date`; `nakshatra` and `tithi` at that city's sunrise; `local_warnings`
(the rule that fails locally, if it is a tithi, yoga, karana or weekday rule;
empty when the cause is the nakshatra).

### vivah_muhurat_2026_days.csv

`date`; `weekday`; `nakshatra`; `engine_strict_pass` (false for the two days
kept against the engine's Venus orb, see Caveats); `note`; location columns
(Ujjain).

### vivah_muhurat_2026_monthly_counts.csv

`year`; `month` (1 to 12); `month_name`; `wedding_day_count`; `note`;
`reference_location`.

### vivah_muhurat_2026_prohibited_windows.csv

`window_name`; `date_range_text` (as published); `reason`.

## Updates

The dataset is refreshed once a year, when the next year's festival table and
muhurat data are computed, and whenever a published date is corrected. Each
release is tagged with the date it was generated. This release: 10 November
2026.

## How to cite

> Vidhata (2026). *Hindu Calendar and Muhurat Data 2026-2028 (computed,
> Vidhata)*. Computed with the Vidhata panchang engine.
> https://vidhata.app. Dataset:
> https://github.com/ranjanravi85-personal/vidhata-hindu-calendar-data
> (also at https://www.kaggle.com/datasets/ranjanravi1/hindu-calendar-muhurat-2026-2028).
> Licensed CC BY 4.0.

BibTeX:

```bibtex
@misc{vidhata_hindu_calendar_2026,
  author       = {{Vidhata}},
  title        = {Hindu Calendar and Muhurat Data 2026-2028 (computed, Vidhata)},
  year         = {2026},
  howpublished = {\url{https://github.com/ranjanravi85-personal/vidhata-hindu-calendar-data}},
  note         = {Computed with the Vidhata panchang engine, https://vidhata.app. CC BY 4.0}
}
```

A short credit is fine in running text: "Source: Vidhata (vidhata.app)".

## License

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).
See `LICENSE`. Contact: contact@vidhata.app.
