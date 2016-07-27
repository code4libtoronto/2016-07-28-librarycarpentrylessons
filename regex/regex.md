---
Software/Library Carpentry - July 28-29, 2016
___

#Regular Expressions

## Introduction

*   A regular expression, or regex, is just a pattern that a string can match
*   Conceptually this is nothing new to you - think of using truncation and wildcards in a catalogue search

	| typical catalogue search | rendered as regex |
	| ---------------- | ----------------- |
	| teen* | `teen[A-Za-z]*` |
	| wom?n | `wom.n` or `wom[a-zA-Z]n` |
  	
*   Regular expressions are like "[wildcards on steroids](http://www.regular-expressions.info/)"!!
*   Warning: regex notation is ugly! This is because we're writing patterns to match strings, but we're writing those patterns *as* strings...using only the symbols on the keyboard (instead of inventing new symbols the way mathematicians do)

## Scenario

You're working with a researcher who needs to locate information within a dataset she has collected. The researcher's data has been transcribed from field notebooks. Data was collected by a number of different grad students, and consists of site names, dates, and instrument readings. 

Each grad student's field notebook is saved as its own data file. There is little consistency between files, because each grad student recorded their information differently. Let's take a look:

Notebook 1:  

> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2009-11-17&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1223.0  
> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-06-24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1122.7  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2009-07-24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	2819.0  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-08-25&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	2971.6  
> Baker 1	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2011-01-05&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	1410.0  
> Baker 2	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2010-09-04&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	4671.6  
> ...  


Notebook 1 uses a single tab between each column as a separator. There are also spaces in the site names. The dates are written in the international standard format.

Notebook 2:

> Davison/May 23, 2010/1724.7  
> Pertwee/May 24, 2010/2103.8  
> Davison/June 19, 2010/1731.9  
> Davison/July 6, 2010/2010.7  
> Pertwee/Aug 4 2010/1731.3  
> Davison/Apr 22, 201/2122.2  
> Pertwee/Sept 3, 2010/3981.0  
> ...

Notebook 2 uses slashes as separators, and there are no spaces in the site names. Dates are in a non-standard format.

## Practice

