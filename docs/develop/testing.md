# Testing

Be a tester, do not be a checker. Automate everything you can if it can be done in reasonable time.

## Static analysis

Automatic eyes on your code; mostly cheap and helpful.

### Cyclomatic complexity

assigns a number to a method resembling the complexity.

This number can be used to identify complex methods which need a refactoring. The number is calculated using the control flow graph, and represents the number of linearly independent paths (for two following `if-else` constructs, the number would be three; two for the first `if-else`, and one to cover the possibly missed block of the second `if-else`).

### Cognitive complexity

tries to enhance cyclomatic complexity to better resemble understandability.

The definition of cognitive complexity is no longer a mathematical model: It tries to calculate the perceived complexity of used structures. It follows simple rules:

- ignore structures with multiple combined statements (syntax sugar like `?`)
- increment for each break in the linear flow
- increment for nested structures

To implement this rules the model uses four different types of increments and detailed specification for common structures (for example, multiple Boolean conditions combined with the same operator increase the score only by one). The increments are defined base on human judgement of the understandability of the structures-

Using this notion, complex & nested algorithms are assigned a much higher number than easy `switch-case` structures. The number allows to compare entirely different methods, and promises to allow sensible comparisons on class / application level.

## Mock Design

Avoid using mocks which specify how they are called [as this locks the details of the implementation with the test](https://martinfowler.com/articles/mocksArentStubs.html). Instead use Stubs (answers specific to the test without reacting to input parameters).

```c-sharp
// pseudocode;
var emailServiceStub = new Mock<IEmailService>();
// whenever the SendEmail(string email, string text) method is called, this stub returns true
emailServiceStub.On(p => p.SendEmail, true); 

var serviceUnderTest = new Notifier(emailServiceStub.Stub);
```

Use fluent assertions for easier reading of tests.

```c-sharp
// library: FluentAssertions
var text = "Lorem ipsum";
test.Should().StartWith("Lorem");
```

Name the test methods using one of the following templates:

```c-sharp
SendEmail_WhenNoEmailProvided_ThenThrowException();
GivenNoEmail_WhenSendEmailIsCalled_ThenThrowException();
```

Structure the tests with act, arrange, assert

```c-sharp
// Arrange
var emailService = new EmailService();

// Act
var result = emailService.SendEmail("info@example.com", "hello world");

// Arrange
result.Should().BeTrue();
```