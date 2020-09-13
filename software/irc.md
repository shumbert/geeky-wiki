# IRC
## Set up weechat to connect on freenode
```
/script install buffers.pl
/server add freenode chat.freenode.net
/set irc.server.freenode.nicks "simal"
/set irc.server.freenode.addresses "chat.freenode.net/7000"
/set irc.server.freenode.ssl on
/set irc.server.freenode.sasl_username "simal"
/set irc.server.freenode.sasl_password "XXXXXXXXX"
/set irc.server.freenode.autoconnect on
/connect freenode
```

## Freenode commands
```
/msg ChanServ help
/msg NickServ help

/msg NickServ REGISTER password youremail@example.com

/nick simal_
/msg NickServ IDENTIFY simal XXXXXXX
/msg NickServ GROUP

/join #deusexhostopia
/msg ChanServ REGISTER #deusexhostopia
/msg ChanServ SET #deusexhostopia GUARD ON
/msg ChanServ SET #deusexhostopia MLOCK +ps
/msg ChanServ SET #deusexhostopia MLOCK +k icanhaskebabz
/msg ChanServ FLAGS #deusexhostopia simal +o
/msg ChanServ OP #deusexhostopia simal
/msg ChanServ DROP #deusexhostopia
```

## Weechat commands
```
/close - close private buffer
/query foo this is a message - open private buffer with foo
/save
```

## Weechat shortcuts
```
Alt-l bare display on/off
Pgup/PgDn scroll up/down one page in buffer history
Alt-Home scroll to top of buffer
Alt-End scroll to bottom of buffer
Alt-Left previous buffer
Alt-Right next buffer
```

## IRC commands
```
/join #channel <password>
/mode #channel b - check banlist for channel
/part #channel
/topic #channel topic
/kick #deusexhostopia nick <message>
```
