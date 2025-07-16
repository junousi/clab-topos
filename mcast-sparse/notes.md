# Poll routers with suzieq instance

## Howto

```
containerlab deploy
docker run -it -p 8501:8501 --network clab -v /home/$USER/inventory.yml:/home/suzieq/inventory.yml -v /home/$USER/pwd:/home/suzieq/pwd --name suzieq netenglabs/suzieq
docker exec -it suzieq bash -c 'JUNOS_PASSWORD=$(cat /home/suzieq/pwd) sq-poller -I /home/suzieq/inventory.yml'
docker exec -it suzieq suzieq-cli
```

## Example with single receiver

```
.--.  .----.   .----.  .--.
|h1|--|rtr1|---|rtr2|--|h2|
'--'  '----'   '----'  '--'
SRC      \.----./      RECV
          |rtr3|
          '----'
            RP
```

Once receiver has joined, we see the SPT tree, with rtr3/RP not participating:

```
suzieq> route show protocol=pim vrf=inet
      namespace hostname   vrf                prefix nexthopIps oifs protocol source  preference  ipvers                      action
0  mcast_sparse     rtr1  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
1  mcast_sparse     rtr2  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
```

Severing the rtr1-rtr2 link, we see the path moving over to rtr3 - in other words SPT becomes same as RPT:

```
admin@rtr1# set interfaces ge-0/0/0 disable
admin@rtr1# commit and-quit
```

```
suzieq> route show protocol=pim vrf=inet
      namespace hostname   vrf                prefix nexthopIps oifs protocol source  preference  ipvers                      action
0  mcast_sparse     rtr1  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
1  mcast_sparse     rtr2  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
2  mcast_sparse     rtr3  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
```
