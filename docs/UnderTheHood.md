[Back](Main.md)  

# Under the hood

For developers who want to intergrate FMTest with other systems.  



# Global Variables used by FMT  
### $$FMT {JSONObject}  
Contains the results and meta data used by FMTest  
```
  "testCaseName": {JSONString} The script name of the TESTSUITE script
  "assertionCount": {JSONNumber} The total number of assertions made for the TESTSUITE,
  "assertionFailCount": {JSONNumber} The total number of fails for the TESTSUITE,
  "assertionPassCount": {JSONNumber} The total number of passes for the TESTSUITE,
  "result": {JSONBoolean} The overall result of the TESTSUITE,
  "resultText": {JSONString} The overall result as text for the TESTSUITE,

  "scripts": []
      "scriptName": {JSONString} Name of the TESTSCRIPT
      "assertionCount": {JSONNumber} The number of assertions for this TESTSCRIPT,
      "assertionFailCount": {JSONNumber} The number of fails for this TESTSCRIPT,
      "assertionPassCount": {JSONNumber} The number of passes for this TESTSCRIPT,
      "result": {JSONBoolean} The overall result of this TESTSCRIPT,

      "tests": []
          "description": {JSONString} The Describe text of the TESTCASE,
          "assertionCount": {JSONNumber} The number of assertions for this TESTCASE,
          "assertionFailCount": {JSONNumber} The number of fails for this TESTCASE,
          "assertionPassCount": {JSONNumber} The number of passes for this TESTCASE,
          "result": {JSONBoolean} The overall result of this TESTCASE,

          "assertions": []
              "description": {JSONString} The thing you are testing in words,
              "failText": {JSONString} The fail text of the assertion,
              "result": {JSONBoolean} The assertion result
```

### $$FMT_OutputBuffer {text}  
Holds the Output text from FMT custom functions until the script FMT:WriteOutputBuffers is run  

### $$FMT_SummaryOutputBuffer {text}  
Holds the Summary Output text from FMT custom functions until the script FMT:WriteOutputBuffers is run 

# Access the outputs  
2 global fields hold the output data that we see.

**FMT::Output** This is the field we see when running tests

**FMT::SummaryOutput** Contains just the Init and Conclude text output. Great for displaying in external services.

Once the tests are complete you can do whatever you like with these.
Some examples would be: 
 * returning FMT::SummaryOutput to Slack when tests are run from a slask command
 * Use GetAsCSS(FMT::Output) and sftp the results to a web server for easy access to the result.
 * Use FMT::SummaryOutput for a local notification
 * Store FMT::Output in a FileMaker table
 * etc etc etc
  

