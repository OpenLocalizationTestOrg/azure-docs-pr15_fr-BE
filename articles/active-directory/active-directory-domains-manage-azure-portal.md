<properties
    pageTitle="Gestion des noms de domaine personnalisé dans votre aperçu Azure Active Directory | Microsoft Azure"
    description="Concepts de gestion et des procédures pour la gestion d’un nom de domaine dans Active Directory de Azure"
    services="active-directory"
    documentationCenter=""
    authors="jeffsta"
    manager="femila"
    editor=""/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/12/2016"
    ms.author="curtand;jeffsta"/>

# <a name="managing-custom-domain-names-in-your-azure-active-directory-preview"></a>Gestion des noms de domaine personnalisé dans votre aperçu Azure Active Directory

Un nom de domaine est une partie importante de l’identificateur de nombreuses ressources de répertoire : il fait partie d’un utilisateur nom ou adresse e-mail d’un utilisateur, une partie de l’adresse d’un groupe et peut faire partie de l’identificateur URI d’application pour une application. Une ressource dans l’aperçu d’Azure Active Directory (AD Azure) peut inclure un nom de domaine qui est déjà vérifié appartenant au répertoire qui contient la ressource. [Nouveautés dans l’aperçu](active-directory-preview-explainer.md) Seul un administrateur global peut effectuer les tâches de gestion de domaine dans Active Directory Azure.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Définir le nom de domaine principal de votre annuaire AD Azure

Lors de la création de votre répertoire, le nom de domaine initial, tel que « contoso.onmicrosoft.com », est également le nom de domaine principal. Le domaine principal est le nom de domaine par défaut pour un nouvel utilisateur lorsque vous créez un nouvel utilisateur. Cela rationalise le processus pour un administrateur de créer de nouveaux utilisateurs dans le portail. Pour modifier le nom de domaine principal :

1.  Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire.

2.  Sélectionnez des **services supplémentaires**, entrez **Azure Active Directory** dans la zone de texte et puis sélectionnez **entrée**.

    ![Gestion des utilisateurs ouverture](./media/active-directory-domains-add-azure-portal/user-management.png)

3. Sur la lame ***nom du répertoire*** , sélectionnez **les noms de domaine**.

4. Sur la lame ** *nom du répertoire* : noms de domaine** , sélectionnez le nom de domaine que vous souhaitez que le nom de domaine principal.

5.  Sur la lame ***domainname*** (autrement dit, la lame qui s’ouvre avec votre nouveau nom de domaine dans le titre), sélectionnez la commande **Rendre principal** . Confirmez votre choix lorsque vous y êtes invité.

    ![Créer un nom de domaine principal](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Vous pouvez modifier le nom de domaine principal de votre répertoire à n’importe quel domaine vérifié personnalisé qui n’est pas fédéré. Modification du domaine principal de votre répertoire ne changera pas les noms de tous les utilisateurs existants.

## <a name="add-custom-domain-names-to-your-azure-ad"></a>Ajouter des noms de domaine personnalisé pour votre annonce Azure

Vous pouvez ajouter des noms de domaine personnalisé jusqu'à 900 à chaque répertoire AD Azure. Le processus pour [Ajouter un nom de domaine personnalisé supplémentaire](active-directory-domains-add-azure-portal.md) est le même pour le premier nom de domaine personnalisé.

## <a name="add-subdomains-of-a-custom-domain"></a>Ajouter des sous-domaines d’un domaine personnalisé

Si vous souhaitez ajouter un nom de domaine de troisième niveau comme « europe.contoso.com » à votre annuaire, vous devez tout d’abord ajouter et vérifiez le domaine de second niveau, par exemple, contoso.com. Le sous-domaine est automatiquement vérifié par AD Azure. Pour voir que le sous-domaine que vous venez d’ajouter a été vérifié, actualisez la page dans le navigateur, qui répertorie les domaines.

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a>Que faire si vous changez le registraire DNS pour le nom de votre domaine personnalisé

Si vous changez le registraire DNS pour le nom de votre domaine personnalisé, vous pouvez continuer à utiliser votre nom de domaine personnalisé avec Azure AD elle-même sans interruption et sans les tâches de configuration supplémentaires. Si vous utilisez votre nom de domaine personnalisé avec Office 365, Intune ou d’autres services qui s’appuient sur des noms de domaine personnalisé dans Azure AD, reportez-vous à la documentation de ces services.

## <a name="delete-a-custom-domain-name"></a>Supprimer un nom de domaine personnalisé

Vous pouvez supprimer un nom de domaine personnalisé de votre annonce Azure si votre organisation n’utilise plus ce nom de domaine, ou si vous devez utiliser ce nom de domaine avec une autre annonce Azure.

Pour supprimer un nom de domaine personnalisé, vous devez d’abord vous assurer qu’aucune ressource dans votre répertoire s’appuient sur le nom de domaine. Vous ne pouvez pas supprimer un nom de domaine à partir de votre répertoire si :

-   N’importe quel utilisateur possède un nom d’utilisateur, adresse électronique ou adresse proxy qui inclut le nom de domaine.

-   N’importe quel groupe possède une adresse de messagerie ou une adresse de proxy qui inclut le nom de domaine.

-   N’importe quelle application dans votre annonce Azure a une identificateur URI qui inclut le nom de domaine d’application.

Vous devez modifier ou supprimer n’importe quelle ressource de ce type dans votre répertoire AD Azure avant de pouvoir supprimer le nom de domaine personnalisé.

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a>Utilisez PowerShell ou graphique d’API pour gérer les noms de domaine

La plupart des tâches de gestion des noms de domaine dans Active Directory de Azure peuvent également être effectuées à l’aide de Microsoft PowerShell, ou par programme à l’aide d’API d’Azure AD graphique (dans la version d’évaluation).

-   [Utilisation de PowerShell pour gérer des noms de domaine dans Active Directory Azure](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

-   [À l’aide du graphique d’API pour gérer les noms de domaine dans Active Directory Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Étapes suivantes

-   [Ajouter des noms de domaine personnalisé](active-directory-domains-add-azure-portal.md)