* We will test our regular expressions using [Regex101](https://regex101.com)
* We need some data to search through. From the scenario above, let's assume that we've loaded all the data from notebook 1 and notebook 2 into one file for our analysis: [Download the sample data](data/sample_data.txt)
* Open the sample data file, copy the contents, and paste it into the "Test String" box in Regex101

## Basics 

### Characters

* The core aspect of a regular expression is a set of one or more characters of text. Try putting a single character of text into the "Regular Expression" box on Regex101, for example: `a`
* The matched text will be highlighted in the "Test String" box
* The "Explanation" box tells you what the expression is doing
* Try a few other expressions, for example: `Baker`, `baker`, `24`,`04`, etc.


### Modifiers

* You likely noticed that your expressions in the previous section matched only the first occurance of that text, and that they were case sensitive. We can use modifiers to change this default behaviour.
* In Regex101 we add modifiers to the second box after the slash. Click on the question mark in that box and have a look at the help pop-up. 
* For now, let's use the `g` modifier. Optional: use the `i` modifier as well.
* Note: when using regex with a programming language, the syntax for this may differ. 

### Metacharacters & operators

There are certain characters that have special meaning in regular expressions, these are `\`, `|`, `(` `)` `.` `[` `]` `*` `+` `?` `{` `}` `^` `$`.

These are used in combination with text characters to construct regular expressions.

| Operator | Description | 
| ----------|-------------| 
| \ | Escape character - use when you need to include a metacharacter as a literal in a regular expression e.g. `\.txt` | 
| \| | OR (alternation) e.g. `wom[a|e]n`    | 
| ( ) | Group e.g. `(....)-(..)-(..)` for a date    | 
| . | Match any single character  e.g. `wom.n`     | 
| [abc] | Match any of a, b, or c. e.g. `[btr]ent` |
| [a-c] | Match any character between a and c. e.g. `[a-z]ent` |
| \* | The preceding item will be matched zero or more times e.g. `teen[a-z]*`    | 
| \+ | The preceding item will be matched one or more times `organi.+`     | 
| ? | The preceding item is optional and will be matched once at most, e.g. `colo?r` Used to make a quantifier 'lazy', e.g. `.+?` |
| {N} | The preceding item is matched exactly N times  `[0-9]{4}`    | 
| {N,} | The preceding item is matched N or more times  `[0-9]{4,}`    |
| {N,M} | The preceding item is matched at least N times, but not more than M times `[0-9]{4,6]`     |  
| ^ | Anchor: matches only at the start of the string e.g. `^b`  When used within a character set, negates the set, i.e. matches all characters *not* in the set - e.g. `[^abc]`      |  
| $ | Anchor: matches only at the end of the string e.g. `b$`      | 
| \b | Anchor: matches at "word boundary" (zero length position), i.e. transition from word to non-word characters. This allows you to perform "whole word only" searchers e.g. `\bword\b`
| \w | Shorthand character class: "word". Marches all the ASCII characters [A-Za-z0-9_] |
| \s | Shorthand character class: "whitespace". Matches non-word characters including space, tab, line break or form feed. |
| \d | Shorthand character class: "digit". Matches numeric characters [0-9]. |



### Building your first expressions 

* You want to find data from the month of June or July: `06|07` or `0(6|7)` (notice that when using the grouping operator, some information appears in the "Match" box in Regex101)  
* You want to find data from the month of May. What problem do you notice if you use the regex `05`? We need to take advantage of context. Try `-05-` instead.
* You want to match all dates that are in the international standard format: `....-..-..`  Another option is to use `(....)-(..)-(..)` which creates three groups, one for year, one for month, and one for day. This is handy when programmatically extracting data using regex

## Quantifiers

Let's work through a more involved example that introduces a number of operators that fall under the category of "quantifiers". Quantifiers specify how many instances of a character, group, or character set must be present (we'll talk about what a character set is later).

It was straightforward to match all the standardized dates, but what about matching all the dates that are in the unstandardized text format? Let's break this task into steps:

1. First of all, try to match a `/` using Regex101. It won't let you do it, because the regex syntax requires this character to mark the beginning and the end of the expression. You need to escape the slash character. Try `\/`. 
2. Now we want to match all the text between two slashes. We don't know exactly how many characters there are, because the month and days have variable number of characters in them. We can use the `*` character to match zero or more more characters: `\/(.*)\/` The parentheses pull the actual date text out into a group.
3. But, there's still a problem with this. Notice that there was a match on the final row where there is no data, only the slashes with no date between. Instead let's use the `+` character, which matches one or more characters: `\/(.+)\/`
4. Now we're getting somewhere. But let's try to break out the parts of the date, like we did for the nice standardized dates. `\/(.+) (.+), (.+)\/`
5. Nearly there, but one date didn't match! It doesn't fit the pattern of the rest of the dates; there is no comma after the day. We can fix this by putting a `?` after the comma, making it optional: `\/(.+) (.+),? (.+)\/`
6. If you have keen eyes, you may have noticed there are a few typos in this dataset. For example, one line has the year '201'. Let's force the year part of the pattern to have four digits. One way to do this would be: `\/(.+) (.+),? (....)\/`. Another option is to use curly braces, which let you specify the number of times the match must occur: `\/(.+) (.+),? (.{4})\/`
7. While we're at it, lets enforce some rules for the days as well. There should only be one or two digits in a day. Curly braces can be used to specify a range in the number of matches: `\/(.+) (.{1,2}),? (.{4})\/`
8. What about that line that is missing the day though? Why does that match? Let's pick up this example again in the section on Character Sets, below.

### Greedy vs lazy quantifiers

* Quantifiers are greedy by default - they will match as much text as they possibly can. A good example is trying to match text within html or xml tags. For example copy the following text into Regex101: 

		Extract everything "within quotes" from "this sentence".

* Using `".+"` matches the entire text from the first quotation mark to the second. Use the question mark to make the expression lazy instead: `".+?"` 
* Another solution would be to require the expression to match anything that is not a quotation mark, using `^`. For example, `"[^"]+"` will match characters that are not quotation marks, and therefore will stop matching each time it gets to an ending quotation mark.
* Use grouping to pull out the text within the quotation marks: `"(.+?)"`

