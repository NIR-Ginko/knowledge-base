# SSH magic keys

SSH passes control keypress sequences to processes that run on remote
host. In case of connection problem SSH may hang in attempt to regain
control on connection.

In order to operate on SSH itself there is magic key sequence:
`~` `Enter`. You may prefix the necessary command with this sequence
and do something with SSH like:

* `~` `Enter` `.` - drop the connection.

