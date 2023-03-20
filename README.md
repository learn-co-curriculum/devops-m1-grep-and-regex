# Grep and Regex

## Learning goals

- Understand the purpose and usage `grep` and `regex`
- Recognize the basic syntax of regular expressions.
- Apply regex and grep for searching and filtering data in a file or directory

## Introduction

In the world of programming and IT, finding patterns in text files is a common task. In this lesson, we will be exploring one of the most powerful ways to match patterns in text.

## `grep`

As we briefly touched on the previous module, `grep` (Global Regular Expression Print) is a command-line tool that you can use to search for patterns within files. 

The basic syntax to match patterns with `grep` is:

```bash
$ grep <pattern> file
```

If you want to search within an entire folder/directory, you can use the `-R` argument:

```bash
$ grep -R <pattern> directory
```

The `<pattern>` listed above is what is known as a *regular expression*.

## Regex

A **regular expression**, commonly referred to as **regex**, is a *pattern-matching* language used to search for text within strings. In other words, it's a type of formula that you can use to specify rules and conditions for text to be *matched* against. It's an extremely powerful tool that can be used for all sorts of tasks, such as finding all instances of a word, extracting specific information from a text file, replacing text within a file, etc.

At its most basic, a regular expression can consist of only the characters themselves. For instance, if you want to use `grep` to find all files that have the word `hello` in them in the current directory, you could do:

```bash
$ grep -R 'hello' .
```

> **Note:** Remember how when running scripts in the same directory, we used `./script.sh`? The `.` symbol is widely used to refer to the current directory.

That basic pattern only scratches the surface, however; regex becomes much more powerful once you start using what are known as *metacharacters*. A **metacharacter** is a character that represents a *pattern* of characters rather than just a single character.

Here's a table listing the most commonly used ones:

|Metacharacter|Pattern|
|:----|:----|
|.|Matches any single character except a newline|
|*|Matches zero or more occurrences of the preceding character|
|+|Matches one or more occurrences of the preceding character|
|?|Matches zero or one occurrence of the preceding character|
|^|Matches the beginning of a line|
|$|Matches the end of a line|
|[...]|Matches any one of the characters within the brackets|
|[^...]|Matches any character that is not within the brackets|
|(…)|Matches the enclosed characters as a group|
|||Matches either the expression before or after the | symbol|

You can also use ranges, like `[A-Z]` or `[0-9]`.

Now let's go over some examples so you see how metacharacters are commonly employed:

```bash
# Match either "color" or "colour" (british spelling)
grep 'colou?r' file.txt
# Match any word beginning with "ca", for example canada or car
grep 'ca.*' file.txt
# Match any line that starts with an uppercase letter
grep '^[A-Z]' file.txt
```

> **Note:** Remember the `#` are comments, which are ignored by the shell and only exist to give the reader information!

Lastly, if you want to use a character that is a metacharacter, you have to *escape* it by adding a `\` behind it. For example, since the `*` symbol is used to match 0 or more occurences, if you want to search for asterisks in files, you would use `\*`.

## Conclusion

That's the gist of it! Until you use regex frequently, it's going to take some time to get used to the way the patterns work. But luckily there are tons of places online you can find commonly used patterns that you can leverage.

For example, you can use [*regex101*](https://regex101.com/) to visualize the patterns being matched. Eventually you'll most likely end up needing some more complicated patterns, like for example, matching telephone numbers with two types of formatting:

```regex
\b\(?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})\b
```

Copy paste that pattern into *regex101*, along some sample text that has phone numbers, like:

```
Here's some random text interspersed with telephone numbers like 123-456-7890 and (123) 456-7890. Notice how it matches only the telephone numbers, even though they have different formatting!
```

And see the result! You can find an explanation for what every metacharacter does on the right sidebar of the page.

Learning how to use regex and grep is crucial for not only developing software, but also operating servers. For instance, you might have a signup form in a website which requests a user to input a phone number; you can use regex to validate the input before actually storing it and considering it legitimate. Likewise, your server might crash or go down, and you have to search through a massive log file in order to find out what went wrong.