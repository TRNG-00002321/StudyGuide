# Levels of Testing

## Acceptance Testing

### Typical Objectives
Acceptance Testing is a process that allows for validating the application in question actually meets the requirements of the application owner and the end users to ensure the successful release of the application. This process not only creates confidence in the system as a whole but also ensures that the application is ready for release to users. While system defect identification is not the primary focus, discovering numerous defects may indicate substantial foundational issues within the application

### Common Types of Acceptance Testing
- User Acceptance Testing
    - The application handles all requirements needed by the end user
- Operational Acceptance Testing
    - Internal administrative tasks can be handled successfully
        - Data is appropriately backed up
        - Logs are generated correctly
        - Installing/un-installing work correctly
        - Security vulnerabilities are handled
- Contractual and Regulatory Acceptance Testing
    - Ensuring the application meets legal/contract requirements
        - Often done in association with an authority witnessing the testing
            - An auditor from the SEC might verify financial records can't be edited
- Alpha Testing
    - Internal testers/developers test an application to see if it works as intended
- Beta Testing
    - People outside the test/dev teams who are sample end users use the application
    - Spot any issues related to end user expectations

### Typical Defects
- Business rules not implemented or interpreted correctly
- Does not mean contract or regulatory requirements
- Poor performance and non-functional failures
    - images don't load correctly or scale incorrectly
    - page loading takes a long time
- Accessibility features don't work correctly

## System Testing

### Typical Objectives
System Testing involves validating functional and non-functional requirements are met when all systems are working together in an application. This includes the database, back end, front end, and supporting cloud infrastructure. Good System Testing can reveal novel defects that are undetectable by lower level testing, and a robust System Testing suite helps create confidence in the system as a whole

### Common Types of System Testing
- End to End testing
    - validating user actions can complete User Stories by fulfilling  Acceptance Criteria
- Performance testing 
    - validating the application is responsive withing contractual obligations
    - validating the application has the scaling potential as planned
- Load testing
    - validating the application can handle the expected number of users
- Compatibility Testing
    - validating the application works in different environments
        - different browsers
        - different operating systems
- Penetration Testing
    - validating the security of the application is robust enough to withstands well known attacks

### Typical Defects
- Incorrect or unexpected functional behavior
- System does not conform to specifications
- Inability to complete all parts of end-to-end tasks
- Performance does not meet minimal requirements
- Application does not meet security requirements
- Cloud environment does not scale appropriately

## Integration Testing

### Typical Objectives
Integration testing is the process of testing how different modules or components of your software work together. It ensures that individual software modules created by different developers with different understandings and programming logic function together seamlessly. It also helps identify and catch any bugs arising from combining modules. The key objectives include creating confidence in the interfaces of the application, ensuring that the join points other programs will interact with are robust, and finding defects to prevent them from escaping into higher levels of the software

### Common Types of Integration Tests
- API Testing
    - verifying an API returns expected results
- Top Down Integration Testing
    - starting at the "highest" level of the application and testing your way down
        - think testing the API of an application, then testing the service layer, then testing the repository layer
- Bottom Up Integration Testing
    - starting at the "lowest" level of the application and testing your way up
        - think testing the repository layer of an application, then testing the service layer, then testing the API
- Incremental Integration Testing
    - test modules and their associated code piece by piece

### Typical Defects
- Incorrect data input/output
    - Missing fields
    - Encoded differently
    - Incompatible data types
- Un-handled communication errors
- Failed security
- Unenforced business requirements

## Unit Testing

### Typical Objectives
Unit testing is a critical process in software development where individual components of a program are tested in isolation to ensure they function correctly. Testers focus on the smallest units of code, such as functions or methods, to identify and fix defects early in development if possible

### Common Types of Unit Tests
- Positive Unit Test
    - given valid input the expected output is returned
- Negative Unit Test
    - given invalid input the expected output is returned

### Typical Defects
- Flow control failures
- Improper logic
- wrong variables used
- environment variables malformed
- properties incorrectly configured

# Types of Tests Revisited & Updated
- **Functional**
  - broad category of tests, relates to features that a user can use (i.e. WHAT the system does)
- **Non-Functional**
  - broad category of tests, relates to the way the software operates (i.e. HOW the system operates)
  - Can include:
    - Security
    - Usability
    - Compatibility
    - Performance
- **Static Testing**
  - broad category, refers to testing/examining a program's code without running it
    - using a linter to analyze the code
    - having a peer analyze the code
    - typically used to verify Quality Assurance practices are being followed
        - comments are being used appropriately
        - recommended versions of dependencies are being used
        - source code organization follows company best practices
        - git strategies are enforced
