

# Module imap #
* [Description](#description)
* [Data Types](#types)
* [Function Index](#index)
* [Function Details](#functions)


An RFC 3501 IMAP Client.
Copyright (c) Copyright (c) 2014, ThusFresh, Inc.

__Behaviours:__ [`gen_server`](gen_server.md).

__Authors:__ Thomas Moulia ([`jtmoulia@pocketknife.io`](mailto:jtmoulia@pocketknife.io)).

__References__* See [RFC 3501](http://tools.ietf.org.md/rfc3501).

<a name="description"></a>

## Description ##



Binaries are used for string-like data.



To allow the imap connection to be properly setup before usage,
there are some lifecycle hooks: a cmds opt specifies a list of
commands which are executed in order in a separately spawned thread


the post_init_callback opt is a function that is run once all cmds
have been completed.

<a name="types"></a>

## Data Types ##




### <a name="type-account">account()</a> ###



<pre><code>
account() = binary()
</code></pre>



  connspec() specifies a tcp connection, see gen_tcp:connect args



### <a name="type-auth">auth()</a> ###



<pre><code>
auth() = <a href="#type-auth_plain">auth_plain()</a> | <a href="#type-auth_xoauth2">auth_xoauth2()</a>
</code></pre>





### <a name="type-auth_plain">auth_plain()</a> ###



<pre><code>
auth_plain() = {plain, Username::binary(), Password::binary()}
</code></pre>





### <a name="type-auth_xoauth2">auth_xoauth2()</a> ###



<pre><code>
auth_xoauth2() = {xoauth2, Account::binary(), AccessToken::binary() | {RefreshToken::binary(), RefreshUrl::binary()}}
</code></pre>





### <a name="type-cmd">cmd()</a> ###



<pre><code>
cmd() = {login, <a href="#type-auth">auth()</a>} | list | {list, binary(), binary()} | {status, <a href="#type-mailbox">mailbox()</a>} | {status, <a href="#type-mailbox">mailbox()</a>, [binary()]} | {examine, <a href="#type-mailbox">mailbox()</a>} | {select, <a href="#type-mailbox">mailbox()</a>} | {search, iodata()} | {fetch, <a href="#type-seqset">seqset()</a>} | {fetch, <a href="#type-seqset">seqset()</a>, [binary()]} | {uid, {fetch, <a href="#type-seqset">seqset()</a>}} | {uid, {fetch, <a href="#type-seqset">seqset()</a>, [binary()]}} | noop | idle
</code></pre>





### <a name="type-cmd_opt">cmd_opt()</a> ###



<pre><code>
cmd_opt() = {dispatch, fun((<a href="#type-response">response()</a>) -&gt; ok)}
</code></pre>





### <a name="type-connspec">connspec()</a> ###



<pre><code>
connspec() = {ssl | plain, Host::binary(), Port::integer()} | {ssl | plain, Host::binary(), Port::integer(), Options::list()} | {ssl | plain, Host::binary(), Port::integer(), Options::list(), Timeout::integer()}
</code></pre>





### <a name="type-imap_term">imap_term()</a> ###



<pre><code>
imap_term() = binary() | integer() | {string, binary()} | [<a href="#type-imap_term">imap_term()</a>] | nil | '[' | ']'
</code></pre>





### <a name="type-mailbox">mailbox()</a> ###



<pre><code>
mailbox() = binary()
</code></pre>





### <a name="type-opt">opt()</a> ###



<pre><code>
opt() = {init_callback, fun(() -&gt; ok)} | {post_init_callback, fun(() -&gt; ok)} | {cmds, [{cmd, <a href="#type-cmd">cmd()</a>}]}
</code></pre>





### <a name="type-response">response()</a> ###



<pre><code>
response() = {'*' | '+' | 'OK' | 'NO' | 'BAD', <a href="#type-imap_term">imap_term()</a>}
</code></pre>





### <a name="type-seqset">seqset()</a> ###



<pre><code>
seqset() = '*' | integer() | [integer()] | {integer() | none, integer() | none}
</code></pre>


<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#auth_to_props-1">auth_to_props/1</a></td><td>Returns the auth as a jsx:encodable proplist.</td></tr><tr><td valign="top"><a href="#auth_to_username-1">auth_to_username/1</a></td><td>Returns the username for the given authorization.</td></tr><tr><td valign="top"><a href="#call-2">call/2</a></td><td>Equivalent to <a href="#call-3"><tt>call(Server, Cmd, [{dispatch, dispatch_to_ref(self())}])</tt></a>.</td></tr><tr><td valign="top"><a href="#call-3">call/3</a></td><td>Equivalent to <a href="#call-4"><tt>call(Server, Cmd, Opts, 5000)</tt></a>.</td></tr><tr><td valign="top"><a href="#call-4">call/4</a></td><td>Call the command, waiting until timeout for all responses.</td></tr><tr><td valign="top"><a href="#cast-2">cast/2</a></td><td>Equivalent to <a href="#cast-3"><tt>cast(Server, Cmd, [{dispatch, dispatch_to_ref(self())}])</tt></a>.</td></tr><tr><td valign="top"><a href="#cast-3">cast/3</a></td><td>Asynchronously cast the cmd.</td></tr><tr><td valign="top"><a href="#clean-1">clean/1</a></td><td>Clean a response to be JSON serializable via jsx.</td></tr><tr><td valign="top"><a href="#clean_list-1">clean_list/1</a></td><td>Clean list command responses, returning an easier to deal with list.</td></tr><tr><td valign="top"><a href="#get_parts_by_type-2">get_parts_by_type/2</a></td><td>Returns the fetch parts by type.</td></tr><tr><td valign="top"><a href="#get_parts_by_type-3">get_parts_by_type/3</a></td><td></td></tr><tr><td valign="top"><a href="#recv-0">recv/0</a></td><td>Equivalent to <a href="#recv-1"><tt>recv(5000)</tt></a>.</td></tr><tr><td valign="top"><a href="#recv-1">recv/1</a></td><td>Receive responses until receiving an IMAP completion message.</td></tr><tr><td valign="top"><a href="#start-1">start/1</a></td><td>Equivalent to <a href="#start-2"><tt>start(ConnSpec, [])</tt></a>.</td></tr><tr><td valign="top"><a href="#start-2">start/2</a></td><td>Start a standalone IMAP connection.</td></tr><tr><td valign="top"><a href="#start_link-1">start_link/1</a></td><td>Equivalent to <a href="#start_link-2"><tt>start_link(ConnSpec, [])</tt></a>.</td></tr><tr><td valign="top"><a href="#start_link-2">start_link/2</a></td><td>Start an IMAP connection as part of the supervision tree.</td></tr><tr><td valign="top"><a href="#stop-1">stop/1</a></td><td>Stop the IMAP client.</td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="auth_to_props-1"></a>

### auth_to_props/1 ###


<pre><code>
auth_to_props(X1::<a href="#type-auth">auth()</a>) -&gt; [<a href="proplists.md#type-property">proplists:property()</a>]
</code></pre>

<br></br>


Returns the auth as a jsx:encodable proplist.
<a name="auth_to_username-1"></a>

### auth_to_username/1 ###


<pre><code>
auth_to_username(X1::<a href="#type-auth">auth()</a>) -&gt; binary()
</code></pre>

<br></br>


Returns the username for the given authorization. This is used
to simplify process registration.
<a name="call-2"></a>

### call/2 ###


<pre><code>
call(Server::pid(), Cmd::<a href="#type-cmd">cmd()</a>) -&gt; {ok, term()} | {'+', term()} | {error, term()}
</code></pre>

<br></br>


Equivalent to [`call(Server, Cmd, [{dispatch, dispatch_to_ref(self())}])`](#call-3).
<a name="call-3"></a>

### call/3 ###


<pre><code>
call(Server::pid(), Cmd::<a href="#type-cmd">cmd()</a>, Opts::[<a href="#type-cmd_opt">cmd_opt()</a>]) -&gt; {ok, term()} | {'+', term()} | {error, term()}
</code></pre>

<br></br>


Equivalent to [`call(Server, Cmd, Opts, 5000)`](#call-4).
<a name="call-4"></a>

### call/4 ###


<pre><code>
call(Server::pid(), Cmd::<a href="#type-cmd">cmd()</a>, Opts::[<a href="#type-cmd_opt">cmd_opt()</a>], Timeout::integer()) -&gt; {ok, term()} | {'+', term()} | {error, term()}
</code></pre>

<br></br>


Call the command, waiting until timeout for all responses.
<a name="cast-2"></a>

### cast/2 ###


<pre><code>
cast(Server::pid(), Cmd::<a href="#type-cmd">cmd()</a>) -&gt; ok
</code></pre>

<br></br>


Equivalent to [`cast(Server, Cmd, [{dispatch, dispatch_to_ref(self())}])`](#cast-3).
<a name="cast-3"></a>

### cast/3 ###


<pre><code>
cast(Server::pid(), Cmd::<a href="#type-cmd">cmd()</a>, Opts::[<a href="#type-cmd_opt">cmd_opt()</a>]) -&gt; ok
</code></pre>

<br></br>


Asynchronously cast the cmd.
<a name="clean-1"></a>

### clean/1 ###


<pre><code>
clean(Resps::term()) -&gt; {atom(), term()}
</code></pre>

<br></br>



Clean a response to be JSON serializable via jsx. In other words,
proplists! For convenience, this function is overloaded to also accept
a list of responses, in which case it will map itself across the list.


NB: Not implemented for all responses -- see function matches.
<a name="clean_list-1"></a>

### clean_list/1 ###


<pre><code>
clean_list(X1::{ok, {term(), [term()]}}) -&gt; {error, term()}
</code></pre>

<br></br>


Clean list command responses, returning an easier to deal with list.
NB: this will discard non-`list` responses.
<a name="get_parts_by_type-2"></a>

### get_parts_by_type/2 ###

`get_parts_by_type(X1, Type) -> any()`

Returns the fetch parts by type.
<a name="get_parts_by_type-3"></a>

### get_parts_by_type/3 ###

`get_parts_by_type(Fetch, Type, SubType) -> any()`


<a name="recv-0"></a>

### recv/0 ###


<pre><code>
recv() -&gt; {ok, term()} | {'+', term()} | {error, term()}
</code></pre>

<br></br>


Equivalent to [`recv(5000)`](#recv-1).
<a name="recv-1"></a>

### recv/1 ###


<pre><code>
recv(Timeout::integer()) -&gt; {ok, term()} | {'+', term()} | {error, term()}
</code></pre>

<br></br>



Receive responses until receiving an IMAP completion message.


Used by call.
<a name="start-1"></a>

### start/1 ###


<pre><code>
start(ConnSpec::<a href="#type-connspec">connspec()</a>) -&gt; {ok, pid()} | term()
</code></pre>

<br></br>


Equivalent to [`start(ConnSpec, [])`](#start-2).
<a name="start-2"></a>

### start/2 ###


<pre><code>
start(ConnSpec::<a href="#type-connspec">connspec()</a>, Opts::[<a href="#type-opt">opt()</a>]) -&gt; {ok, pid()} | term()
</code></pre>

<br></br>


Start a standalone IMAP connection.

__See also:__ [start_link/2](#start_link-2).
<a name="start_link-1"></a>

### start_link/1 ###


<pre><code>
start_link(ConnSpec::<a href="#type-connspec">connspec()</a>) -&gt; {ok, pid()} | term()
</code></pre>

<br></br>


Equivalent to [`start_link(ConnSpec, [])`](#start_link-2).
<a name="start_link-2"></a>

### start_link/2 ###


<pre><code>
start_link(ConnSpec::<a href="#type-connspec">connspec()</a>, Opts::[<a href="#type-opt">opt()</a>]) -&gt; {ok, pid()} | term()
</code></pre>

<br></br>



Start an IMAP connection as part of the supervision tree.


Options:



<dt><code>{cmd, [{cmd, Cmd}]}</code></dt>




<dd><p>A list of valid commands, tagged with <code>cmd</code> which will be called against the
IMAP client from a separate process on start. Use this
to bring the IMAP client to the correct initial state.</p><p></p>For example, if starting an IMAP client to run the IDLE command, the
<code>cmd</code> list may contain
<code>[{cmd, {login, ...}}, {cmd, {select, ...}}, {cmd, idle}]</code>.
</dd>





<dt><code>{init_callback, fun(() -> ok)}</code></dt>




<dd>This function will be called during the IMAP client's <code>init</code>. It is useful
for more complex registration, e.g. using <code>gproc</code>.
</dd>





<dt><code>{post_init_callback, fun(() -> ok)}</code></dt>




<dd>This function will be called after <code>init</code>, and after all commands
specified by the <code>cmds</code> option have successfully completed.
</dd>



<a name="stop-1"></a>

### stop/1 ###


<pre><code>
stop(Pid::pid()) -&gt; ok
</code></pre>

<br></br>


Stop the IMAP client.
