<h1 itemprop="name" class="article-title">A C#.NET toolkit for writing SSIS Script Tasks </h1>

<a href = "http://www.sqlservercentral.com/articles/Integration+Services+%28SSIS%29/76439/">Original</a>
                    

<p>
  <strong>
    
	    By <a href="/Authors/Articles/Stan_Kulp/439977/">Stan Kulp</a>, 
    <span itemprop="datePublished" content="2011-12-12">2011/12/12</span>
  </strong>
</p>
                                    
                    <div itemprop="articleBody" class="content-text"><p>
  It is not necessary to know the C#.NET universe in order to write valuable C#.NET script tasks. Keep in mind that it is being used as a scripting language, not a full-fledged application development language. The ability to perform the following basic operations will allow you to do quite a lot.
</p>
<ul>
  <li>
    Create a C#.NET script task</li>
  <li>
    Create dialog boxes for data output</li>
  <li>
    Access SSIS variables</li>
  <li>
    Parse strings with the split function</li>
  <li>
    Create and loop through list arrays</li>
  <li>
    Read/write ASCII files</li>
  <li>
    Copy, move and delete files</li>
  <li>
    Capture a listing of specified files in a subdirectory</li>
  <li>
    Email a file</li>
  <li>
    Create a database connection to enable C#.NET to talk to SQL Server</li>
  <li>
    Execute T-SQL queries and stored procedures and capture any results</li>
</ul>
<p>
  The purpose of this article is to provide easily-understood example C#.NET code of the above tasks for SSIS package developers who know a programming language, but are unfamiliar with C#.NET.
</p>
<p>
  <strong>Lesson 1: Create an SSIS package with a C#.NET script task</strong>
</p>
<p>
  Open Business Intelligence Development Studio, click the "Create:" link, select "Integration Services Project," type the name of the project in the "Name:" text box and click the "OK" button.
</p>
<p>
</p>
<p>
  <div style="width: 818px;" class="wideImageContainer"><img style="display: block; max-width: 818px; cursor: zoom-in;" alt="" src="/Images/11450.gif" border="0"><div><img style="margin: 0px 3px;" src="/Resources/Images/zoom.gif" align="bottom"><a href="javascript:;">Zoom in</a><span>&nbsp;&nbsp;|&nbsp;&nbsp;</span><a href="javascript:;">Open in new window</a></div></div>
</p>
<p>
</p>
<p>
  A default SSIS package named "Package" will have been created. Double-click on the "Script Task" control flow item to add a script task to the package.
</p>
<p>
</p>
<p>
  <div style="width: 818px;" class="wideImageContainer"><img style="display: block; max-width: 818px; cursor: zoom-in;" alt="" src="/Images/11451.gif" border="0"><div><img style="margin: 0px 3px;" src="/Resources/Images/zoom.gif" align="bottom"><a href="javascript:;">Zoom in</a><span>&nbsp;&nbsp;|&nbsp;&nbsp;</span><a href="javascript:;">Open in new window</a></div></div>
</p>
<p>
</p>
<p>
  Double-click on the Script Task and select "Microsoft Visual Basic 2008" from the Script Language drop-down list, then click on the "Edit Script" button.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11596.gif" border="0">
</p>
<p>
</p>
<p>
  At this point you have created a script task template ready to accept your C#.NET code.
</p>
<p>
</p>
<p>
  <div style="width: 818px;" class="wideImageContainer"><img style="display: block; max-width: 818px; cursor: zoom-in;" alt="" src="/Images/11598.gif" border="0"><div><img style="margin: 0px 3px;" src="/Resources/Images/zoom.gif" align="bottom"><a href="javascript:;">Zoom in</a><span>&nbsp;&nbsp;|&nbsp;&nbsp;</span><a href="javascript:;">Open in new window</a></div></div>
</p>
<p>
</p>
<p>
  <strong>Lesson 2: Create an output dialog box</strong>
</p>
<p>
  Replace the "// TODO: Add your code here" text in the Main procedure with the follwing three statements.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="kwd">string</span><span class="pln"> message </span><span class="pun">=</span><span class="pln"> </span><span class="str">"This variable holds the dialog box message."</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> caption </span><span class="pun">=</span><span class="pln"> </span><span class="str">"This variable holds the dialog box title."</span><span class="pun">;</span><span class="pln">
</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">message</span><span class="pun">,</span><span class="pln"> caption</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  Save and execute the package to display the following dialog box.
</p>
<p>
  <img alt="" src="/Images/11454.gif" border="0">
</p>
<p>
  Among other uses, the output dialog box provides the ability to display the contents of variables while developing a package. Development Studio provides means for doing the same thing, but a popup is a quick and easy way of doing it in your code.
</p>
<p>
  <strong>Lesson 3: Access an SSIS global variable</strong>
</p>
<p>
  Add a global variable to the package by clicking the "Add Variable" button of the variables panel.
</p>
<p>
  <img alt="" src="/Images/11581.gif" border="0">
</p>
<p>
  Change the name of the variable to "TestVariable," its data type to "String," and it's value to "InitialValue."
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11582.gif" border="0">
</p>
<p>
</p>
<p>
  Double-click on the Script Task component to bring up the script task editor.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11584.gif" border="0">
</p>
<p>
</p>
<p>
  Click on the "ReadWriteVariables" button to bring up the "Select Variables" window.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11585.gif" border="0">
</p>
<p>
</p>
<p>
  Check the box in the "User:TestVariable" line and click the "OK" button.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11586.gif" border="0">
</p>
<p>
</p>
<p>
  The script task now has read/write access to the TestVariable. Click the "OK" button to end the variable configuration session.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="kwd">string</span><span class="pln"> temp1 </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> temp2 </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
temp1 </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pun">)</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Variables</span><span class="pun">[</span><span class="str">"TestVariable"</span><span class="pun">].</span><span class="typ">Value</span><span class="pun">;</span><span class="pln">
temp2 </span><span class="pun">=</span><span class="pln"> </span><span class="str">"New Value"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="str">"The current value of the SSIS global variable 'TestVariable' is '"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> temp1 </span><span class="pun">+</span><span class="pln"> </span><span class="str">".'\r\n \r\n The value will be changed to '"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> temp2 </span><span class="pun">+</span><span class="pln"> </span><span class="str">".'"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Variables</span><span class="pun">[</span><span class="str">"TestVariable"</span><span class="pun">].</span><span class="typ">Value</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> temp2</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="str">"The value of SSIS global variable 'TestVariable' has been changed to '"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pun">)</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Variables</span><span class="pun">[</span><span class="str">"TestVariable"</span><span class="pun">].</span><span class="typ">Value</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">".'"</span><span class="pun">);</span></pre>
<p>
  The current value of 'TestVariable' is read by this statement.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     temp1 </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pun">)</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Variables</span><span class="pun">[</span><span class="str">"TestVariable"</span><span class="pun">].</span><span class="typ">Value</span><span class="pun">;</span></em></pre>
<p>
  The first dialog box displays the current value of 'TestVariable' and the value to which it will be changed.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11599.gif" border="0">
</p>
<p>
</p>
<p>
  The new value of 'TestVariable' is set by this statement.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Variables</span><span class="pun">[</span><span class="str">"TestVariable"</span><span class="pun">].</span><span class="typ">Value</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> temp2</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">();</span></em></pre>
<p>
  The second dialog box confirms that the value of 'TestVariable' has been changed.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11600.gif" border="0">
</p>
<p>
</p>
<p>
  Being able to read and write global SSIS variables enables transfer of information between SSIS package components.
</p>
<p>
  <strong>Lesson 4: Parse a string with the Split() function</strong>
</p>
<p>
  In order to transfer data from an ASCII file to a table, each line of the file must be parsed into individual fields. A file that has the fields separated by commas (comma-separated values, or CSV) can be parsed with the C#.NET Split() function.
</p>
<p>
  Here is an example of a line being parsed into individual values with the Split() function.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span><span class="kwd">string</span><span class="pln"> line </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Blow,Joe,1234 Main Street,Anywhere,USA"</span><span class="pun">;</span><span class="pln">
     </span><span class="kwd">string</span><span class="pun">[]</span><span class="pln"> value </span><span class="pun">=</span><span class="pln"> line</span><span class="pun">.</span><span class="typ">Split</span><span class="pun">(</span><span class="str">','</span><span class="pun">);</span></em></pre>
