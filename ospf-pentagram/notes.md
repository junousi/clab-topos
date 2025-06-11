# Suzieq notes

## Topology

```
.--.  .----.   .----.  .--.
|h1|--|rtr6|   |rtr9|--|h2|
'--'  '----'   '----'  '--'
SRC    \ \.----./ /    RECV
        \ |core| /
         -'----'-
            RP
```

```
suzieq> route show protocol=pim prefixlen='64'
      namespace hostname   vrf                prefix nexthopIps oifs protocol source  preference  ipvers                      action
0  mcast_sparse     rtr1  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
1  mcast_sparse     rtr2  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
2  mcast_sparse     rtr3  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
3  mcast_sparse     rtr4  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
4  mcast_sparse     rtr5  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
5  mcast_sparse     rtr6  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
6  mcast_sparse     rtr9  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
```

Path goes via all core nodes even though RP should be pruned already?? TODO
