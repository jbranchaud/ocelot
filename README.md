# ocelot

![Babou the Ocelot](http://i.imgur.com/nYZjBZQ.jpg)

*"Because you're awesome!"*

---

ocelot is a commit annotation language for version systems like git, hg, and
SVN.

The standard syntax primarily allows it to be read and written by machines,
but it is simple enough for humans to easily read and write as well.

## Getting Started

While the ocelot specification is still a work in progress and there is no
GUI tool for generating ocelot commit annotations, you can still write
commits with ocelot annotations manually. In fact, because of ocelot's
simplicity this is a recommended approach.

When it is time to write your commit message, you can start with a short
one-liner identifying the overall purpose of that commit.

    Adding a couple new shapes to this project.

You'll then want to describe the changes associated with key artifacts.

    [src/shapes/Square.java]
    Adding the basis for the Square class, but it is still missing some
    functionality like an area function.
    [src/shapes/Rectangle.java]
    Also adding the Rectangle class which inherits form the existing Shape
    class.

Now, if there are relationships between the files worth mentioning, you will
want to include those next.

    [src/shapes/Square.java=src/shapes/Rectangle.java]
    Square inherits from Rectangle.

The commit message in full ultimately might look something like this:

    Adding a couple new shapes to this project.
    [src/shapes/Square.java]
    Adding the basis for the Square class, but it is still missing some
    functionality like an area function.
    [src/shapes/Rectangle.java]
    Also adding the Rectangle class which inherits form the existing Shape
    class.
    [src/shapes/Square.java=src/shapes/Rectangle.java]
    Square inherits from Rectangle.

This is a rather verbose message that is only made necessary by rather
complex commits. The same commit could be annotated more concisely like so:

    Adding a couple new shapes to this project.
    [src/shapes/Square.java]
    Adding the basis for the Square class, but it is still missing some
    functionality like an area function.
    [src/shapes/Rectangle.java]
    Also adding the Rectangle class which inherits form the existing Shape
    class.

## Benefits

There are a number of benefits that we believe will be gained through
committing to the use of ocelot annotations in commit messages:

- Helps the committer think more deeply about the commit, the relevant
  artifacts, and the way it is all communicated.

- Makes commits easier to understand and conceptualize for other developers
  (for example, during code reviews).

- Embeds more metadata in commit messages which will utlimately improve the
  results of software repository data mining.

## Feedback

At this stage in the ocelot project as we continue to refine the
specification, we both welcome and need feedback from those that are brave
enough to use it.

If you have thoughts or questions about specific features of the language
as well as more general comments, open a new GitHub issue and detail your
thoughts.

Everything is fair game!