<p>
  At this point, value[0] contains "Blow", value[1] contains "Joe", value[2] contains "1234 Main Street", value[3] contains "Anywhere", and value[4] contains "USA."
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="kwd">string</span><span class="pln"> line </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Blow,Joe,1234 Main Street,Anywhere,USA"</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pun">[]</span><span class="pln"> value </span><span class="pun">=</span><span class="pln"> line</span><span class="pun">.</span><span class="typ">Split</span><span class="pun">(</span><span class="str">','</span><span class="pun">);</span><span class="pln">

</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">[</span><span class="lit">0</span><span class="pun">],</span><span class="pln"> </span><span class="str">"First Value"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">[</span><span class="lit">1</span><span class="pun">],</span><span class="pln"> </span><span class="str">"Second Value"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">[</span><span class="lit">2</span><span class="pun">],</span><span class="pln"> </span><span class="str">"Third Value"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">[</span><span class="lit">3</span><span class="pun">],</span><span class="pln"> </span><span class="str">"Fourth Value"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">[</span><span class="lit">4</span><span class="pun">],</span><span class="pln"> </span><span class="str">"Fifth Value"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  The output dialog boxes confirm the content of the value[] array.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11605.gif" border="0"> <img alt="" src="/Images/11604.gif" border="0"> <img alt="" src="/Images/11603.gif" border="0"> <img alt="" src="/Images/11602.gif" border="0"> <img alt="" src="/Images/11601.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 5: Create and loop through an array list</strong>
</p>
<p>
  An array list is an object that can store a list of values in order and release them in the same order.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (Add <strong><em>using System.Collections;</em></strong> to the namespace listing.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="com">//using System.Collections; (Add to the namespace listing)</span><span class="pln">

</span><span class="typ">ArrayList</span><span class="pln"> </span><span class="typ">MyList</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">ArrayList</span><span class="pun">();</span><span class="pln">

</span><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Apple"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Orange"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Banana"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Peach"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Cherry"</span><span class="pun">);</span><span class="pln">

</span><span class="typ">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> value </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pln"> value_loopVariable </span><span class="kwd">in</span><span class="pln"> </span><span class="typ">MyList</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     value </span><span class="pun">=</span><span class="pln"> value_loopVariable</span><span class="pun">;</span><span class="pln">
     </span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(),</span><span class="pln"> </span><span class="str">"ArrayList Value "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> i</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(),</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
     i </span><span class="pun">+=</span><span class="pln"> </span><span class="lit">1</span><span class="pun">;</span><span class="pln">

</span><span class="pun">}</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  This code loads five values into an ArrayList named MyList.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span><span class="typ">Dim</span><span class="pln"> </span><span class="typ">MyList</span><span class="pln"> </span><span class="typ">As</span><span class="pln"> </span><span class="typ">New</span><span class="pln"> </span><span class="typ">ArrayList</span></em><span class="pln">

</span><em><span class="pln">     </span></em><em><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Apple"</span><span class="pun">)</span></em><span class="pln">
</span><em><span class="pln">     </span></em><em><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Orange"</span><span class="pun">)</span></em><span class="pln">
</span><em><span class="pln">     </span></em><em><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Banana"</span><span class="pun">)</span></em><span class="pln">
</span><em><span class="pln">     </span></em><em><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Peach"</span><span class="pun">)</span></em><span class="pln">
</span><em><span class="pln">     </span></em><em><span class="typ">MyList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"Cherry"</span><span class="pun">)</span></em></pre>
<p>
  This code loops through the MyList ArrayList and displays the list values in sequence.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pln"> value_loopVariable </span><span class="kwd">in</span><span class="pln"> </span><span class="typ">MyList</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     value </span><span class="pun">=</span><span class="pln"> value_loopVariable</span><span class="pun">;</span><span class="pln">
     </span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">value</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(),</span><span class="pln"> </span><span class="str">"ArrayList Value "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> i</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(),</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
     i </span><span class="pun">+=</span><span class="pln"> </span><span class="lit">1</span><span class="pun">;</span></em><span class="pln">

</span><em><span class="pun">}</span></em></pre>
<p>
  The output dialog boxes confirm the values contained by the array list.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11610.gif" border="0"> <img alt="" src="/Images/11609.gif" border="0"> <img alt="" src="/Images/11608.gif" border="0"> <img alt="" src="/Images/11607.gif" border="0"> <img alt="" src="/Images/11606.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 6: Write an ASCII file</strong>
</p>
<p>
  This lesson uses a StreamWriter object to create an empty ASCII file with the CreateText method and write five lines of text to the file.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">StreamWriter</span><span class="pln"> </span><span class="typ">Writer</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="typ">Writer</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">File</span><span class="pun">.</span><span class="typ">CreateText</span><span class="pun">(</span><span class="str">"C:\\MyFile.txt"</span><span class="pun">);</span><span class="pln">

</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 1"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 2"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 3"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 4"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 5"</span><span class="pun">);</span><span class="pln">

</span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  This code creates the empty text file C:\MyFile.txt.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span></em><em><span class="typ">Writer</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">File</span><span class="pun">.</span><span class="typ">CreateText</span><span class="pun">(</span><span class="str">"C:\\MyFile.txt"</span><span class="pun">);</span></em></pre>
<p>
  This code writes a line of text to the file.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="str">"Line 1"</span><span class="pun">)</span></em></pre>
<p>
  Open a file manager window and find the "C:\MyFile.txt" ASCII file you just created.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11559.jpg" border="0">
</p>
<p>
</p>
<p>
  Double-Click on it to open it in Notepad to confirm that the five lines of text inserted by the StreamWriter are there.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11549.jpg" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 7: Read an ASCII file</strong>
