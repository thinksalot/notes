### Literals
- Literials match themselves.
- These are characters we use in searching or matching expresion.
- Most alphanumeric characters are literal characters.
- For example, if we search for just *ant*, then *ant* is the literal.

### Metacharacters
- These are special characters.
- They have special meaning and are generally not used as literals.
- For example, a **.** (dot) matches any single character
- Some metacharacters:
    - **.** (dot) - matches any single character
    - **\\** (backslash) - escapes any meta character
    
  
### Character classes
- Represents a collection of characters inside square brackets
- Matches any one of the characters
- For example, **[abcd]** matches any one of a,b,c or d
- Ignores order or duplication. **[aabbccdd]** is same as **[abcd]** ,as
  is **[bcda]**

### Character class ranges
- Ranges can be specified in a character class using **-** (hyphen). Outside a
  character class, hyphen as no special meaning
- **[a-d]** means same as **[abcd]** and **[0-9]** means the same as **[0123456789]**
- Multiple ranges can also specified. **[a-z0-9]**  means a to z and 0 to 9
- Range endpoints are generally from the same range. **[a-z]** is valid but
  **[A-z]** might not always be valid
- Ranges are range of characters, not of numbers. So **[1-50]** matches any one of
  1,2,3,4,5,0 not 1 to 50

### Character class negation
- Character class can be negated using **^** (caret) at the beginning
- For example, **[^abcd]** means match anything other that a or b or c or d

### Predefiend character classes
- **\d** means find a digit, same as **[0-9]**
- **\w** means find a word character, same as **[0-9a-zA-Z_]** 
- **\s** means find a space character

Similarly,
- **\D\** means find a non-digit
- **\W\** means find a non-word character
- **\S\** means find a non-space character
- These are using without the square brackets
