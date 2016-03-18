# To Do

Write a tool to publish packages. Does this presume we have some sort of spec file, or do we go
the route of reading repository trees and reasoning about it? Specs are easier for the tool
writer but extra work for the package creator. The working plan is "specs are optional and are
used to override defaults".

Write something to find predefined symbols - any place in the code where an `#ifdef` or
`#if defined(SYMBOL)` are used, and that symbol wasn't previously defined in the code. Yes this
means writing a subset of a preprocessor. Can't be that hard.

Write code that figures out what search paths must be used; look at #include PATH lines and find
those files and create paths relative to some predeclared base ("root of project").
