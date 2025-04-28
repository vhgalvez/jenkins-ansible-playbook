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
