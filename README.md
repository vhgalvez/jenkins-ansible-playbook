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




ps aux | grep port-forward
Matar todos los port-forward activos:


sudo pkill -f "kubectl port-forward"

nohup kubectl port-forward svc/jenkins 8080:8080 -n jenkins --address 0.0.0.0 > /tmp/jenkins-port-forward.log 2>&1 &


kubectl port-forward svc/jenkins 8080:8080 -n jenkins --address 0.0.0.0





✅ 1. Limpiar procesos previos (opcional, recomendado)
bash
Copiar
Editar
# Matar cualquier port-forward previo que esté ocupando puertos
sudo pkill -f "kubectl port-forward"
✅ 2. Jenkins (http://192.168.0.15:8080)
bash
Copiar
Editar
nohup kubectl port-forward svc/jenkins 8080:8080 -n jenkins --address 0.0.0.0 > /tmp/jenkins-port-forward.log 2>&1 &
✅ 3. Prometheus (http://192.168.0.15:32001)
bash
Copiar
Editar

nohup kubectl port-forward -n monitoring svc/prometheus-server --address 0.0.0.0 32001:80 > /tmp/prometheus-port-forward.log 2>&1 &

✅ 4. Grafana (http://192.168.0.15:32002)
bash
Copiar
Editar
nohup kubectl port-forward -n monitoring svc/grafana --address 0.0.0.0 32002:3000 > /tmp



kubectl get svc -A -o wide | grep -E 'jenkins|grafana|prometheus|longhorn'




nohup kubectl port-forward -n longhorn-system svc/longhorn-system  --address 0.0.0.0 32001:80 > /tmp/prometheus-port-forward.log 2>&1 &
