# Architecture

the architecture should serve its users, and hence must be adapted first to the skills and needs of the programmers actually working with it.

for small projects:
- abstract messy details of subproblems (UI, export, ...)
- prefer passing state around (rather than some form of global state)
- prefer injecting functionality (rather than passing it around)
- cling to existing guidelines (given by framework) & naming (like schema.org)
- avoid dependencies for trivial functionalities (rather copy them into project)
