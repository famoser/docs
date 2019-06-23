# Testing

Be a tester, do not be a checker. Automate everything you can if it can be done in reasonable time.

## Experiences

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