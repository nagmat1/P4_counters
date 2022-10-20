In this example we use counters to stop the mirroring when it reaches certain limit. 

whenever we dump the table in bfrt_python we will not the see the latest values in the table. 

```
bfrt.in_network_caching.pipe.Ingress.mirror_port_ekl> dump()
```

The reason why we don't see the counter values is : 

{bold} Counters are incremented by the data plane asynchronously and the fields are volatile. 


To see the latest values we need to insert some parameters : 
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

As shown above, our table mirror_port_ekl has been extended by ``` counter_spec_bytes``` and ``` counter_spec_pkts ``` . 

As shown in the example we have mirrored 5000000000 bytes file.

Headers ==> 3453768 * 20 = 69075360

Data    ==> 5000000000. 

Total will be 5069075360 which is more less than the mirrored packets. 

Q: What is the latency of updating the counters in Tofino 1? 

A: It varies between 6-8 clocks per stage.  





