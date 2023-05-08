Download Link: https://assignmentchef.com/product/solved-si507-project-01
<br>
<h1>Objectives</h1>

<ul>

 <li>Design a program using object-oriented programming, including class inheritance</li>

 <li>Develop unit tests to verify a program works as specified</li>

 <li>Gain experience working with JSON data from a web API</li>

</ul>

<h1>Overview</h1>

In this project, you will build a simple, command line tool for searching the iTunes store. You will build this application in a series of steps.

<h1>Knowledge Required</h1>

There are a number of topics you’ll have to master to complete this assignment. Most of them are things you’ve seen before but may need to recall. Some of them are new this semester. And a couple are brand new, but easy to master with a pointer or two.




The following are topics we’ve covered in 507 this semester:

<ul>

 <li>Classes and inheritance</li>

 <li>“Special” class methods like __str__( ), __repr__( ), and __len__( )</li>

 <li>Unit testing &amp; test cases</li>

</ul>




The following are covered in the <a href="https://www.programsinformationpeople.org/runestone/static/publicPIP/index.html">textbook</a>, and you have seen them to at least some extent in either 506 or 507.

<ul>

 <li>String manipulation (e.g., extracting substrings)</li>

 <li>Named parameters with default values</li>

 <li>json parsing using the json module</li>

 <li>Accessing Web APIs using requests</li>

 <li>Writing interactive command line programs (prompting for input, allowing user to quit)</li>

</ul>




The following haven’t been covered in either 506 or 507, but we’ll go over them briefly in class:

<ul>

 <li>The webbrowser module (new, but super easy: you just call webbrowser.open(URL))</li>

 <li>Importing self-written modules and the meaning of __name__ == “__main__”</li>

 <li>Understanding the iTunes API (using documentation and “reverse engineering” of json output)</li>

</ul>

<h1>Before you get started</h1>

We have given you three files to start with: <a href="https://www.dropbox.com/s/o219f3a914ecoaq/proj1_f19.py?dl=0">proj1_f19.py</a>, <a href="https://www.dropbox.com/s/pj847gt0ldkiqcu/proj1_f19_test.py?dl=0">proj1_f19_test.py</a>, and <a href="https://www.dropbox.com/s/88cugo8nav6wmir/sample_json.txt?dl=0">sample_json.txt</a> or <a href="https://www.dropbox.com/s/rhl5rh0io5pzh3k/sample_json.json?dl=0">sample_json.json</a>. Here’s how you will use them:

<ul>

 <li>py is where you will define your classes and write any functions you need to run your program. You will also write your interactive code for Part 4 in this file, in the designated code block. There should be no test cases in this file, and there should be no output in the version of this file that you turn in that isn’t related to Part 4.</li>

 <li>py is where you will define your test cases for Parts 1-3. This is the file that you will <em>run</em> while working on Parts 1-3. Note that this file <em>imports</em> proj1_f19.py and can therefore instantiate classes and invoke functions from that file. When grading your project, the graders will run proj1_f19_test.py to grade Parts 1-3, and will run proj1_f19.py to grade Part 4.</li>

 <li>txt provides sample output from the iTunes web API that you will need for Part 3.</li>

</ul>

<h2>Part 1: Implement and test a class system (50 points)</h2>

In this step, you will implement a set of classes to model a part of the iTunes data model and you will write unit tests to show that the class implementation is correct.




Create a base class (“Media”) and two subclasses (“Song” and “Movie”) that represent items in the iTunes store (there are other media types that you do not have to worry about).




Here are some details about each class you’ll need to implement:




Media:

<ul>

 <li>Instance variables: title, author, release year</li>

 <li>Methods: implement the following:</li>

 <li>__init__: takes title, author, and release year as arguments. Use named arguments with defaults.</li>

 <li>__str__: returns “&lt;title&gt; by &lt;author&gt; (&lt;release year&gt;)”, filling in the appropriate instance variables. For example “Bridget Jones’s Diary (Unabridged) by Helen Fielding (2012)”</li>

 <li>__len__: returns 0</li>

