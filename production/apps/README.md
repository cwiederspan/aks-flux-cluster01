# Testing

```bash

kubectl apply -f .

# Spin up busybox in ns1 to test it out
kubectl run curl-cdw -n svcdisc-cust001 --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc-cust001/data

curl http://svcdiscsvc-cust002/data                           # Doesn't work
curl http://svcdiscsvc-cust002.svcdisc-cust002/data    # Does work because of namespace pathing

# Spin up busybox in ns1 to test it out
kubectl run curl-cdw -n svcdisc-cust001 --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc2/data

```
