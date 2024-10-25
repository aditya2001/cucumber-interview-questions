## Cucumber Interview Questions

### 1. What is Cucumber BDD?
Cucumber is an open source tool that supports BDD. It allows us to write test cases using plain english like syntax called as Gherkins.
These tests known as scenarios are easy to understand for both technical and non-technical people. The goal of Cucumber is to help communication between developers, testers and Business Analyst.
```java
Example-
Feature: Login Functionality
   Scenario: Valid Login
   Given user is on login page
   When user enters valid credentials
   Then user should be redirected to home page
```

Benefits-
1. Improved Collaboration - Cucumber improves collaboration across teams by using a common syntax(Gherkins)
2. Documentation - Cucumber scenarios are also documentation.
3. Automation integration - Cucumber integrates with automation tools like selenium, cypress.


### 2. Difference between Cucumber and BDD?
BDD is an approach just like Agile whereas Cucumber is an automation tool that supports BDD but cucumber is not BDD.

BDD - In traditional development, there is a very little collaboration between developers, testers and BA. 
BDD is development approach, which uses a common language, Jherkin that bridges the communication between technical and non-technical people.
1. It enables you to understand how the system should perform from the developer’s and customer’s perspective.
2. Helps reach a wider audience by the usage of non-technical language
3. Enhances communication among the members of a cross-functional product team
4. Focuses on defining ‘behavior’ rather than defining ‘tests’


### 3. What are feature files, step definitions and gherkin syntax?
Feature Files - Feature files are plain text files written using Gherkins syntax, inside which we write scenarios.
Every scenario inside the file describes the functionality of the application.

Step Definitions - Step definitions are the code implementations of the steps defined in the gherkins scenario. Each gherkins steps(Given,When ,Then) is linked to a corresponding code block in the step definition.


### 4. What are cucumber tags?
Cucumber tags are used to organize and selectively run test. Tags are added to scenario or feature file level using @ followed by name.
For ex you can choose certain scenarios to run for smoke test and mark them using @SmokeTest.
mvn test -DCucumber.options="--tags @SmokeTest"

### 5. Folder Structure?
![img.png](img.png)

### 6. Cucumber BDD with TestNG?
![img_1.png](img_1.png)

### 7. What is the role of testNG and runner class in cucumber with testNG?
The testng.xml file and runner class have roles in executing cucumber test in cucumber with testNG framework.
1. testng.xml file -> This configuration file tells testNG to organize and execute test. It specifies which class to run and allows for group, sequence of execution and supports parallel execution.

2. runner class -> The runner class executes the cucumber tests.The runner class extends AbstractTestNGCucumberTests. In this class we define location of feature and step definitions.

### 8. How to run cucumber test in parallel using TestNG?

1. Run Scenarios in Parallel -> To run individual scenarios in parallel, we need to configure our runner class to enable parallel execution.
This is done by overridding the scenarios method in the runner class. 

```java
public class TestNGCucumberRunner extends AbstractTestNGCucumberTests {
    @Override
    @DataProvider(parallel = true)
    public Object[][] scenarios() {
        return super.scenarios();
    }
}
```

2. Parallel execution in testNG.xml -> TestNG allows to run test in parallel by adding a parallel attribute in the suite tag of testng.xml.

```java
<suite name="Test Suite" parallel="classes">
    <test name="TestChrome">
        <parameter name="browser" value="chrome" />
        <parameter name="env" value="uat" />
          <classes>
            <class name="runner.TestRunner"></class>
         </classes>
    </test> <!-- Test -->
```

### 9. How to implement data driven testing in Cucumber using Scenario Outline?
DataDriven testing is achieved using Scenario Outline and Examples Keyword. Scenario Outline allows to run a single scenario multiple times with different set of data.
We provide the placeholders in scenario and during execution cucumber will replace placeholders values from Examples.

![img_2.png](img_2.png)

### 10. What are Hooks in Cucumber?
Hooks allows you run blocks of code before and after scenarios.They setup precondition and clean up after test execution.

@Before

@After

### 11. What is background in Cucumber?
Background is a step that is executed before each scenario and is common all the scenarios.

### 12. What are Data Tables in Cucumber?
Datatables are used to pass list of values to cucumber step definitions.

```java
Scenario: Incorrect Username Login
When A user provides incorrect credentials, and clicks on the login button with
| userName | password     |
| testName | secret_sauce |
| admin    | admin        |


    @And("user select drop down value with$")
    public void userSelectDropDownValueWith(DataTable datatable) throws Exception {
        List<Map<String, String>> ffElements = datatable.asMaps(String.class, String.class);
        for(Map<String, String> ffElement : ffElements){
            selectDropDownPage.selectDropDownValue(ffElement.get("userName"));
        }
    }
```

### 13. @CucumberOptions annotation in runner file?
The Options tag helps create a link between the feature files and the step definition files, with each feature file connecting to a corresponding step definition file.

```java
@CucumberOptions(
        tags = "not @ignore",
        plugin = {"pretty",
                "com.aventstack.extentreports.cucumber.adapter.ExtentCucumberAdapter:",
                "timeline:test-output-thread/",
                "rerun:target/failedrerun.txt"
        },
        monochrome = true,
        glue = { "stepdefs" },
        features = { "src/test/resources/features" }
)
```




