# cccedict

## Demo
Download the current CC-CEDICT file from http://www.mdbg.net/chindict/chindict.php?page=cc-cedict into the demo folder.

```
cd demo
wget -O cedict.gz http://www.mdbg.net/chindict/export/cedict/cedict_1_0_ts_utf-8_mdbg.txt.gz
php -f index.php
```

## About
Reads from a CC-CEDICT Chinese dictionary file, and outputs structured data.

## Options

### Required settings
- setFilePath(string) sets path of file to extract and process

### Optional settings
- setBlockSize(int) sets block size to read and parse at a time
- setStartLine(int) in case you don't want to start from the beginning
- setNumberOfBlocks(float) in case you don't want to read all the way to the end. You can use INF.
- setOptions(array) define which data you want returned (see below)

## Returned data
The parser will return an array with:
- an array of Entry objects filled with data as per your configuration (see below)
- an array of any skipped lines
- the number of parsed lines
- the number of skipped lines

### Customising the Entry object
In most cases, a full Entry object will be more than you need, so you can use the `setOptions(array)` command (see above) to specify the fields that you want the parser to return with each Entry object. Any non-specified fields will not be included. Below are the available options:
- `Entry::F_ORIGINAL` includes the original unparsed line from CC-CEDICT
- `Entry::F_TRADITIONAL` includes a string with the dictionary entry in traditional characters
- `Entry::F_TRADITIONAL_CHARS` includes an array of all traditional characters in the dictionary entry
- `Entry::F_SIMPLIFIED` same as above but in simplified characters
- `Entry::F_SIMPLIFIED_CHARS` same as above but with simplified characters
- `Entry::F_PINYIN` includes a string of pinyin as formatted in CC-CEDICT (numeric but with ideosyncrasies)
- `Entry::F_PINYIN_DIACRITIC` includes a string of pinyin converted to Hanyu Pinyin with diacritics
- `Entry::F_PINYIN_DIACRITIC_EXPANDED` returns the above as an array rather than a string
- `Entry::F_PINYIN_NUMERIC` includes a string of pinyin converted to numeric Hanyu Pinyin
- `Entry::F_PINYIN_NUMERIC_EXPANDED` returns the above as an array rather than a string
- `Entry::F_ENGLISH` includes a string with all the English translations for the dictionary entry
- `Entry::F_ENGLISH_EXPANDED` includes an array with the above English translations

## Limitations, bugs, roadmap

### Opportunities for improvement
- Perhaps it could output various formats (e.g. JSON) instead of arrays
- Any further Chinese in the English translation (references, alternative spellings, or full forms of abbreviations) could be structured and nested
