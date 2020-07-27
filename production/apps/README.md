# Testing

```bash

kubectl apply -f .

# Spin up busybox in ns1 to test it out
kubectl run curl-cdw -n svcdisc-cust001 --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc1-cust001/data

# Spin up busybox in ns1 to test it out
kubectl run curl-cdw -n svcdisc-cust001 --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc2/data

curl http://svcdiscsvc1/data                    # Doesn't work
curl http://svcdiscsvc1.svcdisc-cust001/data    # Does work because of namespace pathing

```
