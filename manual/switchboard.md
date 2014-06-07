

# Module switchboard #
* [Description](#description)
* [Data Types](#types)
* [Function Index](#index)
* [Function Details](#functions)


This module provides the main interface to Switchboard.
Copyright (c) Copyright (c) 2014, ThusFresh, Inc.

__Authors:__ Thomas Moulia ([`jtmoulia@pocketknife.io`](mailto:jtmoulia@pocketknife.io)).

<a name="types"></a>

## Data Types ##




### <a name="type-keytype">keytype()</a> ###



<pre><code>
keytype() = account | active | idlers | {idler | operator | idler_sup, <a href="imap.md#type-mailbox">imap:mailbox()</a>}
</code></pre>





### <a name="type-pubsub_channel">pubsub_channel()</a> ###



<pre><code>
pubsub_channel() = new
</code></pre>


<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#accounts-0">accounts/0</a></td><td>Returns the list of accounts currently being managed by Switchboard.</td></tr><tr><td valign="top"><a href="#add-2">add/2</a></td><td>Equivalent to <a href="#add-3"><tt>add(ConnSpec, Auth, [])</tt></a>.</td></tr><tr><td valign="top"><a href="#add-3">add/3</a></td><td>Add the specified account to be monitored by the switchboard application.</td></tr><tr><td valign="top"><a href="#add_mailbox_monitor-2">add_mailbox_monitor/2</a></td><td>Add a mailbox to be monitored for the provided account.</td></tr><tr><td valign="top"><a href="#await-2">await/2</a></td><td>Equivalent to <a href="#await-3"><tt>await(Account, Type, 5000)</tt></a>.</td></tr><tr><td valign="top"><a href="#await-3">await/3</a></td><td>Wraps gproc's await command for Switchboard.</td></tr><tr><td valign="top"><a href="#checkout-1">checkout/1</a></td><td></td></tr><tr><td valign="top"><a href="#key_for-2">key_for/2</a></td><td>Returns the key for the given account and process type.</td></tr><tr><td valign="top"><a href="#mailbox_monitors-1">mailbox_monitors/1</a></td><td>Returns the list of mailboxes which are being monitored for the
provided Account.</td></tr><tr><td valign="top"><a href="#publish-2">publish/2</a></td><td>Publish a message to the Switchboard channel.</td></tr><tr><td valign="top"><a href="#register_callback-2">register_callback/2</a></td><td>An IMAP InitCallback function used to register the process its called upon
with gproc.</td></tr><tr><td valign="top"><a href="#return-2">return/2</a></td><td></td></tr><tr><td valign="top"><a href="#start-0">start/0</a></td><td>Start the Switchboard application.</td></tr><tr><td valign="top"><a href="#stop-1">stop/1</a></td><td>Stop the account from being monitored.</td></tr><tr><td valign="top"><a href="#stop_mailbox_monitor-2">stop_mailbox_monitor/2</a></td><td></td></tr><tr><td valign="top"><a href="#subscribe-1">subscribe/1</a></td><td>Subscribe to Switchboard messages using the provided channel.</td></tr><tr><td valign="top"><a href="#unsubscribe-1">unsubscribe/1</a></td><td>Unsubscribe from the provided Switchboard channel.</td></tr><tr><td valign="top"><a href="#where-2">where/2</a></td><td>Returns the process of type for the provided account.</td></tr><tr><td valign="top"><a href="#with_imap-2">with_imap/2</a></td><td></td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="accounts-0"></a>

### accounts/0 ###


<pre><code>
accounts() -&gt; [binary()]
</code></pre>

<br></br>


Returns the list of accounts currently being managed by Switchboard.
<a name="add-2"></a>

### add/2 ###


<pre><code>
add(ConnSpec::<a href="imap.md#type-connspec">imap:connspec()</a>, Auth::<a href="imap.md#type-auth">imap:auth()</a>) -&gt; <a href="supervisor.md#type-startchild_ret">supervisor:startchild_ret()</a>
</code></pre>

<br></br>


Equivalent to [`add(ConnSpec, Auth, [])`](#add-3).
<a name="add-3"></a>

### add/3 ###


<pre><code>
add(ConnSpec::<a href="imap.md#type-connspec">imap:connspec()</a>, Auth::<a href="imap.md#type-auth">imap:auth()</a>, Mailboxes::[<a href="imap.md#type-mailbox">imap:mailbox()</a>]) -&gt; <a href="supervisor.md#type-startchild_ret">supervisor:startchild_ret()</a>
</code></pre>

<br></br>



Add the specified account to be monitored by the switchboard application.
Each mailbox provided will be monitored for new emails, and notifications
of new email arrivals will be published to the `new` channel.



Note: This will start an `active` IMAP connection which can be used for queries,
as well as one `idler` IMAP connection per mailbox given. Some email providers
[limit](https://support.google.com/mail/answer/97150?hl=en) the number
of open imap connections.


Once started, the IMAP client processes can be accessed using `where`.
<a name="add_mailbox_monitor-2"></a>

### add_mailbox_monitor/2 ###


<pre><code>
add_mailbox_monitor(Account::<a href="imap.md#type-account">imap:account()</a>, Mailbox::<a href="imap.md#type-mailbox">imap:mailbox()</a>) -&gt; <a href="supervisor.md#type-startchild_ret">supervisor:startchild_ret()</a>
</code></pre>

<br></br>


Add a mailbox to be monitored for the provided account.
<a name="await-2"></a>

### await/2 ###


<pre><code>
await(Account::<a href="imap.md#type-account">imap:account()</a>, Type::<a href="#type-keytype">keytype()</a>) -&gt; pid()
</code></pre>

<br></br>


Equivalent to [`await(Account, Type, 5000)`](#await-3).
<a name="await-3"></a>

### await/3 ###


<pre><code>
await(Account::<a href="imap.md#type-account">imap:account()</a>, Type::<a href="#type-keytype">keytype()</a>, Timeout::non_neg_integer()) -&gt; pid()
</code></pre>

<br></br>


Wraps gproc's await command for Switchboard. This plays an
important role since the IMAP connections move from supervisor init
-> startup cmds -> registering via gproc. Awaiting registration
will provide a ready to go process.
<a name="checkout-1"></a>

### checkout/1 ###

`checkout(Account) -> any()`


<a name="key_for-2"></a>

### key_for/2 ###


<pre><code>
key_for(Account, Type) -&gt; {n, l, {switchboard, {Type, Account}}}
</code></pre>

<ul class="definitions"><li><code>Account = <a href="imap.md#type-account">imap:account()</a></code></li><li><code>Type = <a href="#type-keytype">keytype()</a></code></li></ul>


Returns the key for the given account and process type.



Switchboard processes are registered using descriptive erlang terms via
[gproc](https://github.com/uwiger/gproc). This function
wraps the term with gproc properties and a switchboard namespace.





<dt><code>active</code></dt>




<dd>The active IMAP client. While used internally by Switchboard,
this can also be used externally to make requests.
</dd>




<dt><code>{idler, Mailbox}</code></dt>




<dd>The IMAP client monitoring <code>Mailbox</code> via the <code>idle</code> command.
</dd>




<dt>... others</dt>




<dd>Other processes are intended to be opaque.
</dd>



<a name="mailbox_monitors-1"></a>

### mailbox_monitors/1 ###


<pre><code>
mailbox_monitors(Account::<a href="imap.md#type-account">imap:account()</a>) -&gt; [binary()]
</code></pre>

<br></br>


Returns the list of mailboxes which are being monitored for the
provided Account.
<a name="publish-2"></a>

### publish/2 ###


<pre><code>
publish(X1::<a href="#type-pubsub_channel">pubsub_channel()</a>, Msg) -&gt; Msg
</code></pre>

<ul class="definitions"><li><code>Msg = any()</code></li></ul>

Publish a message to the Switchboard channel.

__See also:__ [subscribe](subscribe.md).
<a name="register_callback-2"></a>

### register_callback/2 ###


<pre><code>
register_callback(Account::<a href="imap.md#type-account">imap:account()</a>, Type::<a href="#type-keytype">keytype()</a>) -&gt; fun((State) -&gt; State)
</code></pre>

<ul class="definitions"><li><code>State = any()</code></li></ul>


An IMAP InitCallback function used to register the process its called upon
with gproc.


This is useful since processes can only be registered with gproc from within
themselves. It is currently used as an imap `post_init_callback`.
<a name="return-2"></a>

### return/2 ###

`return(Account, IMAP) -> any()`


<a name="start-0"></a>

### start/0 ###

`start() -> any()`

Start the Switchboard application.
<a name="stop-1"></a>

### stop/1 ###


<pre><code>
stop(Account::binary()) -&gt; ok | {error, not_found | simple_one_for_one}
</code></pre>

<br></br>


Stop the account from being monitored. Unlike add, this only
requires the account name, e.g. `dispatchonme@gmail.com`
<a name="stop_mailbox_monitor-2"></a>

### stop_mailbox_monitor/2 ###


<pre><code>
stop_mailbox_monitor(Account::<a href="imap.md#type-account">imap:account()</a>, Mailbox::<a href="imap.md#type-mailbox">imap:mailbox()</a>) -&gt; ok | {error, not_found | simple_one_for_one}
</code></pre>

<br></br>



<a name="subscribe-1"></a>

### subscribe/1 ###


<pre><code>
subscribe(X1::<a href="#type-pubsub_channel">pubsub_channel()</a>) -&gt; true
</code></pre>

<br></br>



Subscribe to Switchboard messages using the provided channel.


Channels:



<dt><tt>new</tt></dt>




<dd>This channel provides email arrival notifications. The messages should
take the form of <tt>{new, {Account, Mailbox}, Item}</tt> where Item is
the result of a cleaned ALL fetch (@see imap:call).
</dd>



<a name="unsubscribe-1"></a>

### unsubscribe/1 ###


<pre><code>
unsubscribe(X1::<a href="#type-pubsub_channel">pubsub_channel()</a>) -&gt; true
</code></pre>

<br></br>


Unsubscribe from the provided Switchboard channel.

__See also:__ [subscribe](subscribe.md).
<a name="where-2"></a>

### where/2 ###

`where(Account, Type) -> any()`


Returns the process of type for the provided account.


For example, `where(<<"dispatchonme@gmail.com">>, active)` would return
the `active` IMAP client for `dispatchonme@gmail.com`.


__See also:__ [key_for/2](#key_for-2).
<a name="with_imap-2"></a>

### with_imap/2 ###

`with_imap(Account, Fun) -> any()`


