# Summary

## Definitions and look-ups

"r" before a string indicates that the string is a raw string. 
This means that if there is "\n" in the string, printing it will print "\n" within the string.

## 2.1. Splitting strings on any of multiple delimeters: re.split()

line = 'dwfwrg fcwoirjfw; fwigjfw, wfwg,gfwgw,     www'

// not good:
print(line.split())

import re
// \s* is for al the spaces between the delimiter and the next char
print(re.split(r'[;,\s]\s*', line))

filename = 'spam.txt'
print(filename.endswith(('.txt'))
print(filename.startswith('file:'))

## 2.2. Matching text at the start or end of a string: .endswith() .atartswith()

filename = 'spam.txt'
print(filename.endswith(('.txt', '.md')))

## 2.3. Matching strings using shell wildcard patterns: fnmatch

fnmatch('foo.txt', '*.txt')

For code that explicitly works with filenames, use the glob module of 5.13.

## 2.4. Splitting strings on any of multiple delimeters: re.compile, .match(), .findall(), .finditer()

date = '11/27/2021'
// \d+ means match one or more digits
pattern = re.compile(r'\d+/\d+/\d+')

print('yes') if pattern.match(date) else print('no')

## 2.5. Searching and replacing text

## 2.6. Searching and replacing case-insensitive text

## 2.7. Specifying a regular expression for the shortest match

## 2.8. Writing a regular expression for multiline patterns

## 2.9. Normalizing unicode text to a standard representation

## 2.10. Working with unicode characters in regular expressions

## 2.11. Stripping unwanted characters from strings

## 2.12. Sanitizing and cleaning up text

## 2.13. Aligning text strings

## 2.14. Combining and concatenating strings

## 2.15. Interpolating variables in strings

## 2.16. Reformatting text to a fixed number of columns

## 2.17. Handling HTML and XML entities in text

## 2.18. Tokenizing text

## 2.19. Writing a simple recursive descent parser

## 2.20. Performing text operations on byte strings