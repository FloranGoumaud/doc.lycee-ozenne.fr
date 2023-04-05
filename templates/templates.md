## Créer un template
Pour créer un template dans Proxmox, vous pouvez suivre les étapes suivantes :

1. Créez une machine virtuelle que vous souhaitez utiliser comme modèle. Vous pouvez utiliser une machine virtuelle existante ou créer une nouvelle machine virtuelle pour cette étape.

1. Une fois que la machine virtuelle est configurée selon vos besoins, arrêtez-la.

1. Dans l'interface web de Proxmox, sélectionnez la machine virtuelle que vous souhaitez transformer en modèle et cliquez sur le bouton "Template" dans la barre de menus supérieure.

1. Dans la fenêtre qui s'ouvre, saisissez un nom pour votre nouveau modèle et cliquez sur "Créer le modèle".

1. Le modèle sera maintenant créé et vous pourrez le voir dans la liste des modèles de Proxmox. Vous pouvez utiliser ce modèle pour créer de nouvelles machines virtuelles.
> **Attention :**
> Il est important de noter que les modèles dans Proxmox ne peuvent pas être utilisés pour démarrer des machines virtuelles directement. Vous devez créer une nouvelle machine virtuelle basée sur le modèle et la démarrer à partir de là.
{.is-warning}

# Utiliser le cluster Proxmox
## Créer une machine virtuelle
## Créer un template Debian avec Cloud-Init
Un template permet de gagner du temps lors de la création d'une machine virtuelle. En effet, les mêmes opérations sont souvent répétées pour mettre à disposition une VM (création de la VM, Installation du système, Configuration du système, ...). Un template agit comme une machine de base que l'on va pouvoir cloner.

CloudInit permet quant à lui de configurer automatiquement le nom d'hôte du système installé sur le VM, mais aussi le nom d'utilisateur / mot de passe et les paramètres IP de la carte réseau. Le tout directement depuis l'interface Proxmox.

Plusieurs étapes sont nécessaires à la création du template :
1. Création d'une machine virtuelle
1. Installation d'un Debian
1. Installation de CloudInit
1. Convertion de la VM en Template	

### Création d'une machine virtuelle
Pour cette étape, toute la procédure est indiquée précédement. Nous pensons juste à ajouter **CloudInit Drive** dans le hardware de la VM.


> **Pensez à personnaliser la configuration pour qu'elle corresponde au besoin !**
> En fait, il faut ajuster les paramètres de la machine virtuelle en fonction de ce que l'on souhaite pour notre template. Ressources processeurs, Mémoire vive, Disque, ... Tout se passe à cette étape.
{.is-info}

#  CloudInit et Debian
## Introduction / Contexte
CloudInit est un outil de configuration système qui permet de personnaliser et de provisionner des machines virtuelles dans des environnements de cloud computing.
Il permet de configurer de manière automatisée des paramètres tels que le nom d'hôte, l'adresse IP, les clés SSH, les packages à installer, les fichiers de configuration, etc. en utilisant des fichiers de configuration YAML. Il permet d'automatiser la configuration des machines virtuelles et de s'assurer que toutes les instances sont correctement configurées et cohérentes.
Dans le chapitre dédié à CloudInit, nous verrons comment configurer et utiliser cet outil avec Proxmox.
## Installation d'un Debian et de CloudInit
Nous ne détaillerons pas ici l'installation du Debian mais seulement les points important. Lors de l'installation, voici quelques points sur lesquels il faut prêter attention :
- Définir un mot de passe pour le compte root générique
- Définir un nom d'utilisateur et un mot de passe générique pour le second compte
- Bien penser de sélectionner tous les paramètres correspondant aux besoins du template (partitionnement du disque en fonction du besoin, installation des services ssh, ...)

> **ATTENTION**
> Il faut que cette machine ait bien accès à internet mais évitez de mettre une adresse IP fixe, préférez le DHCP. A default, il est conseillé de revenir en dhcp avant de créer le template.
{.is-warning}

Une fois le Debian installé, on se connecte en root puis on installe le paquet CloudInit :
```
apt-get install cloud-init
```
En fonction du besoin, on installe ce qu'il faut. Dans le cas présent, nous souhaitons juste une machine Debian 11 de base, alors on s'arrête là.

Enfin, on étaint la machine virtuelle.

## Conversion de la VM en template
Avant de convertir la VM en Template, on s'assure de déconfigurer si besoin le VLAN Tag de la carte réseau, sauf si le template est systématiquement dédié au même réseau.

On sélectionne la VM puis on clique sur **Convert to template** dandans le menu **More**.

## Utilisation d'un template 
### Restauration de la VM
Pour se faire il suffit de sélectionner le template puis on clique sur **Clone** dandans le menu **More**.
On renseigne alors le nom de la VM que l'on souhaite, et on sélectionne **Full Clone** dans le menu **Mode**. On valide en cliquant sur **Clone**. Au besoin, on indique l'ID de la VM, le pool de ressources et le serveur de destination dans le cas d'un cluster.
> **Attention :**
> Faire un "full clone" d'un template prends autant de place que le template cloné, priviliégiez donc l'utilisation du "linked clone".
{.is-warning}

> **Attention au nommage de la VM !**
> En effet, le nom donné à la VM sera automatiquement le nom d'hôte du Débian lors de la restauration. Il est donc important d'y prêter attention.
{.is-warning}

### Configuration de la VM (CloudInit)
Lorsque l'opération de restauration est terminée, on sélectionne l'onglet **CloudInit** de la VM pour y paramétrer les paramètres suivants : 
- **User :** Nom d'utilisateur du compte 'non-root'
- **Passcord :** Mot de passe du compte mentionné ci-dessus
- **DNS domain ou DNS servers :** Défini les adresses IP des serveurs DNS et le domaine DNS
- **SSH public key :** Permet d'importer une clef SSH publique
- **IP Config :** Permet de configurer les paramètres IP de la machine

Ensuite, on valide en cliquant sur **Regenerate Image** et la machine est prête. On peut la démarrer ou effectuer d'autres modifications sur le hardware ou les options en fonction du besoin.

> **C'est terminé !**
> La machine est configurée correctement et a appliquer le même nom d'hôte que la VM et les paramètres définis dans l'onglet CloudInit.
{.is-success}


