# Poll routers with suzieq instance

## Howto

containerlab deploy
docker run -it -p 8501:8501 --network clab -v /home/$USER/inventory.yml:/home/suzieq/inventory.yml -v /home/$USER/pwd:/home/suzieq/pwd --name suzieq netenglabs/suzieq
docker exec -it suzieq bash -c 'JUNOS_PASSWORD=$(cat /home/suzieq/pwd) sq-poller -I /home/suzieq/inventory.yml'
docker exec -it suzieq suzieq-cli

## Example with one multicast receiver joined

```
suzieq> route show protocol=pim vrf=inet
      namespace hostname   vrf                prefix nexthopIps oifs protocol source  preference  ipvers                      action
0  mcast_sparse     rtr1  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
1  mcast_sparse     rtr2  inet  225.1.2.3,1.2.3.4/64         []   []      pim                105       0  multicast (ipv4) composite
```
