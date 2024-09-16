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


## FMT.DescribeTest  
`FMT.DescribeTest( describe )`  

Place before a set of Assertions that make up a test scenrio.  
This should be called before calling Assertions of the current test scenerio  

**Paramaters**  
* _describe_  {Text} Description of the scenrio you are testing

**Returns {JSONObject}**  
* _describe_ {text} As passed into the function
* _results_ {JSONArray} Results of each Assertion following this Describe. Note: It is empty at this stage

**$$FMT**  
Adds a new result object to $$FMT.scripts[].tests[]

**$$FMT_OutputBuffer**   
Adds the Description name

**$$FMT_OutputSummaryBuffer**   
No change



## [FMT.Assert](#FMT.Assert)  
Each of the Assert custom functions below has the following:

**Parameters**  
* _describe_ {Text} As passed into the function
* _thing_ {Any} The variable or function to test
* _value_ {Any} The expected value, or thing to find in thing (depending on the assertion)
  
**Returns {JSONObject}**  
* _describe_ {Text} As passed into the function
* _result_ {Boolean} The result of the test
* _errorText_ {Text} Text indicating thing does not have the expected value

**$$FMT**  
Adds a new result object to $$FMT.Scripts[].results[].results[]

**$$FMT_OutputBuffer**   
Adds the resulting text from the test

**$$FMT_OutputSummaryBuffer**   
No change



## FMT.Assert.Equals  
`FMT.Assert.Equals ( describe_thing ; thing ; value )`  

Test that thing = value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)


## FMT.Assert.NotEquals  
`FMT.Assert.NotEquals ( describe_thing ; thing ; value )`  
Test that thing <> value  

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.GreaterThan  
`FMT.Assert.GreaterThan ( describe_thing ; thing ; value )`  

Test that thing > value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.LessThan  
`FMT.Assert.LessThan ( describe_thing ; thing ; value )`  
 
Test that thing < value

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.Empty 
`FMT.Assert.Empty ( describe_thing ; thing )`  
 
Test that thing is empty

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.NotEmpty 
`FMT.Assert.NotEmpty ( describe_thing ; thing )`  

Test that thing is not empty

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.HasJSONKey 
`FMT.Assert.HasJSONKey ( describe_thing ; thing ; value )`  

Test that the JSONObject in thing has the expected Key (definied by value)

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.IsInList  
`FMT.Assert.IsInList ( describe_thing ; thing ; value )`  
 
Test that value is in a FileMaker list
**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)

## FMT.Assert.NotIsInList  
`FMT.Assert.IsInList ( describe_thing ; thing ; value )`  

Test that value is not in a FileMaker list

**Parameters, Return and and Effects**   
[Assert Parameters, Returns and Effects](#FMT.Assert)
  

## Initialisers and Concluders

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
Adds the test script details to $$FMT.Scripts[]

**$$FMT_OutputBuffer**   
Adds the TestScript script name

**$$FMT_OutputSummaryBuffer**   
Adds the TestScript script name


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
Adds the script summary

**$$FMT_OutputSummaryBuffer**   
Adds the script summary


## FMT.InitTestCase 
`FMT.InitTestCase ()`  

**Paramaters {empty}**  

**Returns {JSONObject}**  
The new $$FMT JSONObject

**$$FMT**  
Adds the testcase name

**$$FMT_OutputBuffer**   
Adds the TestCase script name

**$$FMT_OutputSummaryBuffer**   
Adds the TestCase script name

## FMT.ConcludeTestCase   
`FMT.ConcludeTestCase ()`  

Set a variable using this Custom Function after all Test Scripts have been run  

**Paramaters {empty}**  

**Returns {JSONObject}**  
The entire $$FMT JSONObject

**$$FMT**  
No change

**$$FMT_OutputBuffer**  
Adds conclusion info text

**$$FMT_OutputSummaryBuffer**  
Adds conclusion info text


# Helpers

## FMT.StartTimer  
`FMT.StartTimer ("MyTimer")`  

Starts a timer with the given name  

**Paramaters**  
* _identifier_ {text} The name of the timer

**Returns {number}**  
The UTC milliseconds start time

**$$FMT**  
Adds 'identifierStartTime' to the current script

**$$FMT_OutputBuffer**  
Adds "identfier: Timer Started"

**$$FMT_OutputSummaryBuffer**  
no change


## FMT.GetTimer  
`FMT.GetTimer ("MyTimer")`  

Get's the time in Milliseconds since the timer started   


**Paramaters**  
* _identifier_ {text} The name of the timer

**Returns {number}**  
The milliseconds since the timer started

**$$FMT**  
Adds 'identifierEndTime' {JSONNumber} and 'identifierTotalTime' {JSONNumber} to the current script  
If GetTimer is called more than once for the same identifier, it overwrites these values. 

**$$FMT_OutputBuffer**  
Adds "identfier: xxxx ms"

**$$FMT_OutputSummaryBuffer**  
no change