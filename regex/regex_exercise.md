---
Software/Library Carpentry - July 28, 2016
___
#Regular expressions

## Exercise

* First idea looks like `cite\{(.+)\}`. Use escape character for the curly braces. Use bracket to capture the actual reference in a group. Use the . to match any character, and the plus sign to match any character one or more times. 
* Problem: this matches everything between the first and the last curly brace in the entire text! This is because regular expression matching is greedy, it matches as much text as it can. 
* One solution is to have the regex match everything *except* a closing curly brace. We can do this using a character set with the negation metacharacter: `[^}]` resulting in `cite\{([^}]+)\}`
* There is another way to accomplish the same thing and that is using the ? which automatically makes any quantifier 'lazy': `cite\{(.+?)\}`
* Now we've got the contents of our curly braces selected. But what about spaces within the curly braces? The expression is including them right now. We can insert `\s*` outside our group to make sure the leading whitespace is not captured: `cite\{\s*([^}]+)\}`. However, the same doesn't work properly at the end of the brace (i.e. `cite\{\s*([^}]+)\s*\}` is no good. This is because the space after the text is not a curly brace so it matches the expression in the group. The `\s*` is then left to march against zero characters. 
* To resolve this we can use `\b\` to capture the boundary between the word and the non-word characters and force the `\s` to match the actual white spaces. `cite\{\s*\b([^}]+)\b\s*\}`