# XPath and XQuery Tutorial

# XPath
## Introduction

XPath (which stands for XML Path Language) is an expression language used to specify parts of an XML document, which is designed to be used by XML tooling languages such as XSLT or XQuery. XPath used in other DOM structures like HTML.

In case you don't know what XML is, XML is a markup language. This means that it uses a set of tags or rules that provide information about its data. This structure helps to automate processing, editing, formatting, display, printing. It allows for exchange between incompatible systems and easier conversion of data.

XML documents stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data.

Basic syntax rules
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

* XML attribute values must be quoted, e.g.
``` <catfood type="basic"></catfood> ```

XPath is written using expressions, and when these expressions are evaluated on XML documents they produce an object. XPath is typically used to select nodes, compare nodes, ?but technically you can't produce a node or list of nodes?. For that you would want to use something like XQuery.

So unlike regex, you're usually not doing searches on text (though it is possible). Instead, if you have structured documents like these you're doing searches on nodes that tell you about your data. It's basically like doing a search on metadata and seeing the data results you get back.

Now, lets begin to use XPath.


## Practice

We have an export of our data of recent book purchases

### Loading data in BaseX

1. If you've installed BaseX successfully, open your Terminal or command prompt and run BaseX by typing
    ```bash
    $ basexgui
    ```
2. Create a new database by going into Database > New
3. Browse to your `xpath-xquery` directory, click on the `data-books` directory then select Choose. Hit OK.
4. Set the input bar option to XQuery and use that to enter in your XPath expressions

BASEX IS...ADD MORE INFO

* Editor
* Result
* Query Info
* Visualizations: Tree
* Input Bar

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

XPath represents xml as a tree data structure. Here are some common terminologies to describe elements of the XML document tree:

**node** - XML trees are composed of connected XML elements in a hierarchy = nodes of the tree. Note: Nodes and elements are used interchangeably in this lesson.

**level** - a level represents a hierahical connection from one node to another

**path** - the sequence of connections from node to node

**root** - referring to the top of the hierarchy of your XML tree structure

**child** - a node connected directly under the node you're talking about (one level below current node)

**parent** - converse of child, the node connected above the element you're talking about  (one level above current node)

**sibling** - nodes with same parent (same level as current node)

XPath uses path expressions to select nodes in an XML document. The node is selected by following a path or steps. XPath uses the slash to denote traversal of the structure of your document in a path, in the same way as URLs or unix directories.


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

1. talk about the difference between relative and absolute paths then show them an example using tree view

## Operators

Operators are .... ADD MORE INFO

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
|```/catalog/book```|	Select all book elements that are children of catalog|
|```//book```|	Select all book elements no matter where they are in the document|
|```/catalog//book```	| Select all book elements that are descendant of the catalog element, no matter where they are under the catalog element|
|```//@lang```|	Select all attributes that are named lang|
|```/catalog/book[not(@id="bk101")]```|Select all book elements except for the book that has an id "bk101"|


### Exercises

| Expression   | Result |
|-----------------|:-------------|
||I want to see the categories of all of the books but also the publish date.|

## Predicates

Predicates are used to find a specific node or a node that contains a specific value.

Predicates are always embedded in square brackets, and are meant to provide additional filtering information on a node in an expression.

In the table below we have listed some path expressions with predicates and the result of the expressions:

| Expression   | Result |
|-----------------|:-------------|
| ```[1]```  |Select the first element|
| ```[last()]```  |Select the last element|
| ```[last()-1]```  |Select the last but one element (also known as the second last element)|
|```[position()<3]```|Select the first two elements, note the first position starts at 1, not = |
|```[@lang]```|	Select elements that have attribute 'lang'|
|```[@lang='en']```|	Select all the elements that have a "attribute" attribute with a value of "en"|
|```[price>15.00]```|	Select all elements that have a price element with a value greater than 15.00|

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

XPath can do in-text searching and also supports regex with its matches() function. Note: in-text searching is case-sensitive!

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

XPath Axes are .... ADD MORE INFO

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

## FLWOR statements

**For** - the 'for' clause basically states: "for every item in a set of items, do something."

The 'for' clause in XQuery iteratively assigns a variable to every item in a set of items selected using XPath.

e.g.
```
for $titleitem in fn:doc("books.xml")/catalog/book/title
return $titleitem
```

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


## XQuery Update

XQuery has an extension called [XQuery Update Facility](https://www.w3.org/TR/xquery-update-10/)

The XQuery Update Facility provides five basic operations acting upon XML nodes:

* insert one or several nodes inside/after/before a specified node
* delete one or several nodes
* replace a node (and all its descendants if it is an element) by a sequence of nodes.
* replace the contents (children) of a node with a sequence of nodes, or the value of a node with a string value.
* rename a node (applicable to elements, attributes and processing instructions) without affecting its contents or attributes.

BaseX has a [complete implementation](http://docs.basex.org/wiki/XQuery_Update) of the XQuery Update specification.

Running

```
for $zonenode in collection(data-collection-plants)//ZONE
return insert node $zonenode after $zonenode
```

Will find the nodes that match the xpath expression `//ZONE`, then insert an identical <ZONE /> node wherever that node occurs in the document.

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
