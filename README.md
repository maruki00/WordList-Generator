# Word List Generator

## Overview

Word List Generator is a Python script that creates a custom wordlist based on:

- Minimum length
- Maximum length
- Custom character set
- Output file name

It generates all possible combinations (cartesian product) of the given character set within the specified length range and saves them to a file.

---

## Features

- Generate combinations using a custom character set
- Specify starting and ending word lengths
- Automatically overwrite existing output files
- Simple command-line interface
- Asynchronous structure (uses asyncio)

---

## Requirements

- Python 3.x
- No external libraries required (uses built-in modules)

Modules used:

- itertools
- sys
- optparse
- asyncio
- os

---

## Usage

```bash
python3 script.py -f <from_length> -t <to_length> -c <charset> -o <output_file>
```

### Arguments

| Option | Description |
|--------|------------|
| -f     | Starting length of generated words |
| -t     | Ending length of generated words |
| -c     | Character set to use |
| -o     | Output file name |

---

## Example

Generate all combinations from length 3 to 5 using characters ABC123:

```bash
python3 script.py -f 3 -t 5 -c ABC123 -o wordlist.txt
```

This will generate combinations such as:

```
AAA
AAB
AAC
...
12312
```

All combinations between length 3 and 5 will be written to `wordlist.txt`.

---

## How It Works

1. Parses command-line arguments using `optparse`
2. Validates required parameters:
   - FROM length
   - TO length
   - CHARSET
   - OUTPUT file
3. Removes the output file if it already exists
4. Generates combinations using:

```python
itertools.product(CHARSET, repeat=length)
```

5. Writes each generated word to the output file

---

## Validation Rules

- All options (-f, -t, -c, -o) must be provided
- Ending length (-t) must be greater than or equal to starting length (-f)

If validation fails, usage instructions are displayed.

---

## Performance Warning

⚠ This script can generate extremely large files.

The number of generated words equals:

```
len(CHARSET) ^ length
```

For example:

- Charset length: 6
- Word length: 5

Results in:

```
6^5 = 7776 combinations
```

Larger ranges can quickly produce millions or billions of combinations.

Use carefully to avoid:

- Disk space exhaustion
- High CPU usage
- Long execution times

---

## File Handling Behavior

- If the output file already exists, it will be deleted.
- A new file will be created and populated with generated combinations.

---

## Script Structure

Main class:

```python
class Word_List
```

Key methods:

- `get_options()` – Parses and validates CLI arguments
- `generate_word_list()` – Generates and writes combinations

The script starts automatically by calling:

```python
Word_List()
```

---

## Example Output Size Estimation

If:

- Charset = ABCD (4 characters)
- FROM = 2
- TO = 4

Generated combinations:

```
4^2 + 4^3 + 4^4
= 16 + 64 + 256
= 336 words
```

---

## Disclaimer

This tool is intended for:

- Educational purposes
- Testing environments
- Password strength research
- Security lab environments

Do not use generated wordlists for unauthorized activities.

---

## License

Provided as-is for educational and research purposes.
