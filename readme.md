# Java Live Templates for IntelliJ

## What is a LiveTemplate:
A LiveTemplate is a little code snippet that is generate when a pre-defined abbreviation for the snippet is typed.

For example if you were using the templates in this repo and you wanted to log something at info level in a Java class file type `lgi` then press `tab` this will expand to `LOGGER.info(String.format(""));`.

For more information on LiveTemplates see: [Live Templates](https://www.jetbrains.com/idea/webhelp/live-templates.html)

## How to:

1. Download and copy the *xml* file(s) to your templates folder:

 * Windows: `<your home directory>\.<product name><version number>\config\templates`
 * Linux: `~\.<product name><version number>\config\templates`
 * OS X: `~/Library/Preferences/<product name><version number>/templates`

  e.g. `~/Library/Preferences/IntelliJIdea12/templates` on OS X for IntelliJ 12.

2. Restart IntelliJ.
3. To see all templates, go to *Preferences->Live Templates* and expand the Template Group.

To see templates available for a context type `Cmd + J` on Mac OS X or `Ctrl + J` in Windows/Linux.


## LiveTemplate Usage
To use a LiveTemplate, you type the abbreviation for a template then press tab.

Alternatively if you do not remember the shortcut for a template press:
- Windows/Linux: `Ctrl + J`
- Mac OS X: `Cmd + J`

Or for a surround template (a template that uses selected code inside of it) highlight the item you want to insert a template for and press:
- Windows/Linux: `Ctrl + Alt + J`
- Mac: `Cmd + alt + J`

This will result in a list of applicable templates showing up where you can start typing to filter down to the template you want. Select the item you want and press enter.

## Available Custom LiveTemplates
###Traceability

|#|  Abbreviation  | Template
|-|-------------- |---------------
|1| lg            | Declare the logger and initialise it in a static block using the current class name.
|2|  lgd           | Log at the debug level: `LOGGER.debug("");`
|3|  lge           | Log at the error level: `LOGGER.error("");`
|4|  lgi           | Log at the info level: `LOGGER.info("");`
|5|  lgt           | Log at the trace level: `LOGGER.trace("");`

###Testing

|#|  Abbreviation  | Template
|-|-------------- |---------------
|1 | ase | Assert Equals:  `Assert.assertEquals(String.format(""),,);`
|2| asf | Assert false: ` Assert.assertFalse(String.format(""),);`
|3 | asn | Assert null: `Assert.assertNull(String.format(""),);`
|4| asnn | Assert not null: `Assert.assertNotNull(String.format(""),);`
|5 | ast |Assert true: `Assert.assertTrue(String.format(""),);`
|6| eme | Generates the .reset ; .expect ; .replay and .verify for the selected service being mocked.
|7 | junit | Creates the Spring JUnit annotation. Should be run at the top of a test class to ensure it is generated in the correct place.

###Utility
|#|  Abbreviation  | Template
|-|-------------- |---------------
|1| sf | Generates: `String.format("")`. Semicolon intentionally left out so this can be used inside other methods and not just to define a variable.


## Tips and Tricks
If you want to create your own LiveTemplates here are some tips and tricks to get you started:

### 1. Fully Qualified Classname
Use the fully qualified class name when referencing a class instance variable for example instead of

```java
Assert.assertTrue("Somebool should be true", someBool);
```
use

```java
org.junit.Assert.assertTrue("Somebool should be true", someBool);
```
Doing it this way means when using the template you will not have to keep telling IntelliJ what package the object belongs to (IntelliJ will automatically remove the fully qualified name and include it as an import if there is no other object in the given file that has the same class name).

### 2. Custom templates in new groups
- Always add new/custom LiveTemplates to their own group as apposed to the default groups IntelliJ provides.
- This allows people to clone your LiveTemplate repo into their templates folder and not overwrite their existing templates (if you use the same group name it will be placed in a file with that name which will overwrite their existing file when they clone your repo).
- Creating new LiveTemplate groups in IntelliJ is not too intuitive. To do this create your new template in any group, then right click on the template and choose `move to group` then select `new group` and give it a name. Going forward you can create new templates in this new group.

### 3. Easily Create LiveTemplates
To create a LiveTemplate:
1. Select the code fragment you want to turn in to a LiveTemplate
2. Go to the `Tools` menu and click `Save as LiveTemplate `
3. The LiveTemplate creation modal should appear
4. Input the abbreviation you want
5. Configure any variables (if any)  and you're done

### 4. $END$ Builtin Template Variable
This is one of 2 built-in variables (the other will be described below).

This is used to specify where the cursor will be positioned after the template has executed.

For example if you have the template with keyword `sf` configured as
```java
String.format("$END$");
```
then  the cursor will appear between the quotes after executing the LiveTemplate.

### 5. $SELECTION$ Builtin Template Variable
This built-in variable is used to create a surround template. It basically lets the user select text then choose the surround template they want which gets the template wrapped around it.

For example the EasyMock template described above is defined as follows:
```java
org.easymock.EasyMock.reset($SELECTION$);
org.easymock.EasyMock.expect($SELECTION$.$END$).andReturn(/*TODO*/);
org.easymock.EasyMock.replay($SELECTION$);
org.easymock.EasyMock.verify($SELECTION$); //TODO move this to where it is appropriate
```
This allows the user for example to highlight ```myAwesomeService``` then choose ```eme``` from the surround templates which results in the below being generated (cursor will be place before ```).andReturn(```):
```java
org.easymock.EasyMock.reset(myAwesomeService);
org.easymock.EasyMock.expect(myAwesomeService.).andReturn(/*TODO*/);
org.easymock.EasyMock.replay(myAwesomeService);
org.easymock.EasyMock.verify(myAwesomeService); //TODO move this to where it is appropriate
```

## How to Contribute
Fork, update and submit pull requests.
