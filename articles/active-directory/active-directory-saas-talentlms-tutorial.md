<properties 
    pageTitle="Didacticiel : Intégration de Azure Active Directory avec TalentLMS | Microsoft Azure" 
    description="Apprenez à utiliser TalentLMS avec Azure Active Directory pour activer l’ouverture de session unique, la mise en service automatique et bien plus encore !" 
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

#<a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Didacticiel : Intégration de Azure Active Directory avec TalentLMS
  
L’objectif de ce didacticiel est d’afficher l’intégration d’Azure et TalentLMS.  
Le scénario décrit dans ce didacticiel suppose que vous ayez les éléments suivants :

-   Un abonnement Azure valide
-   Un locataire TalentLMS
  
Après la fin de ce didacticiel, les utilisateurs AD Azure que vous avez affecté à TalentLMS pourront ouverture de session unique dans l’application à votre site de la société TalentLMS (service fournisseur initiée signe), ou à l’aide de l' [Introduction dans le panneau d’accès](active-directory-saas-access-panel-introduction.md).
  
Le scénario décrit dans ce didacticiel comprend les éléments suivants :

1.  L’activation de l’intégration de l’application pour TalentLMS
2.  Configuration de l’authentification unique
3.  Configuration d’approvisionnement de l’utilisateur
4.  Affectation d’utilisateurs

![Scénario] (./media/active-directory-saas-talentlms-tutorial/IC777289.png "Scénario")

##<a name="enabling-the-application-integration-for-talentlms"></a>L’activation de l’intégration de l’application pour TalentLMS
  
L’objectif de cette section doit décrire comment activer l’intégration de l’application pour TalentLMS.

###<a name="to-enable-the-application-integration-for-talentlms-perform-the-following-steps"></a>Pour activer l’intégration de l’application pour TalentLMS, effectuez les opérations suivantes :

1.  Dans le portail Azure classique, dans le volet de navigation de gauche, cliquez sur **Active Directory**.

    ![Active Directory] (./media/active-directory-saas-talentlms-tutorial/IC700993.png "Active Directory")

2.  Dans la liste **répertoire** , sélectionnez le répertoire pour lequel vous souhaitez activer l’intégration d’annuaire.

3.  Pour ouvrir la vue des applications, dans la vue du répertoire, cliquez sur **Applications** dans le menu supérieur.

    ![Applications] (./media/active-directory-saas-talentlms-tutorial/IC700994.png "Applications")

4.  Cliquez sur **Ajouter** au bas de la page.

    ![Ajouter application] (./media/active-directory-saas-talentlms-tutorial/IC749321.png "Ajouter application")

5.  Dans la boîte de dialogue **que voulez-vous faire** , cliquez sur **Ajouter une application à partir de la galerie**.

    ![Ajouter une application à partir de gallerry] (./media/active-directory-saas-talentlms-tutorial/IC749322.png "Ajouter une application à partir de gallerry")

6.  Dans la **zone Rechercher**, tapez **TalentLMS**.

    ![Galerie des applications] (./media/active-directory-saas-talentlms-tutorial/IC777290.png "Galerie des applications")

7.  Dans le volet de résultats, sélectionnez **TalentLMS**, puis cliquez sur **Terminer** pour ajouter l’application.

    ![TalentLMS] (./media/active-directory-saas-talentlms-tutorial/IC777291.png "TalentLMS")

##<a name="configuring-single-sign-on"></a>Configuration de l’authentification unique
  
L’objectif de cette section doit décrire comment permettre aux utilisateurs de s’authentifier auprès de TalentLMS avec leur compte Azure annonce à l’aide de la fédération basée sur le protocole SAML. .  
Configuration de l’authentification unique pour TalentLMS vous demande de récupérer une valeur de l’empreinte d’un certificat.  
Si vous n’êtes pas familiarisé avec cette procédure, reportez-vous à la section [comment récupérer la valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).

###<a name="to-configure-single-sign-on-perform-the-following-steps"></a>Pour configurer l’authentification unique, procédez comme suit :

1.  Dans Azure portal classique, sur la page d’intégration **TalentLMS** application, cliquez **sur Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer Single Sign On** .

    ![De configurer l’authentification unique] (./media/active-directory-saas-talentlms-tutorial/IC777292.png "De configurer l’authentification unique")

2.  Dans la page **Comment voulez-vous que les utilisateurs à se connecter à TalentLMS** , sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.

    ![De configurer l’authentification unique] (./media/active-directory-saas-talentlms-tutorial/IC777293.png "De configurer l’authentification unique")

3.  Dans la page **Configurer l’URL App** , dans la zone de texte **TalentLMS URL de connexion** , tapez l’URL de votre en utilisant le modèle suivant «*https://\<nom du locataire\>. TalentLMSapp.com*», puis cliquez sur **suivant**.

    ![URL pour l’ouverture de session] (./media/active-directory-saas-talentlms-tutorial/IC777294.png "URL pour l’ouverture de session")

