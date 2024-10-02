[Back](Main.md)  


# Install
[Download FMTest here](https://github.com/GoyaPtyLtd/FMTest/releases)

https://github.com/GoyaPtyLtd/FMTest/releases
# Getting Started  

# Examples

## Testing Custom Functions
```
Set Variable [ $init ; FMT.InitTestScript ]


# Run the custom function and test as often as needed
Set Variable [ $test ; [
  FMT.Describe ( "Check MyCustomFunction with Numbers" ) &
  FMT.Assert.GreaterThan (  "Result of 300"; MyCustomFunction( 300 ) ; 200 )
  FMT.Assert.LessThan (  "Result of 10"; "MyCustomFunction( 10 ) ; 200 )
]]

Set Variable [ $test ; [
  FMT.Describe ( "Check MyCustomFunction with text" ) &
  FMT.Assert.Equal ( "Result of 'Hi'"; MyCustomFunction( "Hi" ) ; "Hello" )
]]

Set Variable [ $conclude ; FMT.ConcludeTestScript ]
Perform Script [ FMT:WriteOutputBuffers ]
```

## Testing Calculations
```
Set Variable [ $init ; FMT.InitTestScript ()]

# Set the data for the test
Set Field [ MyTable::Field1; 100 ]
Set Field [ MyTable::Field2; 300 ]

Set Variable [$isField3Hidden; GetLayoutObjectAttribute( "MyField3"; "isObjectHidden")]

# Check the results
Set Variable [ $test ; [
  FMT.Describe ( "Check calcs" ) &
  FMT.Assert.Equal ( "Field3 Hidden"; $isField3Hidden ; false ) &
  FMT.Assert.LessThan ( "Field4 Calc"; MyTable::Field4_c ; 250 )
]]

# ### Repeat data setup with different data then checking results as often as needed ### #

Set Variable [ $conclude ; FMT.ConcludeTestScript ]
Perform Script [ FMT:WriteOutputBuffers ]
```
There are lots of places where calculations can exist, but can't be tested.  
Layout Calculations, Tooltip, Security Rules etc etc. 
I suggest placeing any complex scripts as either Custom Functions or Field Calculations.  


## Testing Scripts
```
Set Variable [ $init ; FMT.InitTestScript ]

# Set the data for the test
Set Field [ MyTable::Field1; "Hi" ]
Set Field [ MyTable::Field2; 300 ]

# Perform the script you want to test
Perform Script [ "TheScriptToTest" ]

# Check the results
Set Variable [ $test ; [
  FMT.Describe ( "Check output fields" ) &
  FMT.Assert.Equals ( "MyResult1"; MyTable::MyResult1 ; "Hello" ) &
  FMT.Assert.GreaterThan ( "MyResult2"; MyTable::MyResult2 ; 200 ) &
  FMT.Assert.HasJSONKey ( "MyJSON_Field"; MyTable::AsJSON ; "ID" )
]]

# ### Repeat data setup with different data, performing the script and check results as often as needed ### #

Set Variable [ $conclude ; FMT.ConcludetestScript ]
Perform Script [ FMT:WriteOutputBuffers ]
```

You can have more than one _TEST_ in a single script. Use FMT.Describe to sart a new _TEST_
Simply repeat setting up your data, performing the test script and testing the results as often as you like.
If you want to watch the test results populate in the global field you can call FMT:WriteOutputBuffers as after each test (note: It takes time to refesh the screen, so use sparingly if you have a lot of tests)


## FMTest's (opinionated) Testing Structure  
TESTSUITE has 1 or many TESTSSCRIPTS  
TESTSCRIPT has 1 or many TESTCASES  
TESTCASE has 1 or many ASSERTIONS  