- **Dynamic Testing**
  - broad category, involves interacting with the system while the program runs
        - your typical Acceptance, System, Integration, and Unit tests will almost always fall under Dynamic Testing
- **White Box**
  - Testing with knowledge of the internal structure or code of the application
- **Black Box**
  - Testing functionality without knowing the internal structure or code
  - Only testing WHAT happens, not HOW the feature is implemented
- **Testing Pyramid**
  - **Unit Testing**
    - Testing of the smallest individual parts (units) of the application
    - Base off the testing pyramid, most tests should be unit tests
  - **Integration Testing**
    - Testing the interactions of individual units working together
  - **System Testing**
    - Testing how the system functions as a whole
        - much manual testing is some form of System Testing
  - **Acceptance Testing**
    - user of the application validates that it satisfies their requirements
        - product owner validates correct application was created
        - regulatory body validates local ordinances are being followed
        - end user validates the application is intuitive and engaging
    - Top of pyramid, should have relatively fewer Acceptance Tests than other types
- **Performance Testing**
    - testing how well an application works, not if it works or not
    - typically part of System Testing, but it can be Integration or Unit testing
    - types of Performance Testing:
        - **Endurance**: testing how long an application can be sustained under normal load
            - can reveal defects like memory leaks or poorly configured log management, or other defects that are only revealed over time
        - **Performance**: testing responsiveness and latency under normal load
            - often used when Service Level Agreements (SLAs) specify a level of performance a service should provide, such as time limits on latency or availability agreements
            - confusingly, performance testing is a kind of testing that falls under the category called "Performance Testing"
        - **Load**: measuring performance at differing loads of traffic
            - particularly useful if your service is deployed in an auto-scaling environment in the cloud, can reveal defects in the deployment environment
        - **Stress**: continually increasing the load of a service to capacity to identify the breaking point of the application
- **Compatibility Testing**
  - Testing that a feature or application works the same on different platforms, operating systems, browsers, etc
- **Regression testing**
  - testing done after one or more new features are implemented to check if the new feature/s broke old features
    - one of the major benefits of automated testing is the ability to quickly perform Regression Testing
- **Retesting**
  - testing done after making changes to fix a defect
- **Automated testing**
  - Not subject to human error
  - Quicker than manual testing
  - Initial upfront investment, but saves time in the long run
  - Reliable, can run 24/7
  - Can handle complex and large applications
  - Well suited for unit, integration, regression, and performance testing
- **Manual testing**
  - Subject to human error
  - Slower than automated testing
  - Easier for smaller or simpler applications or features
  - requires less upfront investment or technical knowledge
  - Well suited for Acceptance testing
- **Smoke testing**
  - Subset of acceptance testing, performed on entire system
  - Test that verifies basic and critical functionality to identify glaring defects (i.e. if there's smoke, there's fire)
  - Performed first in a build, so that if it fails we don't need to waste time testing more advanced features
  - e.g. for a calculator, testing that pressing the ON button causes the calculator to start: if this fails there is no point in checking its other features
  - can be thought of similar to a general health check up
- **Sanity testing**
  - Subset of regression testing, performed on specific feature
  - Performs a "sanity check" to verify functionality of a new feature works as intended
  - think of it as a smoke test for your regression testing: if your new feature/update has defects then old tests that interact with the new feature are probably going to fail as well
  - can be thought of as similar to a specialized health check up
- **Exploratory Testing**
  - Type of testing where test cases are not created in advance but instead on the fly in a White Box testing situation
  - The kind of tests to be created are determined by examining the source code and environment where the application will deploy
- **Error Guessing**
    - Type of testing where test cases are not created in advance but instead on the fly in a Black Box testing situation
    - the kind of tests to be created are determined by the tester and their experience working with similar applications in other projects
- **Alpha/Beta testing**
  - Alpha: initial round of Acceptance Testing, usually User Acceptance Testing. Typically internal people are used
  - Beta: limited release to specific end-users for testing, not limited to internal employees
- **Useability Testing**
  - testing the accessibility features of an application to determine the ease of use offered by the service

# Testing Techniques Revisited
- Positive / negative
  - Positive
    - verify the "happy path", or what happens when valid inputs are given
    - e.g. verify that a login form will redirect to the home page when valid username and password are entered
  - Negative
    - verify the "sad path", or the error states that can occur when invalid inputs are given
    - e.g. verify that a login form does NOT redirect to home page when invalid credentials are given
- Equivalence partitioning
  - Possible inputs to try are infinite, so break them up into "classes"
  - Choose a representative from each class to represent entire class
  - e.g. for testing calculator multiplication operation, partition inputs into negative, 0, and positive
  and have 3 test cases: one with negative number, one using 0, one using positive number
