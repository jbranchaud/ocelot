# Ocelot v0.1.0

a versioning system commit annotation DSL

By [Josh Branchaud](http://joshbranchaud.com) and Corey Jergensen

This spec is unstable and will likely change significantly until 1.0 is
reached.

## Objectives

Ocelot aims to be a simple and intuitive domain-specific language for
annotating commits that is both human and machine writable and readable. It
aims to easly map to both
[markdown](http://daringfireball.net/projects/markdown/)
and [YAML](http://www.yaml.org/) so as to be as familiar as possible.
Ocelet will make it easier to encode information in a standard commit
message that details the parts of the commit message that are associated
with particular files as well as what file artifacts in a commit are related
to one another and how.

## Example

Consider a set of changes that are being committed involving the following
files:

    Commit
    Message: "Adding the abstract area method to shape as well as an
    implementation of that method in Square. Also, removed some print
    statements from the util class."
    Files:
    > Shape.java
    > Square.java
    > Utility.java

The above is an example of a standard commit with a few changed files and a
brief commit message that details the changes. Unfortunately, this commit
contains two distinct changes that are not really related in any way. If you
carefully read the commit message and look at the actual changes, you may be
able to see the difference and understand the distinct tasks being
completed. However, an automated approach (such as software repository
miners) will be hard pressed to make this distinction and for more involved
changes, even a human could struggle to understand what's involved in the
commit. Using a simple DSL, we can allow the commmitter to include this
information in their commit message. Consider the following commit message
with Ocelot annotations:

    ---
    [Shape.java|Square.java]
    Adding the abstract area method to shape and a concrete implementation
    of that method to the Square class.
    [Utility.java]
    Removing some print statements that aren't needed anymore.
    ...

With this minimal annotation, we can now understand which parts of the
commit message belong to which artifacts. We also learn that the changes to
`Shape.java` and `Square.java` are unrelated to the changes made to
`Utility.java`. Furthermore, we can also infer a relationship between
`Shape.java` and `Square.java` since they were changed together.

## Specification