4.  Dans la page **configuration de l’authentification unique au TalentLMS** , pour télécharger votre certificat, cliquez sur **Télécharger le certificat**et enregistrez-le localement le fichier de certificat en tant que **c:\\TalentLMS.cer**.

    ![Configurer l’authentification unique] (./media/active-directory-saas-talentlms-tutorial/IC777295.png "Configurer l’authentification unique")

5.  Dans une fenêtre de navigateur web différent, ouvrez une session dans le site de votre entreprise TalentLMS en tant qu’administrateur.

6.  Dans la section **comptes et paramètres** , cliquez sur l’onglet **utilisateurs** .

    ![Paramètres de & compte] (./media/active-directory-saas-talentlms-tutorial/IC777296.png "Paramètres de & compte")

7.  Cliquez sur **Single Sign-On (SSO)**,

8.  Dans la section Single Sign-On, effectuez les opérations suivantes :

    ![L’ouverture de session unique] (./media/active-directory-saas-talentlms-tutorial/IC777297.png "L’ouverture de session unique")

    1.  Dans la liste **type d’intégration de l’authentification unique** , sélectionnez **SAML 2.0**.
    2.  Dans le portail Azure classique, sur la page de la boîte de dialogue **configuration de l’authentification unique à TalentLMS** , copiez la valeur de **l’ID de fournisseur d’identité** et puis la coller dans la zone de texte du **fournisseur d’identité (IdP)** .
    3.  Copier la valeur de **l’empreinte numérique** du certificat exporté et puis la coller dans la zone de texte **D’empreinte digitale du certificat** .

        >[AZURE.TIP] Pour plus d’informations, consultez [comment récupérer la valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI)

    4.  Dans le portail Azure classique, sur la page de la boîte de dialogue **configuration de l’authentification unique à TalentLMS** , copiez la valeur de **L’URL de connexion à distance** et puis la coller dans la zone de texte **URL de connexion à distance** .
    5.  Dans le portail Azure classique, sur la page de la boîte de dialogue **configuration de l’authentification unique à TalentLMS** , copiez la valeur **d’URL de déconnexion à distance** et puis la coller dans la zone de texte **URL de déconnexion à distance** .
    6.  Dans la zone de texte **TargetedID** , tapez **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name**
    7.  Dans la zone de texte **nom** , tapez **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    8.  Dans la zone de texte **nom** , tapez **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    9.  Dans la zone de texte **message** , tapez **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**
    10. Cliquez sur **Enregistrer**.

9.  Sur le portail Azure classique, sélectionnez la confirmation de la configuration d’ouverture de session unique et puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer Single Sign On** .

    ![Configurer l’authentification unique] (./media/active-directory-saas-talentlms-tutorial/IC777298.png "Configurer l’authentification unique")

##<a name="configuring-user-provisioning"></a>Configuration d’approvisionnement de l’utilisateur
  
Afin de permettre aux utilisateurs d’AD Azure pour vous connecter à TalentLMS, il doivent être configurés dans TalentLMS.  
Dans le cas de TalentLMS, la mise en service est une tâche manuelle.

###<a name="to-provision-a-user-accounts-perform-the-following-steps"></a>Pour configurer un compte d’utilisateur, effectuez les opérations suivantes :

1.  Connectez-vous à vos clients **TalentLMS** .

2.  Cliquez sur **utilisateurs**, puis cliquez sur **Ajouter un utilisateur**.

3.  Sur la page de la boîte de dialogue **Ajouter un utilisateur** , effectuez les opérations suivantes :

    ![Ajouter utilisateur] (./media/active-directory-saas-talentlms-tutorial/IC777299.png "Ajouter utilisateur")

    1.  Tapez les valeurs de l’attribut associé du compte d’utilisateur Active Directory Azure dans les zones de texte suivantes : **prénom**, **nom**, **adresse de messagerie**.
    2.  Cliquez sur **Ajouter un utilisateur**.

>[AZURE.NOTE] Vous pouvez utiliser n’importe quel autres TalentLMS utilisateur compte outils de création ou API fournies par TalentLMS à disposition DAS des comptes d’utilisateurs.

##<a name="assigning-users"></a>Affectation d’utilisateurs
  
Pour tester votre configuration, vous devez accorder les utilisateurs AD Azure que vous souhaitez autoriser à l’aide de l’accès de l’application lui en leur affectant.

###<a name="to-assign-users-to-talentlms-perform-the-following-steps"></a>Pour affecter des utilisateurs à TalentLMS, effectuez les opérations suivantes :

1.  Dans le portail Azure classique, créez un compte de test.

2.  Sur la page d’intégration **TalentLMS **application, cliquez sur **affecter des utilisateurs**.

    ![Affecter des utilisateurs] (./media/active-directory-saas-talentlms-tutorial/IC777300.png "Affecter des utilisateurs")

3.  Sélectionnez votre utilisateur de test et cliquez sur **attribuer**, puis cliquez sur **Oui** pour confirmer votre affectation.

    ![Oui] (./media/active-directory-saas-talentlms-tutorial/IC767830.png "Oui")
  
Si vous souhaitez tester vos paramètres d’ouverture de session unique, ouvrez le panneau d’accès. Pour plus d’informations sur le panneau d’accès, consultez [Introduction au panneau d’accès](active-directory-saas-access-panel-introduction.md).