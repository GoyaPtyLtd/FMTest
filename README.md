# FMTest

_FileMaker 2024/21 is required as FMTest uses the new JSONArray functions!_

FMTest is a collection of Custom Functions and Scripts to assist you in testing your calculations and scripts with a minimal reliance on structure. At the smallest you can simply write a script like this:
```
Set Variable [ $myvariable ; A_Calc_Or_ScriptResult_ToTest ]
Set Variable [ $assert ; FMT.Assert.Equals ("My Variable"; $myvariable ; 1 )]
Perform Script [ FMT.WriteOutputBuffers ]
```
Which results in the global output displaying
```
My Variable should equal 1 PASS
```

There are also initialisers and concluders that help get more information
```
Set Variable [ $init ; FMT.InitTestScript ]

Set Variable [ $describe ; FMT.Describe ( "My TestCase" )]
Set Variable [ $myvariable ; A_Calc_Or_ScriptResult_ToTest ]
Set Variable [ $assert ; FMT.Assert.Equals ("My Variable"; $myvariable ; 1 )]

Set Variable [ $conclude ; FMT.ConcludetestScript ]
Perform Script [ FMT.WriteOutputBuffers ]
```
Which results in the global output displaying
```
My TestScript

 My TestCase
  My Variable should equal 1 PASS

My TestScript complete
Of 1 Assertions, ALL PASSED
```

**[FOR MORE INFORMATION - SEE THE DOCS](docs/Main.md)**  

### Integration with other services and/or logging test results  
FMTest is built small by design so you're free to work with it however you'd like.
All test results are logged in the global JSONObject $$FMT that can be used to store in a FileMaker table or integrate with other services.  

For more info on how to integrate FMTest see the [docs](docs/Main.md).
