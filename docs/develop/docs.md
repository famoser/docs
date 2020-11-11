## documentation

document at various granularities, including the justifications behind design decisions.
document how business rules or non-functional requirements (like performance) impacted the argument and why.
for big applications & home-made architectures, you may want to document additional parts as described by Code Complete (Steve Connel), p45.

define error processing:
- corrective (try to continue) / detective (fail)
- active (plausibility checks) / passive (fail if no way to continue)
- propagation (fail at first invalid input or after checking all)
- consistent error messages

be aware of the stability of the environment and take precautions (experimental technologies need a time buffer to account for bugs in tooling).

define code style, tool chain, testing approach (TDD or similar) and definition of done. use conventions to prevent religious wars.

explicitly separate project-specific and general expert knowledge  
write in the form of Tutorials, How-To Guides, Explanations or References.
