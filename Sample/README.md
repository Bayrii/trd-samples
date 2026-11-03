# TRD: English Temporal Reasoning Samples

**270 generated records | Nine task types | 30 records per JSON file**

These samples were generated from the local copy of [Temporal Reasoning Dataset (TRD)](https://github.com/amazon-science/temporal-reasoning-dataset), version 1.0.0, commit `848ebed461ad4fcccf182fd43b3bc9b1fd8e9b11`. They remain in English and are prepared for later Azerbaijani translation.

## Generation and folders

To reproduce these files using the upstream TRD generator:

```bash
trd generate variations --samples 30 --languages en_US --format json --seed 9 --output ./Sample
```

Generation used the local source module, `python -m trd.cli`, with the same settings. The outputs are saved in this repository's `Sample/` folder. `--samples 30` means 30 records per task, producing 270 records in total at the generator's medium difficulty.

The generator initially writes nine files directly inside `variations/`. Each file was then moved into its matching task folder. Filenames, record order and file contents were preserved. Every JSON file is an array of objects with string fields `question` and `answer`.

| Dataset file | Records | TRD task | Corresponding project task: number and name |
|---|---:|---|---|
| [date_addition](variations/date_addition/date_addition_medium_en_US.json) | 30 | Add a stated number of days to a date. | **2.2 — Resolving Relative and Implicit Time References** |
| [date_subtraction](variations/date_subtraction/date_subtraction_medium_en_US.json) | 30 | Subtract a stated number of days from a date. | **2.2 — Resolving Relative and Implicit Time References** |
| [time_addition](variations/time_addition/time_addition_medium_en_US.json) | 30 | Add hours and minutes to a clock time. | **2.2 — Resolving Relative and Implicit Time References**; **5 — Modeling Time Intervals and Duration** |
| [time_subtraction](variations/time_subtraction/time_subtraction_medium_en_US.json) | 30 | Subtract hours and minutes from a clock time. | **2.2 — Resolving Relative and Implicit Time References**; **5 — Modeling Time Intervals and Duration** |
| [date_duration](variations/date_duration/date_duration_medium_en_US.json) | 30 | Calculate elapsed days between dates. | **5 — Modeling Time Intervals and Duration** |
| [time_duration](variations/time_duration/time_duration_medium_en_US.json) | 30 | Calculate elapsed minutes between clock times. | **5 — Modeling Time Intervals and Duration** |
| [date_recurrence](variations/date_recurrence/date_recurrence_medium_en_US.json) | 30 | Find a numbered occurrence in a repeating schedule. | **2.2 — Resolving Relative and Implicit Time References**; supporting schedule arithmetic for **17 — Recurrence and Frequency Analysis**. |
| [interval_date](variations/interval_date/interval_date_medium_en_US.json) | 30 | Find the Monday and Sunday of next week. | **2.2 — Resolving Relative and Implicit Time References**; **5 — Modeling Time Intervals and Duration** |
| [day_of_week](variations/day_of_week/day_of_week_medium_en_US.json) | 30 | Identify a date's weekday. | No direct test match; supporting calendar knowledge for **3 — Time Zone and Calendar Normalization**. |
| **Total** | **270** | | |

Project task numbers and names come from Section 5 of the supplied `Temporal Correlation Benchmark.pdf`. The mapping above is our proposed use of TRD samples, not a claim of full task coverage. Task 2.2 also requires choosing the correct reference and handling missing references; task 5 includes interval boundaries and unknown durations. Those cases need additional examples. The recurrence samples do not test task 17's raw-record counts, unique-event counts or observed frequencies. Weekday identification does not test task 3's time-zone or calendar normalization.

## Review for Azerbaijani translation

All nine templates describe neutral calendar or clock situations. They contain no personal names, places, institutions or culture-specific histories requiring localization. No entities, sentences, dates, numbers or answers were changed, and nothing was translated.

All 270 answers were independently recalculated from the question text. JSON syntax, field types, file placement and record counts passed validation. There are no duplicate questions within or across these nine files.

Preserve these conventions during later translation and evaluation:

- Dates use the Gregorian calendar and `YYYY-MM-DD`; clock times use 24-hour `HH:MM` notation. Clock arithmetic wraps at midnight.
- Date durations count elapsed days, using end date minus start date, rather than counting both endpoint dates.
- Clock durations assume less than 24 hours elapsed. Record 10 in `time_duration` (zero-based index) goes from `23:20` to `01:08`, with answer `108` minutes. Dates are absent, so this assumption must be stated in evaluation instructions.
- Recurrence questions exclude today: occurrence number multiplied by the interval gives the days to add. The source wording, such as "the 2 occurrence", is awkward but retains its intended meaning and was preserved.
- Next week runs from Monday through Sunday, as explicitly stated in each interval question. Weekday answers and the range connector `to` remain English.

These samples are suitable drafts for translation under those conventions. Translation and language review remain to be done. They test calendar and clock reasoning; they do not provide record updates, tool execution or independent development/test splits. Group related templates and scenarios before creating splits.

## Source and license

TRD is by Vittorio Mazzia, Sandro Pollastrini, Davide Bernardi, Chiara Rubagotti and Daniele Amberti. See the [authors' repository](https://github.com/amazon-science/temporal-reasoning-dataset) and its paper reference. The source [CC BY-NC 4.0 license](https://github.com/amazon-science/temporal-reasoning-dataset/blob/848ebed461ad4fcccf182fd43b3bc9b1fd8e9b11/LICENSE) is available upstream.
