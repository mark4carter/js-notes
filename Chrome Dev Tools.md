<h1>Chrome DevTools</h1><br>
A. JQuery in console will return an array
--1. $('date')
--2. Should use $('date')[0]
B.  Inspect Method -inspect()
--1.  inspect($('date')[0])
--2.  DevTools keeps a history of elements you have selected
----a.  $0 brings the last element $1 bring the selection before that
C.  Debugger
--1.  Pressing on the {} will help 'prettify' minified code
--2.  Pressing the pause button a second time will only pause on caught exceptions
--3.  If you click a line number, it inserts a break at that line number
--4.  Resources will show local storage
--5.  In Network tab, you can press shift-f5 to reload all and temp disable cache
D.  Network
--1.  Google closure (closure compiler) can be used to minify
--2.  CSS should be loaded before JavaScript
--3.  Scaled down images before user downloads
E.  Rendering Performance
--1.  Timeline will show fps
--2.  Profiles tab will record what parts of JavaScript take how much CPU time
--3.  Memory leaks
-----a.  Create profile in memory will show if there is a memory leak
-----b.  HeapSnapshot
-------I.   Profiles -> Take Heap Snapshot 
-------II.  Switch view to comparison after takingsecond shot