</ul>

Song (subclass of Media):

<ul>

 <li>Additional instance variables: album, track length</li>

 <li>Methods:</li>

 <li>__init__: takes title, author, release year, album, genre, and track length as arguments. Use named arguments with defaults. Call super( ) to initialize variables that belong to Media</li>

 <li>__str__: add “[&lt;genre&gt;]” to the end of the output from Media.__str__( ). For example “Hey Jude by The Beatles (1968) [Rock]”</li>

 <li>__len__: return track length in seconds</li>

</ul>

Movie (subclass of Media):

<ul>

 <li>Additional instance variables: rating, movie length</li>

 <li>Methods:</li>

 <li>__init__: takes title, author, release year, rating, and movie length as arguments. Use named arguments with defaults. Call super( ) to initialize variables that belong to Media.</li>

 <li>__str__: add “[&lt;rating&gt;]” to the end of the output from Media.__str__( ). For example “Jaws by Steven Speilberg (1975) [PG]”</li>

 <li>__len__: return movie length in minutes (rounded to nearest minute)</li>

</ul>

<h3>Test cases</h3>

Create test cases that show:

<ul>

 <li>All class constructors work as specified, and correctly populate instance variables</li>

 <li>__str__ and __len__ work properly for all three classes</li>

 <li>Classes do NOT have instance variables that are not relevant to them (e.g., Songs and Media do not have a ‘rating’ instance variable)</li>

</ul>




You must implement at least 3 test functions, and include at least 15 assertions (total, across all test functions). It’s fine to include more of either.

<h3>Assessment</h3>

You will be assessed on

<ul>

 <li>Whether your tests cover the criteria listed above</li>

 <li>Whether your tests pass</li>

 <li>Whether you have used super( ) correctly to avoid repeating code</li>

</ul>

<h3>Notes</h3>

For this part, you will be creating objects “by hand,” i.e., by passing explicit information into the constructors. You will not be creating objects using JSON. That will be covered in the next part.

<h2>Part 2: Create objects from JSON (50 points)</h2>

Now add the ability to create objects using JSON. We have provided sample JSON for three media types that iTunes supports. You will show that you can correctly parse each of these JSON objects into properly constructed objects of the correct type.




To avoid repeating code, you should make sure that the Media class does as much of the parsing as possible, and that each subclass only parses information that is specific to that class.




Suggested approach: Add a named parameter ‘json’ to each constructor. This should have a default value of None, so as not to break your Part 1 tests. Depending on the value of json, either create the object from the json or from the explicit parameters used in Part 1.

<h3>Test Cases</h3>

Create test cases that show:

<ul>

 <li>Objects of each class (Media, Song, Movie) are created correctly from the relevant JSON string. “Created correctly” means that instance variables are set to correct values and class methods (eg., __str__, __len__) behave correctly.</li>

</ul>




You must implement at least one test function (three would be reasonable too), with at least 15 assertions to test that all relevant instance variables are created as specified.

<h3>Assessment</h3>

You will be assessed on

<ul>

 <li>Whether your tests cover the criteria listed above</li>

 <li>Whether your tests pass</li>

 <li>Whether you have used super( ) correctly to avoid repeating code</li>

</ul>

<h2>Part 3: Create objects from iTunes API (50 points)</h2>

Add the ability to fetch data from the <a href="https://affiliate.itunes.apple.com/resources/documentation/itunes-store-web-service-search-api/">iTunes API</a>, and create lists of objects from the data retrieved. Since the data may change between calls, you will only need to show that the data returned from a set of pre-defined queries (of your choice) is processed by your program without errors, and that the number of objects created is within an expected range (either 0 or “more than zero but less than or equal to the number of results requested”).

<h3>Test Cases</h3>

