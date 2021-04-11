JUNIT TEST FILES
-----------------------------------------------------------------------------------
Jared Lundy
Jordan Lundy
Chace Nielson
Tony Vo
-----------------------------------------------------------------------------------



TO COMPILE AND RUN:
------------------------------------------------------------------------------------
Jar Files needed:	~ junit-4.13.2.jar
			~ hamcrest-core-1.3.jar
			~ mysql-connector-java-8.0.23.jar (only mandatory for DBTests.java)

Steps to compile and run via command line:

1. Ensure the 3 above jar files are within the directory outside of the tests folder (where java files are)
2. cd into directory before/outside tests folder (where all java files are)
3. javac -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar;mysql-connector-java-8.0.23.jar.; tests\[TestName].java  			
			*you replace [TestName] with whichever test youre running (eg DBTests.java)*
4. java -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar;mysql-connector-java-8.0.23.jar;[full path to test file (ends with \tests)] org.junit.runner.JUnitCore [TestName]
			*you replace [TestName] with whichever test youre running (eg DBTests.java)*
***NOTE: DBTests must be compiled with mysql-connector jar file. The other tests do not need this jar(only junit and hamcrest needed)***

Example on my machine:
- 	cd C:\Users\jarrl\ensf409finalproject-main
-	javac -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar;mysql-connector-java-8.0.23.jar.; tests\DBTests.java
- 	java -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar;mysql-connector-java-8.0.23.jar;C:\Users\jarrl\ensf409finalproject-main\tests org.junit.runner.JUnitCore DBTests

To generate test documentation:
1. cd to directory outside tests folder (where java files are)
2. javadoc -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar.; tests\[TestName].java
-------------------------------------------------------------------------------------
				
					
					TEST DESCRIPTIONS
	
	(note: documentation can be generated via javadoc -cp .;junit.4.13.jar;hamcrest-core-1.3.jar.; [TestName].java)

FILE NAME: CalculatorTest.java
------------------------------------------------------------------------------------
Preamble

This test file tests the functionality of the calculator class after data has been read into the program.
Through mock database data (to avoid unecessary changes to the database), a calculator object is created, 
and then the methods needed to calculate the best price and return the chosen IDs are called(fillChosenItemsArray()).
In the case that, based on the data, there is a possible combo, an expected result is compared to a calculates result
(either via getChosenItemsString() method to return the chosen items, or via getPrice() to return the calculated price).
In the case that a combo cannot be found, the test asserts that the errorMessage() method returns the valid errorMessage.

Test 1: CalculatorGetStringsTest1
CASE: 	Successful calculation of best deal given data, specifically testing choosing proper IDs. 
	Expected IDs chosen from data is compared to the IDs chosen via the calculator's getChosenItemsString() method.
	Assert ensures that the expected and chosen IDs match.

Test 2: CalculatorGetStringsTest2
CASE: 	Successful calculation of best deal given data, specifically testing proper selection of IDs.
	Same test as before, but different dataset to ensure core functionality of calculator is consistent.

Test 3: calculatorGetStringTest3
CASE:	Successful calculation of best deal given data, specifically testing proper selection of IDs.
	Same test as before, but different dataset to ensure core functionality of calculator is consistent.

Test 4, 5, 6: calculatorGetPriceTest1, calculatorGetPriceTest2, calculatorGetPriceTest3
CASE: 	Successful calculation of best price via calculator. Ensures expected price and getPrice() return match.

 
Tests 7, 8, 9: calculatorGetErrorMessage1,calculatorGetErrorMessage2, calculatorGetErrorMessage3
CASE: All tests take in a different dataset and a request that cannot be fulfilled with the given data.
The tests then expects that fillChosenItemsArray() will not be filled. 
Finally, calls errorMessage method and asserts that the errorMessage is outputted in the case of unsuccessful best deal, and that the appropriate manufacturers are outputted in this message (by comparing it to an expected message).



FILE NAME: DBTests.java
	*note: must be run with mysql-connector in classpath due to database connectivity requirements*
