To clear all the counter from the table : 

```
Ingress> for e in mirror_port_ekl.get(regex=True):
  e.data[b'$COUNTER_SPEC_PKTS'] = 0 
  e.push()
```
