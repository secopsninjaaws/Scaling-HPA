# 📌 Auto Scaling com HPA no Kubernetes

Este repositório demonstra como configurar o **Horizontal Pod Autoscaler (HPA)** no Kubernetes para escalar automaticamente os pods com base na utilização de CPU e memória.

## 📂 Estrutura do Repositório

- `namespace.yaml` → Criação do namespace `scaling-nginx`
- `deploy.yaml` → Deployment da aplicação e configuração do HPA
- `serv-ingress.yaml` → Configuração do **Service** e do **Ingress**

## 🏗️ Passo a Passo da Implantação

### 1️⃣ Criar o Namespace  
Aplique o namespace para isolar os recursos do cluster:
```yaml
kubectl apply -f namespace.yaml
```

### 2️⃣ Criar o Deployment com HPA  
O deployment `scaling-nginx` será criado com um **Horizontal Pod Autoscaler** para escalabilidade automática:
```yaml
kubectl apply -f deploy.yaml
```

### 3️⃣ Criar o Service e o Ingress  
O Service permite a comunicação entre os pods, e o Ingress gerencia o tráfego externo:
```yaml
kubectl apply -f serv-ingress.yaml
```

## 🎯 Como funciona o Auto Scaling com HPA?

1. O **HPA** monitora o uso de **CPU** e **memória** dos pods no deployment `scaling-nginx`.
2. Se o consumo de **CPU ou memória ultrapassar 50%**, o HPA escala os pods automaticamente.
3. O número mínimo de réplicas é `1` e o máximo é `20`.
4. A escalabilidade segue estas regras:
   - **Scale-up**: Aumenta o número de réplicas se o consumo for alto.
   - **Scale-down**: Reduz o número de réplicas se o consumo diminuir.

## 🚀 Monitorando o Auto Scaling

Para verificar os pods em execução:
```yaml
kubectl get pods -n scaling-nginx
```

Para visualizar o HPA:
```yaml
kubectl get hpa -n scaling-nginx
```

Para verificar o tráfego roteado:
```yaml
kubectl get ingress -n scaling-nginx
```

## 🛠️ Ajustando o Escalonamento

Caso queira modificar os limites de escalabilidade, edite o arquivo `deploy.yaml` na seção:
```yaml
minReplicas: 1
maxReplicas: 20
```

Isso permitirá aumentar ou reduzir a quantidade de réplicas conforme necessário.

---

💡 **Dica:** Para um escalonamento mais preciso, utilize métricas personalizadas com o **Prometheus Adapter**!