[Back](Main.md)  

# FMTest API
All scripts begin with **FMT:** (colon)  
All Custom Functions begine with **FMT.** (period)

# Scripts
Scripts used in special situations to help display or save test data

## FMT:WriteOutputBuffers 
Writes the available testing output from $$FMT_Output and $$FMT_OutputSummary into the FMT::Output and FMT::Output_Summary global fields.  
Note: FMT::Output and FMT::Output_Summary must be on the layout and writable when this script is called  

**Parameters {empty}**

**Returns {JSONObject}**
* _success_ {JSONBoolean} true if the script has run successfully  
* _errorCode_ {JSONNumber} The FileMaker error if exists
* _errorMessage_ {JSONString} The message if exists



## FMT:Reset  
Resets all Global variables and fields used by FMTest  
   
**Parameters {empty}**  

**Returns {empty}**  


# Custom Functions
Custom Functions make up the 'testing' components. This allows you to write test scripts using as little or as much of FMTest's functions as you like.  


These Custom Functions update 3 main Global Variables as well as returning data.  

* _$$FMT_ {JSONObject} All data and test results are stored here in JSON format allowing for intergration with other platforms   
* _$$FMT_OutputBuffer_ {Text} Holds the Output text from FMT custom functions until the script FMT:WriteOutputBuffers is run  
* _$$FMT_OutputSummaryBuffer_ {Text} Holds the Output Summary text from FMT custom functions until the script FMT:WriteOutputBuffers is run  

For general use, you don't need to know about them. However the effects on each of these globals is discussed in the Custom Function descriptions below.

[More info about the $$FMT JSON structure etc in Under the Hood](UnderTheHood.md)

## FMT.Describe  
`FMT.Describe( testcase_description )`  

Place before a set of Assertions that make up a test case.  
This should be called before calling Assertions of the current test case  

**Paramaters**  
* _testcase_description_  {Text} Description of the test case you are testing

**Returns {JSONObject}**  
* _description_ {text} As passed into the function
* _assertions_ {JSONArray} Results of each Assertion following this Describe. Note: It is empty at this stage

**$$FMT**  
Adds the new test JSONObject to $$FMT.scripts[].tests[]

**$$FMT_OutputBuffer**   
Print the Description

**$$FMT_OutputSummaryBuffer**   
No change



## [FMT.Assert](#FMT.Assert)  
Each of the Assert custom functions below has the following:

**Parameters**  
* _describe_assertion_ {Text} Describe the thing you are asserting
* _value_ {Any} The actual value from your script or calculation
* _expected_value_ {Any} The expected value, or thing to find in thing such as the item  to find in a list
  
**Returns {JSONObject}**  
* _description_ {Text} As passed into the function
* _result_ {Boolean} The result of the test
* _failText_ {Text} Text indicating thing does not have the expected value

**$$FMT**  
Adds the new assertion JSONObject to $$FMT.scripts[].tests[].assertions[]

**$$FMT_OutputBuffer**   
Prints the resulting text from the test

**$$FMT_OutputSummaryBuffer**   
No change



## FMT.Assert.Equal  
`FMT.Assert.Equal ( describe_assertion ; value ; expected_value )`  

Test that thing = value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)


## FMT.Assert.NotEquals  
`FMT.Assert.NotEquals ( describe_assertion ; value ; expected_value )`  
Test that thing <> value  

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.GreaterThan  
`FMT.Assert.GreaterThan ( describe_assertion ; value ; expected_value )`  

Test that thing > value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.LessThan  
`FMT.Assert.LessThan ( describe_assertion ; value ; expected_value )`  
 
Test that thing < value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.Empty 
`FMT.Assert.Empty ( describe_assertion ; value )`  
 
Test that thing is empty

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.NotEmpty 
`FMT.Assert.NotEmpty ( describe_assertion ; value )`  

Test that thing is not empty

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.HasJSONKey 
`FMT.Assert.HasJSONKey ( describe_assertion ; json ; key )`  

