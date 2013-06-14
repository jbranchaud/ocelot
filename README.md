# ocelot

![Babou the Ocelot](http://i.imgur.com/nYZjBZQ.jpg)

*"Because you're awesome!"*

---

ocelot is a commit annotation language for version systems like git, hg, and
SVN.

The standard syntax primarily allows it to be written and read by machines,
but it is simple enough for humans to easily read and write as well.

## Getting Started

While the ocelot specification is still a work in progress and there is no
GUI tool for generating ocelot commit annotations, you can still write
commits with ocelot annotations manually. In fact, because of ocelot's
simplicity this is a recommended approach.

When it is time to write your commit message, you can start with a short
one-liner identifying the overall purpose of that commit (optional).

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

    [src/shapes/Square.java]
    Adding the basis for the Square class, but it is still missing some
    functionality like an area function.
    [src/shapes/Rectangle.java]
    Also adding the Rectangle class which inherits form the existing Shape
    class.
