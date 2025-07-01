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
   source .env
   sudo -E ansible-playbook -i inventory/hosts.ini playbooks/deploy_jenkins_stack.yml
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





curl -Ik https://jenkins.local --insecure -u admin:123456

export JENKINS_AUTH_USER="admin"
export JENKINS_AUTH_PASS="SuperPassword123"


sudo nano .env
# .env para Jenkins (autenticación Traefik)

JENKINS_AUTH_USER=admin
JENKINS_AUTH_PASS=SuperPassword123
JENKINS_AUTH_USER_UI=admin
JENKINS_AUTH_PASS_UI=SuperPassword123


export JENKINS_AUTH_USER="admin"
export JENKINS_AUTH_PASS="SuperPassword123"

source .env
sudo -E ansible-playbook -i inventory/hosts.ini playbooks/deploy_jenkins_stack.yml



[controller]
192.168.0.15 ansible_user=monitoring ansible_ssh_private_key_file=/home/victory/.ssh/id_rsa ansible_become=true ansible_become_method=sudo ansible_become_pass=Gdh88K28


# Variables de entorno para Jenkins
export JENKINS_AUTH_USER=admin
export JENKINS_AUTH_PASS=SuperPassword123
export JENKINS_AUTH_USER_UI=admin
export JENKINS_AUTH_PASS_UI=SuperPassword123


source .env
sudo -E ansible-playbook -i inventory/hosts.ini playbooks/deploy_jenkins_stack.yml