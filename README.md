# Web-Based Corpus Analyzer (WBCA)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Made with HTML/CSS/JS](https://img.shields.io/badge/Made%20with-HTML%2FCSS%2FJS-orange)](https://developer.mozilla.org/en-US/docs/Web)

A powerful, browser-based corpus linguistics tool for analyzing text corpora with support for keyness analysis, concordancing, collocation extraction, and frequency analysis. **All processing happens locally in your browser—no data is sent to any server.**

## 🌐 Access the Tool

- **Web Application**: [https://sites.google.com/view/ishitatu-web-based-corpus-tool](https://sites.google.com/view/ishitatu-web-based-corpus-tool/%E3%83%9B%E3%83%BC%E3%83%A0?authuser=4)
- **Download**: You can also download the HTML file from this repository and run it locally in your browser

---

## 🌟 Features Overview

### Analysis Sections

| Section | Feature | Description |
|---------|---------|-------------|
| 1 | **Data Type & Upload** | Support for plain text and tagged corpora |
| 2 | **Corpus Summary** | Overview of loaded files, tokens, and folder structure |
| 3 | **Target/Reference Selection** | Assign folders to Target or Reference groups for comparative analysis |
| 4 | **KWIC (Concordance)** | Keyword-in-Context search with advanced filtering and sorting |
| 5 | **Text Data** | Original text and visual distribution of search terms across texts or folders|
| 6 | **Collocate Analysis** | Extract collocations with multiple statistical measures |
| 7 | **High-Frequency Features** | Compare most frequent features between Target and Reference |
| 8 | **Keyness Analysis** | Identify statistically significant vocabulary differences with Freq-LL, Text-LL, and MTK |

---

## 📥 Section 1: Data Input Formats

### Plain Text Mode
- Upload `.txt` files directly
- Supports folder uploads to preserve Move/folder structure
- Tokenization options:
  - Treat hyphens as part of words (e.g., `state-of-the-art`)
  - Treat apostrophes as part of words (e.g., `patient's`, `I'm`, `I've`, `I'll`)
- Text preprocessing: Merge short lines (useful for YouTube subtitles/transcripts)

### Tagged Corpus Mode
- Format: `word_POSd_POSs_lemma` (underscore-separated)
- Example: `chronic_kidney_disease_NN_NOUN_disease`
- Parsed from the right as 3 elements (POSd / POSs / lemma)
- Use [TagAnt](https://www.laurenceanthony.net/software/tagant/) for tagging
- Auto-detect option available for mixed corpora

### Upload Options
- **Folder upload**: Use `webkitdirectory` to upload entire folder structures (e.g., Move1, Move2)
- **Multiple file upload**: Upload individual files (assigned to virtual folder "Ungrouped")
- Hidden files (`.DS_Store`, `__MACOSX`, etc.) are automatically excluded

---

## 📋 Section 2: Corpus Summary

After loading your corpus, this section displays:
- **Mode badge**: Plain / Tagged
- **File count**: Total number of files loaded
- **Token count**: Approximate token count (excluding punctuation and spaces)
- **File list table**: Sortable by folder, filename, or token count

---

## 🎯 Section 3: Target/Reference Selection

Assign folders (Moves) to Target and/or Reference groups for comparative analysis:

- **Target**: The corpus you're analyzing (what you want to characterize)
- **Reference**: The comparison corpus (baseline for comparison)
- You can assign the same folder to both Target and Reference
- Displays Token count, Type count, and TTR for each folder
- "All" toggle buttons for quick selection

---

## 🔍 Section 4: KWIC (Keyword in Context)

### Search Modes
| Mode | Description | Example |
|------|-------------|---------|
| **Exact** | Exact word match | `study` or `cell\|cells` (pipe for alternatives) |
| **Wildcard** | `*` = any string, `?` = single character | `*ing`, `un*`, `b?t` |
| **Regex** | Regular expression | `stud(y\|ies\|ied)`, `[A-Z]+ing` |

### Display Options
- **Max lines**: Limit displayed concordance lines (1-5000)
- **Left/Right words**: Context window size (1-100 words each side)
- **Scope**: Target only / Reference only / All folders / Specific folder
- **View**: Surface only / Tagged (word_POSd_POSs_lemma)

### Filtering Options
- **Left filter**: Filter by words in left context
- **Node filter**: Filter by the keyword itself
- **Right filter**: Filter by words in right context
- **Match modes**: Exact match, Partial match, Wildcard, POS (simple/detailed), POS-gram
- **Position-specific**: L1-L5, R1-R5 positions with range option
- **Exclude option**: Exclude matches instead of including them

### Sorting
- Sort by any position (N) in left, node, or right context
- Alphabetical order (A→Z or Z→A)
- Sort key frequency display

### Advanced Mode (Tagged Corpus)
- Pattern format: `surface_POSd_POSs_lemma`
- Use `*` for any value, `|` for multiple values
- Examples:
  - `as_IN_ADP_*` (surface=as, POSd=IN, POSs=ADP)
  - `*_NN|NNS_NOUN_*` (POSd=NN or NNS, POSs=NOUN)

### Color Scheme
- Customizable colors for L1-L5 / Node / R1-R5 positions
- Helps visualize context patterns

---

## 📊 Section 5: Dispersion Plot

Visualize the distribution of search terms across your corpus:

- **Vertical lines**: Indicate occurrence positions within each text
- **Grouping**: By file or by folder
- **Scope**: Target / Reference / All folders
- **Options**: Hide files/folders with no hits
- **Click interaction**: Click a bar to display KWIC for that file/folder
- **Export**: Download as JPEG image

### Advanced Mode
- Synced with KWIC advanced pattern search
- Same pattern matching capabilities

---

## 🔗 Section 6: Collocate Tables (Target vs Reference)

Extract and compare collocations between Target and Reference corpora.

### Input Options
- **Node**: Word or p-frame pattern (e.g., `in the *`)
- **Feature type**: Word, lemma, n-gram, p-frame, POS, etc.
- **Collocate type**: Surface / Lemma / POS (simple/detailed) [Tagged mode]
- **Window size**: Left 1-5, Right 1-5
- **Top N**: Number of collocates to display

### Statistical Measures
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

### Output
- Separate tables for Target and Reference
- Left and Right collocate positions (L5-L1, R1-R5)
- Sortable columns
- Click word to filter KWIC by position (highlighted in purple)
- Export to Excel

---

## 📈 Section 7: High-Frequency Features

Compare the most frequent features between Target and Reference corpora.

### Options
- **Feature type**: Word, lemma, n-gram, p-frame, POS, cluster, etc.
- **n value**: For n-gram, p-frame, POS-gram, cluster
- **Min freq**: Minimum frequency threshold per side
- **Top N**: Number of features to display
- **Case-insensitive**: Toggle case sensitivity
- **Exclude stopwords**: Filter out common function words

### Cluster Analysis
- Extract n-grams containing a specific search word
- Supports wildcards: `*`, `?`, `|`
- Position options: All / Left (start) / Right (end)

### Output Columns
| Column | Description |
|--------|-------------|
| # (T/R) | Rank in Target/Reference |
| Feature | The linguistic feature |
| freq_T / freq_R | Raw frequency |
| norm_T / norm_R | Normalized frequency (per million) |
| files_T / files_R | Number of files containing the feature |

### Filtering
- Feature filter with exact/partial match
- Include/Exclude mode
- Apply to: All / Target only / Reference only

---

## 📊 Section 8: Keyness Analysis

Identify statistically significant vocabulary differences between Target and Reference corpora.

### Options
- **Feature type**: Full range of linguistic features
- **n value**: For n-gram, p-frame, POS-gram, cluster
- **Min total freq**: Minimum combined frequency
- **Top N**: Number of features in table
- **Case-insensitive**: Toggle case sensitivity
- **Use MTK**: Calculate Mean Text Keyness
- **Weighted pooled SD**: Option for MTK calculation
- **Advanced Statistics**: Show dispersion measures

### Keyness Statistics
| Measure | Description |
|---------|-------------|
| **Freq-LL (T)** | Log-likelihood based on raw frequencies |
| **Text-LL (T)** | Log-likelihood based on text/file frequencies |
| **MTK (T)** | Mean Text Keyness (Larsson, Kim, & Egbert, 2025) |

**Interpretation**: Positive values = Target dominant, Negative values = Reference dominant

### MTK (Mean Text Keyness) Formula
```
MTK = (mean_T - mean_R) / pooled_SD
```
Where:
- `mean_T` = average normalized frequency (per 1,000 words) across Target texts
- `mean_R` = average normalized frequency across Reference texts
- **Unweighted pooled SD**: `√((SD₁² + SD₂²) / 2)`
- **Weighted pooled SD**: `√(((n₁-1)SD₁² + (n₂-1)SD₂²) / (n₁+n₂-2))`

### Advanced Statistics (Dispersion)
| Measure | Description | Range |
|---------|-------------|-------|
| Range | Proportion of files containing the feature | 0-1 |
| Juilland's D | Dispersion coefficient | 0-1 (1 = even) |
| Gries's DP | Deviation of proportions | 0-1 (0 = even) |

### P-frame Filler Analysis
For p-frame features (e.g., `in the *`):
- **Fillers_T**: Distribution of words filling `*` in Target
- **Fillers_R**: Distribution of words filling `*` in Reference
- Click filler word to display KWIC for that specific n-gram

### Output Table
| Column | Description |
|--------|-------------|
| # | Rank |
| Feature | The linguistic feature (click for KWIC) |
| freq_T / freq_R | Raw frequency |
| norm_T / norm_R | Normalized frequency (per million) |
| file_T / file_R | file frequency |
| Freq-LL (T) | Frequency-based log-likelihood |
| Text-LL (T) | Text-based log-likelihood |
| MTK (T) | Mean Text Keyness |
| Fillers_T / Fillers_R | P-frame filler distribution |

---

## 🔍 Feature Types Reference

### Plain Text Mode
| Feature Type | Description |
|--------------|-------------|
| Word (surface) | Raw word forms as they appear |
| n-gram (word) | Contiguous word sequences |
| p-frame (word) | N-grams with one slot replaced by `*` |
| Cluster (word) | N-grams containing a specific search word |
| Regex | Regular expression pattern |

### Tagged Mode (Additional Features)
| Feature Type | Description |
|--------------|-------------|
| Word (lemma) | Dictionary/base forms |
| n-gram (lemma) | Contiguous lemma sequences |
| p-frame (lemma) | Lemma-based p-frames |
| Cluster (lemma) | Lemma-based clusters |
| POS (simple) | Simple POS tags (NOUN, VERB, ADJ, etc.) |
| POS (detailed) | Detailed POS tags (NN, NNS, VB, VBD, etc.) |
| POS-gram (simple) | POS tag sequences (simple) |
| POS-gram (detailed) | POS tag sequences (detailed) |

### P-frame Pattern Examples
For n=4: `1 * 34`, `12 * 4`, `123 *` (wildcard at any position except leftmost)

---

## 💾 Export Options

All analysis results can be exported to Excel-compatible CSV format:

- ✅ KWIC concordance lines (all rows, not just displayed)
- ✅ Keyness results with all statistics
- ✅ High-frequency feature lists
- ✅ Collocate tables
- ✅ Dispersion plots (JPEG)

---

## 🔒 Privacy & Security

**All data processing happens locally in your browser.**

- ✅ No data is uploaded to any server
- ✅ No internet connection required after loading the page
- ✅ Your corpus files remain on your computer
- ✅ Suitable for sensitive or confidential data

---

## 🛠️ Technical Notes

### Browser Compatibility
- Modern browsers with ES6+ support
- Chrome, Firefox, Edge, Safari (latest versions)
- JavaScript must be enabled

### Memory Considerations
- Large corpora (>1 million tokens) may require significant browser memory
- Consider splitting very large corpora into smaller files
- Progress bars show loading status for large files

### File Handling
- Hidden files (`.DS_Store`, `__MACOSX`, etc.) automatically excluded
- Punctuation and spaces excluded from token counts
- Sentence boundaries (`. ? !`) respected for n-grams (configurable)

---

## 📚 References

### Mean Text Keyness (MTK)
> Larsson, T., Kim, T., & Egbert, J. (2025). Introducing and comparing two techniques for key lexical bundles analysis. Research Methods in Applied Linguistics, 4(3), Article 100245. https://doi.org/10.1016/j.rmal.2025.100245

### Suggested Citation
If you use WBCA in your research, please cite:
```
Web-Based Corpus Analyzer (WBCA). [Software]. 
Available at: https://sites.google.com/view/ishitatu-web-based-corpus-tool
```

---

## 📝 Quick Start Guide

### Step 1: Upload Your Data
1. Select data type (Plain text, Tagged, or Auto-detect)
2. Configure tokenization options if needed
3. Upload files or folders using the appropriate input
4. Click "Load & Parse Corpus"

### Step 2: Review Corpus Summary (Section 2)
- Check file count and token count
- Verify folder structure is correct

### Step 3: Set Target/Reference (Section 3)
- Check Target column for folders you want to analyze
- Check Reference column for comparison folders
- Review token/type/TTR statistics

### Step 4: Analyze
- **Section 4 (KWIC)**: Search for specific words or patterns
- **Section 5 (Plot)**: Visualize distribution across texts
- **Section 6 (Collocates)**: Find word associations
- **Section 7 (High-Freq)**: Compare frequent features
- **Section 8 (Keyness)**: Identify distinctive vocabulary

### Step 5: Export Results
- Click "Export to Excel" buttons to save results
- Download plots as JPEG images
- Use results in your research

---

## ⚙️ Configuration Options

### Tokenization (Plain Text Mode)
- `☑️ Treat "-" as part of word`: Keep hyphenated compounds together
- `☑️ Treat apostrophe as part of word`: Keep contractions together

### Text Preprocessing
- `☐ Merge short lines into paragraphs`: Combine subtitle-style lines (improves KWIC display)

### N-gram Boundaries
- `☑️ Respect sentence boundaries`: Prevent n-grams from crossing `. ? !`

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🙏 Acknowledgments

- [TagAnt](https://www.laurenceanthony.net/software/tagant/) by Laurence Anthony for POS tagging support
- The corpus linguistics community for methodology and feedback

---

**Happy corpus analyzing! 📖🔬**
