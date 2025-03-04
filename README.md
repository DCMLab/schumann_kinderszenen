![Version](https://img.shields.io/github/v/release/DCMLab/schumann_kinderszenen?display_name=tag)
[![DOI](https://zenodo.org/badge/379600931.svg)](https://doi.org/10.5281/zenodo.7473582)
![GitHub repo size](https://img.shields.io/github/repo-size/DCMLab/schumann_kinderszenen)
![License](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-9cf)


This is a README file for a data repository originating from the [DCML corpus initiative](https://github.com/DCMLab/dcml_corpora)
and serves as welcome page for both 

* the GitHub repo [https://github.com/DCMLab/schumann_kinderszenen](https://github.com/DCMLab/schumann_kinderszenen) and the corresponding
* documentation page [https://dcmlab.github.io/schumann_kinderszenen](https://dcmlab.github.io/schumann_kinderszenen)

For information on how to obtain and use the dataset, please refer to [this documentation page](https://dcmlab.github.io/schumann_kinderszenen/introduction).

# Robert Schumann – Kinderszenen (A corpus of annotated scores)


## Getting the data

* download repository as a [ZIP file](https://github.com/DCMLab/schumann_kinderszenen/archive/main.zip)
* download a [Frictionless Datapackage](https://specs.frictionlessdata.io/data-package/) that includes concatenations
  of the TSV files in the four folders (`measures`, `notes`, `chords`, and `harmonies`) and a JSON descriptor:
  * [schumann_kinderszenen.zip](https://github.com/DCMLab/schumann_kinderszenen/releases/latest/download/schumann_kinderszenen.zip)
  * [schumann_kinderszenen.datapackage.json](https://github.com/DCMLab/schumann_kinderszenen/releases/latest/download/schumann_kinderszenen.datapackage.json)
* clone the repo: `git clone https://github.com/DCMLab/schumann_kinderszenen.git` 


## Data Formats

Each piece in this corpus is represented by five files with identical name prefixes, each in its own folder. 
For example, the first piece has the following files:

* `MS3/n01.mscx`: Uncompressed MuseScore 3.6.2 file including the music and annotation labels.
* `notes/n01.notes.tsv`: A table of all note heads contained in the score and their relevant features (not each of them represents an onset, some are tied together)
* `measures/n01.measures.tsv`: A table with relevant information about the measures in the score.
* `chords/n01.chords.tsv`: A table containing layer-wise unique onset positions with the musical markup (such as dynamics, articulation, lyrics, figured bass, etc.).
* `harmonies/n01.harmonies.tsv`: A table of the included harmony labels (including cadences and phrases) with their positions in the score.

Each TSV file comes with its own JSON descriptor that describes the meanings and datatypes of the columns ("fields") it contains,
follows the [Frictionless specification](https://specs.frictionlessdata.io/tabular-data-resource/),
and can be used to validate and correctly load the described file. 

### Opening Scores

After navigating to your local copy, you can open the scores in the folder `MS3` with the free and open source score
editor [MuseScore](https://musescore.org). Please note that the scores have been edited, annotated and tested with
[MuseScore 3.6.2](https://github.com/musescore/MuseScore/releases/tag/v3.6.2). 
MuseScore 4 has since been released which renders them correctly but cannot store them back in the same format.

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
`pip install -U ms3` (requires Python 3.10 or later) you'll be able to load any TSV like this:

```python
import ms3

labels = ms3.load_tsv("harmonies/n01.harmonies.tsv")
notes = ms3.load_tsv("notes/n01.notes.tsv"")
```


## Version history

See the [GitHub releases](https://github.com/DCMLab/schumann_kinderszenen/releases).

## Questions, Suggestions, Corrections, Bug Reports

Please [create an issue](https://github.com/DCMLab/schumann_kinderszenen/issues) and/or feel free to fork and submit pull requests.

## Cite as

> Hentschel, J., Rammos, Y., Neuwirth, M., Moss, F. C., & Rohrmeier, M. (2024). An annotated corpus of tonal piano music from the long 19th century. Empirical Musicology Review, 18(1), 84–95. https://doi.org/10.18061/emr.v18i1.8903

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
