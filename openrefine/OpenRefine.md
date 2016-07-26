---
Software/Library Carpentry - July 28-29, 2016
---
## Setup
Please look at the Installation Instructions from the OpenRefine project for more details on how to run OpenRefine on your machine. The instructions below are adapted from this [link](https://github.com/OpenRefine/OpenRefine/wiki/Installation-Instructions). We will be using version [2.6-rc2](https://github.com/OpenRefine/OpenRefine/releases/tag/2.6-rc.2) during the workshop. A [Java Runtime Environment (JRE)]('https://www.java.com/en/download/manual.jsp') is required to run OpenRefine. If the installation procedure below fails, make sure you have a working JRE installed on your computer.

###Windows

1. Download [OpenRefine v. 2.6-rc2 for Windows](https://github.com/OpenRefine/OpenRefine/releases/download/2.6-rc.2/openrefine-win-2.6-rc.2.zip)
2. Once you have downloaded the .zip file, uncompress it into a folder wherever you want (such as in C:\Open-Refine).
3. To launch OpenRefine, run the .exe file in that folder. You should see the Command window in which OpenRefine runs.
4. To shut down OpenRefine, press Ctrl-C in the command window that is running OpenRefine. Wait until there's a message that says the shutdown is complete. That window might close automatically, or you can close it yourself. If you get asked, "Terminate all batch processes? Y/N", just press Y.

###Mac OSX

1. Download [OpenRefine v. 2.6-rc2 for Mac](https://github.com/OpenRefine/OpenRefine/releases/download/2.6-rc.2/openrefine-mac-2.6-rc.2.dmg)
2. Once you have downloaded the .dmg file, open it, and drag the OpenRefine icon into the Applications folder.
3. To launch OpenRefine, double-click the OpenRefine app. You'll see the OpenRefine app appear in your dock.
4. If you get an error message preventing you from opening the app because it's from an unidentified developer, do the following (you only have to do it once when you open the app for the first time):
	1. Press the ctrl (Control) key and click on the app icon
	2. Choose Open from the shortcut menu
	3. There should now be an Open button under the "unidentified developer" error message. Click that button to open the app.
5. To shut down OpenRefine, right-click on its icon in the Dock and choose the Quit option.

###Linux

1. Download [OpenRefine v. 2.6-rc2 for Linux](https://github.com/OpenRefine/OpenRefine/releases/download/2.6-rc.2/openrefine-linux-2.6-rc.2.tar.gz)
2. Once you have downloaded the .tar.gz file, uncompress it into a folder wherever you want.
3. To launch OpenRefine, open a shell, navigate to that folder and type ./refine
4. To shut down OpenRefine, press Ctrl-C in the shell that is running OpenRefine.

### Running OpenRefine

OpenRefine is operated from within a web browser (such as Chrome or Firefox). If your browser doesn't open automatically when you start OpenRefine (see above), navigate to [http://127.0.0.1:3333/](http://127.0.0.1:3333/) in your favourite browser to open the OpenRefine window. Please note that even though you use a browser to operate OpenRefine, it is still run locally on your machine, and not on the web. Your data never leaves your machine.

## What is OpenRefine?
OpenRefine is described as a tool for working with ‘messy’ data - but what does this mean? It is probably easiest to describe the kinds of data OpenRefine is good at working with and the sorts of problems it can help you solve.

OpenRefine is most useful where you have data in a simple tabular format, but with internal inconsistencies either in data formats, or where data appears, or in terminology used. It can help you:

* Get an overview of a data set
* Resolve inconsistencies in a data set
* Help you split data up into more granular parts
* Match local data up to other data sets
* Enhance a data set with data from other sources

Some common scenarios might be:

* Where you want to know how many times a particular value appears in a column in your data
* Where you want to know how values are distributed across your whole data set
* Where you have a list of dates which are formatted in different ways, and want to change all the dates in the list to a single common date format. For example:

| Data you have   | Desired data |
|-----------------|:-------------|
| 1st January 2014| 2014-01-01   |
| 01/01/2014      | 2014-01-01   |
| Jan 1 2014      | 2014-01-01   |
| 2014-01-01      | 2014-01-01   |

* Where you have a list of names or terms that differ from each other but refer to the same people, places or concepts. For example:

| Data you have   | Desired data |
|-----------------|:-------------|
| London          | London       |
| London]         | London       |
| London,]        | London       |
| london          | London       |
 
* Where you have several bits of data combined together in a single column, and you want to separate them out into individual bits of data with one column for each bit of the data. For example going from a single address field (in the first column), to each part of the address in a separate field:

| Address in single field | Institution  | Library name  | Address 1 | Address 2 | Town/City | Region | Country | Postcode |
|-------------------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|
| University of Wales, Llyfrgell Thomas Parry Library, Llanbadarn Fawr, ABERYSTWYTH, Ceredigion, SY23 3AS, United Kingdom | University of Wales | Llyfrgell Thomas Parry Library | Llanbadarn Fawr | Aberystwyth | Ceredigion | United Kingdom | SY23 3AS |
| University of Aberdeen, Queen Mother Library, Meston Walk, ABERDEEN, AB24 3UE, United Kingdom | University of Abderdeen | Queen Mother Library | Meston Walk | Aberdeen | United Kingdom | AB24 3UE |
| University of Birmingham, Barnes Library, Medical School, Edgbaston, BIRMINGHAM, West Midlands, B15 2TT, United Kingdom | University of Birmingham | Barnes Library | Medical School | Edgbaston | Birmingham | West Midlands | United Kingdom | B15 2TT |
| University of Warwick, Library, Gibbett Hill Road, COVENTRY, CV4 7AL, United Kingdom | University of Warwick | Library | Gibbett Hill Road | Coventry | United Kingdom | CV4 7AL |

* Where you want to add to your data from an external data source:

| Data you have   | Date of Birth from VIAF (Virtual International Authority File) | Date of Death from VIAF (Virtual International Authority File) |
|-----------------|:-------------|:-------------|
| Braddon, M. E. (Mary Elizabeth) | 1835 | 1915 |
| Rossetti, William Michael       | 1829 | 1919 |
| Prest, Thomas Peckett           | 1810 | 1879 |

---
###Key Points
* OpenRefine is a 'tool for working with messy data'
* OpenRefine works best with data in a simple tabular format
* OpenRefine can help you split data up into more granular parts
* OpenRefine can help you match local data up to other data sets
* OpenRefine can help you enhance a data set with data from other sources
___

## Importing data

### Exercise 1: Create your first Open Refine project (using provided data)
There are several options for getting your data set into OpenRefine. You can upload or import files in a variety of formats including:

* TSV (tab-separated values)
* CSV (comma-separated values)
* Excel
* JSON (javascript object notation)
* XML
* Google Spreadsheet

To import the data for the exercises below, download ['doaj-article-sample.csv'](http://labs.timtom.ch/library-openrefine/data/doaj-article-sample.csv), make note of the file's location, run OpenRefine and:

* Click 'Create Project'
* Choose 'Get Data from this Computer'
* Click 'Choose Files'
* Locate the file called which you previously downloaded 'doaj-article-sample.csv'
* Click 'Next'

The next screen gives you some options to ensure that the data gets imported into OpenRefine correctly. The options vary depending on the type of data you are importing.

In this case you need to:

* Set the 'Character encoding' to ['UTF-8'](https://www.w3.org/International/questions/qa-what-is-encoding)
* Ensure the first row is used to create the column headings
* Make sure OpenRefine doesn't try to automatically detect numbers and dates

Once you are happy click 'Create Project >>'

This will create the project and open it for you. Projects are saved as you work on them, there is no need to save copies as you go along.

To open an existing project in OpenRefine you can click 'Open Project' from the main OpenRefine screen (in the lefthand menu). When you click this, you will see a list of the existing projects and can click on a project's name to open it.

### Going Further
* Look at the other options on the Import screen - try changing some of these options and see how that changes the Preview and how the data appears after import.
* Do you have access to JSON or XML data? If so the first stage of the import process will prompt you to select a 'record path' - that is the parts of the file that will form the data rows in the OpenRefine project.

---
###Key Points

* Use the 'Create Project' option to import data
* You can control how data imports using options on the import screen

---
## The layout of OpenRefine
OpenRefine displays data in a tabular format. Each row will usually represent a 'record' in the data, while each column represents a type of information. This is very similar to how you might view data in a spreadsheet or database.

OpenRefine only displays a limited number of lines of data at one time. You can adjust the number choosing between 5, 10 (the default), 25 and 50.

## Reordering and renaming columns
Many operations in OpenRefine are accessed from the drop down menus at the top of each column. You can re-order the columns by clicking the drop down menu at the top of the first column (labelled 'All'), and choosing 'Edit columns->Re-order / remove columns …'

You can then drag and drop column names to re-order the columns, or remove columns completely if they are not required.

## Sorting data
You can sort data in OpenRefine by clicking on the drop down menu for the column you want to sort on, and choosing 'Sort'

Once you have sorted the data a new '**Sort**' drop down menu will be displayed at the top of the table.


Unlike Excel 'Sorts' in OpenRefine are temporary - that is, if you remove the 'Sort', the data will go back to it's original 'unordered' state. The 'Sort' drop down menu at the top of the table lets you amend the existing sort (e.g. reverse the sort order), remove existing sorts, and make sorts permanent.

You can sort on multiple columns at the same time by adding another sorted column (in the same way).

## Facets
Facets are one of the most useful features of OpenRefine and can help both get an overview of the data in a project as well as helping you bring more consistency to the data.

A 'Facet' allows you to explore a particular dimension of a dataset. It groups all the values that appear in a column, and then allows you to filter the data by these values and edit values across many records at the same time.

The simplest type of Facet is called a 'Text facet'. This simply groups all the text values in a column and lists each value with the number of records it appears in. The facet information always appears in the left hand panel in the OpenRefine interface.

To create a Text Facet for a column, click on the drop down menu at the top of the column and choose 'Facet -> Text Facet'. The facet will then appear in the left hand panel.

The facet consists of a list of values used in the data. You can filter the data displayed by clicking on one of these headings.

You can include multiple values from the facet in a filter at one time by using the 'Include' option which appears when you put your mouse over a value in the Facet.

You can also 'invert' the filter to show all records which do not match your selected values. This option appears at the top of the Facet panel when you select a value from the facet to apply as a filter.

To remove a Facet, hit the 'x' in the top left of the Facet box.

## Exercise 2: Which licences are used for articles in this file?
* Create a facet for the 'Licence' column
* What is the most common licence in the file?
* How many articles in the file don't have a licence assigned?

## Amending data through facets
If you create a text facet you can edit the values in the facet to change the value for several records at the same time. To do this, simply mouse-over the value you want to edit and click the 'edit' option that appears.

This approach is useful in relatively small facets where you might have small variations through punctuation or typing errors etc. For example, a column that should contain only terms from a small restricted list such as days of the week or months of the year.

The list of values in the facet will update as you make edits.

## Exercise 3: Correct the Language values via a facet
* Create a Text facet on the Language column
* Notice that there is both 'EN' and 'English'
* Put the mouse over the 'English' value
* Click 'Edit'
* Type 'EN' and click 'Apply'
* See how the Language facet updates

## More on Facets
As well as 'Text facets' Refine also supports a range of other types of facet. These include:

* Numeric facets
* Timeline facets (for dates)
* Custom facets
* Scatterplot facets

**Numeric and Timeline facets** display graphs instead of lists of values. The graph includes 'drag and drop' controls you can use to set a start and end range to filter the data displayed.

**Scatterplot facets** are less commonly used - for further information on these see the tutorial at http://enipedia.tudelft.nl/wiki/OpenRefine_Tutorial#Exploring_the_data_with_scatter_plots

**Custom facets** are a range of different types of facets, and also allow you write your own custom facets. Some of the default custom facets are:

* **Word facet** - this breaks down text into words and counts the number of records each word appears in
* **Duplicates facet** - this results in a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if the value in the selected column is an exact match for a value in the same column in another row
* **Text length facet** - creates a numeric facet based on the length (number of characters) of the text in each row for the selected column. This can be useful for spotting incorrect or unusual data in a field where specific lengths are expected (e.g. if the values are expected to be years, any row with a text length more than 4 for that column is likely to be incorrect)
* **Facet by blank** - a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if they have no data present in that column. This is useful when looking for rows missing key data.

Facets are intended to group together common values and OpenRefine limits the number of values allowed in a single facet to ensure the software does not perform slowly or run out of memory. If you create a facet where there are many unique values (for example, a facet on a 'book title' column in a data set that has one row per book) the facet created will be very large and may either slow down the application, or OpenRefine will not create the facet. 

## Exercise 4: Find all publications without a DOI
* Use the 'Facet by blank' function to find all publications in this data set without a DOI


## Filters
As well as using Facets to filter the data displayed in OpenRefine you can also apply 'Text Filters' which look for a particular piece of text appearing in a column. Text filters are applied by clicking the drop down menu at the top of the column you want to apply the filter to and choosing 'Text filter'.

As with Facets, the Filter options appear in the left hand panel in OpenRefine. Simply type in the text you want to use in the Filter to display only rows which contain that text in the relevant column.

You can also use regular expressions in the filter.

e.g. thera[a-z]* will create a filter that searches for variations on therapy, therapeutic, etc.

## Working with filtered data
It is very important to note that when you have filtered the data displayed in OpenRefine, any operations you carry out will apply only to the rows that match the filter - that is the data currently being displayed.


## Rows and Records
OpenRefine has two modes of viewing data 'Rows' and 'Records'. So far we've been using the Rows mode, where each row represents a single record in the data set - in this case, an article. In Records mode, OpenRefine can link together multiple rows as belonging to the same Record.

How this works can be seen in the next exercise...

## Exercise 5: Split author names into separate cells
If you look at the Author column you should be able to see that there are multiple names in each cell separated by the pipe symbol "|". To work with the author names effectively we need to split them into separate cells:

* Click the dropdown menu at the top of the Author column
* Choose 'Edit cells->Split multi-valued cells'
* In the prompt type the | symbol and click 'OK'
    * Note that the rows are still numbered sequentially
* Click the 'Records' option to change to Records mode
    * Note how the numbering has changed - indicating that several rows are related to the same record

## Clustering
The Cluster function groups together values in a column that are 'similar' and enables you to merge together several different, but similar, values into a single value.

This is very effective where you have data where there can be minor variations in data values that are likely such as names of people, organisations and places.

To use the the 'Cluster' function, click on the 'Edit Cells' menu option in the relevant column and choose 'Cluster and edit...'

The 'Clusters' are created automatically according to an algorithm.They look at things like character similarity, word order, nearest neighbours, phonetic similarities and more. Each algorithm weights these different elements of the text differently. There are a number of different algorithms supported by OpenRefine - some experimentation maybe required to see which clustering algorithm works best with any particular set of data, and you may find that using different algorithms highlights different clusters.

For more information on the methods used to create Clusters see [https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth)

For each cluster you have the option of 'merging' the values together - that is replace with a single consistent value. By default OpenRefine uses the most common value in the cluster as the new value, but you can select one of the other values by clicking the value itself, or you can simply type the desired value into the 'New Cell Value' box.


## Exercise 6: Use Clustering to clean up author data
* Choose 'Edit cells->Cluster and edit' from the author column (which should be split into individual values from the last exercise)
* Using the 'key collision' method with the 'fingerprint' Keying Function work through the clusters of values, merging them to a single value where appropriate
* Try changing the clustering method being used - which ones work well?

---

###Key Points

* You can reorder, rename and remove columns in OpenRefine
* You can use facets and filters to explore your data
* You can use facets and filters work with a subset of data in OpenRefine
* You can easily correct common data issues using Facets and Clustering

---
## Transforming data

## Introducing Transformations

Through facets, filters and clusters OpenRefine offers relatively straightforward ways of getting an overview of your data, and making changes where you want to standardise terms used to a common set of values.

However, sometimes there will be changes you want to make to the data that cannot be achieved in this way. Such types of changes include:

* Splitting data that is in a single column into multiple columns (e.g. splitting an address into multiple parts)
* Standardising the format of data in a column without changing the values (e.g. removing punctuation or standardising a date format)
* Extracting a particular type of data from a longer text string (e.g. finding ISBNs in a bibliographic citation)

To support this type of activity OpenRefine supports 'Transformations' which are ways of manipulating data in columns. Transformations are normally written in a special language called 'GREL' (Google Refine Expression Language). To some extent GREL expressions are similar to Excel Formula, although they tend to focus on text manipulations rather than numeric functions.

Full documentation for the GREL is available at https://github.com/OpenRefine/OpenRefine/wiki/Google-refine-expression-language. For a more digestible introduction see this [cheat sheet](http://arcadiafalcone.net/GoogleRefineCheatSheets.pdf). This tutorial covers only a small subset of the commands available.

## Common transformations
Some transformations are used regularly and are accessible directly through menu options, without having to type them directly.

Examples of some of these common transformations are given in the table below, with their 'GREL' equivalents. We'll see how to use the GREL version later in this lesson.

Common Transformation  | Action | GREL expression
--------------------| ------------- | -------------
To Uppercase| Converts the current value to uppercase | ```value.toUppercase()```
To Lowercase| Converts the current value to lowercase | ```value.toLowercase()```
To Titlecase| Converts the current value to titlecase (i.e. each word starts with an uppercase character and all other characters are converted to lowercase) | ```value.toTitlecase()```
Trim leading and trailing whitespace | Removes any 'whitespace' characters (e.g. spaces, tabs) from the start or end of the current value | ```value.trim()```

## Exercise 7: Correct Publisher data
* Create a text facet on the Publisher column
* Note that in the values there are two that look identical - why does this value appear twice?
* On the publisher column use the dropdown menu to select 'Edit cells->Common transforms->Trim leading and trailing whitespace'
* Look at the publisher facet now - has it changed? (if it hasn't changed try clicking the Refresh option to make sure it updates)

---

## Writing transformations
To start writing transformations, select the column on which you wish to perform a transformation and choose 'Edit cells->Transform…'. In the screen that displays you have a place to write a transformation (the 'Expression' box) and then the ability to Preview the effect the transformation would have on 10 rows of your data.

The transformation you type into the 'Expression' box has to be a valid GREL expression. The simplest expression is simply the word 'value' by itself - which simply means the value that is currently in the column - that is: make no change.

GREL functions are written by giving a value of some kind (a text string, a date, a number etc.) to a GREL function. Some GREL functions take additional parameters or options which control how the function works. GREL supports two syntaxes:

* value.function(options)
* function(value, options)

Either is valid, and which is used is completely down to personal preference. In these notes the first syntax is used.

Next to the 'Preview' option are options to view:

* **History** - a list of transformations you've previously used with the option to reuse them immediately or to 'star' them for easy access
* **Starred** - a list of transformations you've 'starred' via the 'History' view
* **Help** - a list of all the GREL functions and brief information on how to use them

## Exercise 8: Put titles into Title Case
* Facet by publisher
* Select "Akshantala Enterprises" and "Society of Pharmaceutical Technocrats"
* Change the titles from those to publishers from uppercase to title case using the GREL syntax.

## Undo and Redo
OpenRefine lets you undo, and redo, any number of steps you have taken in cleaning the data. This means you can always try out transformations and 'undo' if you need to. The way OpenRefine records the steps you have taken even allows you to take the steps you've carried out on one data set, and apply it to another data set by a simple copy and paste operation.

The 'Undo' and 'Redo' options are accessed via the lefthand panel.

The Undo/Redo panel lists all the steps you've taken so far. To undo steps, simply click on the last step you want to preserve in the list and this will automatically undo all the changes made since that step.

The remaining steps will continue to show in the list but greyed out, and you can reapply them by simply clicking on the last step you want to apply.

However, if you 'undo' a set of steps and then start doing new transformations, the greyed out steps will disappear and you will no longer have the option to 'redo' these steps.

If you wish to save a set of steps to be re-applied later, or to a different project, you can click the 'Extract' button. This gives you the option to select the steps you want to save, and to copy the transformations included in the selected steps in a format called 'JSON'

To apply a set of steps you have copied or saved in this 'JSON' format use the 'Apply' button and paste in the JSON. In this way you can share transformations between projects and each other.

Undo/Redo data is stored with the Project and is saved automatically as you work, so next time you open the project, you can access your full history of steps you have carried out and undo/redo in exactly the same way.

## Exporting data
Once you have finished working with a data set in OpenRefine you may wish to export it. The export options are accessed through the 'Export' button at the top right of the OpenRefine interface
Export formats support include HTML, Excel and comma- and tab-separated value (csv and tsv). You can also write a custom export, selecting to export specific fields, adding a header or footer and specifying the exact format.

## Data types
Understanding data types and regular expressions will help you write more complex transformations using GREL.

### Data types in OpenRefine
Every piece of data in OpenRefine has a 'type'. The most common 'type' is a 'string' - that is a piece of text. However there are other data types available and transformations let you convert data from one type to another where appropriate. The data types supported are:

* String
* Number
* Date
* Boolean
* Array

### Dates and Numbers
So far we've been looking only at 'String' type data. Much of the time it is possible to treat numbers and dates as strings. For example in the Date column we have the date of publication represented as a String. However, some operations and transformations only work on 'number' or 'date' type operations. The simplest example is sorting values in numeric or date order. To carry out these functions we need to convert the values to a date or number first.

## Exercise 9: Reformat the Date
* Make sure you remove all Facets and Filters
* On the Date column use the dropdown menu to select 'Edit cells->Common transforms->To date'
* Note how the values are now displayed in green and follow a standard convention for their display format (ISO8601) - this indicates they are now stored as date data types in OpenRefine. We can now carry out functions that are specific to Dates
* On the Date column dropdown select 'Edit column->Add column based on this column'. Using this function you can create a new column, while preserving the old column
* In the 'New column name' type "Formatted Date"
* In the 'Expression' box type the GREL expression ```value.toString("dd MMMM yyyy")```

### Booleans and Arrays
#### Booleans
Booleans and Arrays are data types that are more often used while manipulating data in a GREL expression than for actually storing in a cell (in fact, Arrays cannot be stored in a cell in OpenRefine).

A 'Boolean' is a binary value that can either be 'true' or 'false'. Boolean values can be used directly in OpenRefine cell, but is more often used in transformations as part of a GREL expression. For example the GREL expression 
```
value.contains("test")
```
generates a boolean value of either 'true' or 'false' depending on whether the current value in the cell contains the text 'test' anywhere. 

Such tests can be combined with other GREL expressions to create more complex transformations. For example, to carry out a further transformation only if a test is successful. The GREL transformation ```if(value.contains("test"),"Test data",value)``` replaces a cell value with the words "Test data" only *if* the value in the cell contains the string "test" anywhere.

#### Arrays
An 'Array' is a list of values, represented in Refine by the use of square brackets containing a list of values surrounded by inverted commas and separated by commas. For example an array listing the days of the week would look like:

["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]

Arrays can be sorted, de-duplicated, and manipulated in other ways in GREL expressions, but cannot appear directly in an OpenRefine cell. Arrays in OpenRefine are usually the result of a transformation. For example the 'split' function takes a string, and changes it into an array based on a 'separator'. For example if a cell has the value:

"Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday"

This can be transformed into an array using the 'split' function
```
value.split(",")
```
This would create the array containing the days of the week:

["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"]

This can be combined with array operations like 'sort'. For example, assuming the cell contains the same value as above, then the function
```
value.split(",").sort()
```
would result in an array containing the days of the week sorted in alphabetical order:

["Friday","Monday","Saturday","Sunday","Thursday","Tuesday","Wednesday"]

To output a value from an array you can either select a specific value depending on its position in the list (with the first position treated as 'zero'). Most programming languages are like European elevators. They start at zero as opposed to one. There is a zeroth position and the second value is one.

For example
```
value.split(",")[0]
```
would extract the first value from the array created by the 'split' function. In the above example this would be "Monday". 

You can also join arrays together to make a 'String'. The GREL expression would look like
```
value.split(",").sort().join(",")
```
. Taking the above example again, this would result in a string with the days of the week in alphabetical order, listed with commas between each day.

---

## Exercise 10: Reverse author names
In this exercise we are going to use both the Boolean and Array data types.
If you look at the author column, you can see that most of the author names are written in the natural order. However, a few have been reversed to put the family name first.

We can do a crude test for reversed author names by looking for those that contain a comma:

* Make sure you have already split the author names into individual cells using 'Edit cells->Split multi-valued cells' (you should have done this in exercise 5)
* On the author column, use the dropdown menu and select 'Facet->Custom text facet...'
    * The Custom text facet function allows you to write GREL functions to create a facet
* In the Expression box type ```value.contains(",")```
* Click 'OK'
* Since the 'contains' function outputs a Boolean value, you should see a facet that contains 'false' and 'true'. These represent the outcome of the expression, i.e. true = values containing a comma; false = values not containing a comma
* In this facet select 'true' to narrow down to the author names that contain a comma

Now we have narrowed down to the lines with a comma in a name, we can use the 'match' function. The match function allows you to use regular expressions, and output the capture groups as an array, which you can then manipulate.

* On the author column use the dropdown menu and select 'Edit cells->Transform'
* In the Expression box type ```value.match(/(.*),(.*)/)```  The "/",  means you are using a regular expression inside a GREL expression. The parentheses indicate you are going to match a group of characters. The ".*" expression will match any character from 0, 1 or more times. So here we are matching any number of characters, a comma, and another set of any number of characters.
* See how this creates an array with two members in each row in the Preview column

To get the author name in the natural order you can reverse the array and join it back together with a space to create the string you need:

* In the Expression box, add to the existing expression until it reads ```value.match(/(.*),(.*)/).reverse().join(" ")```
* In the Preview view you should be able see this has reversed the array, and joined it back into a string
* Click 'OK'

---
###Key Points
* You can alter data in OpenRefine based on specific instructions
* You can expand the data editing functions that are built-in into OpenRefine by building your own

---

## Looking up data from a URL
OpenRefine can retrieve data from URLs. This can be used in various ways, including looking up additional information from a remote service, based on information in your OpenRefine data.

As an example, you can look up names against the Virtual International Authority File (VIAF), and retrieve additional information such as dates of birth/death and identifiers.

Typically this is a two step process - firstly a step to retrieve data from a remote service, and secondly to extract the relevant information from the data you have retrieved.

To retrieve data from an external source, from the drop down menu at a column heading use the option 'Edit column->Add column by fetching URLs'.

This will prompt you for a GREL expression to create a URL. Usually this would be a URL that uses existing values in your data to build a query. When the query runs OpenRefine will request each URL (for each line) and retrieve whatever data is returned (this may often be structured data, but could be simply HTML).

The data retrieved will be stored in a cell in the new column that has been added to the project. You can then use OpenRefine transformations to extract relevant information from the data that has been retrieved. Two specific OpenRefine functions used for this are:

* parseHtml()
* parseJson()

The 'parseHtml()' function can also be used to extract data from XML.

The next exercise demonstrates this two stage process in full.

---
## Exercise 11: Retrieving journal details from CrossRef via ISSN
Because retrieving data from external URLs takes time, this exercise targets a single line in the data. In reality you would want to run this over many rows (and probably go and do something else while it ran)

* Select a single row from the data set which contains an ISSN by:
    * Clicking the star icon for the relevant row in the first column
    * _Facet by Star_
    * Choose the single row
* In the ISSN column use the dropdown menu to choose 'Edit column->Add column by fetching URLs'
* Give the column a name e.g. "Journal details"
* In the expression box you need to write some GREL where the output of the expression is a URL which can be used to retrieve data (the format of the data could be HTML, XML, JSON, or some other text format)

In this case we are going to use the CrossRef api (read more about the CrossRef service at http://www.crossref.org, read more about the API we are going to use at https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md)

The syntax for requesting journal information from CrossRef is ```http://api.crossref.org/journals/{ISSN}``` where {ISSN} is replaced with the ISSN of the journal

* In the expression box type the GREL ```"http://api.crossref.org/journals/"+value```
* Click 'OK'

You should see a message at the top on the OpenRefine screen indicating it is fetching some data, and how far it has got. Wait for this to complete. Fetching data for a single row should take only ten seconds or so, but fetching data for all rows will take longer. You can speed this up by modifying the "Throttle Delay" setting in the 'Add column by fetching URLs' dialog which controls the delay between each URL request made by OpenRefine. This is defaulted to a rather large 5000 milliseconds (5 seconds).

At this point you should have a new cell containing a long text string in a format called 'JSON' (this stands for Javascript Object Notation, although very rarely spelt out in full).

OpenRefine has a function for extracting data from JSON (sometimes referred to as 'parsing' the JSON). The 'parseJson' function is explained in more detail at [https://github.com/OpenRefine/OpenRefine/wiki/GREL-Other-Functions](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Other-Functions).

* In the new column you've just added use the dropdown menu to access 'Edit column->Add column based on this column'
* Add a name for the new column e.g. "Journal Title"
* In the Expression box type the GREL ```value.parseJson().message.title```
* You should see in the Preview the Journal title displays

The reason for using 'Add column based on this column' is simply that this allows you to retain the full JSON and extract further data from it if you need to. If you only wanted the title and did not need any other information from the JSON you could use 'Edit cells->Transform...' with the same GREL expression.

## Reconciliation services
Reconciliation services allow you to lookup terms from your data in OpenRefine against external services, and use values from the external services in your data.

Reconciliation services can be more sophisticated and often quicker than using the method described above to retrieve data from a URL. However, to use the ‘Reconciliation’ function in OpenRefine requires the external resource to support the necessary service for OpenRefine to work with, which means unless the service you wish to use supports such a service you cannot use the ‘Reconciliation’ approach.

There are a few services where you can find an OpenRefine Reconciliation option available. For example WikiData has a (fledgling) reconciliation service at [https://tools.wmflabs.org/wikidata-reconcile/](https://tools.wmflabs.org/wikidata-reconcile/).

In other cases people have built reconciliation applications for a specific service which you can download and run yourself. These vary in how they work, and what it takes to run them locally. For example there are multiple reconciliation applications for VIAF. Even for the same service (e.g. VIAF) different reconciliation applications (written by different people)  can work in different ways and potentially give different results - so caveat emptor!

One of the most common ways of using the reconciliation option in OpenRefine is with an extension (see below for more on extensions to OpenRefine) can use linked data sources for reconciliation. The extension is called "RDF Refine" and can be downloaded from [http://refine.deri.ie](http://refine.deri.ie).

There also exist extensions to do reconciliation against local data such as csv files (see [http://okfnlabs.org/reconcile-csv/](http://okfnlabs.org/reconcile-csv/)) and maintained lists of values (see [http://okfnlabs.org/projects/nomenklatura/index.html](http://okfnlabs.org/projects/nomenklatura/index.html)).

For more information on using Reconciliation services see [https://github.com/OpenRefine/OpenRefine/wiki/Reconciliation-Service-API](https://github.com/OpenRefine/OpenRefine/wiki/Reconciliation-Service-API)

---
## Exercise 12: Reconcile Publisher names with VIAF IDs
In this exercise you are going to use the VIAF Reconciliation service written by [Jeff Chiu](https://twitter.com/absolutelyjeff). Jeff offers two ways of using the reconciliation service - either via a public service he runs at [http://refine.codefork.com/](http://refine.codefork.com/), or by installing and running the service locally using the instructions at [https://github.com/codeforkjeff/refine_viaf](https://github.com/codeforkjeff/refine_viaf).

If you are going to do a lot of reconciliation, please install and run your own local reconciliation service - the instructions at [https://github.com/codeforkjeff/refine_viaf](https://github.com/codeforkjeff/refine_viaf) make this reasonably straightforward.

Once you have chosen which service you are going to use:

* In the Publisher column use the dropdown menu to choose 'Reconcile->Start Reconciling'
* If this is the first time you've used this particular reconciliation service, you'll need to add the details of the service now
* Click 'Add Standard Service...' and in the dialogue that appears enter:
	*  "http://refine.codefork.com/reconcile/viaf" for Jeff's public service
	* "http://localhost:8080/reconcile/viaf" if you are running the service locally
* You should now see a heading in the list on the left hand side of the Reconciliation dialogue called "VIAF Reconciliation Service"
*  Click on this to choose to use this reconciliation service
*  In the middle box in the reconciliation dialogue you may get asked what type of 'entity' you want to reconcile to - that is, what type of thing are you looking for. The list will vary depending on what reconciliation service you are using.
* In this case choose "Corporate Name" (it seems like the VIAF Reconciliation Service is slightly intelligent about this and will only offer options that are relevant)
*  In the box on the righthand side of the reconciliation dialogue you can choose if other columns are used to help the reconciliation service make a match - however it is sometimes hard to tell what use (if any) the reconciliation service makes of these additional columns
*  At the bottom of the reconciliation dialogue there is the option to "Auto-match candidates with high confidence". This can be a time saver, but in this case you are going to uncheck it, so you can see the results before a match is made
*  Now click 'Start Reconciling'

Reconciliation is an operation that can take a little time if you have many values to look up. However, in this case there are only 6 publishers to check, so it should work quite quickly.

Once the reconciliation has completed two Facets should be created automatically:

* Publisher: Judgement
* Publisher: best candidate's score

These are two of several specific reconciliation facets and actions that you can get from the 'Reconcile' menu (from the column drop down menu).

* Close the 'Publisher: best candidate's score' facet, but leave the 'Publisher: Judgement' facet open

If you look at the Publisher column, you should see some cells have found one or more matches - the potential matches are show in a list in each cell. Next to each potential match there is a 'tick' and a 'double tick'. To accept a reconciliation match you can use the 'tick' options in cells. The 'tick' accepts the match for the single cell, the 'double tick' accepts the match for all identical cells.

* Create a text facet on the Publisher column
* Choose 'International Union of Crystallography'

In the Publisher column you should be able to see the various potential matches. Clicking on a match will take you to the VIAF page for that entity.

* Click a 'double tick' in one of the Publisher column cells for the option "International Union of Crystallography"
* This will accept this as a match for all cells - you should see the other options all disappear
* Check the 'Publisher: Judgement' facet. This should now show that 858 items are 'matched' (if this does not update, try refreshing the facets)

We could do these one by one, but if we are confident with matches, there is an option to accept all:

* Remove all filters/facets from the project so all rows display
* In the Publisher column use the dropdown menu to choose 'Reconcile->Actions->Match each cell to its best candidate'

There are two things that reconciliation can do for you. Firstly it gets a standard form of the name or label for the entity. Secondly it gets an ID for the entity - in this case a VIAF id. This is hidden in the default view, but can be extracted:

* In the Publisher column use the dropdown menu to choose 'Edit column->Add column based on this column...'
* Give the column the name 'VIAF ID'
* In the GREL expression box type ```cell.recon.match.id```
* This will create a new column that contains the VIAF ID for the matched entity

## Extensions
The functionality in OpenRefine can be enhanced by ‘extensions’ which can be downloaded and installed to add functionality to your OpenRefine installation.

A list of Extensions (not necessarily complete) is given at [https://github.com/OpenRefine/OpenRefine/wiki/Extensions](https://github.com/OpenRefine/OpenRefine/wiki/Extensions)

One of these extensions tries to work around the limitation of Reconciliation services described above, by making it possible to use a reconciliation service against ‘linked data’ sources which have SPARQL endpoints. For more information on this see the ‘RDF Extension’ at [http://refine.deri.ie](http://refine.deri.ie). An example of how this works is given in more detail at [http://refine.deri.ie/showcases](http://refine.deri.ie/showcases).

## Using the ‘cross’ function to lookup data in other OpenRefine projects
As well as looking up data in external systems using the methods described above, it is also possible to look up data in other OpenRefine projects on the same computer. This is done using the ‘cross’ function which utilizes a GREL expression.

The ‘cross’ function takes a value from the OpenRefine project you are working on, and looks for that value in a column in another OpenRefine project. If it finds one or more matching rows in the second OpenRefine project, it returns an array containing the rows that it has matched.

As it returns the whole row for each match, you can use a transformation to extract the values from any of the columns in the 

You can use to compare the contents of two OpenRefine projects, or to use data between the two projects.

The [VIB-Bits extension](https://www.bits.vib.be/index.php/software-overview/openrefine) adds a number of very useful functions to OpenRefine including a way of using the 'cross' function with simply point-and-click functionality which makes looking up data from other projects significantly simpler.

###Key Points

* OpenRefine can look up custom URLs to fetch data based on what's in an OpenRefine project
* API calls can be custom built, or one can use existing Reconcilliation services to enrich data
* OpenRefine can be further enhanced by installing extensions

---
##Thanks!
*This lesson was developed by [Thomas Guignard](http://labs.timtom.ch/library-openrefine/) and was adapted for this session.
