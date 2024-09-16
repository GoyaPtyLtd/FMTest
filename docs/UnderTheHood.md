[Back](Main.md)  

# Under the hood

For developers who want to intergrate FMTest with other systems.  



## Global Variables used by FMT  
### $$FMT {JSONObject}  
Contains the results and meta data used by FMTest  
```
  "testCaseName": {JSONString} The script name of the TESTCASE script
  "assertionCount": {JSONNumber} The total number of assertions made for the TESTCASE,
  "failCount": {JSONNumber} The total number of fails for the TESTCASE,
  "passCount": {JSONNumber} The total number of passes for the TESTCASE,
  "result": {JSONBoolean} The overall result of the TESTCASE,
  "resultText": {JSONString} The overall resulat as text for the TESTCASE,

  "scripts": []
      "scriptName": {JSONString} Name of the TESTSCRIPT
      "assertionCount": {JSONNumber} The number of assertions for this TESTSCRIPT,
      "assertionFailCount": {JSONNumber} The number of fails for this TESTSCRIPT,
      "assertionPassCount": {JSONNumber} The number of passes for this TESTSCRIPT,
      "result": {JSONBoolean} The overall result of this TESTSCRIPT,

      "tests": []
          "describe": {JSONString} The Describe text of the TEST,
          "assertionCount": {JSONNumber} The number of assertions for this TEST,
          "assertionFailCount": {JSONNumber} The number of fai;s for this TEST,
          "assertionPassCount": {JSONNumber} The number of passes for this TEST,
          "result": {JSONBoolean} The overall result of this TEST,

          "assertions": []
              "it": {JSONString} The should text of the assertion,
              "failText": {JSONString} The fail text of the assertion,
              "result": {JSONBoolean} The assertion result
```

### $$FMT_OutputBuffer {text}  
Holds the Output text from FMT custom functions until the script FMT:WriteOutputBuffers is run  

### $$FMT_SummaryOutputBuffer {text}  
Holds the Summary Output text from FMT custom functions until the script FMT:WriteOutputBuffers is run 