</p>
<p>
  This lesson creates uses a StreamReader object to read the ASCII file created in the previous lesson.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">StreamReader</span><span class="pln"> </span><span class="typ">Reader</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">StreamReader</span><span class="pun">(</span><span class="str">"C:\\MyFile.txt"</span><span class="pun">);</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> line </span><span class="pun">=</span><span class="pln"> </span><span class="str">""</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">do</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     line </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Reader</span><span class="pun">.</span><span class="typ">ReadLine</span><span class="pun">();</span><span class="pln">
     </span><span class="kwd">if</span><span class="pln"> </span><span class="pun">((</span><span class="pln">line </span><span class="pun">!=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">))</span><span class="pln">
     </span><span class="pun">{</span><span class="pln">
          </span><span class="kwd">string</span><span class="pln"> number </span><span class="pun">=</span><span class="pln"> line</span><span class="pun">.</span><span class="typ">Substring</span><span class="pun">(</span><span class="pln">line</span><span class="pun">.</span><span class="typ">Length</span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">);</span><span class="pln">
          </span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">line</span><span class="pun">,</span><span class="pln"> </span><span class="str">"This is Line # "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> number</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
     </span><span class="pun">}</span><span class="pln">
 </span><span class="pun">}</span><span class="pln"> </span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(!(</span><span class="pln">line </span><span class="pun">==</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">));</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  The resulting popups confirm that it is reading the file we created.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11615.gif" border="0"> <img alt="" src="/Images/11614.gif" border="0"> <img alt="" src="/Images/11613.gif" border="0"> <img alt="" src="/Images/11612.gif" border="0"> <img alt="" src="/Images/11611.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 8. Move, copy and delete files</strong>
</p>
<p>
  Make sure that your C:\ drive has a C:\Temp\ subdirectory. Create one if it does not.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="kwd">string</span><span class="pln"> filename </span><span class="pun">=</span><span class="pln"> </span><span class="str">"MyFile.txt"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pln"> file </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pun">(</span><span class="str">"C:\\"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> filename</span><span class="pun">);</span><span class="pln">

</span><span class="kwd">try</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     file</span><span class="pun">.</span><span class="typ">MoveTo</span><span class="pun">(</span><span class="str">"C:\\Temp\\"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> filename</span><span class="pun">);</span><span class="pln">
     </span><span class="typ">DialogResult</span><span class="pln"> button1 </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="str">"The file has been moved."</span><span class="pun">,</span><span class="pln"> </span><span class="str">"FEEDBACK MESSAGE"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span><span class="kwd">catch</span><span class="pln"> </span><span class="pun">(</span><span class="typ">Exception</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     </span><span class="typ">DialogResult</span><span class="pln"> button2 </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="str">"The file C:\\MyFile.txt does not exist or"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"subdirectory C:\\Temp\\ does not exist or"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"C:\\Temp\\ already contains MyFile.txt."</span><span class="pun">,</span><span class="pln"> </span><span class="str">"ERROR MESSAGE"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span><span class="pln">
</span><span class="pun">}</span><system.addin.addin("scriptmain", description:="" publisher:="" version:="1.0"><system.clscompliantattribute(false)>
</system.clscompliantattribute(false)></system.addin.addin("scriptmain",></pre>
<p>
  If the file C:\MyFile.txt does not exist, or if the C:\Temp\ subdirectory does not exist, or if you have already moved the file, you will get this message box.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11625.jpg" border="0">
</p>
<p>
</p>
<p>
  If everything was set up correctly, you will get this message.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11624.jpg" border="0">
</p>
<p>
</p>
<p>
  Confirm that MyFile.txt is now in C:\Temp\.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11558.jpg" border="0">
</p>
<p>
</p>
<p>
  To copy the file instead of moving it, change
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     file</span><span class="pun">.</span><span class="typ">MoveTo</span><span class="pun">(</span><span class="str">"C:\Temp\" &amp; filename)</span></em></pre>
<p>
  to
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     file</span><span class="pun">.</span><span class="typ">CopyTo</span><span class="pun">(</span><span class="str">"C:\Temp\" &amp; filename)</span></em><span class="str">.</span></pre>
<p>
  To delete the file instead of moving it, change
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     file</span><span class="pun">.</span><span class="typ">MoveTo</span><span class="pun">(</span><span class="str">"C:\Temp\" &amp; filename)</span></em></pre>
<p>
  to
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     file</span><span class="pun">.</span><span class="typ">Delete</span><span class="pun">()</span></em><span class="pun">.</span></pre>
<p>
  <strong>Lesson 9: Capture the names of all the matching files in a subdirectory to an array list</strong>
</p>
<p>
  Make four copies of the MyFile.txt file in C:\TEMP\ and rename all five files MyFile1.txt, MyFile2.txt, MyFile3.txt, MyFile4.txt and MyFile5.txt as shown below.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11556.jpg" border="0">
</p>
<p>
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="kwd">string</span><span class="pln"> message </span><span class="pun">=</span><span class="pln"> </span><span class="str">"The following files matching the pattern 'My*' were found in C:\\Temp\\"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">DirectoryInfo</span><span class="pln"> di </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">DirectoryInfo</span><span class="pun">(</span><span class="str">"C:\\Temp\\"</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pun">[]</span><span class="pln"> fiArr </span><span class="pun">=</span><span class="pln"> di</span><span class="pun">.</span><span class="typ">GetFiles</span><span class="pun">(</span><span class="str">"My*"</span><span class="pun">);</span><span class="pln">
</span><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pln"> fri </span><span class="kwd">in</span><span class="pln"> fiArr</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> di</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> fri</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">message</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Message"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span></pre>
<p>
  The code
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span></em><em><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">DirectoryInfo</span><span class="pln"> di </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">DirectoryInfo</span><span class="pun">(</span><span class="str">"C:\\Temp\\"</span><span class="pun">);</span></em></pre>
<p>
  creates a DirectoryInfo object
</p>
<p>
  The code
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span></em><em><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pun">[]</span><span class="pln"> fiArr </span><span class="pun">=</span><span class="pln"> di</span><span class="pun">.</span><span class="typ">GetFiles</span><span class="pun">(</span><span class="str">"My*"</span><span class="pun">);</span></em></pre>
<p>
  tells the DirectoryInfo object to look for files starting with the two characters "My."
</p>
<p>
  The code
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pln"> fri </span><span class="kwd">in</span><span class="pln"> fiArr</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> di</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> fri</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span></em></pre>
<p>
  loops through the 'fri' values conatined in the file info array.
</p>
<p>
  The popup confirms that only files beginning with "My" were found.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11616.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 10: Email a file</strong>
</p>
<p>
  Email requires the addition of two libraries to the Imports statements of the script task.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     </span></em><em><span class="pln">using </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Net</span><span class="pun">.</span><span class="typ">Mail</span><span class="pun">;</span></em><span class="pln">
</span><em><span class="pln">     </span></em><em><span class="pln">using </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Net</span><span class="pun">;</span></em></pre>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (You can't actually run this code if you do not have access to an SMTP server and know its IP address.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="str">'</span><span class="pln">using </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Net</span><span class="pun">.</span><span class="typ">Mail</span><span class="pun">;</span><span class="pln"> </span><span class="pun">(</span><span class="typ">Uncomment</span><span class="pln"> and add to the </span><span class="typ">Imports</span><span class="pln"> section</span><span class="pun">)</span><span class="pln">
</span><span class="str">'</span><span class="pln">using </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Net</span><span class="pun">;</span><span class="pln"> </span><span class="pun">(</span><span class="typ">Uncomment</span><span class="pln"> and add to the </span><span class="typ">Imports</span><span class="pln"> section</span><span class="pun">)</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">SenderEmail</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"SenderAddress@domain.com"</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">RecipientEmail</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"RecipientAddress@domain.com"</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Subject</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Here is the data"</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Message</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Attached is your data. Have fun."</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">AttachmentPath</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"C:\\TEMP\\MyFile1.txt"</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">SmtpAddress</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"123.123.123.123"</span><span class="pun">;</span><span class="pln">

</span><span class="typ">MailMessage</span><span class="pln"> myHtmlMessage </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">default</span><span class="pun">(</span><span class="typ">MailMessage</span><span class="pun">);</span><span class="pln">
</span><span class="typ">SmtpClient</span><span class="pln"> mySmtpClient </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">default</span><span class="pun">(</span><span class="typ">SmtpClient</span><span class="pun">);</span><span class="pln">

myHtmlMessage </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">MailMessage</span><span class="pun">(</span><span class="typ">SenderEmail</span><span class="pun">,</span><span class="pln"> </span><span class="typ">RecipientEmail</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Subject</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Message</span><span class="pun">);</span><span class="pln">
myHtmlMessage</span><span class="pun">.</span><span class="typ">Attachments</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="kwd">new</span><span class="pln"> </span><span class="typ">Attachment</span><span class="pun">(</span><span class="typ">AttachmentPath</span><span class="pun">));</span><span class="pln">
mySmtpClient </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SmtpClient</span><span class="pun">(</span><span class="typ">SmtpAddress</span><span class="pun">);</span><span class="pln">
mySmtpClient</span><span class="pun">.</span><span class="typ">Credentials</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">CredentialCache</span><span class="pun">.</span><span class="typ">DefaultNetworkCredentials</span><span class="pun">;</span><span class="pln">
mySmtpClient</span><span class="pun">.</span><span class="typ">Send</span><span class="pun">(</span><span class="pln">myHtmlMessage</span><span class="pun">);</span><span class="pln">
myHtmlMessage</span><span class="pun">.</span><span class="typ">Dispose</span><span class="pun">();</span></pre>
<p>
  Replace the bogus values in the first six statements with real values, execute the code, and an email with attachment will be sent.&nbsp;To add more attachments, add more <em>myHtmlMessage.Attachments.Add</em> statements and AttachmentPath variables.
</p>
<p>
  <strong>Lesson 11: Create a database connection</strong>
</p>
<p>
  Create the Customer table by executing the following T-SQL code in SQL Server Management Studio.
</p>
<pre style="" class="prettyprint lang-sql prettyprinted"><span class="kwd">BEGIN</span><span class="pln"> TRY
</span><span class="kwd">DROP</span><span class="pln"> </span><span class="kwd">TABLE</span><span class="pln"> Customer
</span><span class="kwd">END</span><span class="pln"> TRY
</span><span class="kwd">BEGIN</span><span class="pln"> CATCH
</span><span class="kwd">END</span><span class="pln"> CATCH

</span><span class="kwd">CREATE</span><span class="pln"> </span><span class="kwd">TABLE</span><span class="pln"> Customer
</span><span class="pun">(</span><span class="pln">
	CustomerId </span><span class="typ">INT</span><span class="pun">,</span><span class="pln">
	LastName </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">20</span><span class="pun">),</span><span class="pln">
	FirstName </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">20</span><span class="pun">),</span><span class="pln">
	City </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">20</span><span class="pun">),</span><span class="pln">
	State </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">2</span><span class="pun">),</span><span class="pln">
	ZipCode </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">10</span><span class="pun">),</span><span class="pln">
	Phone </span><span class="typ">VARCHAR</span><span class="pun">(</span><span class="lit">12</span><span class="pun">)</span><span class="pln">
</span><span class="pun">)</span></pre>
<p>
  Browse the SQL Server Managment Studio Object Explorer to confirm that the table was created.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11578.gif" border="0">
</p>
<p>
</p>
<p>
  Next, we need an ADO.NET connection to the server and database containing the Customer table so that our SQL Statements can talk to it.
</p>
<p>
  Create an ADO.NET connection to the server/database by right-clicking the "Connection Managers" panel and selecting "New ADO.NET Connection..." from the menu.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11570.gif" border="0">
</p>
<p>
</p>
<p>
  Click the "New" button of the "Configure ADO.NET Connection Manager" window.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11571.gif" border="0">
</p>
<p>
</p>
<p>
  Select the names of the server and database where you created the Customer table from the drop-down menus and click the "OK" button.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11575.gif" border="0">
</p>
<p>
</p>
<p>
  Click the "OK" button to conclude the connection manager configuration session.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11574.gif" border="0">
</p>
<p>
</p>
<p>
  You can see that the new ADO.NET connection manager has been added to the package.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11576.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 12: Execute an INSERT query</strong>
</p>
<p>
  In order to execute T-SQL statements, the <em>System.Data.SqlClient</em> namespace needs to be added to the <em>using</em> section of the script task.
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><em><span class="pln">     using </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">;</span></em></pre>
<p>
  This statement will insert five records into the Customer table.
</p>
<pre style="" class="prettyprint lang-sql prettyprinted"><em><span class="pln">     </span><span class="kwd">INSERT</span><span class="pln"> </span><span class="kwd">INTO</span><span class="pln"> TestDB</span><span class="pun">.</span><span class="pln">dbo</span><span class="pun">.</span><span class="pln">Customer
          </span><span class="pun">(</span><span class="pln">CustomerId</span><span class="pun">,</span><span class="pln">LastName</span><span class="pun">,</span><span class="pln">FirstName</span><span class="pun">,</span><span class="pln">City</span><span class="pun">,</span><span class="pln">State</span><span class="pun">,</span><span class="pln">ZipCode</span><span class="pun">,</span><span class="pln">Phone</span><span class="pun">)</span><span class="pln">
     </span><span class="kwd">VALUES</span><span class="pln">
          </span><span class="pun">(</span><span class="lit">7923</span><span class="pun">,</span><span class="str">'Blow'</span><span class="pun">,</span><span class="str">'Joe'</span><span class="pun">,</span><span class="str">'Chicago'</span><span class="pun">,</span><span class="str">'IL'</span><span class="pun">,</span><span class="str">'12345-9876'</span><span class="pun">,</span><span class="str">'555-555-5555'</span><span class="pun">),</span><span class="pln">
          </span><span class="pun">(</span><span class="lit">7924</span><span class="pun">,</span><span class="str">'Antoinette'</span><span class="pun">,</span><span class="str">'Marie'</span><span class="pun">,</span><span class="str">'Chicago'</span><span class="pun">,</span><span class="str">'IL'</span><span class="pun">,</span><span class="str">'84356-8456'</span><span class="pun">,</span><span class="str">'777-777-7777'</span><span class="pun">),</span><span class="pln">
          </span><span class="pun">(</span><span class="lit">7925</span><span class="pun">,</span><span class="str">'Doe'</span><span class="pun">,</span><span class="str">'Janet'</span><span class="pun">,</span><span class="str">'Houston'</span><span class="pun">,</span><span class="str">'TX'</span><span class="pun">,</span><span class="str">'99354-9445'</span><span class="pun">,</span><span class="str">'333-444-555'</span><span class="pun">),</span><span class="pln">
          </span><span class="pun">(</span><span class="lit">7926</span><span class="pun">,</span><span class="str">'Alverez'</span><span class="pun">,</span><span class="str">'Desmond'</span><span class="pun">,</span><span class="str">'Des Moines'</span><span class="pun">,</span><span class="str">'IA'</span><span class="pun">,</span><span class="str">'79684-8473'</span><span class="pun">,</span><span class="str">'222-222-2222'</span><span class="pun">),</span><span class="pln">
          </span><span class="pun">(</span><span class="lit">7927</span><span class="pun">,</span><span class="str">'Contrary'</span><span class="pun">,</span><span class="str">'Mary'</span><span class="pun">,</span><span class="str">'Boston'</span><span class="pun">,</span><span class="str">'MA'</span><span class="pun">,</span><span class="str">'17545-4564'</span><span class="pun">,</span><span class="str">'111-111-1111'</span><span class="pun">)</span></em></pre>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (Replace the connection manager 'XW4100-9.TestDB' with your connection manager.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="str">'Replace the connection manager '</span><span class="pln">XW4100</span><span class="pun">-</span><span class="lit">9.TestDB</span><span class="str">'</span><span class="pln"> with your connection manager</span><span class="pun">.</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"INSERT INTO TestDB.dbo.Customer (CustomerId,LastName,FirstName,City,State,ZipCode,Phone) VALUES (7923,'Blow','Joe','Chicago','IL','12345-9876','555-555-5555'),(7924,'Antoinette','Marie','Chicago','IL','84356-8456','777-777-7777'),(7925,'Doe','Janet','Houston','TX','99354-9445','333-444-555'),(7926,'Alverez','Desmond','Des Moines','IA','79684-8473','222-222-2222'),(7927,'Contrary','Mary','Boston','MA','17545-4564','111-111-1111')"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlConnection</span><span class="pln"> myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pln"> myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
myCommand</span><span class="pun">.</span><span class="typ">ExecuteNonQuery</span><span class="pun">();</span><span class="pln">
myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span></pre>
<p>
  Execute a query on the Customer table to confirm that the five records were inserted.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11629.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 13: Execute a SELECT query</strong>
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (Replace the connection manager 'XW4100-9.TestDB' with your connection manager.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="str">'Replace the connection manager '</span><span class="pln">XW4100</span><span class="pun">-</span><span class="lit">9.TestDB</span><span class="str">'</span><span class="pln"> with your connection manager</span><span class="pun">.</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"SELECT CustomerId,LastName,FirstName,City,State,ZipCode,Phone FROM TestDB.dbo.Customer"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlConnection</span><span class="pln"> myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pln"> myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">SqlDataReader</span><span class="pln"> reader </span><span class="pun">=</span><span class="pln"> myCommand</span><span class="pun">.</span><span class="typ">ExecuteReader</span><span class="pun">(</span><span class="typ">CommandBehavior</span><span class="pun">.</span><span class="typ">CloseConnection</span><span class="pun">);</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> message </span><span class="pun">=</span><span class="pln"> </span><span class="str">""</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;
</span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="pln">reader</span><span class="pun">.</span><span class="typ">Read</span><span class="pun">())</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Convert</span><span class="pun">.</span><span class="typ">ToInt32</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"CustomerId"</span><span class="pun">]).</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"LastName"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"FirstName"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"City"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"State"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"ZipCode"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"Phone"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">

     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Customer ID: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Last Name: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"First Name: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"City: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"State: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Zip Code: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Phone: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">

</span><span class="pun">}</span><span class="pln">

reader</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">
myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">

</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">message</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Record Detail"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span></pre>
<p>
  The output dialog box confirms that the data in the Customer table has been read.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11630.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 14: Execute an UPDATE query</strong>
</p>
<p>
  The following code contains the SQL statement
</p>
<pre style="" class="prettyprint lang-sql prettyprinted"><em><span class="pln">     </span><span class="kwd">UPDATE</span><span class="pln"> TestDB</span><span class="pun">.</span><span class="pln">dbo</span><span class="pun">.</span><span class="pln">Customer </span><span class="kwd">SET</span><span class="pln"> City </span><span class="pun">=</span><span class="pln"> </span><span class="str">'Seattle'</span><span class="pln"> </span><span class="kwd">WHERE</span><span class="pln"> City </span><span class="pun">=</span><span class="pln"> </span><span class="str">'Chicago'</span></em></pre>
<p>
  which will change the City value from Chicago to Seattle.
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (Replace the connection manager 'XW4100-9.TestDB' with your connection manager.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="str">'Replace the connection manager '</span><span class="pln">XW4100</span><span class="pun">-</span><span class="lit">9.TestDB</span><span class="str">'</span><span class="pln"> with your connection manager</span><span class="pun">.</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"UPDATE TestDB.dbo.Customer SET City = 'Seattle' WHERE City = 'Chicago'"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlConnection</span><span class="pln"> myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pln"> myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
myCommand</span><span class="pun">.</span><span class="typ">ExecuteNonQuery</span><span class="pun">();</span><span class="pln">
myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span></pre>
<p>
  Execute a query on the Customer table to confirm that Chicago was changed to Seattle.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11634.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 15: Execute a query as a stored procedure</strong>
</p>
<p>
  Placing a C#.NET SQL query in a long string is OK for learning purposes, but not in production environments, because queries can get very large.&nbsp;The solution is to place the query in a stored procedure and execute the stored procedure.
</p>
<p>
  To create the previous select query as a stored procedure, copy this code to a SQL Server Mangament Study query window and execute it.
</p>
<pre style="" class="prettyprint lang-sql prettyprinted"><span class="kwd">CREATE</span><span class="pln"> </span><span class="kwd">PROC</span><span class="pln"> SelectCustomer
</span><span class="kwd">AS</span><span class="pln">
</span><span class="kwd">SELECT</span><span class="pln">
&nbsp;&nbsp; &nbsp;CustomerId</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;LastName</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;FirstName</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;City</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;State</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;ZipCode</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;Phone
</span><span class="kwd">FROM</span><span class="pln">
&nbsp;&nbsp; &nbsp;TestDB</span><span class="pun">.</span><span class="pln">dbo</span><span class="pun">.</span><span class="pln">Customer</span></pre>
<p>
  Confirm that the stored procedure was created in SQL Server Management Studio.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11594.gif" border="0">
</p>
<p>
</p>
<p>
  Following is the same code as Lesson 14, except that the SELECT query string has been replaced by "EXEC SelectCustomer."
</p>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code, then save and execute it. (Replace the connection manager 'XW4100-9.TestDB' with your connection manager.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="str">'Replace the connection manager '</span><span class="pln">XW4100</span><span class="pun">-</span><span class="lit">9.TestDB</span><span class="str">'</span><span class="pln"> with your connection manager</span><span class="pun">.</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"EXEC SelectCustomer"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlConnection</span><span class="pln"> myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pln"> myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">SqlDataReader</span><span class="pln"> reader </span><span class="pun">=</span><span class="pln"> myCommand</span><span class="pun">.</span><span class="typ">ExecuteReader</span><span class="pun">(</span><span class="typ">CommandBehavior</span><span class="pun">.</span><span class="typ">CloseConnection</span><span class="pun">);</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">string</span><span class="pln"> message </span><span class="pun">=</span><span class="pln"> </span><span class="str">""</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="pln">reader</span><span class="pun">.</span><span class="typ">Read</span><span class="pun">())</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
     </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Convert</span><span class="pun">.</span><span class="typ">ToInt32</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"CustomerId"</span><span class="pun">]).</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"LastName"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"FirstName"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"City"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"State"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"ZipCode"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">
     </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> reader</span><span class="pun">[</span><span class="str">"Phone"</span><span class="pun">].</span><span class="typ">ToString</span><span class="pun">();</span><span class="pln">

     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Customer ID: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">CustId</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Last Name: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">LName</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"First Name: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">FName</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"City: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Municipality</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"State: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Region</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Zip Code: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Zip</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">
     message </span><span class="pun">+=</span><span class="pln"> </span><span class="str">"Phone: "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">PhoneNumber</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Environment</span><span class="pun">.</span><span class="typ">NewLine</span><span class="pun">;</span><span class="pln">

</span><span class="pun">}</span><span class="pln">

reader</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">
myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">

</span><span class="typ">DialogResult</span><span class="pln"> button </span><span class="pun">=</span><span class="pln"> </span><span class="typ">MessageBox</span><span class="pun">.</span><span class="typ">Show</span><span class="pun">(</span><span class="pln">message</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Record Detail"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">MessageBoxButtons</span><span class="pun">.</span><span class="pln">OK</span><span class="pun">);</span></pre>
<p>
  The result with the stored procedure is identical to the result with the query in a string.
</p>
<p>
</p>
<p>
  <img alt="" src="/Images/11635.gif" border="0">
</p>
<p>
</p>
<p>
  <strong>Lesson 16: Putting it all together</strong>
</p>
<p>
  Execute this T-SQL statement in Microsoft SQL Server Management Studio to create the data for the following demo, which uses most of the tools presented in the previous lessons.
</p>
<pre style="" class="prettyprint lang-sql prettyprinted"><span class="kwd">CREATE</span><span class="pln"> </span><span class="kwd">TABLE</span><span class="pln"> </span><span class="pun">[</span><span class="pln">TestDB</span><span class="pun">].[</span><span class="pln">dbo</span><span class="pun">].[</span><span class="pln">SalesReps</span><span class="pun">](</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">RepId</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">int</span><span class="pun">]</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">LastName</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">varchar</span><span class="pun">](</span><span class="lit">20</span><span class="pun">)</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">FirstName</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">varchar</span><span class="pun">](</span><span class="lit">20</span><span class="pun">)</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">Email</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">varchar</span><span class="pun">](</span><span class="lit">30</span><span class="pun">)</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pln">
</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">ON</span><span class="pln"> </span><span class="pun">[</span><span class="kwd">PRIMARY</span><span class="pun">]</span><span class="pln">
GO

</span><span class="kwd">INSERT</span><span class="pln"> </span><span class="kwd">INTO</span><span class="pln"> </span><span class="pun">[</span><span class="pln">TestDB</span><span class="pun">].[</span><span class="pln">dbo</span><span class="pun">].[</span><span class="pln">SalesReps</span><span class="pun">]</span><span class="pln">
</span><span class="pun">(</span><span class="pln">RepId</span><span class="pun">,</span><span class="pln">LastName</span><span class="pun">,</span><span class="pln">FirstName</span><span class="pun">,</span><span class="pln">Email</span><span class="pun">)</span><span class="pln">
</span><span class="kwd">VALUES</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1234</span><span class="pun">,</span><span class="str">'Smith'</span><span class="pun">,</span><span class="str">'Will'</span><span class="pun">,</span><span class="str">'smithw@domain.com'</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1235</span><span class="pun">,</span><span class="str">'Jones'</span><span class="pun">,</span><span class="str">'Indiana'</span><span class="pun">,</span><span class="str">'jonesi@domain.com'</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1236</span><span class="pun">,</span><span class="str">'Lange'</span><span class="pun">,</span><span class="str">'Jessica'</span><span class="pun">,</span><span class="str">'langj@domain.com'</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1237</span><span class="pun">,</span><span class="str">'Flintstone'</span><span class="pun">,</span><span class="str">'Fred'</span><span class="pun">,</span><span class="str">'flintstonef@domain.com'</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1238</span><span class="pun">,</span><span class="str">'Cowell'</span><span class="pun">,</span><span class="str">'Simon'</span><span class="pun">,</span><span class="str">'cowells@domain.com'</span><span class="pun">)</span><span class="pln">

</span><span class="kwd">CREATE</span><span class="pln"> </span><span class="kwd">TABLE</span><span class="pln"> </span><span class="pun">[</span><span class="pln">TestDB</span><span class="pun">].[</span><span class="pln">dbo</span><span class="pun">].[</span><span class="pln">Sales</span><span class="pun">](</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">RepId</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">int</span><span class="pun">]</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">ItemId</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">int</span><span class="pun">]</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pun">,</span><span class="pln">
&nbsp;&nbsp; &nbsp;</span><span class="pun">[</span><span class="pln">Amount</span><span class="pun">]</span><span class="pln"> </span><span class="pun">[</span><span class="typ">numeric</span><span class="pun">](</span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="lit">2</span><span class="pun">)</span><span class="pln"> </span><span class="kwd3">NULL</span><span class="pln">
</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">ON</span><span class="pln"> </span><span class="pun">[</span><span class="kwd">PRIMARY</span><span class="pun">]</span><span class="pln">
GO

</span><span class="kwd">INSERT</span><span class="pln"> </span><span class="kwd">INTO</span><span class="pln"> </span><span class="pun">[</span><span class="pln">TestDB</span><span class="pun">].[</span><span class="pln">dbo</span><span class="pun">].[</span><span class="pln">Sales</span><span class="pun">]</span><span class="pln">
</span><span class="pun">(</span><span class="pln">RepId</span><span class="pun">,</span><span class="pln">ItemId</span><span class="pun">,</span><span class="pln">Amount</span><span class="pun">)</span><span class="pln">
</span><span class="kwd">VALUES</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1234</span><span class="pun">,</span><span class="lit">98765</span><span class="pun">,</span><span class="lit">1829.37</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1234</span><span class="pun">,</span><span class="lit">74829</span><span class="pun">,</span><span class="lit">7345.87</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1235</span><span class="pun">,</span><span class="lit">85893</span><span class="pun">,</span><span class="lit">9475.72</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1235</span><span class="pun">,</span><span class="lit">12938</span><span class="pun">,</span><span class="lit">2436.34</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1236</span><span class="pun">,</span><span class="lit">56465</span><span class="pun">,</span><span class="lit">9456.12</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1236</span><span class="pun">,</span><span class="lit">74865</span><span class="pun">,</span><span class="lit">3746.99</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1237</span><span class="pun">,</span><span class="lit">43526</span><span class="pun">,</span><span class="lit">6453.54</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1237</span><span class="pun">,</span><span class="lit">38464</span><span class="pun">,</span><span class="lit">4985.84</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1238</span><span class="pun">,</span><span class="lit">64345</span><span class="pun">,</span><span class="lit">8439.66</span><span class="pun">),</span><span class="pln">
</span><span class="pun">(</span><span class="lit">1238</span><span class="pun">,</span><span class="lit">78534</span><span class="pun">,</span><span class="lit">7329.52</span><span class="pun">)</span></pre>
<p>
  Replace the C#.NET script task code in the Main procedure from the previous lesson with the following code. (Replace the connection manager 'XW4100-9.TestDB' with your connection manager.)
</p>
<pre style="" class="prettyprint lang-cs prettyprinted"><span class="com">/*

Be sure that the following four namespaces are included in the </span><em><span class="com">using</span></em><span class="com"> section of the script task.

using System.Collections;
using System.Data.SqlClient;
using System.Net;
using System.Net.Mail;

*/</span><span class="pln">

</span><span class="typ">ArrayList</span><span class="pln"> </span><span class="typ">SalesRepList</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">ArrayList</span><span class="pun">();</span><span class="pln">

</span><span class="kwd">string</span><span class="pln"> mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"SELECT RepId FROM TestDB.dbo.SalesReps"</span><span class="pun">;</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlConnection</span><span class="pln"> myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pln"> myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
</span><span class="typ">SqlDataReader</span><span class="pln"> reader </span><span class="pun">=</span><span class="pln"> myCommand</span><span class="pun">.</span><span class="typ">ExecuteReader</span><span class="pun">(</span><span class="typ">CommandBehavior</span><span class="pun">.</span><span class="typ">CloseConnection</span><span class="pun">);</span><span class="pln">

</span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="pln">reader</span><span class="pun">.</span><span class="typ">Read</span><span class="pun">())</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">SalesRepList</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"RepId"</span><span class="pun">]);</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

