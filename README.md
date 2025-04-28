# Jenkins Ansible Playbook

Este repositorio instala Jenkins en un clúster Kubernetes usando Helm + Ansible.

## Estructura
- `inventory/`: Definición de hosts.
- `group_vars/`: Variables comunes.
- `playbooks/`: Playbooks principales.
- `roles/`: Roles Ansible (Jenkins).

## Uso rápido
```bash
ansible-playbook -i inventory/hosts.ini playbooks/install_jenkins.yml

Requisitos
Ansible

Kubernetes cluster

Helm instalado

yaml
Copiar
Editar

---

## 🔥 Siguientes pasos:
1. **Crea un repositorio en GitHub:**  
   Nombre sugerido: `jenkins-ansible-playbook`
   
2. **Sube esta estructura básica.**

3. **Inicializa el `README.md`