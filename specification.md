# Ocelot v0.4.0

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

    [Shape.java|Square.java]
    Adding the abstract area method to shape and a concrete implementation
    of that method to the Square class.
    [Utility.java]
    Removing some print statements that aren't needed anymore.

With this minimal annotation, we can now understand which parts of the
commit message belong to which artifacts. We also learn that the changes to
`Shape.java` and `Square.java` are unrelated to the changes made to
`Utility.java`. Furthermore, we can also infer a relationship between
`Shape.java` and `Square.java` since they were changed together.

## Specification

The specification for the Ocelot DSL. The markdown equivalent has been
redacted, though most markdown syntax will still be valid within the
comments.

### General Message

For part of the commit message that isn't specific to any particular
artifact, the text should be put at the beginning of the Ocelot annotation
(or optionally after empty brackets).

#### At the beginning (preferred)

    This commit involves refactorings over parts of the codebase.
    # the rest of the annotations

#### After empty brackets

    # some annotations
    []
    This commit involves refactorings over parts of the codebase.

### Single File Annotation

For annotating a single file with some message, wrap the project-relative
path in brackets and then follow with the message:

    [src/zoo/cats/Ocelot.java]
    Adding some great functionality that should increase performance.

Duplicate annotations essentially indicate a separate annotation for the same
file.

    [src/zoo/cats/Ocelot.java]
    Adding some great functionality that should increase performance.
    [src/zoo/cats/Ocelot.java]
    Refactoring the Ocelot constructor.

Alternate approach using the list syntax from markdown.

    [src/zoo/cats/Ocelot.java]
    - Adding some great functionality that should increase performance.
    - Refactoring the Ocelot constructor.

### Multi-File Annotation

    [src/repo/Blob.rb|src/repo/Tree.rb]
    Creating the Blob class and Tree class for my repository project.

### File Relationship Annotation

    [src/repo/Tree.rb=src/repo/Blob.rb]
    The Tree now has a collection of blobs which have been refactored.

### Uni-directional File Relationship Annotation

    [_config.yml=>README.md]
    The config file now ignores the README file.

### Bi-directional File Relationship Annotation

    [WhiteBox.py<=>BlackBox.py]
    Describe some bi-directional relationship here.

This annotation seems to be the same as the *File Relationship Annotation*,
it will be interesting to see if there is a distinction that can be made
between the two.

## Experimental Features

Here are some potential Ocelot features that are more experimental at the
moment. These are things that don't have a specific use case in mind, but
could prove useful in keeping the language extensible.

### Grouped Artifacts

This involves wrapping two or more artifacts in parentheses in order to say
that they are grouped together with respect to some relationship.

    [Shape.java=(Square.java|Rectangle.java)]
    Some message about Shape's relationship to Square and Rectangle for this
    change set.