reader</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">
myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">

</span><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="typ">int</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pln"> </span><span class="kwd">in</span><span class="pln"> </span><span class="typ">SalesRepList</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">ArrayList</span><span class="pln"> lines </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">ArrayList</span><span class="pun">();</span><span class="pln">
&nbsp;&nbsp;&nbsp; lines</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="str">"RepId&nbsp;&nbsp; Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ItemId&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Amount"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"\r\n\r\n"</span><span class="pun">);</span><span class="pln">

&nbsp;&nbsp;&nbsp; mySqlStatement </span><span class="pun">=</span><span class="pln"> </span><span class="str">"SELECT a.RepId,a.FirstName + ' ' + a.LastName AS Name,a.Email,b.ItemId,b.Amount FROM TestDB.dbo.SalesReps a INNER JOIN TestDB.dbo.Sales b ON a.RepId = b.RepId WHERE a.RepId = "</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">();</span><span class="pln">
&nbsp;&nbsp;&nbsp; myADONETConnection </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="typ">SqlConnection</span><span class="pun">)(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Connections</span><span class="pun">[</span><span class="str">"XW4100-9.TestDB"</span><span class="pun">].</span><span class="typ">AcquireConnection</span><span class="pun">(</span><span class="typ">Dts</span><span class="pun">.</span><span class="typ">Transaction</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">as</span><span class="pln"> </span><span class="typ">SqlConnection</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; myCommand </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="typ">Data</span><span class="pun">.</span><span class="typ">SqlClient</span><span class="pun">.</span><span class="typ">SqlCommand</span><span class="pun">(</span><span class="pln">mySqlStatement</span><span class="pun">,</span><span class="pln"> myADONETConnection</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; reader </span><span class="pun">=</span><span class="pln"> myCommand</span><span class="pun">.</span><span class="typ">ExecuteReader</span><span class="pun">(</span><span class="typ">CommandBehavior</span><span class="pun">.</span><span class="typ">CloseConnection</span><span class="pun">);</span><span class="pln">

&nbsp;&nbsp;&nbsp; </span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="pln">reader</span><span class="pun">.</span><span class="typ">Read</span><span class="pun">())</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="pun">{</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">RepId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Convert</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"RepId"</span><span class="pun">]);</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Name</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pun">)</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"Name"</span><span class="pun">];</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Email</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pun">)</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"Email"</span><span class="pun">];</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">ItemId</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Convert</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"ItemId"</span><span class="pun">]);</span><span class="pln">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Amount</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Convert</span><span class="pun">.</span><span class="typ">ToString</span><span class="pun">(</span><span class="pln">reader</span><span class="pun">[</span><span class="str">"Amount"</span><span class="pun">]);</span><span class="pln">

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lines</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="typ">RepId</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"\t"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Name</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"\t"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">ItemId</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">"\t"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Amount</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="pun">}</span><span class="pln">

