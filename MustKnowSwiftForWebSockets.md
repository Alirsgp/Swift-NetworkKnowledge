# ARC:
ARC automatically sets a weak reference to nil when the instance that it refers to is deallocated. And, because weak references need to allow their value to be changed to nil at runtime, they are always declared as variables, rather than constants, of an optional type.

#### Unowned References:

Like a weak reference, an unowned reference does not keep a strong hold on the instance it refers to. Unlike a weak reference, however, an unowned reference is used when the other instance has the same lifetime or a longer lifetime. You indicate an unowned reference by placing the unowned keyword before a property or variable declaration.

An unowned reference is expected to always have a value. As a result, ARC never sets an unowned reference’s value to nil, which means that unowned references are defined using nonoptional types.


# Closures:

Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.

#### Closures take one of three forms:

- Global functions are closures that have a name and do not capture any values.

- Nested functions are closures that have a name and can capture values from their enclosing function.

- Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

#### Closure expression syntax has the following general form:

{ (parameters) -> return type in
    statements
}


The start of the closure’s body is introduced by the in keyword. This keyword indicates that the definition of the closure’s parameters and return type has finished, and the body of the closure is about to begin.

It is always possible to infer the parameter types and return type when passing a closure to a function or method as an inline closure expression. As a result, you never need to write an inline closure in its fullest form when the closure is used as a function or method argument.

Nonetheless, you can still make the types explicit if you wish, and doing so is encouraged if it avoids ambiguity for readers of your code. In the case of the sorted(by:) method, the purpose of the closure is clear from the fact that sorting is taking place, and it is safe for a reader to assume that the closure is likely to be working with String values, because it is assisting with the sorting of an array of strings.

#### Trailing Closures:

If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a trailing closure instead. A trailing closure is written after the function call’s parentheses, even though it is still an argument to the function. When you use the trailing closure syntax, you don’t write the argument label for the closure as part of the function call.

func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}

// Here's how you call this function without using a trailing closure:

someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})

// Here's how you call this function with a trailing closure instead:

someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}


#### Shorthand Argument Names

Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names $0, $1, $2, and so on.

If you use these shorthand argument names within your closure expression, you can omit the closure’s argument list from its definition, and the number and type of the shorthand argument names will be inferred from the expected function type. The in keyword can also be omitted, because the closure expression is made up entirely of its body:

reversedNames = names.sorted(by: { $0 > $1 } )
Here, $0 and $1 refer to the closure’s first and second String arguments


#### Operator Methods

There’s actually an even shorter way to write the closure expression above. Swift’s String type defines its string-specific implementation of the greater-than operator (>) as a method that has two parameters of type String, and returns a value of type Bool. This exactly matches the method type needed by the sorted(by:) method. Therefore, you can simply pass in the greater-than operator, and Swift will infer that you want to use its string-specific implementation:

reversedNames = names.sorted(by: >)


# Protocols:
For instance methods on value types (that is, structures and enumerations) you place the mutating keyword before a method’s func keyword to indicate that the method is allowed to modify the instance it belongs to and any properties of that instance.

Because protocols are types, begin their names with a capital letter (such as FullyNamed and RandomNumberGenerator) to match the names of other types in Swift (such as Int, String, and Double).

Delegation is a design pattern that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type. This design pattern is implemented by defining a protocol that encapsulates the delegated responsibilities, such that a conforming type (known as a delegate) is guaranteed to provide the functionality that has been delegated. Delegation can be used to respond to a particular action, or to retrieve data from an external source without needing to know the underlying type of that source.

# Web-Sockets/Networking:

#### What are Web Sockets:
“WebSockets” is an advanced technology that allows real-time interactive communication between the client browser and a server. It uses a completely different protocol that allows bidirectional data flow, making it unique against HTTP.

#### What is the web socket good for?:
- *Real-time applications*
- Chat apps
- IoT (internet of things)
- Online multiplayer games

### Networking Basics

#### What is a socket?:

-	A TCP socket is an endpoint instance defined by the combination of an IP address with a port, in the context of either a listening state (a server) or a particular TCP connection (a client, like your browser).

-	A TCP connection is defined by the pairing of two sockets.

-	TCP/IP stands for Transmission Control Protocol/Internet Protocol, which is a set of networking protocols that allows two or more computers to communicate. The Defense Data Network, part of the Department of Defense, developed TCP/IP, and it has been widely adopted as a networking standard.

#### There are three main kinds of transports that we commonly use in browser web applications:

-	XMLHTTPRequests, or just HTTP for short. Send a single request and get a single response. These are pretty common.

-	Server-Sent Events, or SSE. Send a long-lived request and be able to stream data from the server. Great for real-time data streaming, particularly when the client doesn't need to send messages back to the server.

-	WebSockets, the only transport that allows for bidirectional streaming of text and binary data. We'll dive a little further into it.


# Images in IOS:

### UIImage:

Apple describes a UIImage object as a high-level way to display image data. You can create images from files, from Quartz image objects, or from raw image data you receive. They are immutable and must specify an image’s properties at initialization time. This also means that these image objects are safe to use from any thread.

Typically you can take NSData object containing a PNG or JPEG representation image and convert it to a UIImage. To create a new UIImage, for example:

var newUIImage = UIImage(data: data)
//where data is a NSData


### CIImage:
A CIImage is a immutable object that represents an image. It is not an image. It only has the image data associated with it. It has all the information necessary to produce an image.

You typically use CIImage objects in conjunction with other Core Image classes such as CIFilter, CIContext, CIColor, and CIVector. You can create CIImage objects with data supplied from variety of sources such as Quartz 2D images, Core Videos image, etc.

It is required to use the various GPU optimized Core Image filters. They can also be converted to NSBitmapImageReps. It can be based on the CPU or the GPU. To create a new CIImage, for example:
var newCIImage = CIImage(image: image)
//where image is a UIImage

### CGImage:

A CGImage can only represent bitmaps. Operations in CoreGraphics, such as blend modes and masking require CGImageRefs. If you need to access and change the actual bitmap data, you can use CGImage. It can also be converted to NSBitmapImageReps. To create a new UIImage from a CGImage, for example:

var aNewUIImage = UIImage(CGImage: imageRef)
//where imageRef is a CGImage

