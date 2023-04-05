# Introduction / Contexte
Dans ce document est expliqué ce que les professeurs peuvent faire dans le cluster SIO.
## Liste des droits des professeurs
| Nom                         | Explication                                                                                                                                      |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Datastore.AllocateSpace     | Ce droit permet à l'utilisateur de créer des images de disque dur virtuel pour les machines virtuelles et de les stocker dans un espace de stockage partagé appelé "Datastore".                        |
| Datastore.AllocateTemplate  | Ce droit permet à l'utilisateur de créer et de stocker des modèles de machines virtuelles dans l'espace de stockage partagé appelé "Datastore". Les modèles sont des machines virtuelles prêtes à l'emploi. |
| Datastore.Audit             | Ce droit permet à l'utilisateur de consulter les journaux d'audit de l'espace de stockage partagé "Datastore".                                       |
| Pool.audit                  | Ce droit permet à l'utilisateur de consulter les journaux d'audit du groupe de ressources appelé "Pool" dans lequel se trouvent les machines virtuelles.                                                       |
| Sys.Syslog                  | Ce droit permet à l'utilisateur de consulter les journaux système du serveur Proxmox.                                                               |
| vm.allocate                 | Ce droit permet à l'utilisateur de créer de nouvelles machines virtuelles sur le serveur Proxmox.                                                 |
| VM.Audit                    | Ce droit permet à l'utilisateur de consulter les journaux d'audit d'une machine virtuelle spécifique.                                              |
| VM.Backup                   | Ce droit permet à l'utilisateur de sauvegarder les disques durs virtuels d'une machine virtuelle spécifique.                                       |
| VM.Clone                    | Ce droit permet à l'utilisateur de créer des copies de machines virtuelles existantes.                                                             |
| VM.Config.CDROM             | Ce droit permet à l'utilisateur de configurer les lecteurs de CD/DVD des machines virtuelles.                                                      |
| VM.Config.CPU               | Ce droit permet à l'utilisateur de configurer les paramètres de CPU des machines virtuelles.                                                       |
| VM.Config.Cloudinit         | Ce droit permet à l'utilisateur de configurer les options de Cloud-init des machines virtuelles.                                                   |
| VM.Config.Disk              | Ce droit permet à l'utilisateur de configurer les disques durs virtuels des machines virtuelles.                                                    |
| VM.Config.HWType            | Ce droit permet à l'utilisateur de configurer les types de matériel des machines virtuelles.                                                        |
| VM.Config.Memory            | Ce droit permet à l'utilisateur de configurer la mémoire RAM des machines virtuelles.                                                              |
| VM.Config.Network           | Ce droit permet à l'utilisateur de configurer les interfaces réseau des machines virtuelles.                                                       |
| VM.Config.Options           | Ce droit permet à l'utilisateur de configurer les options générales des machines virtuelles.                                                       |
| VM.Console                  | Ce droit permet à l'utilisateur de se connecter aux consoles des machines virtuelles.                                                              |
| VM.Migrate                  | Ce droit permet à l'utilisateur de déplacer des machines virtuelles d'un serveur Proxmox à un autre.                                                |
| VM.Monitor                  | Ce droit permet à l'utilisateur de surveiller les ressources utilisées par une machine virtuelle spécifique.                                        |
| VM.PowerMgmt                | Ce droit permet à l'utilisateur de gérer l'alimentation des machines virtuelles (démarrage, arrêt, suspension, etc.).                              |
| VM.Snapshot                 | Ce droit permet à l'utilisateur de créer des instantanés (snapshots) des machines virtuelles.                                                      |
| VM.Snapshot.Rollback        | Ce droit permet à l'utilisateur de restaurer une machine virtuelle à partir d'une snapshot.

# Les Pools
## Pool view

En tant que professeur, vous avez le droit de voir le pool de tous les utilisateurs . Vous pouvez également les éditer et les modifier comme si vous en étiez le propriétaire. En revanche, les élèves ne peuvent voir que leur propre pool et les machines virtuelles disponibles dans le pool "Ressources".
> Votre pool personnel commence par "A-", contrairement aux étudiants qui commence par "B-", il sera donc toujours en haut de la liste.
{.is-success}

 ![vue_prof_pool.png](/img/vue_prof_pool.png)
> N'hésitez pas à rechercher l'utilisateur que vous voulez voir grâce a l'outil associé.
{.is-info}

## Le pool Ressources

En tant que professeur, vous avez la possibilité de créer des templates dans le dossier "Ressources" sur Proxmox. Ces ressources sont accessibles aux élèves, mais ils n'ont pas le droit de les modifier ou de créer leurs propres machines virtuelles dans ce pool. Cependant, les élèves peuvent cloner les machines virtuelles et les templates disponibles dans "Ressources" et les copier dans leur propre pool.

# Les VM et templates
## Les VM
En tant qu'utilisateur de Proxmox, vous avez le droit de créer vos propres machines virtuelles dans votre pool privé. Vous pouvez les utiliser pour tester ou pour effectuer diverses tâches. Cependant, pour les rendre accessibles aux autres utilisateurs, vous devez les créer dans le pool "Ressources".
>**Attention !!**
> Il est important de vérifier sur quel serveur vous allouez votre machine virtuelle et de choisir celui qui est le moins chargé. Cela permet d'éviter de surcharger le cluster et de garantir son bon fonctionnement.
{.is-danger}

La documentation ci-dessous détaille la création et la configuration d'une machine virtuelle. Il conviendra de sélectionner le pool dans lequel nous souhaitons mettre la VM.
- [Creation et Configuration VM *Documentation de création et configuration de VM*](/fr/administration_reseau/infrastructure/cluster_proxmox/creation-configuration_vm)
{.links-list}

## Les templates
Les professeurs peuvent créer des templates pré-configurés pour les machines virtuelles, qui peuvent être utilisés par les élèves pour créer rapidement et facilement des machines virtuelles.  Les templates peuvent également être partagés entre les professeurs pour un usage commun.


- [Les templates *Document pour une utilisation plus complète des Templates*](/fr/administration_reseau/infrastructure/templates)
{.links-list}


