```bash
kubectl create -n istio-system secret tls istio-ingressgateway-certs --key httpbin.example.com.key --cert httpbin.example.com.crt
```

```bash
kubectl apply -f namespaces.yaml
kubectl apply -f .
``` 