-----------------------------------------------------------------------------------------------------------
This test file tests the core functionality of the database aspect of our project. 
Specifically, it tests the connectivity to the database, close() methods, counter method (counts specific items in DB) and deleteSoldItems method (deletes selected items from DB).
It also tests for expected exceptions with database closing.

(For more info on individual tests, generate documentation via javadoc -cp .;junit-4.13.2.jar;hamcrest-core-1.3.jar.; DBTests.java)

Test 1: dbConnectTest
CASE: Successful connection to the database via ReadDatabase's constructor - asserts getDBConnected() boolean return is true

Test 2: dbCloseTest
CASE: Successful closing of all resources via ReadDatabase's close() method - asserts getDBClosed() boolean return false

Test 3: closeExceptionTest
CASE: Unsuccessful closing of all resources due to inappropriate ReadDatabase instantiation - expects and asserts a NullPointerException is thrown

Test 4: readDatabaseTest
CASE: Successful setting of ReadDatabase's private members via String arguments to its constructor - ensures that getters for privates category, type and quantity match arguments to constructor

Test 5: counterTest()
CASE: Counter() method in ReadDatabase accurately counts specific items in database. Asserts counter and coded database count integer match.

Test 6: deleteSoldItemsTest
CASE: Successful deletion of a uniquely added ID to the database. Once unique ID added, ReadDatabase's deleteSoldItems method called to delete from database.
	Then, test searches in database for this ID, which should NOT be found once deleted.


FILE NAME: OutputFileTests.java
-------------------------------------------------------------------------------------------------------------------
A Test file that tests the functionality of creating the output file using makeFile method. 
This test tests both the successful creation of an output test file, using mock data, a calculator to calculate the price and select items, and the makeFile method in OutputFile class.
Also tests that in the case of an item not possibly being made, an appropriate message with manufacturers is made via errorMessage method of OutputFile.

Test 1: outputFileCreationTest
CASE: Successful generation of output file. Test makes an output file Furniture_Order_Form.txt and ensures that the makeFile method indeed creates this output file successfully, as expected 

Test 2: noOutputTest
CASE: Unsuccessful creation of output file due to impossible order fulfillment. Proper error message via errorMessage() of calculator class display is tested, which displays appropriate manufacturers given manufacturer mock data.


FILE NAME: readInputTests.java
--------------------------------------------------------------------------------------------------------------------
Tests the functionality of the ReadInput class, and thus our program's ability to prompt user input, read user input and set the appropraite parameters from these command line inputs.
Note: ReadInput handles any inputs that do not match expected input by re-prompting user entry to that field
Note: will prompt user entry for type, item, quantity FOUR times - please enter all field with valid data each time

Test 1: testReadInput
CASE: ReadInput is able to accept a command line argument, set the private item, type and quantity variables, and getters for those members only return valid/allowable Strings(ie. ReadInput does not allow any non-allowable input to get in the program)

Test 2: testReadInput2
CASE: Same as test above, but now focusing on valid input recognition of the type parameter. Error-check by ensuring only allowed types strictly from the database are equal to the private variables.

Test 3: testReadInput3
CASE: Asserts that getRequest() getter of ReadInput returns what is actually inputted on the command line (matches private members set by ReadInput)

Test 4: nullInput()
CASE: Asserts private ReadInput members never set null, which should be IMPOSSIBLE CASE due to its re-entry prompt when something invalid inputted on command line.


FILE NAME: properSelectionTests.java
----------------------------------------------------------------------------------------------------------------------------------
Tests the functionality of calculator class to chose appropriate IDs from given dataset, and that getChosenItems() and getChosenItemsString() return the expected item IDs.
Also tests boundaries/exceptions when too many elements requested (impossible request).

Test 1: chooseOneExecutiveChair
CASE: 	Successful choice of ID based on order and data given. getChosenItems() array matches expected array of IDs selected.

Test 2: chooseOneExecutiveChairAgain
CASE: 	Successful choice of IDs again. This time, checks that chosen IDs returned from getChosenItemsString() match the expected.

