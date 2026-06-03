[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.nm000228-blue)](https://doi.org/10.82901/nemar.nm000228)

Nieuwland et al. 2018: Multi-site N400 Replication Study
==========================================================

Overview
--------
This is a large-scale (N=356) multi-laboratory replication of DeLong, Urbach &
Kutas (2005), testing whether readers pre-activate the phonological form of
upcoming nouns during sentence comprehension. Participants read sentences
word-by-word (RSVP, 2 words per second) that contained indefinite articles
(a/an) preceding either highly expected or unexpected nouns (based on cloze
probability), while EEG was recorded.

Nine laboratories in the UK collected data following a pre-registered
replication protocol (https://osf.io/eyzaq). The original study by DeLong et
al. reported N400-like effects on the indefinite articles (larger negativity
for unexpected articles). Nieuwland et al. found reliable N400 effects on the
target nouns but no statistically significant effect on the preceding
articles, challenging strong prediction accounts.

Participants
------------
- 356 total participants (222 women / 134 men)
- All right-handed, native English speakers
- Age 18–35 years (mean 19.8)
- Normal or corrected-to-normal vision
- Free from known language or learning disorders
- 89 reported a left-handed parent or sibling

After applying the paper's quality threshold (<60/80 article or noun trials),
334 subjects were retained in the statistical analyses. In this BIDS release
we include ALL subjects for which raw data is available, with an
``included_in_paper`` flag in participants.tsv so users can filter themselves.

Laboratories
------------
| Lab (paper #) | Institution                | Format       | Sfreq    | Channels          |
|---------------|----------------------------|--------------|----------|-------------------|
| BIRM (1)      | University of Birmingham   | BrainVision  | 500 Hz   | 64 EEG            |
| BRIS (2)      | University of Bristol      | BrainVision  | 1000 Hz  | 32 EEG            |
| EDIN (3)      | University of Edinburgh    | BioSemi BDF  | 512 Hz   | 64 EEG + 8 EXG    |
| GLAS (4)      | University of Glasgow      | BioSemi BDF  | 512 Hz   | 128 EEG + 8 EXG   |
| KENT (5)      | University of Kent         | BrainVision  | 500 Hz   | 64 EEG + HEOG/VEOG|
| LOND (6)      | University College London  | BioSemi BDF  | 512 Hz   | 32 EEG + 8 EXG    |
| OXFO (7)      | University of Oxford       | BioSemi BDF  | 2048 Hz  | 64 EEG + 8 EXG    |
| STIR (8)      | University of Stirling     | Neuroscan CNT| 250 Hz   | 64 EEG + EOG      |
| YORK (9)      | University of York         | BrainVision  | 500 Hz   | 64 EEG + HEOG/VEOG|

Paradigm
--------
- Word-by-word RSVP: 200 ms word duration + 300 ms blank (2 words/sec)
- 80 Delong replication sentences + 80 control sentences
- Comprehension questions on a subset of trials (yes/no button response)
- Two counter-balanced stimulus lists (list 1 / list 2)

Tasks
-----
- ``task-delong``: Main experiment (all subjects, all labs)
- ``task-control``: Control grammaticality experiment (BRIS subjects, LOND 1-2)

Events (trial_type values)
--------------------------
Delong experiment:
  a_expected        — article "a", expected (high cloze) context
  an_expected       — article "an", expected (high cloze) context
  a_unexpected      — article "a", unexpected (low cloze) context
  an_unexpected     — article "an", unexpected (low cloze) context
  noun_expected     — target noun, expected condition
  noun_unexpected   — target noun, unexpected condition
  final_expected    — sentence-final word, expected condition
  final_unexpected  — sentence-final word, unexpected condition

Control experiment:
  control_correct   — grammatically correct article
  control_incorrect — grammatically incorrect article

General:
  cloze_marker      — cloze probability marker (trigger 1-100 or 200)
  item_marker       — stimulus item marker (trigger 101-180)
  question          — comprehension question onset
  filler_word       — any other (non-critical) word in sentence
  unknown_trigger   — trigger code not matched to any known category

Event enrichment
----------------
Each event in ``events.tsv`` is enriched (when applicable) with:
  - sequence_id, item_number, list, task_type, condition
  - expected_article / unexpected_article (a or an)
  - expected_noun / unexpected_noun (strings)
  - expected_cloze / unexpected_cloze (0-100)
  - plausibility_expected / plausibility_unexpected (1-7 Likert)
  - sentence_context / sentence_ending (strings)
  - has_question, question_text, question_answer

These come from the authors' REPLICATION_ITEMS.xlsx file on OSF.

participants.tsv columns
------------------------
  participant_id         — sub-<lab><num>
  lab                    — birm/bris/edin/glas/kent/lond/oxfo/stir/york
  lab_number             — 1-9 (paper's numbering)
  institution            — full institution name
  list                   — stimulus list (1 or 2)
  accuracy               — % correct on comprehension questions (from OSF)
  n_article_trials       — article trials kept (out of 80)
  n_noun_trials          — noun trials kept (out of 80)
  included_in_paper      — True if >=60/80 trials (paper's threshold)
  exclusion_note         — e.g. "random_answers", "non_native", "low_trials"
  hand                   — R (all right-handed)
  age_range              — 18-35 (all participants)
  native_language        — English (all participants)
  recording_system       — manufacturer + model

Notes
-----
- Original raw data is kept — no filtering, no resampling, no artifact rejection
- Channel types: EEG, EOG, and misc (peripheral) channels are labeled
- For BDF labs, channels EXG1-8, GSR1/2, Erg1/2, Resp, Plet, Temp are marked misc
- GLAS has a 128-channel BioSemi montage (biosemi128)
- STIR data is read with a custom Neuroscan CNT parser (MNE's built-in
  reader has a bug with the corrupted total_samples header field)
- OXFO has 3 subjects recorded with BrainVision instead of BDF

Reference
---------
Nieuwland, M.S., Politzer-Ahles, S., Heyselaar, E., Segaert, K., Darley, E.,
Kazanina, N., ..., Huettig, F. (2018). Large-scale replication study reveals
a limit on probabilistic prediction in language comprehension. eLife, 7,
e33468. https://doi.org/10.7554/eLife.33468


References
----------
Appelhoff, S., Sanderson, M., Brooks, T., Vliet, M., Quentin, R., Holdgraf, C., Chaumon, M., Mikulan, E., Tavabi, K., Höchenberger, R., Welke, D., Brunner, C., Rockhill, A., Larson, E., Gramfort, A. and Jas, M. (2019). MNE-BIDS: Organizing electrophysiological data into the BIDS format and facilitating their analysis. Journal of Open Source Software 4: (1896).https://doi.org/10.21105/joss.01896

Pernet, C. R., Appelhoff, S., Gorgolewski, K. J., Flandin, G., Phillips, C., Delorme, A., Oostenveld, R. (2019). EEG-BIDS, an extension to the brain imaging data structure for electroencephalography. Scientific Data, 6, 103.https://doi.org/10.1038/s41597-019-0104-8

