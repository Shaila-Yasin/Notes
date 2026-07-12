# Text Preprocessing in NLP — Concepts & Project Notes

A structured walkthrough of the core text preprocessing concepts I learned while building an NLP text-cleaning pipeline, from raw text to tokenized, stopword-free output.

---

## Table of Contents
1. [What is Text Preprocessing?](#1-what-is-text-preprocessing)
2. [Structured vs Unstructured Data](#2-structured-vs-unstructured-data)
3. [Text Cleaning](#3-text-cleaning)
4. [Regular Expressions (Regex)](#4-regular-expressions-regex)
5. [Tokenization](#5-tokenization)
6. [Pretrained Tokenizers](#6-pretrained-tokenizers)
7. [Basic Tokenizer](#7-basic-tokenizer)
8. [Stopwords](#8-stopwords)
9. [Lemmatization](#9-lemmatization)
10. [Text Cleaning Pipeline](#10-text-cleaning-pipeline)

---

## 1. What is Text Preprocessing?

**Definition:** Text preprocessing is the process of converting raw, unstructured text into a clean and structured format that machine learning and deep learning models can understand.

**Example:**

Raw text:
```
OMG!!! I LOVE Python 😍😍
Visit https://python.org
I have 2 books.
```

After preprocessing:
```python
['omg', 'love', 'python', 'visit', 'books']
```

### Why is preprocessing important?

Real-world text contains a lot of noise, including:
- URLs
- Emojis
- Numbers
- HTML tags
- Punctuation
- Mixed capitalization
- Extra spaces
- Stopwords

All of this increases noise and reduces model performance if left unhandled.

---

## 2. Structured vs Unstructured Data

### Structured Data
Organized in a fixed format — tables, databases, Excel files.

| Name | Age |
|------|-----|
| Ali  | 22  |

### Unstructured Data
No fixed format — emails, tweets, reviews, articles, chat messages.

```
I absolutely LOVE this movie!!!
```

> NLP mainly deals with unstructured data.

---

## 3. Text Cleaning

### Lowercasing
**Purpose:** Convert every character to lowercase so identical words aren't treated differently.

```python
text.lower()
```

```
HELLO World → hello world
```

**Benefit:** Reduces vocabulary size — `"Apple"` and `"apple"` become the same word.

### URL Removal
**Purpose:** Remove website links.

```python
r'http\S+'
```

```
Visit https://python.org → Visit
```

### Number Removal

```python
r'\d+'
```

```
I have 25 books. → I have books.
```

### Punctuation Removal

```python
text.translate(str.maketrans('', '', string.punctuation))
```

Key concepts: `string.punctuation`, `translate()`, `maketrans()`

**Alternative (regex):**
```python
r'[^\w\s]'
```

### Removing Extra Spaces

```python
# Method 1
" ".join(text.split())

# Method 2
re.sub(r'\s+', ' ', text).strip()
```

- `\s` → whitespace
- `+` → one or more
- `strip()` → removes leading/trailing spaces

---

## 4. Regular Expressions (Regex)

### Character Classes
| Pattern | Meaning |
|---------|---------|
| `\d` | Digits |
| `\D` | Not digits |
| `\w` | Word characters (letters, numbers, underscore) |
| `\W` | Not word characters |
| `\s` | Whitespace (space, tab, newline) |
| `\S` | Non-whitespace |

### Quantifiers
| Pattern | Meaning | Example |
|---------|---------|---------|
| `+` | One or more | `\d+` matches `5`, `25`, `2026` |
| `*` | Zero or more | |
| `?` | Zero or one | |

### Anchors *(not covered deeply yet)*
- `^` — start of string
- `$` — end of string

### Character Sets
- `[a-z]`, `[A-Z]`, `[0-9]`
- Negation: `[^abc]` → anything except `a`, `b`, `c`

---

## 5. Tokenization

**Definition:** Breaking text into smaller pieces called tokens.

### Word Tokenization
```
I love NLP → ['I', 'love', 'NLP']
```

### Sentence Tokenization
```
Hello. How are you? → ['Hello.', 'How are you?']
```

### Character Tokenization
```python
list(text)
```
```
'Hello' → ['H', 'e', 'l', 'l', 'o']
```
*(Encountered accidentally while debugging — helped clarify the difference between characters and words.)*

### Subword Tokenization
Techniques: **BPE (Byte Pair Encoding)**, **WordPiece**, **SentencePiece**

Used in: GPT, BERT, LLaMA, T5

**Why subword tokenization?**
Handles unknown words, misspellings, and rare words.

```
unbelievable → un, believe, able
```

---

## 6. Pretrained Tokenizers

Learned about:
- Hugging Face Tokenizers
- BERT tokenizer
- GPT tokenizer
- SentencePiece

**When to use them:** When working with pretrained transformer models.

---

## 7. Basic Tokenizer

Built a simple custom tokenizer:

```python
text.split()
```

Learned why this differs from a proper `word_tokenize()` (e.g., handling punctuation, contractions, and edge cases that a naive `.split()` misses).

---

## 8. Stopwords

**Definition:** Very common words with little semantic meaning (e.g., `the`, `is`, `and`, `to`, `of`, `a`).

**Implementation (NLTK):**
```python
from nltk.corpus import stopwords
stopwords.words("english")
```

**Data structure note:** Learned why `set()` is faster than `list()` for stopword lookups (O(1) vs O(n) membership checks).

---

## 9. Lemmatization

**Definition:** Convert words to their dictionary (base) form.

```
running → run
better → good
```

### Lemmatization vs Stemming
| Lemmatization | Stemming |
|----------------|----------|
| Meaning preserved | Cuts endings |
| Dictionary-based | May produce invalid words |

---

## 10. Text Cleaning Pipeline

The full pipeline built, step by step:

```
Raw Text
   ↓
Lowercase
   ↓
Remove URLs
   ↓
Remove Numbers
   ↓
Remove Punctuation
   ↓
Remove Extra Spaces
   ↓
Tokenization
   ↓
Remove Stopwords
   ↓
Final Tokens
```

---

## 📌 Project

This pipeline was implemented as part of a hands-on NLP preprocessing project.

🔗 **Project Link:** [Add your project link here]

---

*Notes compiled while learning and building text preprocessing fundamentals in NLP.*
