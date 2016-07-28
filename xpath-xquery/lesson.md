# XPath and XQuery Tutorial

# XPath
## Introduction

XPath (which stands for XML Path Language) is an expression language used to specify parts of an XML document, which is designed to be used by XML tooling languages such as XSLT or XQuery. XPath can also be used documents with similar structures to XML, like HTML.

In case you don't know what XML is, XML is a markup language. This means that it uses a set of tags or rules that provide information about its data. This structure helps to automate processing, editing, formatting, display, printing.

XML documents stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data. This allows for exchange between incompatible systems and easier conversion of data.

Basic syntax rules
* An XML document is structured using nodes, which include element nodes, attribute nodes and text nodes
* XML elements must have an opening and closing tag, e.g. `<catfood> ` opening tag and ` </catfood>` closing tag
* XML tags are case sensitive, e.g. ` <catfood>` does not equal ` <catFood> `
* XML elements must be properly nested:

```
<catfood>
  <manufacturer>Purina</manufacturer>
    <address> 12 Cat Way, Boise, Idaho, 21341</address>
  <date>2019-10-01</date>
</catfood>
```
* Text nodes (data) are contained inside the opening and closing tags
* XML attribute values must be quoted, e.g.
``` <catfood type="basic"></catfood> ```

XPath is written using expressions, and when these expressions are evaluated on XML documents they produce an object. XPath is typically used to select nodes and compare nodes, but if you want manipulate or edit nodes you would want to use something like XQuery.

You're not querying raw text or just data values like you would in regex. Instead, XPath recognizes that there is a node structure to your document, which allows you to do searches on those nodes that tell you something about your data.

Think of using XPath as a way to do an advanced search like you would in a library catalogue. You can do a search on specific metadata fields by specifying them and then you can see the data results you get back. The benefit of this is that you don't have to know what your data looks like in order to get results back, you just have to know what kind of data you're looking for.

Now, lets begin to use XPath.

## Practice

In this scenario, we received an XML export the most popular books in our system and we want to learn more about these books because it will help inform future purchases.

### Loading data in BaseX

1. If you've installed BaseX successfully, open your Terminal or command prompt and run BaseX by typing
    ```bash
    $ basexgui
    ```
2. Create a new database by going into Database > New
3. Browse to your `xpath-xquery` directory, click on the `data-books` directory then select Choose. Hit OK.
4. Set the input bar option to XQuery and use that to enter in your XPath expressions

BaseX is an XML database engine that allows you to work with XML documents. You can work with it from the command line, but it also provides a simple GUI.

