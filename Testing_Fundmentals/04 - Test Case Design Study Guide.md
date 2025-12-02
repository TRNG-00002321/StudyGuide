# Test Case Design Study Guide

## Testing Pyramid
When designing tests, it is useful to keep the "Testing Pyramid" in mind. This "Test Pyramid" is a visual representation of the abundance of tests based on certain "levels" of testing. More tests exist at the lower level of the pyramid than at the top because they exist at a lower level of abstraction (unit tests), whereas fewer exist at the top and focus on a higher layer of abstraction (system tests, UI tests, UAT).

- Unit Testing
  - Most micro-level of testing
  - Test each component without dependencies
  - Usually requires data mocking
  - Unit testing tools include Junit and TestNg
- Integration Testing
  - Test components with dependencies
  - Check that components work with one another correctly
  - Logically related modules are tested as a group
  - Integration testing tools include those used for Unit testing, along with third party tools like Postman or Thunderclient
- System Testing
  - Test the entire application as a whole
  - Ensure the entire application works without errors
  - System Testing tools include those used for Integration and Unit testing, alongside others like Selenium and Cucumber
- Acceptance Testing 
  - Test individual or whole aspects of an application to determine whether they are "acceptable" or not
  - Often involves making subjective measurements and assessments, such as determining how intuitive the application is to use
  - Can include tests used to validate user, stakeholder, or regulatory requirements are being met by the application
  - Often requires manual testing, particularly for any subjective tests, but automation tools can be used for some forms of Acceptance testing

![Testing Pyramid](testing-pyramid.png)


## Terminology

### Test Case
A **test case** is a set of preconditions, inputs, actions, expected results, and postconditions, developed based on **test conditions**. **Test conditions** are testable aspects of a component or system identified as a basis for testing. This means that a **test case** is a formal collection of resources needed to do the actual testing, and the **test conditions** are the things that need to be tested

### Test Basis & Test Analysis
The **test basis** is the body of knowledge that serves as the foundation for test analysis and design. The process of determining the test basis to identify test conditions is known as **test analysis**. Here is a detailed flow for designing your tests:

1. **Perform Test Analysis**
    - Utilize various resources to determine your **test basis**. These resources may include, but are not limited to:
        - **Requirement Specifications**:
            - Functional requirements
            - Business requirements
            - Accessibility requirements
            - Other relevant specifications
        - **Design Documents**
        - **Risk Analysis Reports**
        - **Traceability Reports**

2. **Identify Test Conditions**
    - Based on the **test basis** identified in the previous step, determine the specific test conditions that need to be tested. Examples of test conditions include:
        - **Functional Test Conditions**: Verify that the login functionality works as expected.
        - **Performance Test Conditions**: Ensure the application can handle 1000 concurrent users.
        - **Security Test Conditions**: Check that user data is encrypted during transmission.
        - **Usability Test Conditions**: Confirm that the user interface is intuitive and accessible.

3. **Craft Test Cases**
    - Use the identified test conditions to develop detailed test cases. Each test case should be designed to verify a specific aspect of the **test conditions**. Examples of test cases include:
        - **Functional Test Case**: Test that a user can successfully log in with valid credentials.
        - **Performance Test Case**: Measure the response time of the application when 1000 users are logged in simultaneously.
        - **Security Test Case**: Verify that data transmitted during login is encrypted using SSL/TLS.
        - **Usability Test Case**: Evaluate the ease of navigation through the main menu for a new user.

### Test Objective
**Test Objectives**, also known as test goals, are your end-reasons for testing. Some typical types of objectives:
- Evaluate work products
- Find defects
- Ensure coverage and compliance
- Reduce risk
- Verify requirements and completeness
- Provide general information
- Build confidence in product/service

### Test Object
Whatever you are testing, whether it be an individual component of an application or the entirety of an application, the thing being tested is your **test object**, also referred to as a test item. 

