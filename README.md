
# Overview

Interface between MPI (the Message Passing Interface standard) and the Lua
scripting language.


# Example usage

```lua
local MPI = require 'MPI'
local buffer = require 'buffer'

local size = buffer.new_buffer(buffer.sizeof(buffer.int))
local rank = buffer.new_buffer(buffer.sizeof(buffer.int))

MPI.Init()
MPI.Comm_rank(MPI.COMM_WORLD, rank)
MPI.Comm_size(MPI.COMM_WORLD, size)

print(buffer.get_typed(rank, buffer.int, 0))
print(buffer.get_typed(size, buffer.int, 0))

MPI.Finalize()
```


# Build instructions

Make sure you have the MPI sources installed.

You can do it in Linux like this for example:

```bash
apt install mpich
```

Check you have `mpicc`

Create a file called `Makefile.in` which contains macros like these:

```
CC = mpicc
LUA_HOME = /path/to/lua-5.2.1
LVER = lua-5.2.1 # can be lua-5.1 or other
```

In this case, `path/to/lua-5.2.1` must contain a compiled lua with the `-fPIC` flag.

Run `make`.

Optionally, you may install local Lua sources by typing `make lua`.

In this casa, your `Makefile.in` will be something like this:

```
CC = mpicc
LUA_HOME = ./lua-5.2.1
LVER = lua-5.2.1 # can be lua-5.1 or other
```


# License

This code is made freely available for anybody's use. I only ask that if you
find it useful, please send me an email about how it works, and in what project
you are using it.


The Lua MPI wrappers are licensed under the same terms as Lua itself.

Copyright (c) 2012, Jonathan Zrake <jonathan.zrake@gmail.com> & Dorian Krause

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
