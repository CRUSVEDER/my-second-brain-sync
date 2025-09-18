---
dg-publish: true
---
## Files

### Opening a file

`with open("myfile.txt", "r") as file:`:

- `with`: Handles errors & manages resources (like Kotlin's `using`).
- `open`: Open the specified file.
- `r`: Open in Readable mode, can also be Append or Write.
- `as file`: What variable to use.

### Manipulating file contents

- `.read()`: Load file contents into file.
- `.write(x)`: Appends line containing `x`.
- `.split()`: Split according to character, default is any whitespace.
- `",".join()`: Join all of a list into a string, as extension function on the joining character. Awkward.

## Debugging

- Syntax error: Just invalid code.
- Name error: Messed up the naming (e.g. var name).
- Logic error: Code compiles, but doesn't do what was expected.

- Regular expressions in Python allow you to create patterns that you can then use to find important strings.
- Regular expression patterns can be built to match specific characters and character combinations.
- Examples of regular expression symbols practiced in this lab:
    - `\w` represents any alphanumeric character.
    - `+` represents one or more occurrences of the previous character in the regular expression.
    - `\d` represents any digit.
    - `\.` represents a period.
    - `{x,y}` represents anywhere between x and y number of occurrences of the previous character in the regular expression. The x and y can be replaced with any two positive integers to indicate an exact range for the number of occurrences.
- The `re` module in Python contains functions that are useful when working with regular expressions.
    - One example is the `re.findall()` function, which takes in a regular expression pattern as well as a string, checks for all instances in the string that match with the pattern and outputs a list of the matches.

**Resources:**

1. Best Python Libraries for Cybersecurity in 2024. [https://medium.com/@Scofield_Idehen/best-python-libraries-for-cybersecurity-in-2024-037a870f39d1](https://medium.com/@Scofield_Idehen/best-python-libraries-for-cybersecurity-in-2024-037a870f39d1)
    
2.  Vulnerability Scanning for Secure Python Development. [https://safetycli.com/](https://safetycli.com/)
    
3. Article 3 - OWASP Dependency-Check and Vulnerability Scanning. [https://www.linkedin.com/pulse/article-3-owasp-dependency-check-vulnerability-scanning-adorsys-p73fe](https://www.linkedin.com/pulse/article-3-owasp-dependency-check-vulnerability-scanning-adorsys-p73fe)
    
4. Python library for Hashicorp Vault implementation. [https://discuss.hashicorp.com/t/python-library-for-hashicorp-vault-implementation/55805](https://discuss.hashicorp.com/t/python-library-for-hashicorp-vault-implementation/55805)
    
5. Continuous Integration With Python: An Introduction. [https://realpython.com/python-continuous-integration/](https://realpython.com/python-continuous-integration/)
    
6. Python for DevOps: An Ultimate Guide. [https://code-b.dev/blog/python-devops](https://code-b.dev/blog/python-devops)
    
7. Building Custom Cybersecurity Tools with Python: A Guide for Beginners. [https://www.linkedin.com/pulse/building-custom-cybersecurity-tools-python-bi6if](https://www.linkedin.com/pulse/building-custom-cybersecurity-tools-python-bi6if)
    
8. Secure Coding in Python: Essential Practices for Data Engineers. [https://www.linkedin.com/pulse/secure-coding-python-essential-practices-data-engineers-priyanka-sain-wewkc](https://www.linkedin.com/pulse/secure-coding-python-essential-practices-data-engineers-priyanka-sain-wewkc)