Create test cases that show that your program responds within expected ranges to a several diverse queries, including common words (“baby,” “love”), less common words that are likely to produce specific matches (“moana,” “helter skelter”), nonsense queries (“&amp;@#!$”), and a blank query.

<h3>Assessment</h3>

You will be assessed on

<ul>

 <li>whether your tests cover the criteria listed above</li>

 <li>whether your tests pass</li>

 <li>whether you construct the correct type of object given the contents of a JSON object</li>

</ul>

<h3>Notes</h3>

The iTunes API limits you to “about 20 calls per minute.” If you don’t make more than 20 API calls in any of your test cases (and you don’t need to make nearly that many), you should be fine. If this turns out to be a problem, you might consider caching results to use offline while debugging. If you took 506 previously you may have access to caching code that you can try to adapt and use here. Caching is not required for this assignment and not even particularly recommended unless you are very comfortable with it. We will work on caching later in the semester.

<h2>Part 4: Create an interactive search interface (50 points)</h2>

For this last part, you will add the ability for users to enter their own queries and receive nicely formatted results. The output should be formatted as follows:

<ul>

 <li>The results should be grouped into Songs, Movies, and Other Media. In each category, the results should be printed using their __str__ representation, one per line.</li>

 <li>Each result should be preceded by a number, starting at 1 and going up, printed at the beginning of the line.</li>

</ul>




When the program first runs, the user should be presented with two options: enter a search term, or enter exit to quit. After a query has been run, a third option becomes available: launch preview. To launch a preview, the user enters the number of the result they want to preview. Your program will then use the webbrowser module to open the trackViewURL embedded in the JSON item description, while also printing the URL to the screen.

<h3>Test Cases</h3>

You do not need to implement test cases for Part 4. We will test this part of your code manually.




Assessment

You will be assessed on:

<ul>

 <li>Whether your program returns expected results (we will compare output with a reference implementation we have built and see if the results are the same)</li>

 <li>Whether the results are grouped and formatted appropriately</li>

 <li>Whether the preview functionality works</li>

 <li>Partial credit is possible if you are only able to get parts of this working</li>

</ul>




<h3>Part 4 Sample Output</h3>

$ python3 proj1_f19.py




Enter a search term, or “exit” to quit: Beatles




SONGS

1 Hey Jude by The Beatles (1968) [Rock]

2 Yesterday by The Beatles (1965) [Rock]

…




MOVIES

24 Help! by Richard Lester (1965) [G]

25 Yellow Submarine by George Dunning (1967) [G]

…




OTHER MEDIA

47 The Beatles by Hunter Davies (2009)

48 Dreaming the Beatles by Rob Sheffield (2017)

…




Enter a number for more info, or another search term, or exit: 1




Launching <a href="https://itunes.apple.com/us/album/hey-jude/400835735?i=400835962&amp;uo=4">https://itunes.apple.com/us/album/hey-jude/400835735?i=400835962&amp;uo=4</a> in web browser…




Enter a number for more info, or another search term, or exit: exit




Bye!




A few notes:

<ul>

 <li>What’s shown above is hypothetical output–not generated by actual code. Your results will almost certainly be different–this is just intended as an example of the format and interaction.</li>

 <li>The “…”s that show up above would NOT be part of your program output. We just didn’t want to fill up a lot of space with lots of search results.</li>

 <li>There should be no repeated numbers–start with 1 and increment the number for each result.</li>

 <li>Your results should be grouped into SONGS, MOVIES, and OTHER MEDIA, and these categories should always appear in the same order</li>

 <li>Where it says “Launching XXX in web browser…” above you should actually launch the specified URL in a web browser.</li>

 <li>You will need to test if the user’s input is a number (in which case you’d launch the browser) or a string (in which case you’d do a new search). The input ‘3’ would launch the browser, since it can be converted to a number. The input ‘2 Live Crew’, however, should be treated as a string. int( ) and str( ) are your friends here.</li>

 <li>You will have to think about what to do when there are no results in a category, or no results at all! Your program should give output that will inform the user of what has happened in such cases.</li>

</ul>





