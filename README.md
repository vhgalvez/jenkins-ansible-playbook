# Jenkins Ansible Playbook

Este repositorio instala Jenkins en un clúster Kubernetes usando Helm + Ansible.

## Estructura
- `inventory/`: Definición de hosts.
- `group_vars/`: Variables comunes.
- `playbooks/`: Playbooks principales.
- `roles/`: Roles Ansible (Jenkins).

## Requisitos
- **Ansible**: Instalado en tu máquina local.
- **Cluster Kubernetes**: Configurado y accesible.
- **Helm**: Instalado y configurado.

## Uso rápido
1. **Instalar las colecciones necesarias:**
   ```bash
   ansible-galaxy collection install kubernetes.core
   ```

2. **Ejecutar el playbook apuntando a tu inventario:**
   ```bash
   ansible-playbook -i inventory/hosts.ini playbooks/install_jenkins.yml
   ```

## 🔥 Siguientes pasos
1. **Crea un repositorio en GitHub:**
   - Nombre sugerido: `jenkins-ansible-playbook`

2. **Sube esta estructura básica al repositorio.**

3. **Inicializa el `README.md` con la información proporcionada.**

4. (Opcional) **Activar entorno virtual de Python si tienes uno configurado:**
   ```bash
   source venv/bin/activate
   ```

## Notas adicionales

- Asegúrate de que tu clúster Kubernetes esté operativo y que Helm esté correctamente configurado para interactuar con él.
- Personaliza las variables en `group_vars/all.yml` según tus necesidades específicas antes de ejecutar el playbook.


```bash
sudo pkill -f "kubectl port-forward"
```

# 🔁 Jenkins (expuesto en 32000 desde dentro del clúster al exterior)

```bash
nohup kubectl port-forward -n jenkins svc/jenkins --address 0.0.0.0 32000:8080 > /tmp/jenkins-port-forward.log 2>&1 &
```

# 📊 Prometheus (expuesto en 32001)

```bash
nohup kubectl port-forward -n monitoring svc/prometheus-server --address 0.0.0.0 32001:80 > /tmp/prometheus-port-forward.log 2>&1 &
```

# 📈 Grafana (expuesto en 32002)

```bash
nohup kubectl port-forward -n monitoring svc/grafana --address 0.0.0.0 32002:3000 > /tmp/grafana-port-forward.log 2>&1 &
```

# 🧠 Longhorn (expuesto en 32003) — nombre correcto: longhorn-frontend

```bash
nohup kubectl port-forward -n longhorn-system svc/longhorn-frontend --address 0.0.0.0 32003:80 > /tmp/longhorn-port-forward.log 2>&1 &
```

```bash
kubectl get svc -A -o wide | grep -E 'jenkins|grafana|prometheus|longhorn'
```



| Servicio    | Tipo      | Puerto interno | NodePort  |
|-------------|-----------|----------------|-----------|
| Jenkins     | NodePort  | 8080            | 32000     |
| Prometheus  | ClusterIP | 80              | (port-forward 32001) |
| Grafana     | ClusterIP | 3000            | (port-forward 32002) |
| Longhorn    | NodePort  | 80              | 32003     |



```bash
sudo ss -tuln | grep -E '32000|32001|32002|32003'
```

| Servicio    | URL de acceso                                |
|-------------|-----------------------------------------------|
| Jenkins     | http://192.168.0.15:32000                     |
| Prometheus  | http://192.168.0.15:32001                     |
| Grafana     | http://192.168.0.15:32002                     |
| Longhorn    | http://192.168.0.15:32003                     |



# 1. Matar port-forward anteriores

```bash
sudo pkill -f "kubectl port-forward"
```
sudo grep "kubectl port-forward" 


# 2. Verificar servicios

   
```bash
kubectl get svc -A -o wide | grep -E 'jenkins|grafana|prometheus|longhorn'
```

# 3. Crear todos los port-forwards

   
```bash

nohup kubectl port-forward -n jenkins svc/jenkins --address 0.0.0.0 32000:8080 > /tmp/jenkins-port-forward.log 2>&1 &

nohup kubectl port-forward -n monitoring svc/prometheus-server --address 0.0.0.0 32001:80 > /tmp/prometheus-port-forward.log 2>&1 &

nohup kubectl port-forward -n monitoring svc/grafana --address 0.0.0.0 32002:3000 > /tmp/grafana-port-forward.log 2>&1 &

nohup kubectl port-forward -n longhorn-system svc/longhorn-frontend --address 0.0.0.0 32003:80 > /tmp/longhorn-port-forward.log 2>&1 &

```

# 4. Comprobar puertos abiertos

```bash
sudo ss -tuln | grep -E '32000|32001|32002|32003'
```


  for ip in 10.17.3.11 10.17.3.12 10.17.3.13 10.17.3.14 10.17.5.20 192.168.0.15; do
    echo "Testing $ip:9100...";
    timeout 2 curl -s http://$ip:9100/metrics | head -1 || echo "FAILED";
  done