## Character sets

Character sets, or character classes, allow you to match only one out of several characters. Place the characters you want to match between square brackets.

In order to illustrate the use of character sets, lets return to our problem of extracting non-standardized dates from text strings. 

* We last used the expression `\/(.+) (.{1,2}),? (.{4})\/`. Why did this pattern match the date that is missing a day? (i.e. "Jan , 2009")
* We can see from the coloured highlighting of the three groups in Regex101 that the 2nd group, which is supposed to match the day, is actually matching the comma. This is because the comma fits the criteria for this group - it comes after the first space, consists of one or two characters. Then the `,?` which is supposed to match the comma simply matches nothing, because it is optional. We need to force the 2nd group to match only numbers, not other characters like commas. 
* We can do this by replacing `.` (any one character) with a character set specifying only numbers: `[0-9]` (any one number between 0 and 9). So now we have `\/(.+) ([0-9]{1,2}),? (.{4})\/`
* We can use the same technique to make our month matching more precise as well. We know that our months should begin with an upper case letter followed by some unknown number of lower case letters. A single upper case letter can be expressed as a character set `[A-Z]` and one or more lower case letters can be expressed as `[a-z]+`. 
* And, we can use this technique to ensure that our expression matches only years that consist of four number characters.
* Our final regex has expanded to: `\/([A-Z][a-z]+) ([0-9]{1,2}),? ([0-9]{4})\/`. Quite a monster!

Regex offers a few shortcut operators that can make your life a bit easier when dealing with character sets, for example `\d` matches all numeric digits `[0-9]` and  `\w` matches all word characters `[A-Za-z0-9]`. We could use these to shorten our expression (though note that this will produce slightly less rigid requirements for the month matches):
`\/(\w+) (\d{1,2}),? (\d{4})\/`

## Anchors

Instead of matching characters, anchors match positions: the beginning or end of a string, or the boundaries between word and non-word characters. For example, copy the following text into Regex101:

	the first instance of the word 'the'

The simple regex `the` makes 3 matches. Use `^the` instead to match only the one at the beginning of the string.

Now, replace the test string in Regex101 with this one:

	the word 'end' could be in the middle of the string or at the end

The simple regex `end` makes 2 matches. Use `end$` instead to match only the one at the end of the string.

Finally, replase the test string in Regex101 with this one:

	to help is to be helpful and helping

The simple rebex `help` makes 3 matches. Use `\bhelp\b` to match only the word 'help'.

Note: another way to approach this example is not to match by position using an anchor, but to use a shorthand operator that matches white spaces: `\s`. For example: `\s(help)\s`. Note the expression actually matches the white spaces on either side of the word, so you need to employ grouping to match the word itself.


## Building regular expressions

*   The right way to build up patterns is to start with something simple that matches part of the data you're working with
*   Test it against your data, but also test that it doesn't match things that it shouldn't, because it can be very hard to track down false positives
*   Once you've done that, extend it piece by piece to handle other cases

## Exercise 1

You are working with an archive of several thousand papers and theses writeen in LaTeX, a text-based document formatting program. The documents look like this:

