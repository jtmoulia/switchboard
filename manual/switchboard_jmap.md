

# Module switchboard_jmap #
* [Description](#description)
* [Function Index](#index)
* [Function Details](#functions)


JMAP Command Handler.
Copyright (c) Copyright (c) 2014, ThusFresh, Inc

__Behaviours:__ [`cowboy_websocket_handler`](cowboy_websocket_handler.md).

__Authors:__ Thomas Moulia ([`jtmoulia@pocketknife.io`](mailto:jtmoulia@pocketknife.io)).
<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#message_id-2">message_id/2</a></td><td>Encode a messageId from a mailboxId and UID.</td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="message_id-2"></a>

### message_id/2 ###


<pre><code>
message_id(MailboxId::binary(), Uid::binary() | integer()) -&gt; binary()
</code></pre>

<br></br>


Encode a messageId from a mailboxId and UID.