Test 3: chooseTooMany
CASE: 	NullPointerException (UPPER BOUNDARY). A request of too many items is requested, and the test expects that getChosenitems() will throw nullpointerexception (fails if this does not occur).

Test 4: chooseZero
CASE: Tests lower boundary of 0 requested. Ensures getChosenItems is not successful when requesting zero items, and ensures this by expecting NullPointerException.

Test 5: chooseNegative
CASE: Tests lowest boundary of negative requested items. Due to ReadInput's re-entry structure for invalid requests, this should never actually occur therefore expect exception.

Test 6: noPossible
Case: No possible combinations. Must reach catch block rather than continuing with calculations.


FILE NAME: multiplePriceTests.java
-----------------------------------------------------------------------------------------------------------------------------------------------------
Builds off the basic functionality to test multiple items being selected and prices calculated by calculator. 
Tests success cases, as well as upper boundary exceptions(exception when too many requested), and lower boundary exceptions (empty database/null)

Test 1: twoMeshChairsPrice
CASE: Beyond upper boundary - requests more than in database. Expects getChosenItems() method to throw NullPointerException, and fails if no exception is thrown.

Tests 2, 4, 6: twoAdjustableDesksPrice, threeDeskLamps, twoSmallFilingPrice
CASE: Successful price calculation within acceptable boundaries. Given data, getPrice() method calculates the expected price, and getMatchFound() returns true for a match.

Tests 3, 5, 7: threeAdjustableDesksPrice, tooManyDeskLamps, threeSmallFilingPrice
CASE: 	Beyond upper boundary - requests more than in database/possible given data. As a result, ensures getChosenItems(), getChosenItemsString() throw exceptions and getMatchFound is false.

Tests 8 and 9: testEmptyInput, testEmptyInput2
CASE: Tests lower boundary - when data from database is empty (except for labels). Asserts that getPrice() doesn't throw exception in both cases and fails if exception thrown. Ensures that it effectively calculates nothing when empty data is given, rather than throw exception.

Test 10: nullPoint
CASE:     Tests that a nullpointer exception is thrown in the case that a calculator is made with an empty array (not even labels) passed to the constructor. Fails if no exception.


FILE NAME: pricesTestFile.java
---------------------------------------------------------------------------------------------------------------------
Tests the simplest functionality of calculator selecting 1 item and calculating its price via getPrice(). 

ALL TESTS: With varying datasets to ensure consistency across all possible data, all tests test that calculator can calculate the best deal for 1 item given data. 
Asserts getMatchFound() is true, and getPrice() is what is expected by the given data.


FILE NAME: priceTests.java
-------------------------------------------------------------------------------------------------------------------------------
Tests that calculator can calculate the best deal for larger than 1 situations, ie. more than one item requested.
Also tests that zero elements will throw exception via getPrice() method, and fails if no exception is thrown.


Test 1: calculatorTest2
CASE: Successful retrieval of selected IDs from getChosenItemsArray() following fillChosenItemsArray() call. 

Tests 2, 3, 4, 6: testPriceCalculation, testPriceFiling, testPriceLamp
CASE: Successful calulation of single item (varying data to ensure consistency). Calculator instantiated with dataset, fillChosenItemsArray() called, then getPrice() compared to expected price.

Test 5: testZeroElementsLamp
CASE: Asserts exception is not thrown when trying to call getPrice() with an empty dataset fed into calculator ctor. Fails if exception or if it proceeds to calculate. Asserts price calculated is zero when empty data.


FILE NAME: OutputFileTest.java
---------------------------------------------------------------------------------------------------------------------------------------------
Further tests the outputfile class and its methods used to create the output order form.
Tests both a successful case, and an unsuccessful case.

Test 1: makeFileTest
CASE: Tests that OutputFile constructor works, and makeFile() creates the correct output file. Asserts boolean returned from makeFile() is true.

Test 2: failToMakeFile
CASE: Unsuccessful output file creation. Succeeds in constructing object, but expects boolean from makeFile() to be false, as the data its given is not sufficient to create a file (ie. invalid name "")

