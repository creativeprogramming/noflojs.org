---
  title: "Read"
  library: "noflo-pgorm"
  layout: "component"

---

```coffeescript
EXPORT=FILTERTOKEN.IN:IN
EXPORT=PACKETIZE.OUT:OUT
EXPORT=READSERVER.SERVER:SERVER
EXPORT=CONSTRUCT.PKEY:PKEY
EXPORT=READSERVER.ERROR:ERROR
EXPORT=READSERVER.QUIT:QUIT
EXPORT=CONSTRUCT.LIMIT:LIMIT
EXPORT=CONSTRUCT.OFFSET:OFFSET
EXPORT=CONSTRUCT.ORDERBY:ORDERBY
EXPORT=PACKETIZE.FILTER:FILTER

'.+' -> REGEXP FilterToken(groups/FilterByGroup)
FilterToken() OUT -> IN Construct(pgorm/ConstructRead)

FilterToken() GROUP -> TOKEN ReadServer(pg/Postgres)
Construct() TEMPLATE -> TEMPLATE ReadServer()
Construct() OUT -> IN ReadServer()

```
Convert to NoFlo packets


```coffeescript
ReadServer() OUT -> IN Packetize(pgorm/JsonToPackets)

```