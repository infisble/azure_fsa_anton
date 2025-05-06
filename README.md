
# Angular Frontend – Nasadenie do Azure

Tento projekt je nasadený v službe Azure Kubernetes Service (AKS) pomocou Docker-u, Azure Container Registry (ACR) a Ingress NGINX.

---

## 🌐 Prístup k aplikácii

👉 Otvor v prehliadači:

```
http://132.164.180.201
```

---

## ☁️ Ako nasadiť aplikáciu do Azure

### 1. Pripojenie ku klastru

```bash
az aks get-credentials --name vovk-fsatfstate-aks --resource-group vovk-fsatfstate
```

---

### 2. Opätovné nasadenie (ak je potrebné)

```bash
kubectl apply -f frontend-service.yaml -n fsa
kubectl apply -f frontend-ingress.yaml -n fsa
```

---

## 🔁 Ako reštartovať aplikáciu (Angular)

Ak si aktualizoval kód, znovu vytvor a nahraj image:

```bash
# Lokálne znovu vytvor image
docker build -t my-angular-app .
docker tag my-angular-app fsaantonregistry.azurecr.io/fsa-frontend:latest
docker push fsaantonregistry.azurecr.io/fsa-frontend:latest

# Reštartuj deployment v Kubernetes
kubectl rollout restart deployment fsa-frontend -n fsa
```

---

## 🧊 Ako pozastaviť klaster (aby si neplatil)

```bash
az aks stop --name vovk-fsatfstate-aks --resource-group vovk-fsatfstate
```

---

## ▶️ Ako znova spustiť klaster

```bash
az aks start --name vovk-fsatfstate-aks --resource-group vovk-fsatfstate
```

Potom sa znova pripoj:

```bash
az aks get-credentials --name vovk-fsatfstate-aks --resource-group vovk-fsatfstate
```

A znova otvor:
```
http://132.164.180.201
```

---

## ✅ Poznámky

- Aplikácia je nasadená cez Ingress NGINX
- IP `132.164.180.201` je staticky pridelená pomocou `loadBalancerIP`
- ACR: `fsaantonregistry`
