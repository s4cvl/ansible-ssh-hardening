# ansible-ssh-hardening

Projet Ansible de sécurisation SSH, configuration de BIND et création d'un utilisateur d'administration sur Oracle Linux.

## Fonctionnalités

### Rôle ssh_bind
- Restreint la connexion SSH de l'utilisateur ansible à la clé de ansible@srv-ansible, depuis son IP uniquement
- Verrouille le mot de passe de l'utilisateur ansible et interdit l'authentification SSH par mot de passe
- Installe BIND en redirection unique (forward only) vers le DNS de l'hôte cible
- DNSSEC désactivé
- Contrôle de la configuration (named-checkconf + test de résolution) avec rollback automatique (block/rescue)

### Rôle admin_user
- Crée un utilisateur d'administration (nom défini dans group_vars)
- Droits sudo avec mot de passe
- Déploie une clé SSH publique stockée dans un vault
- Génère un mot de passe aléatoire et l'affiche à la création

## Arborescence

    ansible.cfg
    site.yml
    inventory/
      staging/
      prod/
    playbooks/
      01_ssh_bind.yml
      02_admin_user.yml
    roles/
      ssh_bind/
      admin_user/

## Prérequis

- Ansible sur le poste de contrôle (srv-ansible)
- Collection ansible.posix
- Utilisateur ansible avec clé SSH et sudo NOPASSWD sur les cibles
- Fichiers .vault_pass_staging et .vault_pass_prod à la racine (non versionnés)

## Utilisation

Staging (inventaire par défaut) :

    ansible-playbook site.yml

Production :

    ansible-playbook -i inventory/prod site.yml

Un seul sous-playbook :

    ansible-playbook playbooks/01_ssh_bind.yml

## Licence

Voir le fichier LICENCE.
