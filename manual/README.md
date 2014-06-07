

# Switchboard #

Copyright (c) Copyright (c) 2014, ThusFresh, Inc.

__Authors:__ Thomas Moulia ([`jtmoulia@pocketknife.io`](mailto:jtmoulia@pocketknife.io)).

Switchboard is a [Spatch](http://spatch.co/) product.

Switchboard provides high-level tools for managing IMAP clients across
multiple email accounts and providers, and an API allowing workers to
process emails as they arrive. It handles the boilerplate of IMAP
connection management and new email monitoring so that you can focus
on innovating around email.


### Case Study: Push Notifications ###

Switchboard's first role was sending new email push notifications to
the [Spatch iOS
app](http://spatch.co). Due to mobile process backgrounding restrictions and battery
abuse, it's difficult to monitor for new emails client-side. Instead,
the Spatch app securely posts users' OAuth tokens to a server running
Switchboard, which begins to monitor the accounts for incoming
emails. When a new email arrives, Switchboard notifies a subscribed
worker, which then sends down a push notification to the app.

In this case, Switchboard handled creating the IMAP connections,
keeping tabs on new emails coming down, and giving the worker
the data that it needed to send down a nicely formatted push
notification.

Check back soon for the push worker!


### Workers ###

See [switchboard_sockets](switchboard_sockets.md) for
documentation and tips on interfacing with Switchboard through
the client API.


### Security ###

It goes without saying that emails are highly sensitive.  Switchboard
is only as secure as the server which it is on. Beyond personal use,
great care should be taken to ensure that both Switchboard and its
environment are secure.

In addition to plain auth, Switchboard's IMAP client supports [XOAUTH2](https://developers.google.com/gmail/xoauth2_protocol).
To keep your user's credentials safe, use XOAUTH2 or a similar
solution whenever possible.


### Switchboard isn't IMAP ###

While the Switchboard API provides some IMAP like functionality, it is
specifically intended to help with real time email processing.  IMAP
is a sharp, if sometimes difficult, tool and will remain preferable for
general programmatic email tasks.


### IMAP Connections ###

For each account, one active IMAP connection is created, plus one IMAP
connection for each mailbox to be monitored. This separation of
responsibilites across IMAP connections allows for simpler management
of the IMAP connections, thought at the cost of [using
multiple IMAP connections](https://support.google.com/mail/answer/97150?hl=en).
Switchboard uses a custom IMAP module, located in
`src/imap.erl`. Its type specs indicate what commands it currently
supports.

## Modules ##


<table width="100%" border="0" summary="list of modules">
<tr><td><a href="imap.md" class="module">imap</a></td></tr>
<tr><td><a href="reloader.md" class="module">reloader</a></td></tr>
<tr><td><a href="rfc2822.md" class="module">rfc2822</a></td></tr>
<tr><td><a href="switchboard.md" class="module">switchboard</a></td></tr>
<tr><td><a href="switchboard_jmap.md" class="module">switchboard_jmap</a></td></tr></table>

