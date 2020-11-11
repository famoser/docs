# Patterns

useful to make program easier understandable & maintainable.

resources:
- https://sourcemaking.com/ for patterns

## Builder

to create complex structures where only some part matters in the context it is used.

Primarily used for testing, the builder provides a default structure, where the test-relevant parts can be set explicitly, but without the need to setup the other parts of the structure.

### Example

```c-sharp
class PersonBuilder
{
    private Person _entity;
    public PersonBuilder()
    {
        this._entity = new Person()
        {
            GivenName = "Martin",
            FamilyName = "Fowler",
            PreferredColor = "Green"
        }
    }

    public PersonBuilder WithGivenName(string givenName)
    {
        this._entity.GivenName = givenName;

        return this;
    }

    public Person Build()
    {
        return this._entity;
    }
}
```

```c-sharp
[TestClass]
class EmailServiceTest
{
    [TestMethod]
    public void FullNameShouldStartWithGivenName()
    {
        // Arrange
        var person = new PersonBuilder().WithGivenName("Dorthe").Build();

        // Act
        var fullName = person.GetFullName();

        // Arrange
        fullName.Should().StartWith("Dorthe");
    }

}
```

### Experiences

Do create realistic structures as close to the business case as possible. This makes reading and debugging easier.

Do not assume anything about the structures returned by the builder. This avoids duplication of business logic inside the builders and ensures the test explicitly configures the structure.