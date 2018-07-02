## Retrieve keys from master node
```
cp /var/lib/localkube/certs/ca.crt .
cp /var/lib/localkube/certs/ca.key .
```
## Create new user
```
sudo apt install openssl
openssl genrsa -out george.pem 2048
openssl req -new -key george.pem -out george-csr.pem -subj "/CN=george/O=lab/"
openssl x509 -req -in george-csr.pem -CA ca.crt -CAkey ca.key -CAcreateserial -out george.crt -days 10000
```

## add new context
```
kubectl config set-credentials george --client-certificate=george.crt --client-key=george.pem
kubectl config set-context george --cluster=kubernetes.lab --user george
```
