# js-notes

<h3> Things I've learned recently </h3>
<ul>
    <li> A .click() event cannot be placed on a object that has not been created.  Its' better to use $(document).on("click", element, funciton() {}); <li>
    <li> One on() function will not overwrite another, even if it's pointed at the same element, you must off() or they will both fire </li>
    <li> To create a div (like a pop up), that covers all, is to create a parten div with position: relative, and the div inside to be position: absolute then use z-index.  Might be able to use both position: relative or absolute, but positions must be applied, or z-index does not work </li>


-Notes taken from books

<h3>Complier Theory</h3>
<ul>
	<li>Tokenizing/Lexing - break up ('var', 'a', '=', '2', and ';')</li>
	<li>Parsing</li>
	<li>Code-Generation</li>
</ul>

<h2>Understanding Scope</h2>
<ol>
  <li>Engine: responsible for compliation and execution</li>
  <li>Compiler: parsing and code-generation</li>
  <li>Scope: collects and maintains a look-up list of all declared identifiers. </li>
</ol>
During `var a = 2;`
<ol>
  <li>Complier declares a variable if not declared already</li>
  <li>Engine then looks up the variable in scopre and assigns to it, if found</li>
</ol>

LHS look-up is trying to find the varaible container(!= the value of container)
RHS look-up is trying to find the value of a variable

`function foo(a) {`
`console.log( a );` The `a` is a RHS declaration
`foo( 2 );` The foo(..) is a RHS declaration, looking for definition of foo

also in 'foo( 2 )', the '2' is passed and a LHS is performed on the 'a', so it can place '2' in it's spot.

<h2> Nested Scope </h2>

A failed RHS error by the Engine will throw a `ReferenceError`.


<h2>this  ????</h2>
<h4><strong>call-stack and call-site</strong></h4>
<p>Excerpt from <a href="https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md"> You Don't Know JS </a></p>
```javascript
function baz() {
    // call-stack is: `baz`
    // so, our call-site is in the global scope

    console.log( "baz" );
    bar(); // <-- call-site for `bar`
}

function bar() {
    // call-stack is: `baz` -> `bar`
    // so, our call-site is in `baz`

    console.log( "bar" );
    foo(); // <-- call-site for `foo`
}

function foo() {
    // call-stack is: `baz` -> `bar` -> `foo`
    // so, our call-site is in `bar`

    console.log( "foo" );
}

baz(); // <-- call-site for `baz`
```

<h4><strong>implicit binding and default binding, confused binding</h4></strong>
```
function foo() {
    console.log( this.a );
}

var obj = {
    a: 2,
    foo: foo
};

function doFunction(fn) {
    fn();
}

var bar = {
    a: 5,
    fooWobj: obj.foo,
    ownFoo: foo,
    ownFoo2: function foo4() { foo(); },
    ownFoo3: function foo5() { obj.foo(); },
    ownFoo4: function foo6() { bar.ownFoo(); },
    ownFoo5: doFunction( bar.ownFoo4 ),
    obj: obj
};

var a = "global a"; // `a` also property on global object

bar.fooWobj(); //5
bar.ownFoo(); //5
bar.ownFoo2(); //global a (why???)
bar.ownFoo3(); //2
bar.ownFoo4(); //5

doFunction( obj.foo );  //global a
doFunction( bar.ownFoo ); //global a
doFunction( bar.ownFoo2 ); //global a
doFunction( bar.fooWobj ); //global a

bar.ownFoo5;
```

Here the doFunction is global a global function, which points <em>this</em> to the global object.

Function foo4 through foo6, do the same as running the function on it's own.  <em> this will point to the calling function or global object as in the case of foo4.

----

<h2>LHS</h2> - looks to see if **variable container** exists
<h2>RHS</h2> - looks up the **value** of a variable

Now, if a variable is found for an RHS look-up, but you try to do something with its value that is impossible, such as trying to execute-as-function a non-function value, or reference a property on a null or `undefined` value, then Engine throws a different kind of error, called a `TypeError`.

`ReferenceError` - cannot find variable
`TypeError` - found in Scope, but illegal/impossible action

-------------

JavaScript engine first compiles code before it executes
it splits up statmes like `var a = 2'` into two separate steps:

1. First, `var a` to declare it in that Scope.  This is performed at the beginning, before code execution.

2. Later, `a = 2` to look up the variable (LHS reference) and assign to it if found.

Unfulfilled RHS result in `ReferenceError`
Unfulfilled LHS reult in an automatic, implciitly-created global of that name or a `ReferenceError` (if in StrictMode).

==================================

<h1>Chapter 2:Lexical Scope</h1>

<h2>Lex-time</h2>
Lexical scope is scope that is defined at lexing time.  It is (mostly) set in stone by the time the lexer processes your code.