### Test Data
When creating test cases you will often have specific data sets for one or more of your test cases: this collection of data is your **test data**. Oftentimes initial **test data** can be aggregated and sorted during the test analysis activity, and then later specified once test conditions are determined. For instance, if your test object is a registration feature and your test objective is to validate username constraints are enforced by the application, during your test analysis you would determine what the constraints should be (character length, character types, unique, minimum number of non alphabet characters required, etc.), and then when designing your tests you would provide specific values that meet (or don't, depending on the type of testing you are doing) those constraints

### Test Suite
Similar or related test cases can be organized into groupings called **test suites**. These groupings can be due to related test objectives, test objects, test data, etc.

### Positive & Negative Testing
**Positive testing** and **negative testing**, also known as "happy path" and "sad path" testing, are two fundamental testing strategies. Positive testing is used too confirm that things work correctly when user interactions and data used are valid. For instance, if your test objective is to confirm a registration feature works correctly, you could do positive testing by checking that a new user is created in the system when a valid username and any other relevant details are provided to the system.

On the flip side, **negative testing** would involve the inverse: you would provide the system with invalid new user data (username that is too long, not enough characters, missing special characters, empty, etc) and confirm that the system does not create an account for the user

### Defect
A core goal of testing is to discover **defects**: a **defect** is any failed requirement or deviation of an expected outcome. This could be a business requirement not being met, a software feature not working correctly, gaining access to resources you are not supposed to, etc.

Note that the terms **defect** and "bug" can be used interchangeably, but **defect** is the more formal way of describing deviations from expected results

### Error
In software work, any mistake a developer adds to code, whether calling the wrong variable, forgetting to implement a business rule, or any other mistake, is called an **error**. It is **errors** that lead to defects being present in code

### Failure
Anytime a defect is executed/triggered in your application it will trigger one or more **failures**. Note that defects and **failures** represent the same thing, a deviation from the expected or required. The main difference is in how the defect is revealed: **failures** happen when a defect is triggered in a active application (this can be user discovered in production or tester discovered in the testing environment). This means that all **failures** are defects, but not all defects are **failures**.

## Technique

### Use Case
A **Use Case** is a tool used in software development to define the required user interactions for creating or modifying an application. It plays a crucial role by helping developers and testers identify test scenarios that cover the entire system from start to finish. Use Case Testing, a part of black box testing, ensures that the system meets both technical requirements and user expectations. Because it is a black box technique, **use cases** tend to be used to further develop the test cases at the system and acceptance level. This means **use cases** are an organizational tool for developing and grouping your tests by describing real world scenarios for how end users interact with the system being tested, and what should happen based on those interactions.

Some features of **use case** testing:
- **User Interaction**: Defines required user interactions for new or modified applications
- **Black Box Testing**: Helps identify test scenarios that cover the entire system from start to finish
- **Mutual Understanding**: Requires a mutual understanding between business experts and developers
- **User-Centric Approach**: Ensures the system meets both technical requirements and user expectations

### Black Box & White Box Testing
**Black box** and **white box** testing are two fundamentally different approaches to testing software. In **black box** testing you build and execute tests based off the system specifications, design documentation, and your general understanding of how the application is supposed to work. It is called **black box** because the underlying implementation, the source code and application environment, is unavailable to you, and therefore should have no bearing on how you design your tests. This makes system and acceptance testing more prevalent in **black box testing**.

**White box** testing has the tester use the internal structure of the application being tested to create tests: the source code, internal configurations, application environment, and any other internally used resources are available to the tester. All levels of testing can be done in **white box** testing


### Black Box: State Transition Diagram
Anytime you have a system or service where there are multiple "states" to consider, a **state transition diagram** can be used to organize your data before creating your test cases. A **state transition diagram** is simply a flow chart that shows the various states in the service and the way they connect to each other, including at minimum a starting state and one or more ending states. For instance, if you are testing a reimbursement system you may have the following states of a reimbursement request: "pending", "accepted", "rejected". Each state of the request would have different actions, expectations, and other general requirements associated with it, and if you have your states organized in a **state transition diagram** it will be easier to organize the tests you create and prevent redundant overlap

### Black Box: Decision Table
When a user must make a string of "decisions" using a service, such as providing multiple inputs to a form, a **decision table** can be used to organize the inputs and expected results of providing the data. For instance, if testing a login feature, you could craft a decision table where all combinations of "valid" usernames and passwords are matched with "invalid" usernames and passwords, and for each possible combo list the expected results (logged in or rejected). By organizing the data combinations in a **decision table** you can accommodate the potential combinations of inputs and test the inputs produce the expected results

### Black Box: Boundary Value Analysis
When creating test data for business requirements, there will often be "boundaries" that are specified by those requirements. For instance, if testing a registration feature, there may be limits on how many characters can be included in the username. These restrictions create your natural "boundaries", which make for great determiners for your test data. Determining what these boundaries are and organizing your test data by those boundaries is called **boundary value analysis**. Typically when performing **boundary value analysis** you would determine your boundaries and then organize your valid and invalid data by selecting values just in the boundaries of requirements and just outside the boundaries. You would then let these values represent their "class" of data in your tests

### Black Box: Equivalence Partitioning
Similar to boundary value analysis, **equivalence partitioning** is a technique where you divide your test data in to "classes" of data and use a single value to represent the entirety of the class. This technique is useful when you don't have requirements that create natural boundaries for your data, or when the amount of potential test data is overwhelmingly large. By implementing **equivalence partitioning** you can optimize the number of test cases you need while keeping your tests from being redundant

### Black Box: Error Guessing
**Error guessing** is a black box testing technique where the tester leverages experience and prior knowledge of similar applications to make educated guesses about potential failure points in the software being tested. This method involves designing tests around these educated guesses to uncover defects that might not be evident through other testing techniques. Error guessing is particularly useful when requirements are minimal or ambiguous, or when trying to create new tests. By anticipating where errors are likely to occur, testers can create targeted test cases that effectively identify defects

### White Box: Exploratory Testing
**Exploratory Testing** is a software testing technique where testers actively engage with the application to discover its functionalities and potential issues. Unlike traditional testing methods that rely on predefined test cases, exploratory testing relies on the tester’s creativity, intuition, and experience. Testers explore the software without a specific plan, learning about its behavior and identifying defects in real-time. This method is particularly useful when requirements are unclear or incomplete, as it allows testers to adapt and respond to the software’s actual performance. Exploratory testing encourages testers to think critically and investigate the application from various angles

### White Box: Statement Testing
**Statement testing** is the practice of writing tests to execute statements in source code. This type of testing can be used to detect defects caused by developer error. It can also be used to help identify parts of the code that are not being reached, which might indicate dead code or logic errors. Statement testing is often used in combination with other testing techniques to narrow down the location where errors and/or defects are being triggered. **Statement testing** is often measured by code coverage: the number of lines of code involved in a test case. An application with 80% code coverage executes 80% of the lines of code during testing. Note that it is not always necessary to achieve 100% code coverage: you may use other testing techniques or tools to test parts of your code that are not part of your code coverage report

### Checklist Testing
**Checklist testing** involves following a pre-determined list of actions to perform your testing. This method is akin to checking items off a grocery or chore list, ensuring that each step is completed and accounted for. The checklist typically includes specific tasks or conditions that need to be met, such as verifying login functionality, checking data input fields, or ensuring that navigation links work correctly. By systematically going through the checklist, testers can ensure that all critical aspects of the software are examined. This approach helps in maintaining consistency and thoroughness in testing, as it provides a clear and structured way to track what has been tested and what still needs attention. Additionally, checklist testing can be particularly useful in regression testing, where previously tested functionalities are re-verified to ensure that new changes have not introduced any new defects

### Conditional Testing
**Conditional testing** involves grouping different combinations of conditions to determine the expected outcomes for each scenario. For example, if a user is logged in, they should be able to see user information on the homepage; if not, they should not be able to access the homepage. This method of organization helps ensure the various conditions and their expected outcomes are tested

## Static Testing

### Static Testing vs Dynamic Testing
**Static testing** involves verifying software to ensure it meets quality standards before any code execution occurs, as opposed to **dynamic testing**, which is done by executing code and checking its results. Almost any work product can be examined using static testing, including requirement specifications, source code, test plans, and project documentation. **Static testing** involves manual examination or tool-assisted (think a linter) analysis to evaluate readability, completeness, correctness, and consistency. In order for **static testing** to be efficient the resources being analyzed need to follow some form of consistent structure, syntax, or practice, in order to have repeatable and meaningful analysis.

### Static Testing Workflow
1. **Planning**:
   - Define the objectives of the static testing, select appropriate techniques and tools, and assign roles and responsibilities to team members.

2. **Preparation**:
   - Gather all necessary documentation, such as business requirements, functional specifications, and code, and set up the static analysis tools if automated tools are being used.

3. **Execution**:
   - Conduct code reviews, static analysis, walkthroughs, and inspections to identify issues like syntax errors, logic flaws, security vulnerabilities, and adherence to coding standards.

4. **Documentation and Reporting**:
   - Document all findings, including identified defects and areas for improvement, and provide feedback to the development team for necessary corrections.

5. **Follow-up**:
   - Ensure that all identified issues are addressed and resolved, and conduct re-reviews or re-analysis if necessary to verify the fixes.

6. **Closure**:
   - Finalize the static testing process by ensuring all objectives have been met and archive all relevant documentation for future reference.

### Review Roles
A common static testing technique is simply called a **review**. The most formal versions of **reviews** involve multiple roles:
- **Manager**: Decides what is to be reviewed and provides resources for the review
- **Author**: Is the creator of the resource under review, and is responsible for fixes
- **Moderator**: In charge of the effective running of review meetings; this includes mediation, time management, and fostering a blameless culture
- **Scribe**: Records anomalies from reviewers and general review information, such as decisions made during the review
- **Reviewer**: Performs reviews: a reviewer may be someone working on the project, a subject matter expert, or someone brought in to help with the process
- **Review Leader**: In charge of planing the review: decides who will be involved and organizes when and where the review will happen

### Review Techniques
There are multiple types of **reviews**:
- **Informal Review**: Informal reviews do not follow a defined process and do not require formal documentation. Their main objective is to find defects in the testable resources.
- **Walkthrough**: Led by the author, walkthroughs can serve multiple objectives such as evaluating quality, building confidence, and generating new ideas. Individual reviews by participants may or may not be required before a group review
- **Technical Review**: Conducted by technically qualified reviewers and led by a moderator, technical reviews aim to gain consensus on technical issues, detect defects, and evaluate quality
- **Inspection**: The most formal type of review, inspections follow a complete process to find anomalies, evaluate quality, and collect metrics for process improvement. The author cannot act as the review leader or scribe