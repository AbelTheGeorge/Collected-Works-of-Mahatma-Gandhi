# The Collected Works of Mahatma Gandhi

This repository contains a comprehensive JSON dataset of the "Collected Works of Mahatma Gandhi" (CWMG). It has been extracted from The Collected Works of Mahatma Gandhi (CWMG) project, a meticulous documentation initiative by the Government of India that ran from September 1956 to October 2, 1994. 
The dataset encompasses 98 volumes, featuring nearly 50,000 pages of text and over 45,000 individual documents, including letters, speeches, articles, and interviews.

## Dataset Overview

*   **Total Documents:** 45,458
*   **Total Volumes:** 98
*   **Dataset Size:** ~100 MB
*   **Format:** JSON

## Dataset Structure

The dataset is a single JSON file containing a list of objects, where each object represents a section or document.

### Schema

```json
[
  {
    "volume": "1",
    "section": "1",
    "document_type": "LETTER",
    "document_date": "09-01-1906",
    "title": "LETTER TO THE EDITOR, THE VEGETARIAN",
    "contents": "Main contents of the section. Footnote references in the contents are
                 present as numbers in curly brackets as follows {1} {2}.",
    "footnotes": {
      "1": "This is the footnote for reference {1}.",
      "2": "This is the footnote for reference {2}."
    },
    "original_language": "English",
    "source": "The Vegetarian, 19-2-1891; also C.W. 1 & S.N. 1"
  }
]
```

### Field Descriptions

| Field | Type | Description |
| :--- | :--- | :--- |
| `volume` | String | The volume number (1-98) in which the document appears. |
| `section` | String | The section number within the volume. |
| `document_type` | String | The category of the document. A hybrid strategy was used for classification: title parsing for explicit types and a Google Gemma 27B model for inference on ambiguous titles. |
| `document_date` | String | The date the document was produced, in `YYYY-MM-DD` format. For documents with uncertain dates, a bound is provided (e.g., `"Before 1923-04-12"` or `"After 1905-11-28"`). Note: 317 documents have an unknown date. |
| `title` | String | The title of the document as provided by the CWMG project. |
| `contents` | String | The main body of the text attributed to Mahatma Gandhi. Footnote references are embedded as `{1}`, `{2}`, etc. |
| `footnotes` | Object | A dictionary of footnotes provided by the CWMG editors for context. The keys correspond to the references in the `contents`. **Note:** Footnotes in the original text reset on each page; they have been re-indexed here to be unique within each document. |
| `original_language` | String | The language in which the document was originally written. All non-English documents were translated to English by the CWMG project while maintaining authenticity to the original|
| `source` | String | Information on where the original document was procured by the CWMG project. Note: 6,224 documents have a missing or unknown source. See the section below for an explanation of abbreviations. |

## Data Distribution

### Document Categories
The 45,458 documents are classified into 20 distinct types:
| Category     | Count | Category  | Count |
| :----------- | :---- | :-------- | :---- |
| LETTER       | 29567 | ARTICLE   | 5014  |
| SPEECH       | 3305  | TELEGRAM  | 2031  |
| NOTE         | 1447  | STATEMENT | 946   |
| INTERVIEW    | 792   | REPLY     | 372   |
| DISCUSSION   | 356   | MESSAGE   | 451   |
| CABLE        | 259   | REQUEST   | 187   |
| RESOLUTION   | 115   | ADVICE    | 110   |
| HOMAGE       | 110   | ADDRESS   | 97    |
| INTRODUCTION | 89    | QUESTIONS | 81    |
| MEMOIR       | 78    | REMARK    | 51    |

### Original Language Distribution
While all text in the dataset is in English, the original language of the work is noted:

| Language | Count | Language | Count | Language | Count |
| :--- | :--- | :--- | :--- | :--- | :--- |
| English | 39465 | Urdu | 18 | Bengali | 1 |
| Gujarati | 5048 | Marathi | 2 | Oriya | 1 |
| Hindi | 921 | Tamil | 1 | French | 1 |

##  `source` abbreviations
The `source` field contains abbreviations that refer to the archives where the original documents are held. The key is as follows:

*   **S. N.** : Sabarmati Sangrahalaya, Ahmedabad.
*   **G. N.** : Documents available in the Gandhi National Museum and Library, New Delhi.
*   **M.M.U.** : Reels of the Mobile Microfilm Unit.
*   **S. G.** : Photostats of the Sevagram Collection available in the Gandhi National Museum and Library, New Delhi.
*   **C.W.** : Documents secured by the Collected Works of Mahatma Gandhi project.
*   **N. A. I.** : National Archives of India.
*   **C.S.O.** : Colonial Secretary’s Office.
*   **C.O.** : Colonial Office.
*   **J&P** : Judicial and Public Records.
*   **Lt. G.** / **L.G.** : Lieutenant Governor.

## `document_type` assignment

A hybrid strategy was used to assign type to every document:

1. Where possible the document type was parsed directly from the **title** (most titles include type/contextual markers such as “Letter to …”, “Speech at …”, etc.).
2. For titles that did not make the type explicit, an open-source LLM (Google Gemma 27B) was used to classify the document into one of the predefined types based on the document text.

This automated classification is generally accurate for clear-cut categories (letters, speeches, long articles) but may be imperfect for borderline cases. Use with care if your research relies on perfectly-labelled genres.

## Dataset Use-Cases
This dataset is primarily intended for:
* Natural language processing (NLP) research in social and historical contexts
* Sentiment analysis and political discourse studies
* Historical text analysis and computational humanities
* Language modeling and text generation research
* Educational and academic research on Mahatma Gandhi's philosophy and writings
* Stylometric or authorship-style analyses across genres.
* Teaching and experimentation with historical text preprocessing (OCR-cleaning, footnote resolution)

The sizeable corpus (~100MB) makes it suitable for small to moderate-scale NLP applications.

---

# About the Source Material

This dataset is derived from the official CWMG project undertaken by the Government of India. It is crucial to understand the distinction between the two primary digital editions of this work.

#### The Original CWMG Project (Print & Digital)
The Government of India's CWMG project was a monumental effort to authenticate and document Mahatma Gandhi's writings and speeches. Commenced in 1956 and concluded in 1994, it resulted in 100 printed volumes.

A digital version of this original collection is credited as:
> *The Collected Works of Mahatma Gandhi (digital), New Delhi, Publications Division Government of India, 2005, 100 vols.*

#### The Electronic Book Version (This Dataset's Source)
In 1999, a revised electronic edition was published. This version was later found to contain errors and inconsistencies compared to the original print edition and was subsequently withdrawn. The page and volume numbers in this edition are not identical to the original.

This dataset is sourced from this **1999 electronic version** because the original digital version does not contain machine-readable (parseable) text. The electronic version was created using Optical Character Recognition (OCR), which introduced some of the aforementioned errors.

While this dataset attempts to clean and structure the content, it is ultimately a representation of this "erroneous" version. Users should be aware of potential discrepancies with the original 1958-1994 print volumes.

The source material for this dataset should be credited as:
> *The Collected Works of Mahatma Gandhi (Electronic Book), New Delhi, Publications Division Government of India, 1999, 98 vols.*

This dataset would not be possible without:
* The Government of India's Publications Division for the original CWMG project (1956-1994)
* The creators and maintainers of the CWMG electronic edition (1999)
* All historians, researchers, and archivists who contributed to preserving Mahatma Gandhi's legacy


## License and Citation

This dataset is made available under the **Creative Commons Attribution-NonCommercial-NoDerivs 3.0 Unported License**.

By using this dataset, you agree to the terms of this license. You must provide appropriate attribution, may not use the material for commercial purposes, and if you remix, transform, or build upon the material, you may not distribute the modified material.

When using this data, please cite the original source material it is derived from:

> **The Collected Works of Mahatma Gandhi (Electronic Book), New Delhi, Publications Division Government of India, 1999, 98 vols.**

Additionally, a link back to this GitHub repository is appreciated.

## Contact

For dataset-specific questions or reporting errors, please open an issue on this GitHub repo. Pull requests to improve parsing, correct metadata, or add derived files (for example cleaned-text versions or CSV export) are welcome — **please** ensure that any contributions respect the CC BY-NC-ND 3.0 license.
