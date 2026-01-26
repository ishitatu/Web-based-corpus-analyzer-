# Web-Based Corpus Analyzer (WBCA)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Made with HTML/CSS/JS](https://img.shields.io/badge/Made%20with-HTML%2FCSS%2FJS-orange)](https://developer.mozilla.org/en-US/docs/Web)

A powerful, browser-based corpus linguistics tool for analyzing text corpora with support for keyness analysis, concordancing, collocation extraction, and advanced grammatical pattern searches. **All processing happens locally in your browser—no data is sent to any server.**

## 🌟 Features Overview

### Core Analysis Functions

| Section | Feature | Description |
|---------|---------|-------------|
| 1 | **Data Upload** | Support for plain text, tagged corpora, and CSV/ZIP formats |
| 2 | **Corpus Summary** | Overview of loaded files, tokens, and folder structure |
| 3 | **Target/Reference Selection** | Assign folders to Target or Reference groups for comparative analysis |
| 4 | **KWIC (Concordance)** | Keyword-in-Context search with advanced filtering and sorting |
| 5 | **Dispersion Plot** | Visual distribution of search terms across texts |
| 6 | **Collocate Analysis** | Extract collocations with multiple statistical measures |
| 7 | **High-Frequency Features** | Compare most frequent features between Target and Reference |
| 8 | **Keyness Analysis** | Identify statistically significant vocabulary differences |

### Advanced Analysis (CSV Mode)

| Section | Feature | Description |
|---------|---------|-------------|
| 11 | **Dependency Grammar** | Pattern search using dependency relations |
| 12 | **Constituent (Phrase Structure)** | Pattern search using phrase structure grammar |

---

## 📥 Data Input Formats

### 1. Plain Text Mode
- Upload `.txt` files directly
- Supports folder uploads to preserve Move/folder structure
- Tokenization options:
  - Treat hyphens as part of words (e.g., `state-of-the-art`)
  - Treat apostrophes as part of words (e.g., `patient's`, `I'm`)
- Text preprocessing: Merge short lines (useful for YouTube subtitles)