It implements XQuery 3.1/XPath 2.0 according to the W3C standard. That means we can work with XML fragments, XML files, or databases of XML documents by using XPath and XQuery. BaseX also provides visualizations, simple search and its own set of [commands](http://docs.basex.org/wiki/Commands) which won't be covered in this lesson.

* Input Bar: where you can input your XPath expressions or XQuery queries in a single line
* Editor: write and edit XQuery code, XML
* Result: query result window
* Query Info: processing information from your XPath/XQuery statements
* Tree View: provides a tree visualization of your XML document

Looking at `xpath-xquery/data-books/books.xml`:**

```xml
<?xml version="1.0"?>
<catalog>
   <book id="bk101" category="TECHNOLOGY">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <publish_date>2000-10-01</publish_date>
      <description>An in-depth look at creating applications
      with XML.</description>
   </book>
   <book id="bk102" category="FANTASY">
      <author>
      <name>Ralls, Kim</name>
      <secondaryname>Ralston, Kim</secondaryname>
      </author>
      <title lang='en'>Midnight Rain</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2000-12-16</publish_date>
      <description>A former architect battles corporate zombies,
      an evil sorceress, and her own childhood to become queen
      of the world.</description>
      <description>Not sure what the title has to do with corporate zombies.</description>
      <description>Not sure what the title has to do with evil queens.</description>
   </book>
   <book id="bk103" category="FANTASY">
      <author>Corets, Eva</author>
      <title lang='fr'>Maeve Ascendant</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2000-11-17</publish_date>
      <description>After the collapse of a nanotechnology
      society in England, the young survivors lay the
      foundation for a new society.</description>
   </book>
   <book id="bk104" category="FICTION">
      <author>Corets, Eva</author>
      <title lang='en'>Oberon's Legacy</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2001-03-10</publish_date>
      <description>In post-apocalypse England, the mysterious
      agent known only as Oberon helps to create a new life
      for the inhabitants of London. Sequel to Maeve
      Ascendant.</description>
   </book>
   <book id="bk105" category="FICTION">
      <author>Corets, Eva</author>
      <title lang='it'>The Sundered Grail</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2001-09-10</publish_date>
      <description>The two daughters of Maeve, half-sisters,
      battle one another for control of England. Sequel to
      Oberon's Legacy.</description>
   </book>
   <book id="bk106" category="NON-FICTION">
      <author>Randall, Cynthia</author>
      <title lang='en'>Lover Birds</title>
      <genre>Romance</genre>
      <price>4.95</price>
      <publish_date>2000-09-02</publish_date>
      <description>When Carla meets Paul at an ornithology
      conference, tempers fly as feathers get ruffled.</description>
   </book>
   <book id="bk107" category="ROMANCE">
      <author>Thurman, Paula</author>
      <title>Splish Splash</title>
      <genre>Romance</genre>
      <price>4.95</price>
      <publish_date>2000-11-02</publish_date>
      <description>A deep sea diver finds true love twenty
      thousand leagues beneath the sea.</description>
   </book>
   <book id="bk108" category="FICTION">
      <author>Knorr, Stefan</author>
      <title>Creepy Crawlies</title>
      <genre>Horror</genre>
      <price>12.95</price>
      <publish_date>2000-12-06</publish_date>
      <description>An anthology of horror stories about roaches,
      centipedes, scorpions  and other insects.</description>
   </book>
   <book id="bk109" category="SCIFI">
      <author>Kress, Peter</author>
      <title>Paradox Lost</title>
      <genre>Science Fiction</genre>
      <price>15.95</price>
      <publish_date>2000-11-02</publish_date>
      <description>After an inadvertant trip through a Heisenberg
      Uncertainty Device, James Salway discovers the problems
      of being quantum.</description>
   </book>
   <book id="bk110" category="TECHNOLOGY">
      <author>O'Brien, Tim</author>
      <title>Microsoft .NET: The Programming Bible</title>
      <genre>Computer</genre>
      <price>36.95</price>
      <publish_date>2000-12-09</publish_date>
      <description>Microsoft's .NET initiative is explored in
      detail in this deep programmer's reference.</description>
   </book>
   <book id="bk111" category="">
      <author>O'Brien, Tim</author>
      <title>MSXML3: A Comprehensive Guide</title>
      <genre>Computer</genre>
      <price>36.95</price>
      <publish_date>2000-12-01</publish_date>
      <description>The Microsoft MSXML3 parser is covered in
      detail, with attention to XML DOM interfaces, XSLT processing,
      SAX and more.</description>
   </book>
   <book id="bk112" category="">
      <author>Galos, Mike</author>
      <title>Visual Studio 7: A Comprehensive Guide</title>
      <genre>Computer</genre>
      <price>49.95</price>
      <publish_date>2001-04-16</publish_date>
      <description>Microsoft Visual Studio 7 is explored in depth,
      looking at how Visual Basic, Visual C++, C#, and ASP+ are
      integrated into a comprehensive development
      environment.</description>
   </book>
</catalog>

```


## Selecting Nodes

In BaseX, bring up the tree visualization of your document.

XPath understands XML as a tree data structure. XPath expressions are written in a way that represents searching and traversing through this tree. In other words, a node is selected by following a path or a number of steps to get to that node.

![XML Node Tree](http://www.w3schools.com/xml/nodetree.gif)

Here are some common terminologies to describe the different parts of the XML document tree:

**node** - A node is a unit in the document. A node can be an element node, an attribute node, a text node.

**element** - XML trees are composed of connected XML elements in a hierarchy = nodes of the tree. An XML element is everything from (including) the element's start tag to (including) the element's end tag.

**level** - a level represents a hierarchical connection from one node to another

**path** - the sequence of connections from node to node

**root** - referring to the top of the hierarchy of your XML tree structure

**child** - a node connected directly under the node you're talking about (one level below current node)

**parent** - converse of child, the node connected above the element you're talking about  (one level above current node)

**sibling** - nodes with same parent (same level as current node)

XPath uses the slash to denote traversal of the structure of your document in a path, in the same way as URLs or unix directories.

## Abbreviated Syntax

In XPath, all of your expressions are evaluated based on a context. The default context is your root node, indicated by a slash (/).

The most useful path expressions are listed below:

| Expression   | Description |
|-----------------|:-------------|
| ```nodename```| Select all nodes with the name "nodename"   |
| ```/```  | Select from the root node, subsequent slashes indicate selecting a child node from current node  |
| ```//``` | Select direct and indirect child nodes in the document from the current node - this gives you the ability to "skip levels" |
| ```.```       | Select the context node, the context node being the current node you're starting your path expression from   |
|```..```  | Select the parent of the context node|
|```@```   |Select attributes|


### Examples

| Path Expression   | Expression Result |
|-----------------|:-------------|
|```catalog```|	Select all nodes with the name "catalog"|
|```/catalog```|	Select the root element catalog. Note: If the path starts with a slash ( / ) it always represents an absolute path to an element!|
|```//author```| Select all nodes with the name "author"|
|```//author/..``` |Selects all of the parents of the nodes with the name "author"|
|```/catalog/book[@id="bk101"]```|Select book nodes where the id attribute corresponds to "bk101"|


### Exercises

Now you try XPath using a different context. In BaseX, if you go to the tree view and double-click on a book node, your context will start at that book node. From your current context:

| Path Expression   | Expression Result |
|-----------------|:-------------|
|  | Select the context book node|
| | Select the context's parent node|
|| Select the author node|
|| Select the author node irregardless of context - the absolute path|

## Operators

Operators are used to compare nodes. There are mathematical operators, boolean operators. Here are some useful ones:

| Operator   | Explanation |
|-----------------|:-------------|
| &#124;|Pipe chains expressions and brings back results from either expression |
|```=```|Equivalent comparison, can be used for numeric or text values|
|```!=```|Is not equivalent comparison|
|```<, <=```|Greater than, greater than or equal to|
|```>, >=```|Less than, less than or equal to|
|```or```|Boolean or|
|```and```|Boolean and|
|```not```|Boolean not|

Note: '!=' != 'not', for instance in this snippet

```xml
<book id='bk101'></book>
<book></book>
<book type='paperback'></book>
<book id='bk102'></book>
<book id='bk103'></book>
```

The expression ```@id != 'bk101'``` will bring back

```xml
<book id='bk102'></book>
<book id='bk103'></book>
```

While the expression ```not(@id='bk101')``` will bring back

```xml
<book></book>
<book type='paperback'></book>
<book id='bk102'></book>
<book id='bk103'></book>
```

This is because != indicates the existence of an @id, whie the not() expression expresses to bring back everything except @id='bk101'

### Examples

| Path Expression   | Expression Result |
|-----------------|:-------------|
|```/catalog/book```|	Select all book nodes that are children of catalog|
|```//book```|	Select all book nodes no matter where they are in the document|
|```/catalog//book```	| Select all book nodes that are descendant of the catalog nodes, no matter where they are under the catalog nodes|
|```//@lang```|	Select all attributes that are named lang|
|```/catalog/book[not(@id="bk101")]```|Select all book nodes except for the book that has an id "bk101"|


### Exercises

| Expression   | Result |
|-----------------|:-------------|
||I want to see the categories of all of the books but also the publish date.|
||Select books that are either romance or fiction and are less than ten dollars. Hint: use `and` and `or`|

## Predicates

Predicates are used to find a specific node or a node that contains a specific value.

Predicates are always embedded in square brackets, and are meant to provide additional filtering information on a node in an expression.

In the table below we have listed some path expressions with predicates and the result of the expressions:

| Expression   | Result |
|-----------------|:-------------|
| ```[1]```  |Select the first node|
| ```[last()]```  |Select the last node|
| ```[last()-1]```  |Select the last but one node (also known as the second last node)|
|```[position()<3]```|Select the first two nodes, note the first position starts at 1, not = |
|```[@lang]```|	Select nodes that have attribute 'lang'|
|```[@lang='en']```|	Select all the nodes that have a "attribute" attribute with a value of "en"|
|```[price>15.00]```|	Select all nodes that have a price node with a value greater than 15.00|

What other values can you use on text in xml? you can see numbers, text, booleans

Selecting Unknown Nodes
XPath wildcards can be used to select unknown XML nodes.

|Wildcard	|Description|
|-----------------|:-------------|
|```*```	|Matches any element node|
|```@*```|	Matches any attribute node|
|```node()```|	Matches any node of any kind|


In the table below we have listed some path expressions and the result of the expressions:

|Path Expression|	Result|
|-----------------|:-------------|
|```/catalog/*```	|Select all the child element nodes of the catalog element|
|```//*```	|Select all elements in the document|
|```//title[@*]```	|Select all title elements which have at least one attribute of any kind|


### Exercises

|Path Expression|	Result|
|-----------------|:-------------|
|   ```//@*```    |What do you expect as your result?|
|  |For all nodes that have the language attribute, select the immediate parent|
||Select all the title elements of the book elements of the catalog element that have a price element with a value greater than 15.00|
|```//title[@lang!="en"]```|What do you expect as your result?|
|```/catalog/book[title[not(@lang='en')]][position()<4]/author/text()```|What do you expect as your result?|


## In-text search

XPath can do in-text searching using functions and also supports regex with its matches() function. Note: in-text searching is case-sensitive!

|Path Expression|	Result|
|-----------------|:-------------|
|```//author[contains(.,"Matt")]```| Matches on all author nodes, in current node contains Matt (case-sensitive)|
|```//author[starts-with(.,"G")]```|Matches on all author nodes, in current node starts with G (case-sensitive)|
|```//author[ends-with(.,"w")]```|Matches on all author nodes, in current node ends with w (case-sensitive)|
|```//author[matches(.,"Matt.*")]```| regular expressions match 2.0 |

### Exercises

| Expression   | Result |
|-----------------|:-------------|
||Match all publish date nodes, from January to May (Note: all dates are in yyyy-mm-dd format)|

### Exercises

Now try XPath with `xpath-xquery/data-menu/menu.xml`

| Expression   | Result |
|-----------------|:-------------|
||I want to know all of the foods with a nutritional value of 800 calories and less than or equal to 200 grams of sugar|
||I want to view the reviews of all foods with a review rating below 5|
||I want to compare the corporate and review description of these foods|
||I want to compare the cost of a food, the amount of sugar, and its review rating|
||I want to find all foods that have Waffle in its name|


## Complete syntax: XPath Axes

XPath Axes fuller syntax of how to use XPath. Provides all of the different ways to specify the path by describing more fully the relationships between nodes and their connections. The XPath specification describes 13 different axes:

* self ‐‐ the context node itself
* child ‐‐ the children of the context node
* descendant ‐‐ all descendants (children+)
* parent ‐‐ the parent (empty if at the root)
* ancestor ‐‐ all ancestors from the parent to the root
* descendant‐or‐self ‐‐ the union of descendant and self • ancestor‐or‐self ‐‐ the union of ancestor and self
* following‐sibling ‐‐ siblings to the right
* preceding‐sibling ‐‐ siblings to the left
* following ‐‐ all following nodes in the document, excluding descendants
* preceding ‐‐ all preceding nodes in the document, excluding ancestors • attribute ‐‐ the attributes of the context node


|Path Expression|	Result|
|-----------------|:-------------|
|```/descendant::book```|Select all book element nodes|
|```//attribute::lang```|Select all lang attribute nodes|



# XQuery

## Introduction

XQuery is a language used to query XML data. Single files, collection of files, or databases.

Below are a few examples of how XQuery can be used:

* Querying XML data to return XML documents
* Extracting and searching through XML data
* Combining, grouping, sorting, aggregating XML data
* Transforming XML documents into other XML, HTML or markup-based documents
* Cleaning XML data
* Publishing data from databases onto the web or in applications

## Functions
We've been using functions like contains, matches. For simplicity, BaseX hides the complete query but we were using the fn:doc function everytime we were querying a document!

A function is an action or set of actions that you can reuse. In XPath/XQuery, a function takes in a parameter or set of parameters to bring back a new result.

Functions on strings and numeric types, recognize dates and can do comparisons. For a list of functions, visit the [W3C Function specification.](https://www.w3.org/TR/xpath-functions/#func-replace)

Some useful string functions:

* fn:replace('query', 'input', 'replacementvalue')
* fn:upper-case('query')
* fn:lower-case('query')
* fn:normalize-space('query')

It's also possible to write your own reusable functions!

## FLWOR statements

XQuery statements are written with FLWOR clauses. If you are familiar with SQL, you structure your queries using clauses like SELECT, FROM, WHERE clauses and similarly can be used to join documents.

**For** - the 'for' clause basically states: "for every item in a set of items, do something."

The 'for' clause in XQuery iteratively assigns a variable to every item in a set of items selected using XPath.

e.g. if you were to copy and paste this query into the Editor window:

```
for $titleitem in fn:doc("books.xml")/catalog/book/title
return $titleitem
```

You would get all of the titles of each book back.

**Let** - the 'let' clause basically declares a value without iteration. In XQuery, you assign a single result to a variable using let, which can be a single value, element or a whole set of elements. Your subsequent statements will act on an aggregate set of items.

e.g.

```
let $cost = 300
```

e.g.

```
let $prices := fn:doc("books.xml")/catalog/book/price
let $sum := sum($prices)
return $sum
```

e.g.

```
for $author in fn:doc("books.xml")//author
  let $secondname := $author//secondaryname
return $secondname
```

**Where** - the 'where' clause is a boolean (true/false) statement that filters out nodes that do not satisfy this statement

```
for $author in fn:doc("books.xml")//author
  let $secondname := $author//secondaryname
  where $secondname[starts-with(.,"C")]
return $secondname
```

**Order By** - the default order of the results of an XPath/XQuery expression is the document order. the 'order' clause will sort or group items together based on this expression

e.g.
```
for $title in fn:doc("books.xml")/catalog/book/title
order by $title descending
return $title
```

**Return** - the 'return' clause will bring back specified the nodes


### Exercises


Generate a report of all Fantasy books alphabetically sorted by author

```
<report><title>Book Report Stats</title> {
for $item in fn:doc("books.xml")/catalog/book
let $author := $item/author/text()
let $title := $item/title/text()
where fn:contains($item/genre, "Fantasy")
order by $title
return<object><id>{$author}</id><title>{$title}</title></object> }</report>
```

## Querying Databases

Up until now we've been querying single documents, but XPath and XQuery lets you query multiple documents using fn:collection("databasename") or in BaseX you can just use collection("databasename"). To specify a single document use fn:doc("file") or in a database in BaseX use db:open("database", "file").

XPath example:
```
fn:collection("data-collection-plants")/CATALOG/PLANT/COMMON
```

## XQuery Update

XQuery has an extension called [XQuery Update Facility](https://www.w3.org/TR/xquery-update-10/)

In SQL there is the UPDATE clause which is used to update records in a table. In XQuery, the XQuery Update Facility (XQUF) provides five basic operations acting upon XML nodes:

* **insert node:** insert one or several nodes inside/after/before a specified node
* **delete node:** delete one or several nodes
* **replace node:** replace a node (and all its descendants if it is an element) by a sequence of nodes.
* **replace value of node:** replace the contents (children) of a node with a sequence of nodes, or the value of a node with a string value.
* **rename node:** rename a node (applicable to elements, attributes and processing instructions) without affecting its contents or attributes.

BaseX has a [complete implementation](http://docs.basex.org/wiki/XQuery_Update) of the XQuery Update specification that you'll want to take a look at to structure your queries.

### Example

Running

```
for $zonenode in collection(data-collection-plants)//ZONE
return insert node $zonenode after $zonenode
```

Will find the nodes that match the xpath expression `//ZONE`, then insert an identical <ZONE /> node wherever that node occurs in the document.

### Exercises

* Rename the AVAILABILITY node to SERIALNO in the entire plant database.

```
for $availability in fn:collection(data-collection-plants)//AVAILABILITY
return rename node $availability as 'SERIALNO'
```

* Replace all occurrences of the word leaf with leaves in the entire plant database.

```
for $text in fn:collection(data-collection-plants)//text()
return replace value of node $text with fn:replace($text, "leaf", "leaves")
```
### Non-updating functions

There's also copy, modify, return. BaseX also has its own update function.

# Reference

## Setup

[Install basex](http://basex.org/products/download/)

Mac:
[Install a JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
You need to install [homebrew](http://brew.sh/)
Once that's installed, run
```bash
brew install basex
```

Windows: use installer
Linux: use the distribution package

In your terminal, run

```$ basexgui```

## Additional Resources
[XML Path Language (XPath) W3C Recommendation](https://www.w3.org/TR/xpath/)

## XML data samples in the wild

[York University 1](https://digital.library.yorku.ca/yul-95212/hairdressing-mr-gino-bay-beauty-salon/datastream/MODS/view)

[York University 2](https://digital.library.yorku.ca/yul-93087/dog-obedience-course-lawrence-plaza/datastream/MODS/view)

[York University 3](https://digital.library.yorku.ca/yul-233240/mariposa-festival/datastream/MODS/view)

[University of Toronto Scarborough 1](http://digitalscholarship.utsc.utoronto.ca/projects/islandora/object/nearbystudies%3A546/datastream/MODS/view)

[University of Toronto Scarborough 2](http://digitalscholarship.utsc.utoronto.ca/projects/islandora/object/nearbystudies%3A585/datastream/MODS/view)
