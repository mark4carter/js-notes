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

