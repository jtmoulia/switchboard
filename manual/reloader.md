

# Module reloader #
* [Description](#description)
* [Function Index](#index)
* [Function Details](#functions)


Erlang module for automatically reloading modified modules
during development.
Copyright (c) 2007 Mochi Media, Inc.

__Behaviours:__ [`gen_server`](gen_server.md).

__Authors:__ Matthew Dempsky ([`matthew@mochimedia.com`](mailto:matthew@mochimedia.com)).
<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#all_changed-0">all_changed/0</a></td><td>Return a list of beam modules that have changed.</td></tr><tr><td valign="top"><a href="#code_change-3">code_change/3</a></td><td>gen_server code_change callback (trivial).</td></tr><tr><td valign="top"><a href="#handle_call-3">handle_call/3</a></td><td>gen_server callback.</td></tr><tr><td valign="top"><a href="#handle_cast-2">handle_cast/2</a></td><td>gen_server callback.</td></tr><tr><td valign="top"><a href="#handle_info-2">handle_info/2</a></td><td>gen_server callback.</td></tr><tr><td valign="top"><a href="#init-1">init/1</a></td><td>gen_server init, opens the server in an initial state.</td></tr><tr><td valign="top"><a href="#is_changed-1">is_changed/1</a></td><td>true if the loaded module is a beam with a vsn attribute
and does not match the on-disk beam file, returns false otherwise.</td></tr><tr><td valign="top"><a href="#reload_modules-1">reload_modules/1</a></td><td>code:purge/1 and code:load_file/1 the given list of modules in order,
return the results of code:load_file/1.</td></tr><tr><td valign="top"><a href="#start-0">start/0</a></td><td>Start the reloader.</td></tr><tr><td valign="top"><a href="#start_link-0">start_link/0</a></td><td>Start the reloader.</td></tr><tr><td valign="top"><a href="#stop-0">stop/0</a></td><td>Stop the reloader.</td></tr><tr><td valign="top"><a href="#terminate-2">terminate/2</a></td><td>gen_server termination callback.</td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="all_changed-0"></a>

### all_changed/0 ###


<pre><code>
all_changed() -&gt; [atom()]
</code></pre>

<br></br>


Return a list of beam modules that have changed.
<a name="code_change-3"></a>

### code_change/3 ###


<pre><code>
code_change(Vsn::_OldVsn, State, Extra::_Extra) -&gt; State
</code></pre>

<br></br>


gen_server code_change callback (trivial).
<a name="handle_call-3"></a>

### handle_call/3 ###


<pre><code>
handle_call(Req::Args, From, State) -&gt; tuple()
</code></pre>

<br></br>


gen_server callback.
<a name="handle_cast-2"></a>

### handle_cast/2 ###


<pre><code>
handle_cast(Req::Cast, State) -&gt; tuple()
</code></pre>

<br></br>


gen_server callback.
<a name="handle_info-2"></a>

### handle_info/2 ###


<pre><code>
handle_info(Info, State) -&gt; tuple()
</code></pre>

<br></br>


gen_server callback.
<a name="init-1"></a>

### init/1 ###


<pre><code>
init(X1::[]) -&gt; {ok, State}
</code></pre>

<br></br>


gen_server init, opens the server in an initial state.
<a name="is_changed-1"></a>

### is_changed/1 ###


<pre><code>
is_changed(M::atom()) -&gt; boolean()
</code></pre>

<br></br>


true if the loaded module is a beam with a vsn attribute
and does not match the on-disk beam file, returns false otherwise.
<a name="reload_modules-1"></a>

### reload_modules/1 ###


<pre><code>
reload_modules(Modules::[atom()]) -&gt; [{module, atom()} | {error, term()}]
</code></pre>

<br></br>


code:purge/1 and code:load_file/1 the given list of modules in order,
return the results of code:load_file/1.
<a name="start-0"></a>

### start/0 ###


<pre><code>
start() -&gt; ServerRet
</code></pre>

<br></br>


Start the reloader.
<a name="start_link-0"></a>

### start_link/0 ###


<pre><code>
start_link() -&gt; ServerRet
</code></pre>

<br></br>


Start the reloader.
<a name="stop-0"></a>

### stop/0 ###


<pre><code>
stop() -&gt; ok
</code></pre>

<br></br>


Stop the reloader.
<a name="terminate-2"></a>

### terminate/2 ###


<pre><code>
terminate(Reason, State) -&gt; ok
</code></pre>

<br></br>


gen_server termination callback.
