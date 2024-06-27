## <a name="_y3fwxd6c6re"></a>**Report for Assignment 1**
**Project chosen**

**Name**: Kinto.js

**URL**: <https://github.com/Kinto/kinto.js?tab=readme-ov-file>

**Number of lines of code**: 16 882

**The tool used to count the lines of code:** Lizard

![image](https://github.com/KortsH/kinto.js/assets/156069447/95d090fe-bfb4-4899-bc8b-718ca6668464)

**Programming language**: TypeScript

## <a name="_7sgym325bj2t"></a>**Coverage measurement**

**Existing tool:** Npm test

**Documentation: <https://kintojs.readthedocs.io/en/latest/contributing/>**

**How to run:** Using the documentation stated above, after setting up the virtual environment and activating bin, we used npm test cover to obtain the coverage of kinto.js. The commands are stated below:

git clone https://github.com/KortsH/kinto.js.git

cd kinto.js

npm install

python3 -m venv venv

source venv/bin/activate

./venv/bin/pip install kinto

npm install intern --save-dev

source ./venv/bin/activate

pip install kinto\_attachment

npm run test-cover

![image](https://github.com/KortsH/kinto.js/assets/156069447/58476fae-7f25-4cc1-a401-b7b574feb9d0)


**Our coverage tool**

For writing our own coverage tool, we ran into some issues. We presented this to our TA during the Q&A session and provided a possible solution, which they liked and gave us the green light to go ahead, should the professor also confirm this. This meant that we still followed all of the steps for making our own branch coverage tool, with around 50 unique branch IDs (even in files with a 100% branch coverage). 

The TA in the first Q&A session told us to contact the professor via email, to whom we sent three emails with no answer and when asked about it during the second Q&A session, she said to contact her via Canvas instead. After doing that she did not reply but had some TAs reply with one possible solution, which we already had tried. 

We continued work with the solution that we presented to the TA but we did manage to find a solution to our issues. This meant that our branch coverage tool after running the test gave us these results:

In the collection.ts file:
{

unKnownType: 2,

knownType: 2949,

arrayHasEntires: 906,

arrayHasNoEntires: 2043,

isCached: 211,

isNotCached: 1897,

noRecordId: 39,

recordId: 630,

captureStackTrace: 2,

noCaptureStackTrace: 0,

baseAdapter: 1566,

notBaseAdapter: 2,

idSchemaUndefined: 1537,

idSchemaDefined: 29,

idSchemaNotObject: 2,

idSchemaGenerateUndefined: 2,

idSchemaValidateUndefined: 2,

idSchemaValidated: 23,

remoteTransformersUndefined: 1286,

remoteTransformersNotArray: 2,

remoteTransformersArray: 272,

remoteTransformersNotObject: 2,

remoteTransformersEncodeUndefined: 2,

remoteTransformersDecodeUndefined: 2,

remoteTransformersValidated: 273,

hookNotArray: 2,

hookArray: 16,

notDeletedIdenticalOrLastModified: 80,

deletedUnsynced: 38,

notSynced: 126,

identical: 4,

lastModified: 4,

deleted: 2,

notDeleted: 6,

synced: 105,

syncedIdentical: 26,

syncedNotIdentical: 44,

importChange: 44,

notLocal: 653,

remoteDeleted: 73,

notRemoteDeleted: 685,

pullOnly: 8,

notPullOnly: 231,

isLocal: 239

}



In the KintoBase.ts file:
{

apiAccessed: 287,

apiDoesntExist: 1,

apiAccessedDontCreateNew: 3295,

apiDoesntExistCreateNew: 251,

collectionNameMissing: 1,

collectionNameProvided: 542

}


In the index.ts file:
{

constructorDefaults: 6,

constructorOptions: 280,

adaptersAccessed: 542,

apiClassAccessed: 251

}


This would’ve given us only one branch that was not covered by the tests and because the project has a 96% test coverage rate we decided to mainly focus on their own tool to find the lines and branches, where we could improve their tests.

This tool can be found on the branch of unique-IDs-and-branching. To use this tool, run the tests (coverage tests work too) and find the last print statements of the specific file coverage data in the terminal (due to the nature of TypeScript we can’t use console.log this once at the end of the file but rather have to print them many times). 

## <a name="_im5dkci1h08j"></a>**Coverage improvement (Individual tests)**
## <a name="_q5hos6871h20"></a>**Aaron Serpilin**
### <a name="_1duhgquarx6q"></a>**Test for batch.ts, line 72 and additional extra test**

**Commit SHA:** 40e665218583dc851242934953f86daff97443ab

**Link:** <https://github.com/KortsH/kinto.js/commit/40e665218583dc851242934953f86daff97443ab>

Coverage before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/10e7702c-66df-40a3-9b58-49330da7d0da)

Coverage after:

![image](https://github.com/KortsH/kinto.js/assets/156069447/0899731b-f9a9-46c2-94c0-5ac73b4f6446)

![image](https://github.com/KortsH/kinto.js/assets/156069447/96c88b02-8840-4f2c-b7f6-5bade1eec269)

**In the batch.ts tests we had the following improvements:**

Statements coverage improvement: 100% to 100%

Branches coverage improvement: 84.21% to 89.47%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 100% to 100%

**The tests were implemented for the following methods and properties:**

- Matching Responses and Requests Length: Ensuring the function throws an error if the lengths don't match.
- Handling HTTP 500 Errors: Adding responses to the errors list.
- Handling HTTP 200<=x<400 Responses: Adding responses to the published list.
- Handling HTTP 404 Responses: Adding responses to the skipped list with and without matching regex.
- Handling HTTP 412 Responses: Adding responses to the conflicts list.

#### <a name="_egcs2uvfz00s"></a>**What was improved? How was it tested?**

All enhancements for this branch were done on the batch-testing-branch. It initially had 1448 passing tests, and following the addition of the two test cases increased coverage of line 72, and increased the passing tests to 1450. 

![image](https://github.com/KortsH/kinto.js/assets/156069447/48421a00-c3f2-4472-96ec-bc773dcd04eb)

The aggregate function which includes line 72 of batch.ts is placed beneath for reference:

![image](https://github.com/KortsH/kinto.js/assets/156069447/0e3f036a-61c6-4587-82b1-a5ff25818d8f)

The aggregate function here is in charge of categorizing the batch requests based on their server responses. When categorizing them, there are 4 main groups. The first, if the error status is between 200 and 399, the requests are pushed into the published array. Second, if it is 404, it is it pushed into the skipped list. Third, if it is 412 it is pushed into the conflicts list, and finally if the error status is anything else, it is pushed into the errors array. Diving into the test itself, the test creates a request with a path that does not match the expected regex pattern and a corresponding response with a 404 status code. Following this, we call the aggregate function with this request and response, after which the test checks that the skipped array in the result contains an entry with an undefined ID, as the path does not match the regex. The test ensures that the code handling the 404 responses to the skipped array is executed by checking if the regex fails to match the request path, leading to an undefined ID.

In addition to this, although the number of covered lines did not increase, the following test case was added to deal with server errors (such as status code 500). This led the number of passed tests to increase to 1450. 

Here is the corresponding test case:

![image](https://github.com/KortsH/kinto.js/assets/156069447/0f7d9ba1-275e-47d3-8534-c26b971d5937)

The reason why this function correctly deals with the server status errors is because there is no other test case that deals with these errors. The rest of the framework focuses on errors ranging between 200s and 400s, and when multiple 500s errors occur simultaneously yet not individually. Hence, adding a check for an individual 500 status code allows it to tackle more tests. Essentially, this test performs the same operations as the previous tests for 404 status codes, by creating a request and response and with a status code of 500. Following this, it invokes the aggregate function as well and then looks for the corresponding regex regarding the status code. 

### <a name="_virc8emxxtc7"></a>**Test for requests.ts, lines 103-109 and 169**
**Commit SHA:** 5577ef177aa72932775a31e6adc3f4acfd5f6c68

**Link:** <https://github.com/KortsH/kinto.js/commit/5577ef177aa72932775a31e6adc3f4acfd5f6c68>

**Commit SHA**: 5577ef177aa72932775a31e6adc3f4acfd5f6c68

**Link**: <https://github.com/KortsH/kinto.js/commit/b6d893e859160f98deca08c3258c4f46e1cb60b9>

Coverage Before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/ad1cc9cb-759d-412a-b779-39e8a97c5b57)

Coverage After:

![image](https://github.com/KortsH/kinto.js/assets/156069447/9a2bd2f4-c17e-43ea-b4eb-06797dd6b3ba)

**In the requests.ts tests we had the following improvements:**

Statements coverage improvement: 100% to 100%

Branches coverage improvement: 90.9% to 96.96%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 100% to 100%

**The tests were implemented for the following methods and properties:**

- createRequest
- deleteRequest
- updateRequest
- jsonPatchPermissionsRequest
- addAttachmentRequest

These tests covered handling headers, safe options, permissions, patch options, and gzipped options.

#### <a name="_a4wjssygcz58"></a>**What was improved? How was it tested?**

In the same fashion as the previous tests, the improvements for requests.ts was done on a separate branch from the default master branch. Hence, its starting coverage point was the original 1448 passing tests again, with lines 103-110 and 169 of said file not being covered. Following the addition of the two test cases, lines 103-109 and line 169 gained coverage, with only line 110 not gaining coverage. Here is the corresponding coverage analysis where two additional tests were passed and 8 additional lines gained coverage in the requests.ts file:

The corresponding functions are the ones below:

![image](https://github.com/KortsH/kinto.js/assets/156069447/7ccf9b46-2810-47ee-a55e-4267af426358)

![image](https://github.com/KortsH/kinto.js/assets/156069447/acdddcf6-7f18-497f-b0d5-be3fb4f917d5)

For reference, lines 103-110 and line 169 are included beneath from the requests.ts file:

![image](https://github.com/KortsH/kinto.js/assets/156069447/0eac6ad0-eb24-41ca-aa65-9919aabd614f)

![image](https://github.com/KortsH/kinto.js/assets/156069447/752c8e3b-e0d3-4e32-8b36-14e025a45386)

Out of the two test cases, the test case for line 169 is a lot more simpler. When analyzing line 169, its functionality comes down to correctly appending to the custom request path the result of the ternary operator. Therefore, this functionality can be easily tested by adding a test case checking if the result of the ternary operator is correctly added to the path. In our test, we used an edge value (null) and checked if nothing is added. 

Diving into lines 103-109, within the jsonPatchPermissionsRequest function, these lines are in charge of iterating over the permissions object and then creating JSON Patch operations. Hence, in order to increase coverage of these lines one must create an object and verify if the JSON operations are included in the request body. Given this, the test case firstly makes a `permissions` object that has the read and write functions (the info inside the principal is arbitrary - hence I just added my name). After defining the permissions’ principal, we use it to make the corresponding JSON request. Following this, the final step is to merely assert if the entries match those placed in the request. Hence, by then activating the loop due to the presence of 1 principal, this test correctly ensures that the creation of the JSON Patch operations correctly use the provided permissions.
## <a name="_isiodwxicptw"></a>**Henri Korts**
### <a name="_i9ya4kulf0fc"></a>**Test for KintoBase.ts, line 103**

**Commit SHA:** 3992f912f6b4c3be6a4c51ad9d723761a5d35f8b

**Link**: <https://github.com/KortsH/kinto.js/commit/3992f912f6b4c3be6a4c51ad9d723761a5d35f8b>

Coverage before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/b41b0ef7-99f9-4a0a-b1ef-187050d23b34)

Coverage after:

![image](https://github.com/KortsH/kinto.js/assets/156069447/7128ce25-a23f-45d4-8b75-0b91b428932d)

**In the KintoBase.ts tests we had the following improvements:**

Statements coverage improvement: 95.53% to 100%

Branches coverage improvement: 100% to 100%

Functions coverage improvement: 83.33 % to 100%

Lines coverage improvement: 95.83% to 100%

**The tests were implemented for the following methods and properties:**

- The static adapters property of the *KintoBase* class.
- The *localFields* property of a collection instance.
- The *ApiClass* getter method of the *KintoBase* class.
#### <a name="_c5dmy2sm494c"></a>**What was improved?**
The improvements focus on verifying correct functionality and enforcing expected behaviours in the *KintoBase* class:

- Ensured that the static adapters property returns the correct adapters.
- Verified that the *localFields* property contains the appropriate local fields.
- Enforced that the *ApiClass* getter method throws an error if it is not implemented by a subclass, ensuring proper subclass implementation and adherence to the class design.
#### <a name="_wbi0nzj7eoim"></a>**How was it tested?**
The testing approach included the following steps:

- **Static Properties:**
  - Checked the value returned by the adapters static property to ensure it is as expected.
  - Verified that the *localFields* property of a collection instance includes specific local fields.
- **ApiClass Getter:**
  - Created a subclass of *KintoBase* that does not implement the *ApiClass* method.
  - Initialized an instance of this subclass before each test with necessary configurations like an adapter and event emitter.
  - Tested that accessing the *api* property on this instance throws an error with a specific message, confirming that subclasses must implement the *ApiClass* method.
### <a name="_lu18z5d18o90"></a>**Test for Utils.ts, Lines 150 and 249**

**Commit SHA:** 3f720b82b4edaa9363ce1d2ec87ffce5a76f0abd

**Link:** <https://github.com/KortsH/kinto.js/commit/3f720b82b4edaa9363ce1d2ec87ffce5a76f0abd>

Coverage before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/be140ac6-b98d-460d-a6d9-6a610ca31a55)

Coverage after:

![image](https://github.com/KortsH/kinto.js/assets/156069447/ae208a18-0169-40bf-845a-0bed5b9162f3)

**In the utils.ts tests we had the following improvements:**

Statements coverage improvement: 99.04% to 100%

Branches coverage improvement: 97.08% to 99.2%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 99% to 100%

**The tests were implemented for the following methods:**

- arrayEqual
- toDataBody
#### <a name="_7n28uchwcqfx"></a>**What was improved?**
The improvements focus on validating the correct functionality of the *arrayEqual* and *toDataBody* utility functions:

- Ensured that the *arrayEqual* function correctly determines whether two arrays are equal, considering various cases such as different lengths, different elements, and empty arrays.
- Verified that the *toDataBody* function correctly converts a resource into a data body format, handling both object and string inputs appropriately and throwing errors for invalid arguments.
#### <a name="_eu6pchahlq06"></a>**How was it tested?**
The testing approach included the following steps:

- **arrayEqual Function:**
  - Tested that the function returns false when the input arrays have different lengths.
  - Checked that the function returns false when arrays have the same length but different elements.
  - Confirmed that the function returns true when the arrays are identical.
  - Verified that the function returns true for two empty arrays.
- **toDataBody Function:**
  - Tested that the function returns the same object if the input resource is already an object.
  - Checked that the function returns an object with an id property if the input resource is a string.
  - Verified that the function throws an error with a specific message when the input is an invalid argument (e.g., a number or undefined).

## <a name="_twqz9fdl2w10"></a>**Aida Marija Bielinskaite**
### <a name="_96goh2eo1dmi"></a>**Test for base.ts (from adapters), lines 149-153**         

**Commit SHA:** e945db072b050021051dbe97bcafdb806894557e

**Link:** <https://github.com/Kinto/kinto.js/commit/e945db072b050021051dbe97bcafdb806894557e>

Coverage before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/01fbb3f0-638d-4c2e-a5f0-6a298dcff784)

Coverage after:

![image](https://github.com/KortsH/kinto.js/assets/156069447/83bac9e5-9cfa-41a5-af57-c9feaab64450)

**In the base.ts (from adapters) tests we had the following improvements:**

Statements coverage improvement: 83.33% to 100%

Branches coverage improvement: 100% to 100%

Functions coverage improvement: 80.00 % to 100%

Lines coverage improvement: 83.33% to 100%

**The new tests were implemented for the following methods:**
- saveMetadata
- getMetadata

*saveMetadata: This method is intended to save metadata associated with the database. It should store the provided metadata and return the saved metadata or nul*l.

*getMetadata: This method is intended to retrieve metadata associated with the database. It should return the metadata of type T.*

#### <a name="_gcsejobp8mcu"></a>**What was improved:** 
The *saveMetadata* and *getMetadata* methods in the *BaseAdapter* class were not tested. Specifically, lines 149-153, where these methods throw a "Not Implemented." error, were not covered by the existing tests. Thus, it was necessary to add tests to call saveMetadata and getMetadata methods and check that they actually throw the expected "Not Implemented." error.
#### <a name="_2vq8fimr70jm"></a>**How was it tested:**
saveMetadata: 

A test was added to call the *saveMetadata* method. This triggers the throw new Error("Not Implemented."); condition, causing the method to throw an error. The test then asserts that the error message is "Not Implemented.".

getMetadata:

A test was added to call the *getMetadata* method. This triggers the throw new Error("Not Implemented."); condition, causing the method to throw an error. The test then asserts that the error message is "Not Implemented.".

### <a name="_1czp05catgie"></a>**Test for base.ts (from http), line 956**

**Commit SHA:** e3c57e1ba4dba7e22a155005dad1ceb7510aa794

**Link:** <https://github.com/Kinto/kinto.js/commit/e3c57e1ba4dba7e22a155005dad1ceb7510aa794>

Coverage before:

![image](https://github.com/KortsH/kinto.js/assets/156069447/85a02b06-9bf1-4755-a86f-bd614cec3b6a)

Coverage after:

![image](https://github.com/KortsH/kinto.js/assets/156069447/9f5a639a-3c45-4be4-8996-a375f62fc4e7)

**In the base.ts (from http) tests we had the following improvements:**

Statements coverage improvement: 98.69% to 99.34%

Branches coverage improvement: 91.75% to 92.78%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 98.69% to 99.34%

**The tests were implemented for the following method:**
- deleteBucket

*deleteBucket: This method is intended to delete a bucket from the server. It should validate that a bucket ID is provided and throw an error if it is not. When a valid bucket ID is provided, it should proceed to delete the bucket and return the response.*

#### <a name="_ewxrynsmwp35"></a>**What was improved:**

The *deleteBucket* method in the *KintoClientBase* class was not fully tested. Specifically, the scenario where the method throws an error due to a missing bucket ID (line 956) was not covered by the existing tests. Thus, it was necessary to add a test to call the *deleteBucket* method without a valid bucket ID and check that it throws the expected "A bucket id is required." error.

#### <a name="_ylwr15al13b1"></a>**How it was tested:**

A test was added to call the *deleteBucket* method with an empty string as the bucket ID. This triggers the condition *if (!bucketObj.id)*, causing the method to throw an error. The test then asserts that the error message is "A bucket id is required." This ensures that the method correctly handles the error scenario when no bucket ID is provided.

## <a name="_cw8b7bhth63g"></a>**Zoe Petroianu**
### <a name="_ljyzavipnm0v"></a>**Test for bucket.ts (from http), line 400**
Method name: *deleteCollection*

**Commit SHA:** 691675766997282efab63ed8328f57e5fa7554b2

**Link:** <https://github.com/KortsH/kinto.js/commit/691675766997282efab63ed8328f57e5fa7554b2>

**Coverage before:**

![image](https://github.com/KortsH/kinto.js/assets/156069447/b7274eba-fc63-484f-b2cf-905019fd4adc)

**Coverage after:**

![image](https://github.com/KortsH/kinto.js/assets/156069447/1cb34001-037f-4759-a24d-dc80c2c63b0d)

***In the bucket.ts (from adapters) tests, we had the following improvements:***

Statements coverage improvement: 95.45% to 96.36%

Branches coverage improvement: 88.63% to 90.90%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 95.45% to 96.36%

1. *deleteCollection*: This function takes a collection ID string or an object containing the collection data and deletes it from a Kinto bucket. 
#### <a name="_p0ulrrtpe5aq"></a>**What was improved:** 

The *deleteCollection* method in the Bucket class was not tested for cases where the collection object does not have an ID. This correlates with line 400 in bucket.ts,* where a “A collection id is required.” error is thrown. Therefore, a test was added that calls the deleteCollection method and checks that the error is thrown when necessary.

#### <a name="_rt9a3v9k9fak"></a>**How it was tested:**

A test was added that calls the deleteCollection method with a collection object that does not have an ID. This triggers the method to throw the error “A collection id is required.” The test added to *bucket\_tests.ts*** then checks that an error was indeed thrown and that the error message is “A collection id is required.”
### <a name="_dv66p7g2171n"></a>**Test for bucket.ts (from http), lines 255, 710, 750**
Method name: *setData*

**Commit SHA:** 5500fecb8034d4edf4bd3daa5980c41968d70dee

**Link: <https://github.com/KortsH/kinto.js/commit/5500fecb8034d4edf4bd3daa5980c41968d70dee>**

Method name: *setPermissions*

**Commit SHA:** ca9073f3407cb45782087162a188df2e00dfb68e

**Link:** <https://github.com/KortsH/kinto.js/commit/ca9073f3407cb45782087162a188df2e00dfb68e>

Method name: *addPermissions*

**Commit SHA:** 95de8a526c66251464d1dcc16290486d696661ed

**Link:** <https://github.com/KortsH/kinto.js/commit/95de8a526c66251464d1dcc16290486d696661ed>

**Coverage before:**

![image](https://github.com/KortsH/kinto.js/assets/156069447/6e6645c6-768b-4d4a-bf52-872592e1a1fc)

**Coverage after:**

![image](https://github.com/KortsH/kinto.js/assets/156069447/f4748a81-5f96-4556-83ef-be40dc9a5425)

***In the bucket.ts (from adapters) tests, we had the following improvements:***

Statements coverage improvement: 95.45% to 98.18%

Branches coverage improvement: 88.63% to 95.45%

Functions coverage improvement: 100% to 100%

Lines coverage improvement: 95.45% to 98.18%

1. *setData*: This function sets or updates the data of a bucket.
1. *setPermissions*: This function replaces the existing permissions with the ones provided for a bucket.
1. *addPermissions*: This function appends permissions to the existing permissions for a bucket.
#### <a name="_gmmvgwshe7og"></a>**What was improved:** 

The methods *setData*, *setPermissions*, and *addPermissions* in the bucket class were all not tested for the cases where the object argument is invalid. This correlates to lines 255, 710, and 750 in bucket.ts. For *setData*, this is the line (255)  where an “A bucket object is required.” error is thrown. For *setPermissions* and *addPermissions*, these are the lines (710 and 750, respectively) where an “A permissions object is required.” error is thrown. Therefore, tests were added that call these methods and ensure errors are thrown when necessary.

#### <a name="_y0j2vxswl03y"></a>**How it was tested:**

A test was added to verify the error handling for each function. For each test, the corresponding function was called with an undefined data object that triggered the method to throw the error “A bucket object is required” or  “A permissions object is required.” The tests added to *bucket\_tests.ts* then check that an error was thrown with the corresponding error message signifying that it handled this case correctly.


## <a name="_r9dc7mbayht2"></a>**Overall**

**Old coverage results:**

![image](https://github.com/KortsH/kinto.js/assets/156069447/ea9761d9-7b7b-4e5c-b509-1ba2ea0032a8)

**New coverage results (all tests together):**

![image](https://github.com/KortsH/kinto.js/assets/156069447/0b30accb-482d-485b-bd53-045dffa10f8c)

## <a name="_la6k60own7ly"></a>**Statement of individual contributions**

**Aaron Serpilin** worked on improving test coverage for *batch.ts* and *requests.ts*. He added new test cases that increased the passing tests from 1448 to 1450, covering critical lines and ensuring proper handling of various status codes and JSON Patch operations for the requests.ts file. As to batch.ts, he added new test cases that increased the passing tests from 1448 to 1450 as well on its own branch. These test cases ensured the proper handling of error responses, 404 responses with undefined IDs, and various scenarios within the aggregate function, enhancing coverage and reliability.

**Henri Korts** contributed to the coverage improvement in *KintoBase.ts* and *Utils.ts*. He added tests that improved the overall coverage metrics, ensuring that critical logic paths were validated and the code's robustness was enhanced.

**Aida** focused on *base.ts* in the adapters directory. She added tests for specific lines to ensure edge cases and critical logic paths were thoroughly tested, contributing to the code's overall reliability.

**Zoe** added tests for *bucket.ts*, targeting specific lines to ensure thorough validation and covering previously untested paths. Her efforts enhanced the software's robustness and fault tolerance. She created test cases that checked the error handling of four different functions and improved the overall coverage. These tests included checking for a collection ID and checking for a valid object argument, ensuring proper error responses.

[ref1]: Aspose.Words.24677b30-d03a-44e8-a371-b7372ef35f7e.002.png
[ref2]: Aspose.Words.24677b30-d03a-44e8-a371-b7372ef35f7e.003.png
[ref3]: Aspose.Words.24677b30-d03a-44e8-a371-b7372ef35f7e.015.png