- Boundary value analysis
    - most defects occur at the boundaries of requirements, so instead of picking arbitrary values for your "classes" of data, like in Equivalence Partitioning, you pick values at the boundaries of relevant requirements
- State transition diagram
  - Identifies the different states of the system and the possibilities of navigating between the states
  - e.g. defect life cycle is an example of state transition. project management tools model these states
- Decision tables
  - List all possible combinations of inputs and the resulting output
  - Provides visualization of test data inputs and expected outputs
- Use Cases
    - a way of organizing test data and scenarios that need to be tested to verify requirements are being met
    - typically contains the following information
        - id
        - Use Case name
        - description
        - System being tested
        - preconditions
        - actors (software/people involved)
    - once the scenarios are determined and test data is organized for the Use Case then Test Cases can be created

# Junit
Junit is a popular testing framework for enterprise applications. It allows for creating integration and unit tests for your back end applications. Junit makes use of annotations to control testing in your application
```java
package org.revature.basic;

import org.junit.*;

public class BasicAnnotationTests {

    @BeforeClass
    public static void setup(){
        System.out.println("This runs before all tests");
    }

    @Before
    public void beforeEach(){
        System.out.println("This runs before each test");
    }

    /*
        a test is considered to pass if no exception is thrown by the test method. The Assert class is
        useful for forcing an exception to be thrown if your expected condition is not met: the class many
        many helper methods to validate that your expected output is returned from the method being tested. If the expected value is not present the assert method will throw an AssertionException, failing the
        test, and indicating a defect has been discovered
    */
    @Test
    public void testOne(){
        System.out.println("testOne called");
        /*
            the Assert class's assert methods follow the format of
            1. expected value
            2. actual value

            if you want to return a custom message instead of the default option on a failed assertion you
            can provide a String as the first argument with your custom message
        */
        Assert.assertEquals(11,5+5); // this assertion check will fail, so an exception will be thrown that fails the test
    }

    @Test
    public void testTwo(){
        System.out.println("testTwo called");
        Assert.assertTrue(true); // this assertion check will pass, no exception will be thrown, so the test will pass
    }

    @After
    public void afterEach(){
        System.out.println("This runs after each test");
    }

    @AfterClass
    public static void afterAll(){
        System.out.println("This runs after all tests");
    }
}
```
if testing for exceptions the code looks a little different
```java
package org.revature.exceptions;

import org.junit.Test;

import java.util.ArrayList;

import static org.junit.Assert.*;

public class ExceptionTesting {

    @Test
    public void exceptionTestingWithLambda(){
        IndexOutOfBoundsException e = assertThrows(IndexOutOfBoundsException.class, ()->{
            new ArrayList<Integer>().add(1,1);
        });
        assertEquals("Index: 1, Size: 0", e.getMessage());
    }

    @Test
    public void exceptionTestingWithoutLambda(){
        try{
            new ArrayList<Integer>().add(1,1);
            fail("this should not happen");
        } catch(IndexOutOfBoundsException e){
            assertEquals("Index: 1, Size: 0", e.getMessage());
        }
    }

}
```
Junit also has some other helpful features, like letting you ignore tests, parameterize data, or create  test suites to control which tests you want executed
```java
package org.revature.ignore;

import org.junit.Assert;
import org.junit.Ignore;
import org.junit.Test;

public class TestIgnore {

    @Ignore("you can say why you ignore a test")
    @Test
    public void ignoredTest(){
        Assert.fail("this test should not run");
    }
}
```
```java
package org.revature.parameter;

import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameter;
import org.junit.runners.Parameterized.Parameters;

import java.util.Arrays;
import java.util.Collection;

@RunWith(Parameterized.class)
public class ParameterizedTest {

    /*
        this method tells Junit what data sets to use when running any tests in this class. In this case each test in this class will be
        executed twice, first time using the first collection of data, second time using the second set of data
    */
    @Parameters
    public static Collection<Object[]> inputs(){
        return Arrays.asList(
                new Object[][]{
                    {10,true},
                    {9,false}
                }
        );
    }

    @Parameter // defaults to first value in collection
    public int number;
    @Parameter(1) // this tells Junit to set the value of this field to whatever the element at the 1st index position is
    public boolean isEven;

    @Test // because there are two data sets this test will be run twice, first with the even number, second time with the odd number
    public void isEvenPositiveAndNegative(){
        Assert.assertEquals(isEven, number%2==0);
    }

}
```
```java
package org.revature.suite;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;

// you can use this test suite class to execute the tests in the given Suite classes
@RunWith(Suite.class)
@Suite.SuiteClasses({
        TestSuiteOne.class,
        TestSuiteTwo.class
})
public class TestSuite {
    /*
        SuiteClasses above stores the test classes you want associated with this suite. When this class is referenced for testing, whether by
        Junit through your IDE or by Maven during a testing phase, the classes in the SuiteClasses annotation will have their tests executed
    */
}
```

