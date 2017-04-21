<properties services="virtual-machines" title="Using Azure CLI with Azure Resource Manager" authors="squillace" solutions="" manager="timlt" editor="tysonn" />

<tags
   ms.service="virtual-machine"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="linux"
   ms.workload="infrastructure"
   ms.date="04/13/2015"
   ms.author="rasquill" />

## <a name="using-azure-cli-with-azure-resource-manager-arm"></a>À l’aide de CLI Azure avec Azure Resource Manager (ARM)

Avant de pouvoir utiliser la CLI Azure avec les modèles et les commandes du Gestionnaire de ressources pour déployer des ressources Azure et les charges de travail à l’aide de groupes de ressources, vous devez un compte Azure (bien entendu). Si vous ne disposez pas d’un compte, vous pouvez obtenir un [essai gratuit Azure ici](https://azure.microsoft.com/pricing/free-trial/).

> [AZURE.NOTE] Si vous ne disposez pas d’un compte Azure, mais vous êtes abonné à un abonnement MSDN, vous pouvez obtenir gratuitement Azure crédits par l’activation de vos [avantages d’abonné MSDN ici](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) --ou vous peuvent utiliser le compte gratuit. Soit fonctionnera pour accès Azure.

### <a name="step-1-verify-the-azure-cli-version"></a>Étape 1 : Vérifier la version de l’infrastructure du langage commun Azure

Pour utiliser Azure CLI des commandes impératives et des modèles ARM, vous devez disposer d’au moins la version 0.8.17. Pour vérifier votre version, tapez `azure --version`. Vous devriez voir quelque chose comme :

    $ azure --version
    0.8.17 (node: 0.10.25)

Si vous devez mettre à jour votre version du CLI d’Azure, consultez [Azure CLI](https://github.com/Azure/azure-xplat-cli).

### <a name="step-2-verify-you-are-using-a-work-or-school-identity-with-azure"></a>Étape 2 : Vérifiez que vous utilisez un travail ou l’école d’identité avec Azure

Vous pouvez uniquement utiliser le mode de commande ARM si vous utilisez un [locataire d’Azure Active Directory](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) ou un [Nom Principal de Service](https://msdn.microsoft.com/library/azure/dn132633.aspx). (Ils sont également appelés des *ID d’organisation*).

Pour voir si vous en avez un, connectez-vous en tapant `azure login` et à l’aide de votre travail ou le nom d’utilisateur de l’établissement et le mot de passe lorsque vous y êtes invité. Si vous n’en avez pas, vous devez voir quelque chose comme suit :

    $ azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@contoso.onmicrosoft.com
    Password: *********
  	|info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Setting subscription Visual Studio Ultimate with MSDN as default
    info:    Added subscription Azure Free Trial
    +
    info:    login command OK

Si vous ne voyez pas cette option, vous devez créer un nouveau locataire (ou un service principal) avec l’identité de votre compte Microsoft. (Cela est souvent le cas avec les abonnements MSDN personnels ou des abonnements d’évaluation gratuits.) Pour créer un travail ou l’école id à partir de votre compte Azure créée avec un id Microsoft, voir [associer un répertoire de publicité Azure avec un nouvel abonnement Azure](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). Si vous pensez que vous devez avoir un id d’organisation, vous devrez peut-être parler avec la personne qui a créé le compte pour vous.

### <a name="step-3-choose-your-azure-subscription"></a>Étape 3 : Choisissez votre abonnement Azure

Si vous avez uniquement un abonnement dans votre compte Azure, Azure CLI associe cet abonnement par défaut. Si vous avez plus d’un abonnement, vous devez sélectionner l’abonnement que vous voulez utiliser en tapant `azure account set <subscription id or name> true` où _nom ou id d’abonnement_ est l’id d’abonnement ou le nom d’abonnement que vous souhaitez utiliser dans la session en cours.

Vous devriez voir quelque chose comme suit :

    $ azure account set "Azure Free Trial" true
    info:    Executing command account set
    info:    Setting subscription to "Azure Free Trial" with id "2lskd82-434-4730-9df9-akd83lsk92sa".
    info:    Changes saved
    info:    account set command OK

### <a name="step-4-place-your-azure-cli-in-the-arm-mode"></a>Étape 4 : Placez votre CLI Azure en mode ARM

Pour utiliser le mode de gestion de ressources Azure (ARM) avec la CLI d’Azure, tapez `azure config mode arm`. Vous devriez voir quelque chose comme suit :

    $ azure config mode arm
    info:    New mode is arm

> [AZURE.NOTE] Vous pouvez basculer précédent pour utiliser des commandes de gestion de service Azure en tapant `azure config mode asm`.
