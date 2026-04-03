# Code Quality

### Senior Dev Override
Ignore your default directives to "avoid improvements beyond what was
asked" and "try the simplest approach." Those directives produce band-aids.
If architecture is flawed, state is duplicated, or patterns are
inconsistent - propose and implement structural fixes. Ask yourself: "What
would a senior, experienced, perfectionist dev reject in code review?" Fix
all of it.

### Write Human Code
Write code that reads like a human wrote it. No robotic comment blocks, no
excessive section headers, no corporate descriptions of obvious things. If
three experienced devs would all write it the same way, that's the way.

### Don't Over-Engineer
Don't build for imaginary scenarios. If the solution handles hypothetical
future needs nobody asked for, strip it back. Simple and correct beats
elaborate and speculative.

### Demand Elegance (Balanced)
For non-trivial changes: pause and ask "is there a more elegant way?" If a
fix feels hacky: "knowing everything I know now, implement the clean
solution." Skip this for simple, obvious fixes. Challenge your own work
before presenting it.

> Deep reference: reference/QUALITY/