<<<<<<< HEAD
> \documentclass{article}  
> \begin{document}  
> \section*{Discussion}  
> Granger's work on graphs \cite{dd-gr2007}, particularly ones obeying Snape's Inequality \cite{ snape87 } (but see \cite{quirrell89}, has opened up new lines of research. However, studies at Unseen University \cite{stibbons2008} highlight several dangers.  
> \end{document}
=======
> Granger's work on graphs \cite{dd-gr2007}, particularly ones obeying Snape's Inequality \cite{ snape87 } (but see \cite{quirrell89}, has opened up new lines of research. However, studies at Unseen University \cite{stibbons2008} highlight several dangers.
>>>>>>> origin/master

All the LaTeX formatted papers use the same labels to refer to items in a shared bibliography. These citations have certain characteristics:

* Citations are written using '\cite{}', with a reference ID stored within the curly braces. 
* Reference IDs contain a combination of letters and numbers. 
* There may be white space before or after reference IDs. 
* The reference IDs may be split across more than one line of text, and there can be multiple citations per line. 

Your ultimate goal is to find out how often citations appear together, i.e. how often paper x is cited in the same document as paper y. As a first step, you need to extract the set of citation labels from each document, and that's the problem you'll tackle in this exercise. 

* [Download the sample text](data/exercise1_data.txt) and paste it into Regex101.
* Write a regular expression that matches all of the citations in the sample text. Use grouping to ensure you match only the citations themselves, without any surrounding characters.
<<<<<<< HEAD


## Exercise 2

Let's practice making matches with xml data. Imagine a simple book catalogue with the following xml elements and attributes:

> \<catalog>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \<book id="bk101">  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<author>Gambardella, Matthew\</author>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<title>XML Developer's Guide\</title>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<genre>Computer\</genre>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<price>44.95\</price>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<publish\_date>2000-10-01\</publish_date>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<description>An in-depth look at creating applications with XML.  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\</description>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \</book>  
> \</catalog>  

   
*(sample data source: [Microsoft documentation](https://msdn.microsoft.com/en-us/library/ms762271(v=vs.85).aspx))*


[Download the sample text](data/exercise2_data.txt) and paste it into Regex101. 

Write a variety of regular expressions to match tags, attributes, and content, for example:

* Match all text between angle brackets (tags)
* Match all prices
* Match all prices of $40 or greater
* Match all book IDs
* Match all book ID numbers (without the preceding 'bk')
* Match all publication dates in 2001 or 2002
* Match all author's last names
* What else can you think of?

As you'll soon see, our next session on XPath/XQuery will make pinpointing specific xml nodes a **lot** easier. You'll be able to use XPath to identify specific nodes and combine it with regex to select content.


## More Practice
=======
>>>>>>> origin/master

Go through the exercises at:  
Regex One: http://regexone.com/  
Regex golf: http://regex.alf.nu/

## Exercise 2

Let's practice making matches with xml data. Imagine a simple book catalogue with the following xml elements and attributes:

> \<catalog>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \<book id="bk101">  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<author>Gambardella, Matthew\</author>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<title>XML Developer's Guide\</title>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<genre>Computer\</genre>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<price>44.95\</price>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<publish\_date>2000-10-01\</publish_date>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      \<description>An in-depth look at creating applications with XML.  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\</description>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \</book>  
> \</catalog>  

   
*(sample data source: [Microsoft documentation](https://msdn.microsoft.com/en-us/library/ms762271(v=vs.85).aspx))*


[Download the sample text](data/exercise2_data.txt) and paste it into Regex101. 

Write a variety of regular expressions to match tags, attributes, and content, for example:

* Match all text between angle brackets (tags)
* Match all prices
* Match all prices of $40 or greater
* Match all book IDs
* Match all book ID numbers (without the preceding 'bk')
* Match all publication dates in 2001 or 2002
* Match all author's last names
* What else can you think of?

As you'll soon see, our next session on XPath/XQuery will make pinpointing specific xml nodes a **lot** easier. You'll be able to use XPath to identify specific nodes and combine it with regex to select content.


## More Practice

Go through the exercises at:  
Regex One: http://regexone.com/  
Regex golf: http://regex.alf.nu/


## Regular expressions & python: extracting data

* It isn't really enough to just find matches using regex; you need to then extract the matched text and do things with it. This is why regex is typically used in combination with a programming language.
* You'll be able to put this into practice after tomorrow's Python lessons
* For now, here's a simple script to give you the idea:

		# read the first half-dozen data records from two files
		readings = []
		for filename in ('data-1.txt', 'data-2.txt'):
			lines = open(filename, 'r').read().strip().split('\n\)
			readings += lines[2:8]
			
		# import python regular expression library
		import re
		
		# use regex to match and print the matches
		for r in readings:
			if re.search('/([A-Z][a-z]+) ([0-9]{1.2}),? ([0=9]{4})/', r):
				print r
				
## Thanks!

*   This [software carpentry lesson](http://v4.software-carpentry.org/regexp/index.html) was originally developed by Greg Wilson, and has been modified for this event by Leanne Trimble.
