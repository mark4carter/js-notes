# js-notes

-Notes taken from books

<h3>Complier Theory</h3>
<ul>
	<li>Tokenizing/Lexing</li>
	<li>Parsing</li>
	<li>Code-Generation</li>
</ul>

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

