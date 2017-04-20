<properties 
    pageTitle="Didacticiel : Intégration d’Azure Active Directory avec ThousandEyes | Microsoft Azure" 
    description="Apprenez à utiliser ThousandEyes avec Azure Active Directory pour activer l’ouverture de session unique, la mise en service automatique et bien plus encore !" 
    services="active-directory" 
    authors="jeevansd"  
    documentationCenter="na" 
    manager="femila"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="09/11/2016" 
    ms.author="jeedes" />

#<a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Didacticiel : Intégration d’Azure Active Directory avec ThousandEyes
  
L’objectif de ce didacticiel est d’afficher la configuration de l’authentification unique entre Azure Active Directory (AD Azure) et ThousandEyes.
  
Le scénario décrit dans ce didacticiel suppose que vous ayez les éléments suivants :

-   Un abonnement Azure valide
-   Authentification unique ThousandEyes abonnement activé
  
À la fin de ce didacticiel, le DAS auquel vous avez affecter ThousandEyes accéder pourront à l’ouverture de session unique dans l’application à votre site de la société ThousandEyes (service fournisseur initiée signe) ou en utilisant le panneau d’accès DAS.

1.  L’activation de l’intégration de l’application pour ThousandEyes
2.  Configuration de l’authentification unique
3.  Configuration d’approvisionnement de l’utilisateur
4.  Affectation d’utilisateurs

![Scénario] (./media/active-directory-saas-thousandeyes-tutorial/IC790059.png "Scénario")

##<a name="enabling-the-application-integration-for-thousandeyes"></a>L’activation de l’intégration de l’application pour ThousandEyes
  
L’objectif de cette section doit décrire comment activer l’intégration de l’application pour ThousandEyes.

###<a name="to-enable-the-application-integration-for-thousandeyes-perform-the-following-steps"></a>Pour activer l’intégration de l’application pour ThousandEyes, effectuez les opérations suivantes :

1.  Dans le portail Azure classique, dans le volet de navigation de gauche, cliquez sur **Active Directory**.

    ![Active Directory] (./media/active-directory-saas-thousandeyes-tutorial/IC700993.png "Active Directory")

2.  Dans la liste **répertoire** , sélectionnez le répertoire pour lequel vous souhaitez activer l’intégration d’annuaire.

3.  Pour ouvrir la vue des applications, dans la vue du répertoire, cliquez sur **Applications** dans le menu supérieur.

    ![Applications] (./media/active-directory-saas-thousandeyes-tutorial/IC700994.png "Applications")

4.  Cliquez sur **Ajouter** au bas de la page.

    ![Ajouter application] (./media/active-directory-saas-thousandeyes-tutorial/IC749321.png "Ajouter application")

5.  Dans la boîte de dialogue **que voulez-vous faire** , cliquez sur **Ajouter une application à partir de la galerie**.

    ![Ajouter une application à partir de gallerry] (./media/active-directory-saas-thousandeyes-tutorial/IC749322.png "Ajouter une application à partir de gallerry")

6.  Dans la **zone Rechercher**, tapez **ThousandEyes**.

    ![Galerie des applications] (./media/active-directory-saas-thousandeyes-tutorial/IC790060.png "Galerie des applications")

7.  Dans le volet de résultats, sélectionnez **ThousandEyes**, puis cliquez sur **Terminer** pour ajouter l’application.

    ![ThousandEyes] (./media/active-directory-saas-thousandeyes-tutorial/IC790061.png "ThousandEyes")

##<a name="configuring-single-sign-on"></a>Configuration de l’authentification unique
  
Cette section explique comment permettre aux utilisateurs de s’authentifier à ThousandEyes avec leur compte Azure Active Directory, à l’aide de fédération basée sur le protocole SAML.

###<a name="to-configure-single-sign-on-perform-the-following-steps"></a>Pour configurer l’authentification unique, procédez comme suit :

1.  Dans Azure portal classique, sur la page d’intégration **ThousandEyes** application, cliquez **sur Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer Single Sign On** .

    ![Configurer la fonctionnalité d’authentification unique] (./media/active-directory-saas-thousandeyes-tutorial/IC790062.png "Configurer la fonctionnalité d’authentification unique")

2.  Dans la page **Comment voulez-vous que les utilisateurs à se connecter à ThousandEyes** , sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.

    ![Configurer la fonctionnalité d’authentification unique] (./media/active-directory-saas-thousandeyes-tutorial/IC790063.png "Configurer la fonctionnalité d’authentification unique")

