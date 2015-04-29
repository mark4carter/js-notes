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