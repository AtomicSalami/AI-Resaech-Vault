# How do we even "tokenize" or create "tokens"?

Tokenization is a way to convert text into a sequence of numerical IDs that are more efficient and easier for computers to process than raw text. Instead of dealing with individual characters or bytes, we create a **vocabulary** of common patterns and represent text using these learned patterns.

## Why tokenize?

Think of it like creating a shorthand system. Instead of writing "New York City" every time, you might create a shorthand symbol. Similarly, tokenization finds common patterns in text and gives them shorter representations.

## Step-by-Step Process

### Step 1: Text to Bytes

Let's start with an example from the FineWeb dataset description:

```
Initially, we were operating under the assumption that *more deduplication is always better*, so our first approach was to take the entire dataset (all 90+ dumps) and deduplicate them together as one big dataset using MinHash.
```

First, we convert this text to its UTF-8 byte representation (each byte is a number from 0-255):

```
73, 110, 105, 116, 105, 97, 108, 108, 121, 44, 32, 119, 101, 32, 119, 101, 114, 101, 32, 111, 112, 101, 114, 97, 116, 105, 110, 103, 32, 117, 110, 100, 101, 114, 32, 116, 104, 101, 32, 97, 115, 115, 117, 109, 112, 116, 105, 111, 110, 32, 116, 104, 97, 116, 32, 42, 109, 111, 114, 101, 32, 100, 101, 100, 117, 112, 108, 105, 99, 97, 116, 105, 111, 110, 32, 105, 115, 32, 97, 108, 119, 97, 121, 115, 32, 98, 101, 116, 116, 101, 114, 42, 44, 32, 115, 111, 32, 111, 117, 114, 32, 102, 105, 114, 115, 116, 32, 97, 112, 112, 114, 111, 97, 99, 104, 32, 119, 97, 115, 32, 116, 111, 32, 116, 97, 107, 101, 32, 116, 104, 101, 32, 101, 110, 116, 105, 114, 101, 32, 100, 97, 116, 97, 115, 101, 116, 32, 40, 97, 108, 108, 32, 57, 48, 43, 32, 100, 117, 109, 112, 115, 41, 32, 97, 110, 100, 32, 100, 101, 100, 117, 112, 108, 105, 99, 97, 116, 101, 32, 116, 104, 101, 109, 32, 116, 111, 103, 101, 116, 104, 101, 114, 32, 97, 115, 32, 111, 110, 101, 32, 98, 105, 103, 32, 100, 97, 116, 97, 115, 101, 116, 32, 117, 115, 105, 110, 103, 32, 77, 105, 110, 72, 97, 115, 104, 46
```

**Why UTF-8 bytes?** UTF-8 can represent any character in any language using 1-4 bytes per character. By working with bytes, we can handle any text uniformly.

### Step 2: Initial Vocabulary

We start with a vocabulary of 256 tokens (IDs 0-255), where each token represents a single byte value. This gives us our **base vocabulary**.

**Important distinction: Byte vs Character**

- A **byte** = a number from 0-255 (8 bits of data)
- A **character** = what humans recognize as a letter, symbol, or digit

These are NOT the same thing:

- **ASCII characters** (basic English): 1 character = 1 byte
    - 'A' = 65, 'b' = 98, ' ' = 32
- **Unicode characters** (international): 1 character = 2-4 bytes in UTF-8
    - 'é' = [195, 169] (2 bytes)
    - '中' = [228, 184, 173] (3 bytes)
    - '🚀' = [240, 159, 154, 128] (4 bytes)

**Example**: The text `"Café"` contains:

- **4 characters** as humans see it
- **5 bytes** in UTF-8: `[67, 97, 102, 195, 169]`

So our initial 256 tokens represent individual byte values, not complete characters. Some bytes represent full ASCII characters, while others are just pieces of multi-byte Unicode characters.

### Step 3: Byte-Pair Encoding (BPE) Algorithm

Now comes the clever part! We iteratively find the most frequent pair of adjacent tokens and merge them into a new token.

**How it works:**

1. **Count pairs**: Look at all adjacent token pairs in our data
    
    - `116, 105` (which represents "ti") appears 5 times
    - `101, 32` (which represents "e ") appears 9 times
    - `32, 116` (which represents " t") appears 7 times
    - etc.
2. **Merge most frequent**: Take the most frequent pair and create a new token
    
    - `101, 32` → `256` (our first new token beyond the base 256)
3. **Update the sequence**: Replace all occurrences of `101, 32` with `256`
    
4. **Repeat**: Continue this process, creating tokens 257, 258, 259... until we reach our desired vocabulary size (typically 30k-100k tokens)
    

### Step 4: The Result

After many iterations, we end up with:

- **A vocabulary** of learned tokens (e.g., 50,000 tokens total)
- **Shorter sequences** representing the same text
- **Meaningful units** like common words, word parts, or character combinations

**Example progression:**

- Original: 200+ bytes
- After BPE: Maybe 50-80 tokens
- Each token captures common patterns like "the", "ing", " and", etc.

## Key Benefits

1. **Compression**: Fewer tokens to represent the same information
2. **Efficiency**: Faster processing for AI models
3. **Vocabulary management**: Fixed vocabulary size regardless of text length
4. **Language agnostic**: Works with any language through UTF-8
5. **Handles rare words**: Can represent any text, even words not seen during training

## Why This Matters for AI

Language models like GPT work with these token sequences rather than raw text. Good tokenization means:

- Models can process text more efficiently
- Better representation of language patterns
- Consistent handling of different languages and special characters

The vocabulary becomes the model's "alphabet" - instead of 26 letters, it has 50,000+ learned patterns that capture the structure of human language!