### Mockito
Mockito is a framework that makes Mocking objects and Stubbing methods easy. A few key pieces of terminology:
- Mock: an object we can control in order to focus our tests on another resource
    - think mocking a dao object inside a service in order to do unit testing of the service object
- Stub: a method with a pre-determined result

A common practice is to use mock objects to stub methods in order to perform unit testing for a class that has sub dependencies (think your project service and dao objects)
```java
package org.example;

/*
    There will be times when testing applications that the structure of your code will not
    allow for easy unit testing. Consider a web application that has an API, service layer,
    and repository layer. Each layer of the application will in some way, shape, or form,
    require data that has been operated on in the other layers. This is not conducive for
    unit testing (but it is great for integration testing). In situations where you need
    to perform unit testing on these integrated classes and their methods you can make
    use of "Mock" objects to "Stub" method results.
    - Mock: a mock object can be used to reference methods of a needed object without actually
            walking through the logic of executing the method code
    - Stub: a method that has a pre-determined return value, often used in unit testing
 */

import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.mockito.Mockito;

public class MockMainTest {

    private Main main;

    @Before
    public void setup(){
        /*
            When we use Mockito to create a mock version of our class we are using
            Mockito to create a version of the object that we have fine-tune control
            over. This will allow us to do things like pre-determine return values, check
            the flow of code execution, and even change the expected results of the methods
            in the mock object.
         */
        main = Mockito.mock(Main.class);
    }

    @Test
    public void stubMethodResults(){
        /*
            By default, a mock object will return whatever the non-initialized value
            of the return type the method should return. We need to tell the mock object
            what value to return when the method is called with the given arguments
         */
        Mockito.when(main.addContent(5,5)).thenReturn(10);

        // Normally, this would return 10
        int result = main.addContent(5,5);
        Assert.assertEquals(10, result);
    }

    @Test
    public void returnNotRealisticValue(){
        /* 
            you can make the return value whatever you want, as long as the data type
            matches the expected return type
        */ 
        Mockito.when(main.addContent(5,5)).thenReturn(300);
        int sum = main.addContent(5,5);
        Assert.assertEquals(300, sum);
    }

    @Test
    public void throwAnException(){
        // Here we tell Mockito to throw an exception with the method with the given arguments is called
        Mockito.when(main.addContent(5,5)).thenThrow(new ArithmeticException("This exception was stubbed!"));
        ArithmeticException exception = Assert.assertThrows(ArithmeticException.class, () -> {
            main.addContent(5,5);
        });
        Assert.assertEquals("This exception was stubbed!", exception.getMessage());
    }

    @Test
    public void checkPathOfExecution(){
        Mockito.when(main.addContent(5,5)).thenReturn(10);
        /* 
            Mockito also allows us to check things like how many times a method is executed and what data is passed into
            the method
        */ 
        main.addContent(5,5);
        Mockito.verify(main).addContent(5,5);
    }

    public void checkMultipleExecutions(){
        Mockito.when(main.addContent(5,5)).thenReturn(10);
        main.addContent(5,5);
        main.addContent(5,5);
        Mockito.verify(main, Mockito.times(2)).addContent(5,5);
        Mockito.verify(main, Mockito.atLeast(1)).addContent(5,5);
        Mockito.verify(main, Mockito.atMost(2)).addContent(5,5);
    }

}
```

### Junit Test Reports
if you want test reports that can be viewed outside of your IDE you can use the Maven Surefire Plugin by adding it to a build section in your project POM.xml

```xml
  <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>3.3.1</version>
        </plugin>
      </plugins>
  </build>
```
the default plugin settings will generate both text and xml test reports, not particularly easy to read, but the XML option can be uploaded into AIO to record the results of your test cases, though you will need to manually link the tests to any associated issues. The surefire plugin can also be configured to include/exclude tests from being executed when the test phase is reached in the maven life cycle

### API Testing
API testing is a form of integration testing where you verify that HTTP Requests and Responses are working as intended. Some common features to check:
- is the HTTP Status in the response correct?
- is the structure of the JSON in the response correct?
- are the correct headers returned in the response?
- is an incorrectly formatted JSON rejected by the application?
- is the correct data returned in the response json?