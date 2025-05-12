# 2 Byte-Pair Encoding (BPE) Tokenizer

Problem (unicode1): Understanding Unicode
1. What Unicode character does `chr(0)` return?
   - It represents the NULL character.
2. How does this character's string representation differ from its printed representation?
   - It is represented as the following: `\x00` whereas it's printed representation doesn't output anything at all.
3. What happens when this character occurs in text?
   1. This character is created when processing printed text. During encoding it's important to add this character at the end as a possible delimiter. During printing it is not visible.


Problem (unicode2): Unicode Encodings:
1. What are some reasons to prefer training our tokenizer on UTF-8 encoded bytes, rather than UTF-16 or UTF-32? 
   - UTF-16 and UTF-32 use 2-3 bytes to represent characters. This is often inadequate for a multi-byte encoding scheme. Specifically with BPE or work based encoding. The variable byte sizing for encoding of UTF-8 makes it best for tokenization.
2. Consider the following (incorrect) function, which is intended to decode a UTF-8 byte string into a Unicode string. Why is this function incorrect? Provide an example of an input byte string that yields inorrect results. 
```python
def decode_utf8_bytes_to_str_wrong(bytestring: bytes):
    return "".join([bytes([b]).decode("utf-8") for b in bytestring])
```
   - The code is incorrect because it attempts to decode the input string at a per-byte level. UTF-8 does not encode strings at a per-byte level. Hence, each Unicode representation does not map to direct one byte from the UTF-8 encoding. UTF-8 is encodes in a byte-variable fashion. The following is produced from the input 'Hello there, this a function ƒ':
   ```python
   UnicodeDecodeError: 'utf-9' codec can't decode byte 0xc6 in position 0: unexpected end of data
   ```
   The symbol ƒ is a multi-byte symbol which is incorrectly processed by the function `decode_utf8_bytes_to_str_wrong`. 
3. Give a two byte sequence that does not decude to any Unicode Character(s):
   - Unicode cannot decode the following sequence of two bytes `\c386`. This is because the Unicode specification requires that the leading two bits of a multibyte sequence always start with the two left most bits set to `11` and the two leftmost continuation bits set to `10`. Hence, it's invalid to have have a starting sequence such as `\c386` which starts the leading bits with `10`. 

