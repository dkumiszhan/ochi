# Query DSL is vaguely based on these rules:

initial query 
   : booleanclause and query : booleandclause or query : booleanclause 

```
query
   : booleanClause booleanSuffixClause || "NOT" query

booleaSuffixClause:
   emptyString || OR query || AND query

booleanClause
   : binaryClause || unaryClause

binaryClause
   : portItemClause binaryOperator integer || ipItemClause binaryOperator ipv4

binaryOperator
   : "eq" || "==" || "ne" || "!="

portItemClause
   : "tcp.port" || "udp.port"

ipItemClause
   : "ip.src" || "ip.dst"

integer:
   : regex([0-9]+)

ipv4:
   : regex([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3})
```


# Examples (not all supported yet)

`ip.src eq 192.168.1.12 and ip.port == 8080`  
`ip.src eq 192.168.1.12 or udp.port == 12`  
`ip.src != 192.168.1.12 or udp.port == 12`  
`ip.src != 192.168.1.12 or udp.port == 12`  
`not ip.src != 192.168.1.12`  
`not (ip.src != 192.168.1.12)`