### 2. Tagged Corpus Mode
- Format: `word_POSd_POSs_lemma` (underscore-separated)
- Example: `chronic_kidney_disease_NN_NOUN_disease`
- Use [TagAnt](https://www.laurenceanthony.net/software/tagant/) for tagging
- Auto-detect option available for mixed corpora

### 3. CSV Mode (Advanced)
- Load pre-processed corpus data from CSV or ZIP files
- Required columns: `file`, `token`
- Optional columns:
  - `move` - Folder/Move classification
  - `sent_id`, `sent_text` - Sentence information
  - `lemma`, `pos`, `xpos` - Morphological information
  - `dep`, `head_id`, `head_text`, `head_lemma`, `head_pos` - Dependency grammar
  - `chunk`, `cpath`, `cpath_norm`, `is_chunk_head` - Constituent/phrase structure
  - `tags_raw` - Biber tags for register analysis

---

## 🔍 Feature Types for Analysis

### Word-Level Features
| Feature Type | Description |
|--------------|-------------|
| Word (surface) | Raw word forms as they appear |
| Word (lemma) | Dictionary/base forms |

### N-gram Features
| Feature Type | Description |
|--------------|-------------|
| n-gram (word) | Contiguous word sequences |
| n-gram (lemma) | Contiguous lemma sequences |
| Cluster | N-grams containing a specific search word |

### P-frame (Phraseological Framework)
| Feature Type | Description |
|--------------|-------------|
| p-frame (word) | N-grams with one slot replaced by `*` |
| p-frame (lemma) | Lemma-based p-frames |

### POS-Based Features
| Feature Type | Description |
|--------------|-------------|
| POS (simple) | Simple POS tags (NOUN, VERB, ADJ, etc.) |
| POS (detailed) | Detailed POS tags (NN, NNS, VB, VBD, etc.) |
| POS-gram (simple) | POS tag sequences (simple) |
| POS-gram (detailed) | POS tag sequences (detailed) |

### Combined Features
| Feature Type | Description |
|--------------|-------------|
| Word_POS | Combined word and POS tag |
| n-gram_POS | N-gram with POS information |

---

## 📊 Statistical Measures

### Keyness Statistics
| Measure | Description |
|---------|-------------|
| **Freq-LL** | Log-likelihood based on raw frequencies (G² statistic) |
| **Text-LL** | Log-likelihood based on text/file frequencies |
| **MTK** | Mean Text Keyness (Larsson, Kim, & Egbert, 2025) |

MTK Formula:
```
MTK = (mean_T - mean_R) / pooled_SD
```
Where:
- `mean_T` = average normalized frequency (per 1,000 words) across Target texts
- `mean_R` = average normalized frequency across Reference texts
- `pooled_SD` = pooled standard deviation

### Dispersion Measures
| Measure | Description | Range |
|---------|-------------|-------|
| Range | Proportion of files containing the feature | 0-1 |
| Juilland's D | Dispersion coefficient | 0-1 (1 = even) |
| Gries's DP | Deviation of proportions | 0-1 (0 = even) |

### Collocation Statistics
| Statistic | Description |
|-----------|-------------|
| Frequency | Raw co-occurrence count |
| t-score | Student's t-test statistic |
| z-score | Standard score |
| MI | Mutual Information |
| MI² | MI squared |
| MI³ | MI cubed |
| LL (G²) | Log-likelihood ratio |
| LogDice | Logarithmic Dice coefficient |
| Dice | Dice coefficient |
| Delta P | Directional association measure |

---

## 🎯 KWIC (Concordance) Features

### Search Modes
- **Exact**: Exact word match (use `|` for alternatives: `cell|cells`)
- **Wildcard**: `*` matches any string, `?` matches single character
- **Regex**: Full regular expression support

### Filtering Options
- **Left/Right Context Filter**: Filter by words in context
- **Node Filter**: Filter by the keyword itself
- **POS Filter**: Filter by part-of-speech tags
- **Biber Tag Filter**: Filter by register features (CSV mode)
- **Position-specific Filtering**: L1-L5, R1-R5 positions

### Sorting
- Sort by any position in left/right context
- Alphabetical (A→Z or Z→A)
- Frequency display for sort keys

### Advanced Mode (Tagged Corpus)
- Pattern format: `surface_POSd_POSs_lemma`
- Multi-token pattern matching
- Example: `as_IN_ADP_* *_DT_DET_* *_NN|NNS_NOUN_*`

---

## 🌳 Dependency Grammar Analysis (Section 11)

### Pattern Search Elements
- **Node**: Head word of the construction
- **Modifier 1-3**: Dependent words with specific relations

### Search Criteria per Element
- Word (surface/lemma)
- POS tag (simple/detailed)
- Dependency relation (nsubj, dobj, amod, etc.)
- Specific element or wildcard (`*`)

### 28 Built-in Presets
Including patterns for:
- Subject-Verb constructions
- Verb-Object patterns
- Noun modifications
- Prepositional phrases
- Clausal complements
- And more...

### Output
- Pattern frequency table with Target/Reference comparison
- Concordance view with highlighted grammatical elements
- Export to CSV/Excel

---

## 🏗️ Constituent (Phrase Structure) Analysis (Section 12)

### Pattern Elements
- **Feature**: Target word or phrase
- **Chunk Type**: NP, VP, PP, ADJP, ADVP, S, SBAR, etc.
- **Depth**: Level in phrase structure tree
- **Parent Chunk**: Containing phrase type
- **Full Path**: Complete constituent path

### Analysis Options
- Extract all patterns matching criteria
- Filter by frequency threshold
- Filter by specific features or chunk types

### Output
- Pattern frequency with keyness statistics
- Concordance with full sentence context
- Export functionality

---

## 📈 High-Frequency Features (Section 7)

Compare the most frequent features between Target and Reference corpora:

### Output Columns
| Column | Description |
|--------|-------------|
| # | Rank |
| Feature | The linguistic feature |
| freq_T / freq_R | Raw frequency in Target/Reference |
| norm_T / norm_R | Normalized frequency (per million) |
| files_T / files_R | Number of files containing the feature |

### Options
- Feature type selection
- Minimum frequency threshold
- Top N features to display
- Case-sensitive/insensitive
- Stopword exclusion
- Feature filtering (include/exclude)

---

## 🎨 Dispersion Plot (Section 5)

Visualize the distribution of search terms across your corpus:

- Vertical lines indicate occurrence positions
- Group by file or folder
- Click bars to show KWIC for that file/folder
- Download as JPEG

---

## 💾 Export Options

All analysis results can be exported to Excel-compatible CSV format:

- KWIC concordance lines
- Keyness results with all statistics
- High-frequency feature lists
- Collocate tables
- Dependency/Constituent patterns

---

## 🔒 Privacy & Security

**All data processing happens locally in your browser.**

- No data is uploaded to any server
- No internet connection required after loading the page
- Your corpus files remain on your computer
- Suitable for sensitive or confidential data

---

## 🛠️ Technical Notes

### Browser Compatibility
- Modern browsers with ES6+ support
- Chrome, Firefox, Edge, Safari (latest versions)
- JavaScript must be enabled

### Memory Considerations
- Large corpora (>1 million tokens) may require significant browser memory
- Consider splitting very large corpora into smaller files

### Hidden File Handling
- `.DS_Store`, `__MACOSX`, and other hidden files are automatically excluded

### Sentence Boundary Options
- N-grams can respect sentence boundaries (`. ? !`)
- Configurable via checkbox in upload section

---

## 📚 References

### Mean Text Keyness (MTK)
> Larsson, T., Kim, T., & Egbert, J. (2025). Mean Text Keyness: A statistical approach to keyness that accounts for variability across texts.

### Suggested Citation
If you use WBCA in your research, please cite:
```
Web-Based Corpus Analyzer (WBCA). [Software]. 
Available at: [Your GitHub URL]
```

---

## 📝 Quick Start Guide

### Step 1: Upload Your Data
1. Select data type (Plain text, Tagged, or Auto-detect)
2. Upload files or folders
3. Click "Load & Parse Corpus"

### Step 2: Review Corpus Summary
- Check file count and token count
- Verify folder structure

### Step 3: Set Target/Reference
- Assign folders to Target group (what you're analyzing)
- Assign folders to Reference group (comparison corpus)

### Step 4: Analyze
- Use KWIC for concordance search
- Compute keyness to find distinctive vocabulary
- Extract collocates for word association patterns
- Explore grammatical patterns (CSV mode)

### Step 5: Export Results
- Click "Export to Excel" buttons to save results
- Use results in your research or further analysis

---

## ⚙️ Configuration Options

### Tokenization (Plain Text)
- `☑️ Treat "-" as part of word`: Keep hyphenated compounds together
- `☑️ Treat apostrophe as part of word`: Keep contractions together

### Text Preprocessing
- `☐ Merge short lines`: Combine subtitle-style lines into paragraphs

### N-gram Boundaries
- `☑️ Respect sentence boundaries`: Prevent n-grams from crossing sentence-ending punctuation

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🙏 Acknowledgments

- TagAnt by Laurence Anthony for POS tagging support
- JSZip library for ZIP file handling
- The corpus linguistics community for methodology and feedback

---

**Happy corpus analyzing! 📖🔬**
