https://digital.library.yorku.ca/yul-95212/hairdressing-mr-gino-bay-beauty-salon/datastream/MODS/view
https://digital.library.yorku.ca/yul-93087/dog-obedience-course-lawrence-plaza/datastream/MODS/view
https://digital.library.yorku.ca/yul-233240/mariposa-festival/datastream/MODS/view
http://digitalscholarship.utsc.utoronto.ca/projects/islandora/object/nearbystudies%3A546/datastream/MODS/view
http://digitalscholarship.utsc.utoronto.ca/projects/islandora/object/nearbystudies%3A585/datastream/MODS/view

## Setup

Install basex: http://basex.org/products/download/

Mac:
Install a JDK: http://www.oracle.com/technetwork/java/javase/downloads/index.html
You need to install homebrew: http://brew.sh/
Once that's installed, run
```brew install basex```

Windows: use installer
Linux: use the distribution package

In your terminal, run

```$ basexgui```


# Introduction
Introduction to XPath

XPath (which stands for XML Path Language) is an expression language used to specify parts of an XML document, which is designed to be used by XML tooling languages such as XSLT or XQuery. XPath used in other DOM structures like HTML.

In case you don't know what XML is, XML is a markup language. This means that it uses a set of tags or rules that provide information about its data. This structure helps to automate processing, editing, formatting, display, printing. It allows for exchange between incompatible systems and easier conversion of data.

XML documents stores data in plain text format. This provides a software- and hardware-independent way of storing, transporting, and sharing data.

Basic syntax rules
* XML elements must have an opening and closing tag, e.g. ``` <catfood> ``` opening tag and ``` </catfood>``` closing tag
* XML tags are case sensitive, e.g. ``` <catfood>``` does not equal ``` <catFood> ```
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

Lets begin our examples of using XPath

Load your data

1. If you've installed BaseX successfully, open your Terminal or command prompt and run BaseX by typing

    ``` $ basexgui ```
2. Create a new database by going into Database > New
3. Browse to your xml-samples directory, click on the book directory then select Choose. Hit OK.
4. Set the input bar option to XQuery and use that to enter in your XPath expressions

XPath Exercise:

- load data
- use input bar to do basic xpath and see what xml you get back (introduce xpath syntax)
- use input bar to do basic xpath using tree view



Selecting Nodes

XPath uses path expressions to select nodes in an XML document. The node is selected by following a path or steps.  We call it a 'path' because uses notations like URLS or unix directories, so using slashes to indicate traversing the structure of the document.

Looking at books.xml

```
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

XPath represents xml as a tree data structure. Here are some common terminologies to describe elements of the document tree:

root - top of the tree

child - nested directly under the element you're talking about

parent - converse of child, the node nested above the element you're talking about

sibling

level

path

In XPath, the most useful path expressions are listed below:

| Expression   | Description |
|-----------------|:-------------|
| nodename| Select all nodes with the name "nodename"   |
| /       | Select from the root node, subsequent slashes indicate selecting a child node from current node  |
| //      | Select direct and indirect child nodes in the document from the current node - this gives you the ability to "skip levels" |
| .       | Select the context node   |
|```..```      	| Select the parent of the current node
|@	      |Select attributes


Example:

| Path Expression   | Expression Result |
|-----------------|:-------------|
|catalog|	Select all nodes with the name "catalog"|
|/catalog|	Select the root element catalog. Note: If the path starts with a slash ( / ) it always represents an absolute path to an element!|

When your current context node is a book node:

| Path Expression   | Expression Result |
|-----------------|:-------------|
| . | Select the context book node|
| ```..``` | Select the context book node|
|/catalog/book/author| Select the author node|
|author| Select the author node|

1. talk about the difference between relative and absolute paths then show them an example using tree view


| Path Expression   | Expression Result |
|-----------------|:-------------|
|/catalog/book|	Select all book elements that are children of catalog|
|//book|	Select all book elements no matter where they are in the document|
|/catalog//book	| Select all book elements that are descendant of the catalog element, no matter where they are under the catalog element|
|//@lang|	Select all attributes that are named lang|

Predicates
Predicates are used to find a specific node or a node that contains a specific value.

Predicates are always embedded in square brackets.

In the table below we have listed some path expressions with predicates and the result of the expressions:

| Expression   | Expression Result |
|-----------------|:-------------|
| [1]  |Select the first element|
| [last()]  |Select the last element|
| [last()-1]  |Select the last but one element (also known as the second last element)|
|[position()<3]|Select the first two elements|
|[@lang]|	Select elements that have attribute 'lang'|
|[@lang='en']|	Select all the elements that have a "attribute" attribute with a value of "en"|
|[price>15.00]|	Select all elements that have a price element with a value greater than 15.00|


Selecting Unknown Nodes
XPath wildcards can be used to select unknown XML nodes.

|Wildcard	|Description|
|-----------------|:-------------|
|*	|Matches any element node|
|@*|	Matches any attribute node|
|node()|	Matches any node of any kind|

In the table below we have listed some path expressions and the result of the expressions:

|Path Expression|	Result|
|-----------------|:-------------|
|/catalog/*	|Select all the child element nodes of the catalog element|
|//*	|Select all elements in the document|
|//title[@*]	|Select all title elements which have at least one attribute of any kind|


TEST
|Path Expression|	Result|
|-----------------|:-------------|
| / or /.      |Select the document root node|
| /catalog      |Select the catalog node|
|  /catalog/book or //book     |Select all book element nodes|
|  /catalog/book/price or //price     |Select all price element nodes|
| //@lang      |Select all language attribute nodes|
|  //price/text() or /catalog/book/price/text()     |Select text nodes of all price element nodes|
|  /catalog/book/*     |Select all child nodes of book element nodes|
|   //@*    |Select all attributes|
|  ```//@lang/..```       |Select the immediate parent node of attribute language|
|/catalog/book[price>15.00]/title	|Select all the title elements of the book elements of the catalog element that have a price element with a value greater than 15.00|
|//title[not(@lang='en')]|hello|
|/catalog/book[title[not(@lang='en')]][position()<4]/author/text()|hello|



XPath Axes
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
|/descendant::book|Select all book element nodes|
|//attribute::lang|Select all lang attribute nodes|


XPath and in-text search
case-sensitive
//author[contains(.,"Matt")]
//author[starts-with(.,"G")]
//author[ends-with(.,"w")]

XPath and Regex matches
//author[matches(.,"Matt.*")]

XQuery

Introduction

FLWOR statements

For - the 'for' clause basically states: "for every item in a set of items, do something."
