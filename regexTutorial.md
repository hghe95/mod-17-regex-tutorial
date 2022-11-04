# Regex Tutorial

The following is a tutorial explaining a specific regular expression, or regex for short. A regex can be described as a series of characters that can define a specific search pattern. Regexes are used for matching characters within a string, parsing, data validation, etc. Because of these uses they are very useful in search and 'find and replace' functions.

## Summary

The following regex script is used for matching a URL link for validation. It will be used throughout the tutorial to describe the different components of a regex. These regex componenets will be separated in the different sections below.
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
    In the context of regex, anchors are considered the bookends. 
    * ^ is the anchor at the start ^(https?:\/\/) and can be used in two different ways:
        * to show an exact match. ie ^Reg would match with "Regex" and "Regular". It should be noted that all regex are 
        case-sensitive
        * to show possible matches. This will be discussd in bracket expressions.
    * $ is the anchor at the end ([\/\w \.-]*)*\/?$
### Quantifiers
    A quantifier determines the limits of the regex in terms of matches. A very common quantifier are minimum and maximum character setters. They can also be considered either lazy or greedy, though they are inherently greedy. Later on in the tutorial we will cover lazy and greedy matches.

    Based on our URL regex we can identify all of these quantifiers:
    * There are * used to for the latter part of the regex. [\/\w \.-]* and ([a-z\.]{2,6})([\/\w \.-]*) may match 0 or more times.
    * There is one + used at [\da-z\.-], where it may match one or more time.
    * {2, 6} is used in the middle of the regex to match the [a-z\.] pattern at minimum 2, and at max 6 times.
    * There are three instances of ? being used. The first at the beginning where "https", "(https?:\/\/)", and "/" may match 0 or more times.
### Character Classes
    In a regex, a character class defines a set of characters of which any can occur in an input string to make a match. Here is a list of common character classes:
    * .- Matches any character except the newline character (\n)
    * \d- Matches with any Arabic numeral. It is equivalent to [0-9]
    * \w- Matches with any alphanumeric character including underscore (_). It is equivalent to [A-Za-z0=9_]
    * \s- Matches a single whitespace character, this includes tabs and line breaks
    It should be noted that inverse matches are possible with the last three character classes by simply capitalizing the letter. For instance, \D matches non-digits.

    As seen in our URL regex, a couple of character classes are used:
    * [\da-z\.-] - \d is used to represent that any Arabic numeral will match
    * [\/\w \.-] - \w is used to represend that any alphanumeric character will match
### Grouping and Capturing
    In order to group sections of a regex you need to use parentheses (). This creates grouping constructs which will help break up parts of the the regex. Everything inside of the parentheses is considered a subexpression. Subexpressions look for parts of the string that match exactly with the subexpression itself. For instance the grouping construct of (and) will match for parts of the string with "and". So words like "grand" and "stand" would match.

    Our URL regex contains four different subexpressions:
    * (https?:\/\/)
    * ([\da-z\.-]+)
    * ([a-z\.]{2,6})
    * ([\/\w \.-]*)

    Grouping Constructs are divided into two categories: capturing and non-capturing. The details behind these categories are somewhat advanced for this tutorial. But the important thing to note is that capturing groups store matched character sequences for possible re-use. Non-capturing groups simply do not do this. In order for a non-capturing group to be made, the characters ?: need to be placed at the beginning of the subexpression within the parenthesis. 
### Bracket Expressions
    Also known as positive character groups, bracket expressions specifies which patterns we want to match. The characters inside of the brackets will specify which characters would match. For instance, [abc] will look for any string that matches the characters a, b, or c. (ie ant, ccc, broke, cba, etc.).

    Most regex will include a hyphen (-) to represent a range:
    * [a-z] for all lowercase letters
    * [A-Z] for all uppercase letters
    * [a-zA-Z] for lowercase and uppercase letters
    * [0-9] for all numbers from 0-9
    * [_-] for the special characters (_) underscore and (-) hyphen

    In our URL regex bracket expressions are used three times 
    * [\da-z\.-] - any number, undercase letters, dots , slashes , and hyphens will match
    * [a-z\.] - any lowercase letter, slashes, and dots will match
    * [\/\w \.-] - any alphanumeric character, dots, slashes, and hyphens will match
### Greedy and Lazy Match
    As seen in the previous quantifiers section, quantifiers can be either lazy or greedy.
    * Greedy - will match as many occurrences as possible. These include:
        * *- Matches 0 or more times
        * +- Matches one or more times
        * {}- These have three different functions:
            * { n } - Matches the pattern n number of times
            * { n, } - Matches the pattern at least n number of times
            * { n, x} - Matches the pattern from a minimum of n number of times to max of x number of times

    * Lazy - will match as few occurrences as possible. 
        * Quantifiers must be set as lazy by adding a ? symbol after it. 
        * ?- Matches the pattern 0 or one time

    Based on our URL regex we can identify which parts are lazy and greedy matches

    Lazy:
    * https?
    * (https?:\/\/)? 
    * /?
    
    Greedy: 
    * [\/\w \.-]* 
    * ([a-z\.]{2,6})([\/\w \.-]*) 
    * [\da-z\.-]+
    * [a-z\.]{2,6}

## Author
    Henry He is an aspiring web developer who always forgets to hydrate when working.  
    Github: https://github.com/hghe95
