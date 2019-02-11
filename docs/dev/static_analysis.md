# Static analysis

Automatic eyes on your code; mostly cheap and helpful.

## Cyclomatic complexity

assigns a number to a method resemblingy the complexity.

This number can be used to identify complex methods which need a refactoring. The number is calculated using the control flow graph, and represents the number of linearly independent paths (for two following `if-else` constructs, the number would be three; two for the first `if-else`, and one to cover the possibly missed block of the second `if-else`).

## Cognitive complexity

tries to enhance cyclomatic complexity to better resemble understandability.

The definition of cognitive complexity is no longer a mathematical model: It tries to calculate the perceived complexity of used structures. It follows simple rules:

- ignore structures with multiple combined statements (syntax sugar like `?`)
- increment for each break in the linear flow
- increment for nested structures

To implement this rules the model uses four different types of increments and detailed spezification for  common structures (for example, multiple boolean conditions combined with the same operator increase the score only by one). The increments are defined base on human judgement of the understandability of the strucutres-

Using this notion, complex & nested algorithms are assigned a much higher number than easy `switch-case` structures. The number allows to compare entirely different methods, and promises to allow sensible comparisons on class / application level.
