## General Information

### Project Information

Moon-Moon is an IRC bot run with the Lua programming language; however,
the syntax used in the development version is called 'MoonScript' - this
syntax can be compiled using Leafo's MoonScript program `moonc` and then
loaded as Lua bytecode.

### Dependencies

[Lua](http://www.lua.org)

[LuaRocks](https://luarocks.org) (recommended)

[MoonScript](https://moonscript.org)

[pgmoon](https://github.com/RyanSquared/pgmoon)

[basexx](https://github.com/aiq/basexx)

[cqueues](http://25thandclement.com/~william/projects/cqueues.html)

[luafilesystem](https://keplerproject.github.io/luafilesystem/)

## Getting Started

### Installing Dependencies with LuaRocks

To install rocks locally, pass the `--local` flag to the `luarocks` command.
This downloads and installs rocks to a local directory without requiring
access to system directories. LuaRocks is recommended to allow for easy
installation of all the required software.

```sh
$ luarocks install basexx
$ luarocks install cqueues
$ luarocks install luafilesystem
$ luarocks install moonscript
```

### Configuration

Lua is used as a configuration language; bots must each have their own separate
`.lua` file in `$XDG_CONFIG_HOME/moonmoon` (which defaults to `$HOME/.config`).

```lua
bot "#!" {
	server = "irc.hashbang.sh";
	port = 6697; -- TLS is automatically set if port == 6697
	autojoin = {
		"#!FusionScript";
	};
};
```

## The Coroutine System

Moon Moon takes advantage of a coroutine-based asynchronous system which
allows the software to have multiple things "running" at once - it's
almost like having a threaded program, without threads. This offers some
advantages:

 1. A single Lua state
 2. Fewer callbacks
 3. Cleaner code base

Adding in a routine to the queue is simple, as demonstrated by the below
examples programmed in MoonScript and Lua for convenience:

**MoonScript**

```moonscript
cqueues = require 'cqueues'
queue   = require 'queue'

queue\wrap ->
	while true
		cqueues.sleep 5
		print 'Hello, World!'
```

**Lua**

```lua
local cqueues = require("cqueues")
local queue   = require("queue")
queue:wrap(function()
	while true do
		cqueues.sleep(5)
		print("Hello, World!")
	end
end)
```
