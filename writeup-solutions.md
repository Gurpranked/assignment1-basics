# 2 Byte-Pair Encoding (BPE) Tokenizer

Problem (unicode1): Understanding Unicode
1. What Unicode character does `chr(0)` return?
   - It represents the NULL character.
2. How does this character's string representation differ from its printed representation?
   - It is represented as the following: `\x00` whereas it's printed representation doesn't output anything at all.
3. What happens when this character occurs in text?
   1. This character is created when processing printed text. During encoding it's important to add this character at the end as a possible delimiter. During printing it is not visible.