3.  Dans la page **Configurer l’URL App** , dans la zone de texte **ThousandEyes URL de connexion** , les utilisateurs de l’URL, utilisez pour vous connecter à votre application de ThousandEyes de type (par exemple : «*https://app.thousandeyes.com/login/sso*»), puis cliquez sur **suivant**. 

    ![Configurer des URL de l’application] (./media/active-directory-saas-thousandeyes-tutorial/IC790064.png "Configurer des URL de l’application")

4.  Dans la page **configuration de l’authentification unique au ThousandEyes** , pour télécharger votre certificat, cliquez sur **Télécharger le certificat**et puis enregistrez le fichier de certificat localement sur votre ordinateur.

    ![Configurer la fonctionnalité d’authentification unique] (./media/active-directory-saas-thousandeyes-tutorial/IC790065.png "Configurer la fonctionnalité d’authentification unique")

5.  Dans une fenêtre de navigateur web différents, connectez-vous à votre site d’entreprise **ThousandEyes** en tant qu’administrateur.

6.  Dans le menu du haut, cliquez sur **paramètres**.

    ![Paramètres] (./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Paramètres")

7.  Cliquez sur **le compte**

    ![Compte] (./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Compte")

8.  Cliquez sur l’onglet **sécurité et l’authentification** .

    ![Sécurité et authentification] (./media/active-directory-saas-thousandeyes-tutorial/IC790068.png "Sécurité et authentification")

9.  Dans la section **Installation de Single Sign-On** , effectuez les opérations suivantes :

    ![Le programme d’installation de l’authentification unique] (./media/active-directory-saas-thousandeyes-tutorial/IC790069.png "Le programme d’installation de l’authentification unique")

    1.  Sélectionnez **Activer l’ouverture de session unique**.
    2.  Dans le portail classique de Microsoft Azure, sur la page **configuration de l’authentification unique à ThousandEyes** , copiez la valeur de **L’URL de connexion à distance** et puis la coller dans la zone de texte **URL de la Page connexion** .
    3.  Dans le portail classique de Microsoft Azure, sur la page **configuration de l’authentification unique à ThousandEyes** , copiez la valeur **d’URL de déconnexion à distance** et puis la coller dans la zone de texte **URL de la Page déconnexion** .
    4.  Dans le portail classique de Microsoft Azure, sur la page **configuration de l’authentification unique à ThousandEyes** , copiez la valeur de **l’URL de l’émetteur** et puis la coller dans la zone de texte **d’Émetteur de fournisseur d’identité** .
    5.  Dans le **Certificat d’identité du fournisseur**, cliquez sur **Choisir un fichier**et ensuite télécharger le certificat que vous avez téléchargé à partir du portail classique Microsoft Azure.
    6.  Cliquez sur **Enregistrer**.

10. Sur le portail Azure classique, sélectionnez la confirmation de la configuration d’ouverture de session unique et puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer Single Sign On** .

    ![Configurer la fonctionnalité d’authentification unique] (./media/active-directory-saas-thousandeyes-tutorial/IC790070.png "Configurer la fonctionnalité d’authentification unique")

##<a name="configuring-user-provisioning"></a>Configuration d’approvisionnement de l’utilisateur
  
Afin de permettre aux utilisateurs d’AD Azure pour vous connecter à ThousandEyes, il doivent être configurés dans ThousandEyes.  
Dans le cas de ThousandEyes, la mise en service est une tâche manuelle.

###<a name="to-provision-a-user-account-to-thousandeyes-perform-the-following-steps"></a>Pour configurer un compte d’utilisateur à ThousandEyes, effectuez les opérations suivantes :

1.  Ouvrez une session en tant qu’administrateur dans le site de votre entreprise ThousandEyes.

2.  Cliquez sur **paramètres**.

    ![Paramètres] (./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Paramètres")

3.  Cliquez sur **compte**.

    ![Compte] (./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Compte")

4.  Cliquez sur l’onglet **comptes et les utilisateurs** .

    ![Comptes & utilisateurs] (./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Comptes & utilisateurs")

5.  Dans la section **Ajouter des utilisateurs et des comptes** , procédez comme suit :

    ![Ajouter des comptes d’utilisateurs] (./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Ajouter des comptes d’utilisateurs")

    1.  Tapez le **nom**, les **E-mails** et les autres détails d’un compte Azure Active Directory valide que vous souhaitez mettre en service dans les zones de texte liées.
    2.  Cliquez sur **Ajouter un nouvel utilisateur pour le compte**.

        >[AZURE.NOTE] Le titulaire du compte DAS recevront un message électronique incluant un lien pour confirmer et activer le compte.

>[AZURE.NOTE] Vous pouvez utiliser n’importe quel autres ThousandEyes utilisateur compte outils de création ou API fournies par ThousandEyes à disposition DAS des comptes d’utilisateurs.

##<a name="assigning-users"></a>Affectation d’utilisateurs
  
Pour tester votre configuration, vous devez accorder les utilisateurs AD Azure que vous souhaitez autoriser à l’aide de l’accès de l’application lui en leur affectant.

###<a name="to-assign-users-to-thousandeyes-perform-the-following-steps"></a>Pour affecter des utilisateurs à ThousandEyes, effectuez les opérations suivantes :

1.  Dans le portail Azure classique, créez un compte de test.

2.  Sur la page d’intégration **ThousandEyes** application, cliquez sur **affecter des utilisateurs**.

    ![Affecter des utilisateurs] (./media/active-directory-saas-thousandeyes-tutorial/IC790075.png "Affecter des utilisateurs")

3.  Sélectionnez votre utilisateur de test et cliquez sur **attribuer**, puis cliquez sur **Oui** pour confirmer votre affectation.

    ![Oui] (./media/active-directory-saas-thousandeyes-tutorial/IC767830.png "Oui")
  
Si vous souhaitez tester vos paramètres d’ouverture de session unique, ouvrez le panneau d’accès. Pour plus d’informations sur le panneau d’accès, consultez [Introduction au panneau d’accès](active-directory-saas-access-panel-introduction.md).