Test that the JSONObject in thing has the expected Key (definied by value)

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.IsInList  
`FMT.Assert.IsInList ( describe_assertion ; list ; expected_value )`  
 
Test that value is in a FileMaker list
**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.NotIsInList  
`FMT.Assert.IsInList ( describe_assertion ; list ; expected_value )`  

Test that value is not in a FileMaker list

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)
  

# Initialisers and Concluders

## FMT.InitTestScript 
`FMT.InitTestScript ()`  

**Paramaters {empty}**  

**Returns {JSONObject}**  
* _scriptName_ {JSONObject} 
* _tests_ {JSONArray} An empty Array
* _result_ {Boolean} The overall result of the script (initially true) 
* _assertionCount_ {JSONNumber} The number of assertions made for this test script (initially 0)  
* _assertionPassCount_ {JSONNumber} The number of passes in this test script (initially 0)  
* _assertionfailCount_ {JSONNumber} The number of fails in this test script (initially 0)  

**$$FMT**  
Adds the test script details to $$FMT.scripts[]

**$$FMT_OutputBuffer**   
Prints the TestScript script name

**$$FMT_OutputSummaryBuffer**   
Prints the TestScript script name


## FMT.ConcludeTestScript 
`FMT.ConcludeTestScript ()`  

Test that value is not in a FileMaker list

**Paramaters {empty}**  

**Returns {JSONObject}**  
* _scriptName_ {JSONObject} 
* _assertions_ {JSONArray} Results for all test Scenerios per 'FMT.Describe' 
* _result_ {Boolean} The overall result of the script 
* _assertionCount_ {JSONNumber} The number of assertions made for this test script
* _assertionPassCount_ {JSONNumber} The number of passes in this test script
* _assertionFailCount_ {JSONNumber} The number of fails in this test script

**$$FMT**  
No change

**$$FMT_OutputBuffer**   
Prints the script summary

**$$FMT_OutputSummaryBuffer**   
Prints the script summary


## FMT.InitTestCase 
`FMT.InitTestCase ()`  

**Paramaters {empty}**  

**Returns {JSONObject}**  
The new $$FMT JSONObject

**$$FMT**  
Adds the testcase name

**$$FMT_OutputBuffer**   
Prints the TestCase script name

**$$FMT_OutputSummaryBuffer**   
Prints the TestCase script name

## FMT.ConcludeTestCase   
`FMT.ConcludeTestCase ()`  

Set a variable using this Custom Function after all Test Scripts have been run  

**Paramaters {empty}**  

**Returns {JSONObject}**  
The entire $$FMT JSONObject

**$$FMT**  
No change

**$$FMT_OutputBuffer**  
Prints conclusion info text

**$$FMT_OutputSummaryBuffer**  
Prints conclusion info text


# Helpers

## FMT.StartTimer  
`FMT.StartTimer ("MyTimer")`  

Starts a timer with the given name  

**Paramaters**  
* _identifier_ {text} The name of the timer. Default: The script name

**Returns {number}**  
The UTC milliseconds start time

**$$FMT**  
Adds 'identifierStartTime' to the current script JSONObject

**$$FMT_OutputBuffer**  
Prints "identfier: Timer Started"

**$$FMT_OutputSummaryBuffer**  
no change


## FMT.GetTimer  
`FMT.GetTimer ("MyTimer")`  

Get's the time in Milliseconds since the timer started   


**Paramaters**  
* _identifier_ {text} The name of the timer. Default: The script name

**Returns {number}**  
The milliseconds since the timer started

**$$FMT**  
Adds 'identifierEndTime' {JSONNumber} and 'identifierTotalTime' {JSONNumber} to the current script JSONObject    
If GetTimer is called more than once for the same identifier in the same test script it overwrites these values 

**$$FMT_OutputBuffer**  
Prints "identfier: xxxx ms"

**$$FMT_OutputSummaryBuffer**  
no change
