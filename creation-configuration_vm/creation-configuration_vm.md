# Introduction/ contexte
Proxmox est une solution de virtualisation qui permet de créer et de gérer des machines virtuelles et des conteneurs Linux. La création de machines virtuelles sur Proxmox est un processus relativement simple et offre de nombreuses possibilités aux utilisateurs.

# Création d'une VM sur Proxmox 
La création d'une VM sur Proxmox VE implique les étapes suivantes :

1. Connectez-vous à l'interface web de Proxmox VE en utilisant un navigateur web.
2. Sélectionnez l'hôte sur lequel vous souhaitez créer la VM.
>**Attention**
>Créer votre VM sur le serveur le moins rempli pour assurer le bon fonctionnement du cluster et ne pas surcharger une machine.
{.is-danger}
3. Cliquez sur "Créer une machine virtuelle" pour lancer l'assistant de création de VM.
4. Configurez les paramètres de la VM, tels que le système d'exploitation, la mémoire, le stockage, le réseau et les options avancées.
5. Cliquez sur "Créer" pour créer la VM.
6. Possibilités d'une VM sur Proxmox VE
> Lorsque vous faites de grosses modifications sur votre VM vous pouvez diminuer le risque de tout perdre en faisant régulierement des snapshots : les snapshots permettent de créer des sauvegardes rapides de la VM et de restaurer rapidement l'état précédent en cas de problème et donc éviter de perdre des données importantes.
{.is-info}

## Migrer une VM
La migration de VMs permet de déplacer des machines virtuelles d'un hôte à un autre afin d'optimiser la disponibilité et la performance des VMs et donc ne pas surcharger un hôte plus qu'un autre.
Pour ce faire il y a seulement deux étapes à comprendre pour faire la manipulation
1. Allez sur la VM que vous voulez migrer et cliquez sur "Migrate"
1. Sélectionnez l'hôte le plus adapté, donc le moins rempli, soit en mémoire utilisée ( en vert ) ou en usage du processeur ( en bleu ).
![migrate3.png](/img/migrate3.png)
## Les possibilitées
Les machines virtuelles créées sur Proxmox VE offrent de nombreuses possibilités aux utilisateurs.
Voici quelques exemples :
- Virtualisation de serveurs : les VM peuvent être utilisées pour créer des serveurs virtuels pour différents services et applications.
- Test de logiciels : les développeurs peuvent utiliser des VM pour tester des logiciels dans différents environnements.
