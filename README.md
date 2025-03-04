![Version](https://img.shields.io/github/v/release/DCMLab/schumann_kinderszenen?display_name=tag)
[![DOI](https://zenodo.org/badge/379600931.svg)](https://zenodo.org/badge/latestdoi/379600931)
![GitHub repo size](https://img.shields.io/github/repo-size/DCMLab/schumann_kinderszenen)
![License](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-9cf)


This is a README file for a data repository originating from the [DCML corpus initiative](https://github.com/DCMLab/dcml_corpora)
and serves as welcome page for both 

* the GitHub repo [https://github.com/DCMLab/schumann_kinderszenen](https://github.com/DCMLab/schumann_kinderszenen) and the corresponding
* documentation page [https://dcmlab.github.io/schumann_kinderszenen](https://dcmlab.github.io/schumann_kinderszenen)

For information on how to obtain and use the dataset, please refer to [this documentation page](https://dcmlab.github.io/schumann_kinderszenen/introduction).



<!-- TOC -->
* [Robert Schumann - Kinderszenen (A corpus of annotated scores)](#robert-schumann---kinderszenen-a-corpus-of-annotated-scores)
  * [Version history](#version-history)
  * [Getting the data](#getting-the-data)
    * [With full version history](#with-full-version-history)
    * [Without full version history](#without-full-version-history)
  * [Data Formats](#data-formats)
    * [Opening Scores](#opening-scores)
    * [Opening TSV files in a spreadsheet](#opening-tsv-files-in-a-spreadsheet)
    * [Loading TSV files in Python](#loading-tsv-files-in-python)
  * [How to read `metadata.tsv`](#how-to-read-metadatatsv)
    * [File information](#file-information)
    * [Composition information](#composition-information)
    * [Score information](#score-information)
    * [Identifiers](#identifiers)
  * [Generating all TSV files from the scores](#generating-all-tsv-files-from-the-scores)
  * [Questions, Suggestions, Corrections, Bug Reports](#questions-suggestions-corrections-bug-reports)
  * [License](#license)
  * [File naming convention](#file-naming-convention)
  * [Overview](#overview)
<!-- TOC -->

# Robert Schumann - Kinderszenen (A corpus of annotated scores)

This corpus of annotated [MuseScore](https://musescore.org) files has been created within
the [DCML corpus initiative](https://github.com/DCMLab/dcml_corpora) and employs
the [DCML harmony annotation standard](https://github.com/DCMLab/standards). It is one out of nine similar corpora that
have been grouped together
to [An Annotated Corpus of Tonal Piano Music from the Long 19th Century](https://doi.org/10.5281/zenodo.7483349)
which comes with a data report that is currently in press at Empirical Musicology Review.

## Version history

See the [GitHub releases](https://github.com/DCMLab/schumann_kinderszenen/releases).

## Getting the data

### With full version history

The dataset is version-controlled via [git](https://git-scm.com/). In order to download the files with all
revisions they have gone through, git needs to be installed on your machine. Then you can clone this
repository using the command

```bash
git clone https://github.com/DCMLab/schumann_kinderszenen.git
```

### Without full version history

If you are only interested in the current version of the corpus, you can simply download and unpack
[this ZIP file](https://github.com/DCMLab/schumann_kinderszenen/archive/refs/heads/main.zip).

## Data Formats

Each piece in this corpus is represented by four files with identical names, each in its own folder. For example,
the first movement has the following files:

* `MS3/n01.mscx`: Uncompressed MuseScore file including the music and annotation labels.
* `notes/n01.tsv`: A table of all note heads contained in the score and their relevant features (not each of them
  represents an onset, some are tied together)
* `measures/n01.tsv`: A table with relevant information about the measures in the score.
* `harmonies/n01.tsv`: A list of the included harmony labels (including cadences and phrases) with their positions in
  the score.

### Opening Scores

After navigating to your local copy, you can open the scores in the folder `MS3` with the free and open source score
editor [MuseScore](https://musescore.org). Please note that the scores have been edited, annotated and tested with
[MuseScore 3.6.2](https://github.com/musescore/MuseScore/releases/tag/v3.6.2).
MuseScore 4 has since been released and preliminary tests suggest that it renders them correctly.

### Opening TSV files in a spreadsheet

Tab-separated value (TSV) files are like Comma-separated value (CSV) files and can be opened with most modern text
editors. However, for correctly displaying the columns, you might want to use a spreadsheet or an addon for your
favourite text editor. When you use a spreadsheet such as Excel, it might annoy you by interpreting fractions as
dates. This can be circumvented by using `Data --> From Text/CSV` or the free alternative
[LibreOffice Calc](https://www.libreoffice.org/download/download/). Other than that, TSV data can be loaded with
every modern programming language.

### Loading TSV files in Python

Since the TSV files contain null values, lists, fractions, and numbers that are to be treated as strings, you may want
to use this code to load any TSV files related to this repository (provided you're doing it in Python). After a quick
`pip install -U ms3` (requires Python 3.10) you'll be able to load any TSV like this:

```python
import ms3

labels = ms3.load_tsv('harmonies/n01.tsv')
notes = ms3.load_tsv('notes/n01.tsv')
```

## How to read `metadata.tsv`

This section explains the meaning of the columns contained in `metadata.tsv`.

### File information

| column                 | content                                                    |
|------------------------|------------------------------------------------------------|
| **fname**              | name without extension (for referencing related files)     |
| **rel_path**           | relative file path of the score, including extension       |
| **subdirectory**       | folder where the score is located                          |    
| **last_mn**            | last measure number                                        |
| **last_mn_unfolded**   | number of measures when playing all repeats                |
| **length_qb**          | length of the piece, measured in quarter notes             |
| **length_qb_unfolded** | length of the piece when playing all repeats               |
| **volta_mcs**          | measure counts of first and second endings                 |
| **all_notes_qb**       | summed up duration of all notes, measured in quarter notes |
| **n_onsets**           | number of note onsets                                      |
| **n_onset_positions**  | number of unique note onsets ("slices")                    |

### Composition information

| column             | content                   |
|--------------------|---------------------------|
| **composer**       | composer name             |
| **workTitle**      | work title                |
| **composed_start** | earliest composition date |
| **composed_end**   | latest composition date   |
| **workNumber**     | Catalogue number(s)       |
| **movementNumber** | 1, 2, or 3                |
| **movementTitle**  | title of the movement     |

### Score information

| column          | content                                                |
|-----------------|--------------------------------------------------------|
| **label_count** | number of chord labels                                 |
| **KeySig**      | key signature(s) (negative = flats, positive = sharps) |
| **TimeSig**     | time signature(s)                                      |
| **musescore**   | MuseScore version                                      |
| **source**      | URL to the first typesetter's file                     |
| **typesetter**  | first typesetter                                       |
| **annotators**  | creator(s) of the chord labels                         |
| **reviewers**   | reviewer(s) of the chord labels                        |

### Identifiers

These columns provide a mapping between multiple identifiers for the sonatas (not for individual movements).

| column          | content                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------|
| **wikidata**    | URL of the [WikiData](https://www.wikidata.org/) item                                                   |
| **viaf**        | URL of the Virtual International Authority File ([VIAF](http://viaf.org/)) entry                        |
| **musicbrainz** | [MusicBrainz](https://musicbrainz.org/) identifier                                                      |
| **imslp**       | URL to the wiki page within the International Music Score Library Project ([IMSLP](https://imslp.org/)) |

## Generating all TSV files from the scores

When you have made changes to the scores and want to update the TSV files accordingly, you can use the following
command (provided you have pip-installed [ms3](https://github.com/johentsch/ms3)):

```python
ms3
extract - M - N - X - D  # for measures, notes, expanded annotations, and metadata
```

If, in addition, you want to generate the reviewed scores with out-of-label notes colored in red, you can do

```python
ms3
review - M - N - X - D  # for extracting measures, notes, expanded annotations, and metadata
```

By adding the flag `-c` to the review command, it will additionally compare the (potentially modified) annotations in
the score
with the ones currently present in the harmonies TSV files and reflect the comparison in the reviewed scores.

## Questions, Suggestions, Corrections, Bug Reports

Please [create an issue](https://github.com/DCMLab/schumann_kinderszenen/issues) and/or feel free to fork and submit pull requests.

## License

Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License ([CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)).

![cc-by-nc-sa-image](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)

## File naming convention

The file names listed in the [Overview](#overview) below refer to the
[13 pieces contained in op. 15](https://imslp.org/wiki/Kinderszenen,_Op.15_(Schumann,_Robert)).

## Overview
|file_name|measures|labels|standard|              annotators              | reviewers  |
|---------|-------:|-----:|--------|--------------------------------------|------------|
|n01      |      22|    44|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei, JH|
|n02      |      40|   123|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei, JH|
|n03      |      31|    58|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei, JH|
|n04      |      17|    53|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei, JH|
|n05      |      16|    48|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei, JH|
|n06      |      24|    84|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n07      |      24|    71|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n08      |      32|    73|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n09      |      24|    46|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN. JHei    |
|n10      |      57|    67|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n11      |      48|   140|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n12      |      32|    92|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |
|n13      |      25|    49|2.3.0   |Tal Soker (2.1.1), John Heilig (2.3.0)|AN, JHei    |


*Overview table automatically updated using [ms3](https://ms3.readthedocs.io/).*
