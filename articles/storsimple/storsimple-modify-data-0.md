<properties 
   pageTitle="Modifier les données 0 paramètres sur un périphérique StorSimple | Microsoft Azure"
   description="Apprenez à utiliser Windows PowerShell pour StorSimple pour reconfigurer l’interface réseau 0 des données sur le périphérique StorSimple."
   services="storsimple"
   documentationCenter=""
   authors="alkohli"
   manager="carmonm"
   editor="" />
<tags 
   ms.service="storsimple"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="08/17/2016"
   ms.author="alkohli" />

# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a>Modifier les paramètres d’interface réseau 0 données sur votre périphérique de StorSimple

## <a name="overview"></a>Vue d’ensemble

Votre périphérique Microsoft Azure StorSimple a six interfaces réseau, à partir de données de 0 à 5 des données. Les données 0 interface est toujours configuré par le biais de l’interface Windows PowerShell ou la console série et est automatiquement activé pour le cloud. Notez que vous ne pouvez pas configurer les interface réseau 0 des données via le portail classique Azure. 

Les données de la première configuration par l’intermédiaire de l’Assistant Installation lors de l’interface 0 initiale du déploiement du périphérique StorSimple. Lorsque le périphérique est dans un mode de fonctionnement, vous devrez peut-être reconfigurer les données 0 paramètres. Ce didacticiel fournit deux méthodes pour modifier les données 0 paramètres réseau, les deux de Windows PowerShell et de StorSimple.

Après avoir lu ce didacticiel, vous pourrez :

- Modifier les données 0 paramètre par le biais de l’Assistant Configuration du réseau
- Modifier les paramètres de réseau 0 de données par le biais de la `Set-HcsNetInterface` applet de commande



## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modifier les paramètres de réseau 0 de données via l’Assistant d’installation
Vous pouvez reconfigurer les paramètres de réseau 0 de données par connexion à l’interface Windows PowerShell de votre périphérique StorSimple et le lancement d’une session de l’Assistant d’installation. Effectuez les opérations suivantes pour modifier les données 0 paramètres :

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a>Pour modifier les paramètres de réseau 0 de données via l’Assistant d’installation

1. Dans le menu de la console série, choisissez l’option 1, **Connectez-vous à l’aide d’un accès complet**. Lorsque vous y êtes invité fournir le **mot de passe administrateur**. Le mot de passe par défaut est `Password1`.

2. À l’invite de commandes, tapez :

    `Invoke-HcsSetupWizard`

3. Un Assistant d’installation s’affiche pour vous aider à configurer les données 0 interface de votre périphérique. Fournir de nouvelles valeurs pour l’adresse IP, la passerelle et masque de réseau.

> [AZURE.NOTE] Les contrôleurs fixes IPs devra être reconfiguré par le biais de la page de **configuration** du périphérique StorSimple dans Azure portal classique. Pour plus d’informations, accédez aux [interfaces réseau de modifier](storsimple-modify-device-config.md#modify-network-interfaces).


## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modifier les paramètres de réseau 0 de données via l’applet de commande Set-HcsNetInterface
Une autre façon de reconfigurer les données 0 et interface réseau à l’aide de la `Set-HcsNetInterface` applet de commande. L’applet de commande est exécutée à partir de l’interface Windows PowerShell de votre périphérique StorSimple. Lorsque vous utilisez cette procédure, le contrôleur fixé IPs peut également être configuré ici. Effectuez les opérations suivantes pour modifier les données 0 paramètres : 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a>Pour modifier les paramètres de réseau 0 de données par le biais de l’applet de commande Set-HcsNetInterface

1. Dans le menu de la console série, choisissez l’option 1, **Connectez-vous à l’aide d’un accès complet**. Lorsque vous y êtes invité fournir le mot de passe administrateur. Le mot de passe par défaut est `Password1`.

2. À l’invite de commandes, tapez :

    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
    
    Dans les crochets, tapez les valeurs suivantes pour les données de 0 :
                                            
    - Adresse IPv4
    
    - Passerelle IPv4
    
    - Masque de sous-réseau IPv4
    
    - Adresse IPv4 fixe pour contrôleur 0

    - Adresse IPv4 fixe pour contrôleur 1

    Pour plus d’informations sur l’utilisation de cette applet de commande, accédez à [Windows PowerShell de référence d’applet de commande StorSimple](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Étapes suivantes

- Pour configurer les interfaces réseau autres que les données de 0, vous pouvez utiliser la [page Configurer dans Azure portal classique](storsimple-modify-device-config.md). 

- Si vous rencontrez des problèmes lors de la configuration des interfaces réseau, consultez [résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md).

