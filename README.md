# FMTest

FMTest is a collection of Custom Funstions and Scripts to assist you in testing your calcultaions and scripts with a minimal reliance on building test scripts in a certain way.
At the smallest you can simply wite a script like this
```
Set Variable [ $assert ; FMT.Assert.Equals ("My Variable"; $myvriable ; 1 )]
Perform Script [ FMT.WriteOutputBuffers ]
```
Which results in the global output displaying
```
My Variable should equal 1 PASS
```

There are also initialisers and concluders that help get more information
```
Set Variable [ $init ; FMT.InitTestScript ()]
Set Variable [ $describe ; FMT.Describe ( "My test scenario" )]
Set Variable [ $assert ; FMT.Assert.Equals ("My Variable"; $myvar ; 1 )]
Set Variable [ $conclude ; FMT.ConcludetestScript ()]
Perform Script [ FMT.WriteOutputBuffers ]
```
Which results in the global output displaying
```
My TestScript

 My test scenario
  My Variable should equal 1 PASS

My TestSuite Script complete
Of 1 Assertions, ALL PASSED
```

# FMTest will be released as an add-on soon
