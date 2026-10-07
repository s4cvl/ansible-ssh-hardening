# ansible-ssh-hardening

Playbook Ansible de sécurisation SSH et d'installation de BIND sur Oracle Linux.

## Fonctionnalités

- Restreint la connexion SSH de l'utilisateur `ansible` à la clé de `ansible@srv-ansible`, depuis son IP uniquement
- Verrouille le mot de passe de l'utilisateur `ansible` et interdit l'authentification SSH par mot de passe
- Installe et active BIND (`named`)

## Prérequis

- Ansible sur le poste de contrôle (srv-ansible)
- Utilisateur `ansible` avec clé SSH et sudo NOPASSWD sur les cibles

## Utilisation

1. Adapter `srv_ansible_ip` dans `playbook.yml` et l'inventaire `inventaire.yml`
2. Lancer :

    ansible-playbook playbook.yml

## Licence

MIT
