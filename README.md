# openproject

deploy openproject
```bash
kubectl create deployment openproject --image=openproject/community:11
kubectl expose deployment openproject --port=80 --name=openproject
```
> user: `admin` pass: `admin`

delete everything:
```bash
kubectl delete deploy/openproject svc/openproject ing/openproject
```

create ingress value:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: openproject
spec:
  tls:
    - hosts:
      - openproject.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: openproject.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: openproject
            servicePort: 80
EOF
```

