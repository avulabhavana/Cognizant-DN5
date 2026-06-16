# NUnit and Moq Hands-on - Customer Communication Library

## Overview

This project demonstrates Unit Testing in .NET using **NUnit** and **Moq** frameworks.

The application contains a `CustomerComm` class that sends emails to customers through an `IMailSender` dependency. Using dependency injection and mocking, the functionality is tested without sending actual emails.

## Objectives

* Understand Unit Testing concepts.
* Learn Test-Driven Development (TDD) fundamentals.
* Implement automated tests using NUnit.
* Use Moq to mock dependencies.
* Understand loosely coupled and testable design.
* Verify functionality using assertions.

## Technologies Used

* C#
* .NET
* NUnit
* NUnit3TestAdapter
* Moq
* Visual Studio

## Project Structure

```text
CustomerCommSolution
│
├── CustomerCommLib
│   ├── CustomerComm.cs
│   ├── IMailSender.cs
│   └── MailSender.cs
│
└── CustomerComm.Tests
    └── CustomerCommTests.cs
```

## Application Design

### IMailSender Interface

```csharp
public interface IMailSender
{
    bool SendMail(string toAddress, string message);
}
```

### CustomerComm Class

```csharp
public class CustomerComm
{
    private IMailSender _mailSender;

    public CustomerComm(IMailSender mailSender)
    {
        _mailSender = mailSender;
    }

    public bool SendMailToCustomer()
    {
        _mailSender.SendMail(
            "cust123@abc.com",
            "Some Message"
        );

        return true;
    }
}
```

## Unit Test Implementation

The test project uses:

* `[TestFixture]`
* `[OneTimeSetUp]`
* `[TestCase]`
* `Assert.That()`
* `Moq`

### Sample Test

```csharp
[TestCase]
public void SendMailToCustomer_ShouldReturnTrue()
{
    bool result = _customerComm.SendMailToCustomer();

    Assert.That(result, Is.True);
}
```

## Mocking with Moq

A mock object is created for the `IMailSender` dependency:

```csharp
_mockMailSender = new Mock<IMailSender>();

_mockMailSender
    .Setup(x => x.SendMail(It.IsAny<string>(),
                           It.IsAny<string>()))
    .Returns(true);
```

This allows testing without sending real emails.

## Test Result

```text
Total Tests : 1
Passed      : 1
Failed      : 0
Skipped     : 0
```

## Concepts Demonstrated

### Unit Testing

Testing the smallest unit of code in isolation.

### Functional Testing

Testing complete application functionality from a user perspective.

### Automated Testing

Tests execute automatically and validate expected outcomes.

### Loosely Coupled Design

Classes depend on interfaces rather than concrete implementations, making testing easier.

### Mocking

Dependencies are simulated using Moq to isolate the code under test.

## Benefits

* Faster testing
* Better code quality
* Easier maintenance
* Early bug detection
* Improved testability

## Conclusion

This project successfully demonstrates Unit Testing using NUnit and Moq. The CustomerComm class was tested independently by mocking its IMailSender dependency, resulting in reliable and maintainable automated tests.

