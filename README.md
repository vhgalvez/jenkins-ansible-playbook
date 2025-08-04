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

2. **Configurar las variables de entorno:**

   ```bash
   sudo nano .env
   # Ejemplo de contenido del archivo .env
   JENKINS_AUTH_USER=admin
   JENKINS_AUTH_PASS=SuperPassword123
   JENKINS_AUTH_USER_UI=admin
   JENKINS_AUTH_PASS_UI=SuperPassword123
   DOCKERHUB_USERNAME=tu_usuario
   DOCKERHUB_TOKEN=tu_token
   GITHUB_TOKEN=tu_github_token
   ```

3. **Cargar las variables de entorno:**

   ```bash
   source .env
   ```

4. **Ejecutar el playbook para desplegar Jenkins:**

   ```bash
   sudo -E ansible-playbook -i inventory/hosts.ini playbooks/deploy_jenkins_stack.yml
   ```

5. **Verificar el estado de Jenkins:**
   ```bash
   kubectl get pods -n jenkins
   kubectl logs -n jenkins jenkins-0 -c jenkins --tail=100
   ```

## Desinstalar Jenkins

Para desinstalar Jenkins y limpiar los recursos:

```bash
sudo -E ansible-playbook -i inventory/hosts.ini playbooks/uninstall_jenkins.yml
```

## Notas adicionales

- Asegúrate de que tu clúster Kubernetes esté operativo y que Helm esté correctamente configurado para interactuar con él.
- Personaliza las variables en `group_vars/all.yml` según tus necesidades específicas antes de ejecutar el playbook.
- Usa los siguientes comandos para depuración:
  ```bash
  kubectl logs -f -n jenkins jenkins-0
  kubectl get secret -n jenkins
  ```

## Variables de entorno para Jenkins

Ejemplo de configuración de variables de entorno:

```bash
export JENKINS_AUTH_USER="admin"
export JENKINS_AUTH_PASS="SuperPassword123"
export JENKINS_AUTH_USER_UI="admin"
export JENKINS_AUTH_PASS_UI="SuperPassword123"
```

## Comandos útiles

- Verificar configuración de pods:
  ```bash
  kubectl get pods -n jenkins
  ```
- Ver logs del contenedor principal:
  ```bash
  kubectl logs -n jenkins jenkins-0 -c jenkins --tail=100
  ```
- Ver logs del contenedor de inicialización:
  ```bash
  kubectl logs -f -n jenkins jenkins-0 -c init-config
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
