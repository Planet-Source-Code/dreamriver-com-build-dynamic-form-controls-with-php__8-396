<div align="center">

## Build Dynamic Form Controls with PHP


</div>

### Description

Describes how to create dynamic HTML forms using php.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[dreamriver\.com](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/dreamriver-com.md)
**Level**          |Intermediate
**User Rating**    |4.1 (33 globes from 8 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Controls/ Forms/ Dialogs/ Menus](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/controls-forms-dialogs-menus__8-3.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/dreamriver-com-build-dynamic-form-controls-with-php__8-396/archive/master.zip)





### Source Code

```
<i>Note: This article was originally written for and published by <a href="http://www.internet.com">Internet.com</a> on <a href="http://www.phpbuilder.com">phpbuilder.com</a>
</i>
<h1>&quot;Build Dynamic Form Controls with PHP&quot;</h1>
<img src='../images/rCreech.jpg' width='110' height='120' hspace='15' vspace='10' border='0' align="left" alt='Richard Creech, Dreamriver.com'>
<h4>Introduction</h4>
<p>How do you build html form objects to make them dynamic? Why would you want to? What are examples of dynamic form objects scripted in php? We'll answer these questions and more, and provide you with simple, usable code in the pages ahead. By the time you've finished reading you will be able to create these dynamic form objects yourself and build better and smarter forms.
</p>
<h4>Background - It all starts at the Form</h4>
<p>Our look at 'Building Dynamic Form Controls' is based on the understanding that you know html form objects and how to use html form objects in a web page. Briefly, these objects include text box, textarea, checkbox, radio, select, hidden, reset, submit, button and image objects and the form element itself. Each form object should be given a name. Each named object will have a value. The combination of name and value attributes are known as name=value pairs. Here's a plain text input type example of a name=value pair:
</p>
Text
<code>
/* the name=value pair is firstName=  */<br>
&lt;input type="text" name="firstName" value="">
</code>
<p>Using the standard form attribute called "action" is the way we decide what process or file will do something with our form data.
</p>
<code>
&lt;form name="myForm" method="post" action="mailto:yourEmail@yourDomain.com">
</code>
<p>Alternatively - and frequently - we want a script to handle our form, and not simply email the data as in the form code above. It is here, in handling form objects after they are parsed by php, that we begin our discussion.
</p>
<h4>Dynamic Scripting of Form Objects</h4>
<p>Remember filling out that web form, clicking on submit - but you missed something and got an error message instead? So you clicked on the 'Back' button, the form page loaded and ... all your entries were gone and you had to start from scratch again? Here's code to use instead. By using dynamic handling of any name=value pair we can avoid 'dead end' forms, and make it easy for the user to provide us data. We do this by building a form containing these objects. The objects themselves contain the values that we need. Here's how you code some of the more common objects on that form to retrieve the values you need:
</p>
<h4>Build a Dynamic Text Input Type</h4>
<code>
/* The current value for $firstName will reappear in the text input type */<br>
&lt;input type="text" name="firstName" value="&lt;?php echo $firstName;?>">
</code>
<p>When the form is submitted and then redisplayed it will contain the current value for the form object. Note that these values are not available forever! Unless otherwise handled, the values persist only while processing the form. If any another page is loaded without our form variables then we lose our $firstName variable value - and all our other variables. We will see one way to make variable values persist when we consider the hidden input type a bit later. But first let's take a simpler case - the textarea input type:
</p>
<h4>Build a Dynamic Textarea Input Type</h4>
Textarea - Simple example
<code>
/* Outcome: the textarea box is repopulated with the original input */<br>
&lt;textarea name="query" cols="75" rows="5" wrap="soft"&gt;&lt;?php echo $query;?&gt;&lt;/textarea&gt;<br>
</code>
<p>This is one of my favorite uses of dynamic form controls. It just makes sense to automatically offer data that you will need, rather than re-enter it. If you have a long-winded sql statement that you will often need to retype then regenerating it with dynamic controls makes perfect sense. We can also use the 'if' decision structure to test if the user has chosen the functionality, in this case to 'reuse' the last query:
</p>
Textarea - example with Decision<br>
<code>
/* Outcome: the textarea box is repopulated with the original input - if chosen */<br>
&lt;textarea name="query" cols="75" rows="5" wrap="soft"&gt;&lt;?php if ($showLastQuery == "reuse") {echo $query;}?&gt;&lt;/textarea&gt;<br>
</code>
<p>The user can make a choice to 'show the last query' by using the radio input type:
</p>
<h4>Build a Dynamic Radio Input Type</h4>
<code>
/* Outcome: the radio input type chosen by the user remains checked */<br>
&lt;input type="radio" name="showLastQuery" value="reuse"<br>
&lt;?php if($showLastQuery == 'reuse'){echo " CHECKED";}?&gt;&gt; Reuse Query <br>
&lt;input type="radio" name="showLastQuery" value="blank"<br>
&lt;?php if($showLastQuery == 'blank'){echo " CHECKED";}?&gt;&gt; Blank <br>
</code>
<p>This code needs to make a decision in order to know if it should be ' CHECKED', or not. If no radio input type has been checked then there is no change to the ' CHECKED' indicator. Again, our code is simply maintaining the status quo for our form - we're wanting to display another form exactly like the one the user just filled out... and we can if we replicate each object with its correct value. And now on to checkboxes, which are just like radio input types, but with a little twist...
</p>
<h4>Build a Dynamic Checkbox Input Type</h4>
<code>
/* Outcome: the checkbox input type chosen by the user remains checked */<br>
&lt;input type="checkbox" name="showSummary"&lt;?php if($showSummary == "on"){echo " CHECKED";}?&gt;&gt; Summary<br>
</code>
<p>This example code uses a 'showSummary' object - but the named object could be any of your checkboxes too. In order to test for the existence of a choice in the checkbox we test for the named object's value, and if the value is set then indicate so in our code as above. To put this another way, we look to see if our checkbox variable is "on". If it is, we dynamically render this in the form checkbox object. Because each checkbox should have its own name and value then we can test for and recreate any number of additional checkboxes as needed. To use the code above all you need to do is replace:
1. the form object name with your own,
2. the text label for the object, in this case it is called 'Summary'. Use your own.
</p>
<p>Now that we can build single form controls, let's move on to the multi faceted select list:
</p>
<h4>Build a Dynamic Select List</h4>
<code>
/* Outcome: the select option chosen by the user remains selected */<br>
Category &lt;select name="snack"&gt;<br>
	&lt;option value="&lt;?php echo $snack;?&gt;" SELECTED&gt;&lt;?php echo $snack;?>&lt;/option&gt;<br>
	&lt;option value="1"&gt;Apples&lt;/option&gt;<br>
	&lt;option value="Oranges"&gt;Oranges&lt;/option&gt;<br>
	&lt;option value="Kiwis"&gt;Kiwis&lt;/option&gt;<br>
&lt;/select&gt;<br><br>
What it looks like:<br>
Category <select name="snack">
<option value="<?php echo $snack;?>" SELECTED><?php echo $snack;?></option>
<option value="1">Apples</option>
<option value="Oranges">Oranges</option>
<option value="Kiwis">Kiwis</option>
</select>
</code>
<p>
The distinguishing feature of this object is the use of the word ' SELECTED' which causes the option value associated with the label to be displayed to the user. Note that ' SELECTED' is a different word than ' CHECKED' - you need to use ' SELECT' with the select form object. While this code will return us the original form values and it is what we will use in our form, you should know that it also has unwanted side effects. One side effect is that NO text will show as the default value. It is nice to be able to see some choices. I haven't found a workable solution for this, other than using one form to add data with and another for updating the data. But it is really nice to just use the one form everywhere, including it where needed:
</p>
<code>
/* Outcome: myForm.php is parsed and inserted at the current page location */<br>
&lt;?php include("myForm.php");?&gt;<br>
</code>
<p>
The included file could be an 'Add User Data' form or perhaps a database search form. By making the form available again - retaining user set values - we make it easy for the user to make corrections or refine their search.
</p>
A Second Select Side Effect
<p>The second and not so obvious side effect concerns the selected object value. Look at the 'Apples' line. The value for this selection is actually "1". If you were to insert that value into a database and later retrieve it, then 'Apples' would NOT show as the selected value, instead the character "1" would display. Accordingly, we need to be careful in choosing the value so as to replicate or at least closely match the related label in order to maintain some semblance of interface continuity. Overall, using a dynamic select list means compromising 'perfect' functionality in order to achieve better efficiency in form design and usage - but still it's worth it.
</p>
<h4>Build a Dynamic Hidden Input Type</h4>
<p>Next we look at an input type with more obscure utility - the hidden input type:
</p>
Hidden
<code>
/* Outcome: the name=value pair is passed along to the next script, but may be seen with 'View Source' */<br>
&lt;input type="hidden" name="goal" value="&lt;?php echo $goal;?&gt;"&gt;<br>
</code>
<p>
I use $goal frequently in forms. It can act as the trigger in a switch() decision control construct, like this:
</p>
<code>
/* attain the goal - insert, update, delete, select, password lookup */<br>
switch ($goal) {<br>
  case "Add" // offer the insert form - user adds a new listing<br>
    	include("addForm.php");<br>
    break;<br>
}<br>
</code>
<p>
Thus we use a hidden variable which tells our processing script exactly what our goal is - and we could dynamically regenerate the hidden variable for use in the next page too. Sometimes I make this variable do double duty by using it as the page heading, which saves a bit of coding and correctly reports the purpose of the page.</p>
<p>
 The last singular input type we'll look at is the submit input type:
</p>
<h4>Build a Dynamic Submit Input Type</h4>
Submit - Simple<br>
<code>
/* Outcome: the submit button will display a variable as its value */<br>
&lt;input type="submit" name="submit" value="&lt;?php echo $goal;?&gt;"&gt;<br>
</code>
Submit - more than one variable used in label<br>
<code>
/* Outcome: the submit button will display more than one variable as its value */<br>
&lt;input type="submit" name="submit" value="&lt;?php echo"$goal #$diagramid - $buildingname";?&gt;"&gt;  <br>
</code>
<p>This submit button indicates its purpose to the user with $goal. We will know if it's a delete, update or other operation we're about to launch, because it's written right on the button! Furthermore, we reuse the database unique key and 'buildingname' to clearly establish the data we're working with. It's to the point. It lessens the chances of user error after too many cups of coffee and or too late in the morning...
</p>
<p>That pretty well arrives at the end of the standard form controls most used - but what about combination controls? What are they, how can they help us and what does their code look like?
</p>
<h4>Build a Combination Control</h4>
<code>
/* Outcome: the combo control will pass the embedded hidden value of a unique id */<br>
&lt;form name="Manage-Yellow-Listings" action="adminResult.php" method="post" target="_blank"&gt;<br>
&lt;input type="hidden" name="recordNumber" value="&lt;?php echo $recordNumber;?&gt;"&gt;<br>
<br>
&lt;?php // The formuser and formpassword objects help maintain admin security ?&gt;<br>
&lt;input type="hidden" name="formuser" value="&lt;?php echo $formuser;?&gt;"&gt;<br>
&lt;input type="hidden" name="formpassword" value="&lt;?php echo $formpassword;?&gt;"&gt;<br>
<b>Admin Goal</b>
&lt;input type="radio" name="goal" value="Delete"&gt;Delete <br>
&lt;input type="radio" name="goal" value="Update" CHECKED&gt;Update <br>
&lt;input type="submit" name="submit" value=" Process "&gt;<br>
&lt;/form&gt;<br><br>
It looks like this:
<table bgcolor="silver" border="3"><tr><td align="center">
<b>Admin Goal</b>
<input type="radio" name="goal" value="Delete">Delete
<input type="radio" name="goal" value="Update" CHECKED>Update
<input type="submit" name="submit" value=" Process ">
</td></tr></table>
</code>
<p>This simple piece of code is REALLY handy. It gives you point and click database administration by bringing in the record index number as a hidden variable and offering a choice of radio buttons to trigger either the update or the delete process. Essentially all you need to do is look at the data for the record, click on 'Process' or keep scrolling down to the next record, which contains a similar dynamic control. What could be easier for a database administrator?
</p>
<h4>Build a Javascript Back Control</h4>
<p>Our knowledge of building dynamic forms would not be complete without some mention of Javascript. Javascript, a language from the folks at Netscape - but also supported in Internet Explorer - gives us at least one useful control:
</p>
Back Button<br>
<code>
/* Outcome: makes a navigation control to go back, apparently faster than browser controls. */ <br>
&lt;input type="button" name="goBack" value="&lt;== Back" onclick="history.back(1)"&gt;<br>
</code>
<br>
<p>With this control you need to be aware that 'Back' means to the page last loaded in your browser, and not necessarily the logical previous page on the website. Care must be taken if using Javascript to build other controls because the Javascript language and its versions are unevenly supported in all browsers - or perhaps not supported at all. The Back history.location method was first introduced in Navigator 2 and Internet Explorer 3. If your users have one of those browsers or newer, then this control is fairly safe to use.
</p>
<h4>Looking at More Source Code</h4>
You can see most of these controls in live action at <a href="http//www.dreamriver.com/phpYellow/">http//www.dreamriver.com/phpYellow/</a> . You can also download the php source code for phpYellow and see how these controls all fit and flow together, as well as observing the password and username secured backend Administration pages and source code in the distribution files. The distribution files may be found at <a href="http//www.dreamriver.com/software/">http//www.dreamriver.com/software/</a> . Please note, the source code for phpYellow is not up for discussion here - there remains lots of room for improvement and there is another forum for that - rather it is the dynamic rendering of form objects described herein which I will be happy to answer your questions on at any time.
<h4>Build a Control - Summary</h4>
<p>We've looked at almost every html form object input type. We've shown sample code, with comments, detailing how the object behavior is dynamically rendered. We learned that it's really just name=value pairs, and that we use php as the provider of the value. Along the way we learned a few tricks and techniques in handling these controls. We even saw a useful combination control and got our first glimpse at Javascript enhanced controls. Overall, we now know how to dynamically script form objects in php by approaching them one object at at time. Building dynamic controls makes our forms smarter, improves the user surfing experience and can reduce the amount of time you spend developing static html forms. One dynamic form will often do the job much better!
</p>
		<p style="color:silver;">End of Document</p>
```

