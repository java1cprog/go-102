# Go 102 Workshop

## 2. Object-Oriented Programming in Go

From the [Go FAQ](https://golang.org/doc/faq#Is_Go_an_object-oriented_language):

> Is Go an object-oriented language?  Yes and no.

Go has no classes or type hierarchy, no inheritance or subclassing, and
no explicit interfaces. But Go has types and methods and allows an
object-oriented style of programming.

OO is a software design philosophy, based around the concept of modelling
real-world or abstract "objects" in code.  There are four primary principles
that are generally cited as a requirement for a language to be "object
oriented":

1. *Abstraction* is the concept of exposing only the essential characteristics
   and behaviour of an object to a collaborator, so as to provide a simple
   external interface.

1. *Encapsulation* is complementary to abstraction.  Whereas abstraction
   focuses on the observable behaviour of an object, encapsulation focuses on
   the implementation of that object which gives rise to the behaviour, through
   the wrapping of data and behaviour into a single unit (usually a class).

1. *Inheritance* is a method of code reuse, and is the ability for a class to
   "inherit" features of another class through subclassing.

1. *Polymorphism* is the application of a single interface to objects of
   different types.

Although these principles are taken by many to be absolutely essential for any
language which claims to support OOP, we're going to scale things back.  At the
simplest level, OOP is about objects.  There are numerous definitions of "an
object" in terms of software, but we'll use the following simple definition:

> An object is a data structure that has both state and behaviour.

Go's type system and the ability to create methods on types gives us the
ability to create these "objects," so let's see how it's done.


### Methods

Given our previous definition of an object, a custom `struct` type can contain
the state (data) of an object.  But what about the behaviour?  That behaviour
is provided by _methods_.

Let's create a `Rectangle` type, with a width and a height. From this, it's
simple to calculate the area, so let's write a function to do that.

```go
type Rectangle struct {
	Width  int
	Height int
}

func Area(r Rectangle) int {
	return r.Width * r.Height
}

func main() {
	r := Rectangle{3, 4}
	fmt.Println(Area(r))    // area 12
}
```

It works as expected, but now we need to either repeat the calculation or copy
the function everywhere we want to calculate the area.  We can solve this by
turning the function into a method.

> A method is a function that is bound to a receiver.

Go does not have classes, but you can define methods on any type.  The method
receiver appears in its own argument list between the func keyword and the
method name.

```go
type Rectangle struct {
	Width  int
	Height int
}

func (r Rectangle) Area() int {
	return r.Width * r.Height
}

func main() {
	r := Rectangle{3, 4}
	fmt.Println(r.Area())   // area 12
}
```

Comparing the two versions, it's a very simple, yet powerful change.

```go
// function, called with Area(r)
func Area(r Rectangle) int {
	return r.Width * r.Height
}

// method, called with r.Area()
func (r Rectangle) Area() int {
	return r.Width * r.Height
}
```

It's actually worth pointing out that the `method` version is effectively just
syntactic sugar: under the hood it takes the receiver and puts it as the first
argument, just as happens in the function version.

#### Exercise #2

> Declare a new struct type to hold information about a tennis player,
> including the number of matches played and the number won.  Add a method to
> this type that calculates the win ratio for the player.  Create a new player,
> and output the win ratio for them.


### Interfaces

...

### Embedding

...

### Composition

...

> Everyone knows composition is more powerful than inheritance, Go just makes
> this non optional.
-- http://dave.cheney.net/2015/11/15/the-legacy-of-go