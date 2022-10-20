To clear all the counter from the table : 

```
Ingress> for e in mirror_port_ekl.get(regex=True):
  e.data[b'$COUNTER_SPEC_PKTS'] = 0 
  e.push()
```

Example : 
```
bfrt.in_network_caching.pipe.Ingress.mirror_port_ekl> dump(table=True, from_hw=True)
----- mirror_port_ekl Dump Start -----
Default Entry:
Entry data (action : NoAction):
    $COUNTER_SPEC_BYTES            : 0
    $COUNTER_SPEC_PKTS             : 0

pipe.Ingress.mirror_port_ekl entries for action: Ingress.acl_mirror
hdr.ipv4.src_addr    filesize    mirror_session      $COUNTER_SPEC_BYTES    $COUNTER_SPEC_PKTS
-------------------  ----------  ----------------  ---------------------  --------------------
0xC0A80102           0x00000000  0x05                         5241763862               3453768


----- mirror_port_ekl Dump End -----


```
