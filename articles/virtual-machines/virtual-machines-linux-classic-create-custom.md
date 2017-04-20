<properties
    pageTitle="Créer une VM Linux | Microsoft Azure"
    description="Apprenez à créer un ordinateur virtuel personnalisé avec le modèle classique de déploiement exécutant le système d’exploitation Linux."
    services="virtual-machines-linux"
    documentationCenter=""
    authors="iainfoulds"
    manager="timlt"
    editor="tysonn"
    tags="azure-service-management"/>

<tags
    ms.service="virtual-machines-linux"
    ms.workload="infrastructure-services"
    ms.tgt_pltfrm="vm-linux"
    ms.devlang="na"
    ms.topic="article"
    ms.date="08/23/2016"
    ms.author="iainfou"/>

# <a name="how-to-create-a-custom-linux-vm"></a>Comment faire pour créer une machine virtuelle de Linux personnalisée

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)]Pour la version du Gestionnaire de ressources, consultez [ici](virtual-machines-linux-create-cli-complete.md).

Cette rubrique décrit comment créer un ordinateur virtuel personnalisé (VM) avec la CLI d’Azure en utilisant le modèle de déploiement classique. Nous utilisons une image de Linux à partir des **IMAGES** disponibles sur Azure. Les commandes CLI d’Azure offrent les options de configuration suivantes, entre autres :

- Connexion à un réseau virtuel de la machine virtuelle
- Ajout de la machine virtuelle à un service cloud existant
- Ajout de la machine virtuelle à un compte de stockage existant
- Ajout de la machine virtuelle à un ensemble de disponibilité ou un emplacement

> [AZURE.IMPORTANT] Si vous souhaitez que votre machine virtuelle pour utiliser un réseau virtuel, afin de vous y connecter directement par nom d’hôte ou de l’ensemble des connexions de coexistence, assurez-vous que vous spécifiez le réseau virtuel lorsque vous créez l’ordinateur virtuel. Un ordinateur virtuel peut être configuré pour vous joindre à un réseau virtuel que lorsque vous créez l’ordinateur virtuel. Pour plus d’informations sur les réseaux virtuels, consultez [Vue d’ensemble du réseau virtuel Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).


## <a name="how-to-create-a-linux-virtual-machine-using-the-classic-deployment-model"></a>Comment faire pour créer un ordinateur virtuel de Linux en utilisant le modèle de déploiement classique

[AZURE.INCLUDE [virtual-machines-create-LinuxVM](../../includes/virtual-machines-create-linuxvm.md)]