&nbsp;&nbsp;&nbsp; reader</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">
&nbsp;&nbsp;&nbsp; myADONETConnection</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">

    </span><span class="kwd">string</span><span class="pln"> file_content </span><span class="pun">=</span><span class="pln"> </span><span class="str">""</span><span class="pun">;</span><span class="pln">
    </span><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">string</span><span class="pln"> line_loopVariable </span><span class="kwd">in</span><span class="pln"> lines</span><span class="pun">)</span><span class="pln">
    </span><span class="pun">{</span><span class="pln">
        file_content </span><span class="pun">+=</span><span class="pln"> line_loopVariable </span><span class="pun">+</span><span class="pln"> </span><span class="str">"\r\n"</span><span class="pun">;</span><span class="pln">
    </span><span class="pun">}</span><span class="pln">

&nbsp;&nbsp;&nbsp; </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">StreamWriter</span><span class="pln"> </span><span class="typ">Writer</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">null</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">Writer</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">File</span><span class="pun">.</span><span class="typ">CreateText</span><span class="pun">(</span><span class="str">"C:\\SalesReport"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">".txt"</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">WriteLine</span><span class="pun">(</span><span class="pln">file_content</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">Writer</span><span class="pun">.</span><span class="typ">Close</span><span class="pun">();</span><span class="pln">

&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">SenderEmail</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"sender@domain.com"</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">RecipientEmail</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> email</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Subject</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Sales Report"</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">Message</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"Attached is your sales report."</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">AttachmentPath</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"C:\\SalesReport"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">".txt"</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="kwd">string</span><span class="pln"> </span><span class="typ">SmtpAddress</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="str">"123.123.123.123"</span><span class="pun">;</span><span class="pln">

&nbsp;&nbsp;&nbsp; </span><span class="typ">MailMessage</span><span class="pln"> myHtmlMessage </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">default</span><span class="pun">(</span><span class="typ">MailMessage</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">SmtpClient</span><span class="pln"> mySmtpClient </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">default</span><span class="pun">(</span><span class="typ">SmtpClient</span><span class="pun">);</span><span class="pln">

&nbsp;&nbsp;&nbsp; myHtmlMessage </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">MailMessage</span><span class="pun">(</span><span class="typ">SenderEmail</span><span class="pun">,</span><span class="pln"> </span><span class="typ">RecipientEmail</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Subject</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Message</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; myHtmlMessage</span><span class="pun">.</span><span class="typ">Attachments</span><span class="pun">.</span><span class="typ">Add</span><span class="pun">(</span><span class="kwd">new</span><span class="pln"> </span><span class="typ">Attachment</span><span class="pun">(</span><span class="typ">AttachmentPath</span><span class="pun">));</span><span class="pln">
&nbsp;&nbsp;&nbsp; mySmtpClient </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">SmtpClient</span><span class="pun">(</span><span class="typ">SmtpAddress</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; mySmtpClient</span><span class="pun">.</span><span class="typ">Credentials</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="typ">CredentialCache</span><span class="pun">.</span><span class="typ">DefaultNetworkCredentials</span><span class="pun">;</span><span class="pln">
&nbsp;&nbsp;&nbsp; mySmtpClient</span><span class="pun">.</span><span class="typ">Send</span><span class="pun">(</span><span class="pln">myHtmlMessage</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; myHtmlMessage</span><span class="pun">.</span><span class="typ">Dispose</span><span class="pun">();</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="kwd">foreach</span><span class="pln"> </span><span class="pun">(</span><span class="typ">int</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pln"> </span><span class="kwd">in</span><span class="pln"> </span><span class="typ">SalesRepList</span><span class="pun">)</span><span class="pln">
</span><span class="pun">{</span><span class="pln">
&nbsp;&nbsp;&nbsp; </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pln"> file </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">new</span><span class="pln"> </span><span class="typ">System</span><span class="pun">.</span><span class="pln">IO</span><span class="pun">.</span><span class="typ">FileInfo</span><span class="pun">(</span><span class="str">"C:\\SalesReport"</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="typ">Rep_loopVariable</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="str">".txt"</span><span class="pun">);</span><span class="pln">
&nbsp;&nbsp;&nbsp; file</span><span class="pun">.</span><span class="typ">Delete</span><span class="pun">();</span><span class="pln">
</span><span class="pun">}</span></pre>
<p>
  The demo code reads all the RepIds in the SalesReps table into an ArrayList. It then loops through the array list and joins the SalesReps table with the Sales table for each RepId. It creates an ASCII file report for each representative, then emails that report as an attachement to the representative. After the RepId ArrayList finishes, it is looped through again to delete the ASCII files created for each representative.
</p>
<p>
  If you want to make the demo actually work, you will have to replace the sender email address and the email addresses in the SalesReps table with real email addresses that you can acces, and enter a valid SMTP IP address.
</p>
<h3>
  Conclusion
</h3>
<p>
  The basic programming tools presented in this article can enable SSIS package developers familiar with one or more programming languages but not with C#.NET to write useful SSIS script tasks almost immediately.
</p>
<p>
  For another example of what can be done with these tools, see my previous SQL Server Central article <strong><a href="http://www.sqlservercentral.com/articles/Execution+Logging/69858/">Copy and Paste SSIS Execution Monitoring with Failure-Alert Email</a></strong>. This package is written in VB.NET, but the tools are exactly the same.
</p>
</div>

                    

<div class="content-meta">
  

<div class="share-tools">
  <div class="addthis_toolbox addthis_default_style ">
    <p>Thank this author by sharing:</p>
    <a class="addthis_button_google_plusone at300b" g:plusone:annotation="none"><div id="___plusone_1" style="text-indent: 0px; margin: 0px; padding: 0px; background: none repeat scroll 0% 0% transparent; border-style: none; float: none; line-height: normal; font-size: 1px; vertical-align: baseline; display: inline-block; width: 24px; height: 15px;"><iframe title="+1" data-gapiattached="true" src="https://apis.google.com/u/0/se/0/_/+1/fastbutton?usegapi=1&amp;annotation=none&amp;size=small&amp;hl=en-US&amp;origin=http%3A%2F%2Fwww.sqlservercentral.com&amp;url=http%3A%2F%2Fwww.sqlservercentral.com%2Farticles%2FIntegration%2BServices%2B(SSIS)%2F76439%2F&amp;gsrc=3p&amp;jsh=m%3B%2F_%2Fscs%2Fapps-static%2F_%2Fjs%2Fk%3Doz.gapi.en.BL6kwY7kJos.O%2Fm%3D__features__%2Fam%3DAQ%2Frt%3Dj%2Fd%3D1%2Ft%3Dzcms%2Frs%3DAGLTcCM_GOkJcVRrBNGMJmjE7Rz7IVWt-w#_methods=onPlusOne%2C_ready%2C_close%2C_open%2C_resizeMe%2C_renderstart%2Concircled%2Cdrefresh%2Cerefresh&amp;id=I1_1418395015529&amp;parent=http%3A%2F%2Fwww.sqlservercentral.com&amp;pfname=&amp;rpctoken=11206071" name="I1_1418395015529" id="I1_1418395015529" vspace="0" tabindex="0" style="position: static; top: 0px; width: 24px; margin: 0px; border-style: none; left: 0px; visibility: visible; height: 15px;" scrolling="no" marginwidth="0" marginheight="0" hspace="0" frameborder="0" width="100%"></iframe></div></a>
    <a title="LinkedIn" target="_blank" href="http://www.addthis.com/bookmark.php?v=300&amp;winname=addthis&amp;pub=ra-4f3bb4c87aeb8915&amp;source=tbx-300&amp;lng=es-AR&amp;s=linkedin&amp;url=http%3A%2F%2Fwww.sqlservercentral.com%2Farticles%2FIntegration%2BServices%2B(SSIS)%2F76439%2F&amp;title=A%20C%23.NET%20toolkit%20for%20writing%20SSIS%20Script%20Tasks%20-%20SQLServerCentral&amp;ate=AT-ra-4f3bb4c87aeb8915/-/-/548afd8623c70903/3&amp;frommenu=1&amp;uid=548afd86cd5e3272&amp;ct=1&amp;pre=http%3A%2F%2Fwww.sqlservercentral.com%2Farticles%2FIntegration%2BServices%2B(SSIS)%2F76439%2F&amp;tt=0&amp;captcha_provider=nucaptcha" class="addthis_button_linkedin at300b"><span class="at16nc at300bs at15nc at15t_linkedin at16t_linkedin"><span class="at_a11y">Share on linkedin</span></span></a>
    <a href="#" title="Facebook" class="addthis_button_facebook at300b"><span class="at16nc at300bs at15nc at15t_facebook at16t_facebook"><span class="at_a11y">Share on facebook</span></span></a>
    <a href="#" title="Tweet" class="addthis_button_twitter at300b"><span class="at16nc at300bs at15nc at15t_twitter at16t_twitter"><span class="at_a11y">Share on twitter</span></span></a>
    <a href="#" style="display: inline-block;" class="addthis_counter addthis_bubble_style"><a href="#" title="View more services" target="_blank" class="addthis_button_expanded">2</a><a class="atc_s addthis_button_compact"><span></span></a></a>
  <div class="atclear"></div></div>
  <script type="text/javascript">
      var addthis_config = {
          pubid: "ra-4f3bb4c87aeb8915"
      };

      SSC.loadScript("s7.addthis.com/js/250/addthis_widget.js");
  </script>
</div>
  <ul>
	  <li><span isratingcontrol="true"><img src="/Resources/Images/FilledStar.png"> <img src="/Resources/Images/FilledStar.png"> <img src="/Resources/Images/FilledStar.png"> <img src="/Resources/Images/FilledStar.png"> <img src="/Resources/Images/EmptyStar.png">  <a id="ctl00_ctl00_MainContent_MainContent_DisplayLimiterControl_ContentMetadata2_RateThisLink" onclick="IFramePopup_Open(this, event, '/sqlservercentral2/Controls/Rating/RatingPopup.aspx?ContentItemID=76439', 330, 'RateThis', '__doPostBack(\'ctl00$ctl00$MainContent$MainContent$DisplayLimiterControl$ContentMetadata2$ctl05\',\'[ifpe_arg]\')');" href="javascript:;">&nbsp;Rate this</a></span></li>
    <li>
      <img src="/Resources/Images/Discuss.gif">&nbsp;
	    <a href="/Forums/FindPost1220012.aspx">Join the discussion</a>
    </li>
    <li>
  <a href="javascript:;" class="add-to-briefcase" data-content-item-id="76439">
    <img src="/Resources/Images/briefcase.gif" align="bottom">&nbsp;
    Add to briefcase
  </a>
</li>
	  
      <li>
        

<a href="Printable" onclick="window.open('Printable', null, 'width=600,height=600,menubar=1,resizable=1,scrollbars=1,location=0,status=0'); return false;">
  <img src="/Resources/Images/print.gif" alt="">&nbsp;
  Print
</a>
      </li>
	  
  </ul>
</div>


<div class="content-views">
	Total article views: 13858
	<span class="Separator">|</span>
	Views in the last 30 days: 48
</div>

                </td>
                <td rowspan="2" width="20">&nbsp;</td>
                
                    <td width="315">
                        
                        
                            <div class="BarSpacer"></div>
                            <div>
                                <div class="BarLeft"></div>
                                <div class="Bar">
                                    <div class="Subheading"></div>
                                    Related Articles
                                </div>
                                

<div class="IndentedColumn">
    <div class="contentSummary">
    
        
        
            <div class="SearchResult" id="f801103">
                <div class="SearchType forum"><div>FORUM</div></div>
                <div class="SearchDetails">
                    <h3>
                        <a href="/Forums/FindPost801103.aspx">How to receive a Message from a MSMQ using Message Queue task with out message label as "String Message"</a>
                    </h3>
                    <ul class="byline">
                      <li>2009/10/09</li>
                      
                    </ul>
                    
                        <p>Receive message from a MSMQ using message queue task with lable other than "String Message".</p>
                    
                </div>
            </div>
        
        
        
            <div class="SearchResult" id="f718851">
                <div class="SearchType forum"><div>FORUM</div></div>
                <div class="SearchDetails">
                    <h3>
                        <a href="/Forums/FindPost718851.aspx">can you please write some messages with this string "Timeout Expired" to sqlagent log</a>
                    </h3>
                    <ul class="byline">
                      <li>2009/05/18</li>
                      
                    </ul>
                    
                        <p>can you please write some messages with this string "Timeout Expired" to sqlagent log</p>
                    
                </div>
            </div>
        
        
        
            <div class="SearchResult" id="f497615">
                <div class="SearchType forum"><div>FORUM</div></div>
                <div class="SearchDetails">
                    <h3>
                        <a href="/Forums/FindPost497615.aspx">Create Login Script</a>
                    </h3>
                    <ul class="byline">
                      <li>2012/04/13</li>
                      
                    </ul>
                    
                        <p>Error with Create Login Script</p>
                    
                </div>
            </div>
        
        
        
            <div class="SearchResult" id="b92651">
                <div class="SearchType blog"><div>BLOG</div></div>
                <div class="SearchDetails">
                    <h3>
                        <a href="/blogs/sqlballs/2011/10/17/sql-university-lesson-3-page-compression/">SQL University Lesson 3 Page Compression</a>
                    </h3>
                    <ul class="byline">
                      <li>2011/10/17</li>
                      
                    </ul>
                    
                        <p>
Lesson 2: Internal Structures, Vardecimal, &amp; Row Compression 


Welcome to Lesson 3 on Compress...</p>
                    
                </div>
            </div>
        
        
        
            <div class="SearchResult" id="b96469">
                <div class="SearchType blog"><div>BLOG</div></div>
                <div class="SearchDetails">
                    <h3>
                        <a href="/blogs/sherry-lis-bi-corner/2012/12/03/mdx-23-hello-world-lesson-in-mdx/">MDX #23 – “Hello World!” Lesson in MDX</a>
                    </h3>
                    <ul class="byline">
                      <li>2012/12/03</li>
                      
                    </ul>
                    
                        <p>Almost every tool we learned has some sort of “Hello World!” tutorial lesson.
So here comes the “He...</p>
                    
                </div>
            </div>
        
        
    
    </div>
</div>

                            </div>
                        

<div id="tagCloud">
    <div class="BarLeft"></div><div class="Bar">Tags</div>

    <div class="IndentedColumn">
        <div class="IndentedTagColumn">
           <table id="ctl00_ctl00_MainContent_MainContent_DisplayLimiterControl_TagCloud1_TagsList" style="border-collapse:collapse;" border="0" cellspacing="0">
	<tbody><tr>
		<td valign="top">
			        <a href="/articles/C%23/">c#</a> 
			        
			        &nbsp;&nbsp;&nbsp;
		        </td>
	</tr><tr>
		<td valign="top">
			        <a href="/articles/Integration+Services+(SSIS)/">integration services (ssis)</a> 
			        
			        &nbsp;&nbsp;&nbsp;
		        </td>
	</tr><tr>
		<td valign="top">
			        <a href="/articles/SMTP/">smtp</a> 
			        
			        &nbsp;&nbsp;&nbsp;
		        </td>
	</tr><tr>
		<td valign="top">
			        <a href="/articles/T-SQL/">t-sql</a> 
			        
			        &nbsp;&nbsp;&nbsp;
		        </td>
	</tr>
</tbody></table>
        </div>
    </div>
</div>
<!-- -->
                        
                        <div class="BarSpacer">&nbsp;</div>
                        <div class="IndentedColumn">
                            <div class="IndentedTagColumn">
                                <a href="/Contributions/Home"><img src="/Resources/Images/Writeforus_M1.gif" alt="Contribute"></a>
                            </div>
                        </div>
                    
                    
                </td>
            </tr>
        </tbody></table>
    
		


    

<script type="text/javascript">
//<![CDATA[

var Page_ValidationActive = false;
if (typeof(ValidatorOnLoad) == "function") {
    ValidatorOnLoad();
}

function ValidatorOnSubmit() {
    if (Page_ValidationActive) {
        return ValidatorCommonOnSubmit();
    }
    else {
        return true;
    }
}
        WebForm_AutoFocus('ctl00_ctl00_MainContent_MainContent_DisplayLimiterControl_RegistrationControl_EmailAddress');Sys.Application.initialize();
//]]>
</script>
</form>

				<!-- [content_end] -->
			</td>
			
		</tr>
	</tbody></table>
	<table class="MainLayoutContainer MainLayoutContainerBottom" width="100%" border="0" cellpadding="0" cellspacing="0">
		<tbody><tr class="BodyRow">
			<td class="BottomLeft">&nbsp;</td>
			<td>
				<div class="Footer">
					Copyright © 2002-2014 Simple Talk Publishing. All Rights Reserved. <a href="http://www.sqlservercentral.com/About/Privacy/">Privacy Policy.</a> <a href="http://www.sqlservercentral.com/About/Terms">Terms of Use.</a> <a href="mailto:abuse@sqlservercentral.com">Report Abuse.</a>
				</div>
			</td>
			<td class="BottomRight">&nbsp;</td>
