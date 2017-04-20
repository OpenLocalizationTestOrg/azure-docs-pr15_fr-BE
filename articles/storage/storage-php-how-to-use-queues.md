<properties
    pageTitle="Comment faire pour utiliser le stockage de file d’attente à partir de PHP | Microsoft Azure"
    description="Apprenez à utiliser le service de stockage de file d’attente d’Azure pour créer et supprimer des files d’attente, insérer, obtenir et supprimer les messages. Exemples sont écrits en PHP."
    documentationCenter="php"
    services="storage"
    authors="robinsh"
    manager="carmonm"
    editor="tysonn"/>

<tags
    ms.service="storage"
    ms.workload="storage"
    ms.tgt_pltfrm="na"
    ms.devlang="PHP"
    ms.topic="article"
    ms.date="08/11/2016"
    ms.author="robinsh"/>

# <a name="how-to-use-queue-storage-from-php"></a>Comment faire pour utiliser le stockage de file d’attente à partir de PHP

[AZURE.INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]
<br/>
[AZURE.INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Vue d’ensemble

Ce guide vous explique comment exécuter des scénarios courants en utilisant le service de stockage de file d’attente d’Azure. Ces exemples sont écrits via les classes dans le Kit de développement logiciel Windows pour PHP. Les scénarios couverts comprennent Insertion, lecture, mise en route et suppression des messages de la file d’attente, ainsi que création et suppression de files d’attente.

[AZURE.INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[AZURE.INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Création d’une application PHP

La seule condition requise pour la création d’une application PHP qui accède au stockage de la file d’attente d’Azure est le faisant référence à des classes dans le Kit de développement Azure pour PHP à partir de votre code. Vous pouvez utiliser les outils de développement pour créer votre application, y compris le bloc-notes.

Dans ce guide, vous allez utiliser les fonctionnalités de stockage de file d’attente qui peuvent être appelées au sein d’une application PHP localement ou dans le code s’exécutant dans un rôle web Azure, le rôle de travail ou le site Web.

## <a name="get-the-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure

[AZURE.INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a>Configurez votre application pour accéder au stockage de la file d’attente

Pour utiliser l’API pour le stockage de la file d’attente d’Azure, vous devez :

1. Référence du fichier de chargeur automatique à l’aide de l’instruction [require_once] .
2. Référencer toutes les classes que vous pouvez utiliser.

L’exemple suivant montre comment inclure le fichier de chargeur automatique et faire référence à la classe **ServicesBuilder** .

> [AZURE.NOTE]
> Cet exemple montre comment (et autres exemples dans cet article) suppose que vous avez installé les bibliothèques clientes de PHP pour Azure via Composer. Si vous avez installé les bibliothèques manuellement, vous devez faire référence à la `WindowsAzure.php` fichier de chargeur automatique.

    require_once 'vendor/autoload.php';
    use WindowsAzure\Common\ServicesBuilder;


Dans les exemples ci-dessous, les `require_once` instruction apparaît toujours, mais seules les classes qui sont nécessaires pour exécuter l’exemple seront référencés.

## <a name="set-up-an-azure-storage-connection"></a>Configurer une connexion de stockage Azure

Pour instancier un client de stockage de file d’attente d’Azure, vous devez avoir une chaîne de connexion valide. Le format de la chaîne de connexion de service de file d’attente est la suivante.

Pour accéder à un service direct :

    DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]

Pour accéder au stockage de l’émulateur :

    UseDevelopmentStorage=true


Pour créer un client de service d’Azure, vous devez utiliser la classe **ServicesBuilder** . Vous pouvez utiliser une ou l’autre des techniques suivantes :

* Passez la chaîne de connexion directement.
* Utiliser le **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :
    * Par défaut, il est fourni avec prise en charge d’une source externe, les variables d’environnement.
    * Vous pouvez ajouter de nouvelles sources en étendant la classe **ConnectionStringSource** .

Pour les exemples présentés ici, la chaîne de connexion sera passée directement.

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;

    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);


## <a name="create-a-queue"></a>Créer une file d’attente

Un objet **QueueRestProxy** vous permet de créer une file d’attente à l’aide de la méthode **createQueue** . Lorsque vous créez une file d’attente, vous pouvez définir des options dans la file d’attente, mais cela n’est pas requis. (L’exemple ci-dessous montre comment définir des métadonnées sur une file d’attente.)

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;
    use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    // OPTIONAL: Set queue metadata.
    $createQueueOptions = new CreateQueueOptions();
    $createQueueOptions->addMetaData("key1", "value1");
    $createQueueOptions->addMetaData("key2", "value2");

    try {
        // Create queue.
        $queueRestProxy->createQueue("myqueue", $createQueueOptions);
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

> [AZURE.NOTE] Ne vous fiez pas sur le respect de la cas pour les clés de métadonnées. Toutes les clés sont lus à partir du service en minuscules.


## <a name="add-a-message-to-a-queue"></a>Ajouter un message à une file d’attente

Pour ajouter un message à une file d’attente, utilisez **QueueRestProxy -> createMessage**. La méthode prend le nom de la file d’attente, le texte du message et message options (facultatives).

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;
    use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    try {
        // Create message.
        $builder = new ServicesBuilder();
        $queueRestProxy->createMessage("myqueue", "Hello World!");
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

## <a name="peek-at-the-next-message"></a>Lire le message suivant

Vous pouvez lire un message (ou messages) à l’avant d’une file d’attente sans le supprimer de la file d’attente en appelant **QueueRestProxy -> peekMessages**. Par défaut, la méthode **peekMessage** retourne un seul message, mais vous pouvez modifier cette valeur en utilisant la méthode **PeekMessagesOptions -> setNumberOfMessages** .

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;
    use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    // OPTIONAL: Set peek message options.
    $message_options = new PeekMessagesOptions();
    $message_options->setNumberOfMessages(1); // Default value is 1.

    try {
        $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

    $messages = $peekMessagesResult->getQueueMessages();

    // View messages.
    $messageCount = count($messages);
    if($messageCount <= 0){
        echo "There are no messages.<br />";
    }
    else{
        foreach($messages as $message)  {
            echo "Peeked message:<br />";
            echo "Message Id: ".$message->getMessageId()."<br />";
            echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
            echo "Message text: ".$message->getMessageText()."<br /><br />";
        }
    }

## <a name="de-queue-the-next-message"></a>File d’attente du message suivant

Votre code supprime un message d’une file d’attente en deux étapes. Tout d’abord, vous appelez **QueueRestProxy -> listMessages**, qui rend le message invisible pour tout autre code qui lit à partir de la file d’attente. Par défaut, ce message restera invisible pendant 30 secondes. (Si le message n’est pas supprimé dans cette période, il va devenir visible sur la file d’attente à nouveau.) Pour terminer la suppression du message de la file d’attente, vous devez appeler **QueueRestProxy -> deleteMessage**. Ce processus en deux étapes de suppression d’un message garantit que lorsque votre code ne parvient pas à traiter un message en raison d’une défaillance matérielle ou logicielle, une autre instance de votre code peut obtenir le même message et essayez à nouveau. Votre code appelle **deleteMessage** droite une fois que le message a été traité.

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    // Get message.
    $listMessagesResult = $queueRestProxy->listMessages("myqueue");
    $messages = $listMessagesResult->getQueueMessages();
    $message = $messages[0];

    /* ---------------------
        Process message.
       --------------------- */

    // Get message ID and pop receipt.
    $messageId = $message->getMessageId();
    $popReceipt = $message->getPopReceipt();

    try {
        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

## <a name="change-the-contents-of-a-queued-message"></a>Modifier le contenu d’un message en file d’attente

Vous pouvez modifier le contenu d’un message sur place dans la file d’attente en appelant **QueueRestProxy -> updateMessage**. Si le message représente une tâche, vous pouvez utiliser cette fonctionnalité pour mettre à jour de l’état de la tâche. Le code suivant met à jour le message de la file d’attente avec le nouveau contenu, et il définit le délai d’attente de visibilité pour étendre un autre 60 secondes. Cela enregistre l’état d’un travail qui est associé avec le message, et il donne au client un autre minute pour continuer à travailler sur le message. Vous pouvez utiliser cette technique pour effectuer le suivi de plusieurs étapes de flux de travail dans la file d’attente messages, sans avoir à recommencer depuis le début en cas d’échec d’une étape de traitement en raison d’une défaillance matérielle ou logicielle. En général, vous conservez un nombre d’essais, et si le message est relancé plus de *n* fois, vous le supprimez. Cette option empêche un message qui déclenche une erreur d’application chaque fois qu’elle est traitée.

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    // Get message.
    $listMessagesResult = $queueRestProxy->listMessages("myqueue");
    $messages = $listMessagesResult->getQueueMessages();
    $message = $messages[0];

    // Define new message properties.
    $new_message_text = "New message text.";
    $new_visibility_timeout = 5; // Measured in seconds.

    // Get message ID and pop receipt.
    $messageId = $message->getMessageId();
    $popReceipt = $message->getPopReceipt();

    try {
        // Update message.
        $queueRestProxy->updateMessage("myqueue",
                                    $messageId,
                                    $popReceipt,
                                    $new_message_text,
                                    $new_visibility_timeout);
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

## <a name="additional-options-for-de-queuing-messages"></a>Options supplémentaires pour les files d’attente de messages

Il existe deux méthodes que vous pouvez personnaliser la récupération des messages à partir d’une file d’attente. Tout d’abord, vous pouvez obtenir un lot de messages (32 maximum). Ensuite, vous pouvez définir un délai d’attente plus longs ou plus courts de visibilité, permettant à votre code plus ou moins de temps à traiter entièrement chaque message. L’exemple de code suivant utilise la méthode **getMessages** pour obtenir les 16 messages en un seul appel. Puis il traite chaque message à l’aide d’une boucle **for** . Il définit également le délai d’expiration de l’invisibilité à cinq minutes pour chaque message.

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;
    use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    // Set list message options.
    $message_options = new ListMessagesOptions();
    $message_options->setVisibilityTimeoutInSeconds(300);
    $message_options->setNumberOfMessages(16);

    // Get messages.
    try{
        $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                         $message_options);
        $messages = $listMessagesResult->getQueueMessages();

        foreach($messages as $message){

            /* ---------------------
                Process message.
            --------------------- */

            // Get message Id and pop receipt.
            $messageId = $message->getMessageId();
            $popReceipt = $message->getPopReceipt();

            // Delete message.
            $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
        }
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

## <a name="get-queue-length"></a>Obtenir la longueur de la file d’attente

Vous pouvez obtenir une estimation du nombre de messages dans une file d’attente. La méthode **QueueRestProxy -> getQueueMetadata** demande le service de file d’attente pour renvoyer les métadonnées relatives à la file d’attente. L’appel de la méthode **getApproximateMessageCount** sur l’objet retourné fournit un décompte du nombre de messages dans une file d’attente. Le nombre n’est approximatif, car les messages peuvent être ajoutés ou supprimés une fois que le service de file d’attente répond à votre demande.

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    try {
        // Get queue metadata.
        $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
        $approx_msg_count = $queue_metadata->getApproximateMessageCount();
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }

    echo $approx_msg_count;

## <a name="delete-a-queue"></a>Supprimer une file d’attente

Pour supprimer une file d’attente et tous les messages qu’il contient, appelez la méthode **QueueRestProxy -> deleteQueue** .

    require_once 'vendor/autoload.php';

    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException;

    // Create queue REST proxy.
    $queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

    try {
        // Delete queue.
        $queueRestProxy->deleteQueue("myqueue");
    }
    catch(ServiceException $e){
        // Handle exception based on error codes and messages.
        // Error codes and messages are here:
        // http://msdn.microsoft.com/library/azure/dd179446.aspx
        $code = $e->getCode();
        $error_message = $e->getMessage();
        echo $code.": ".$error_message."<br />";
    }


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris les notions de base du stockage de la file d’attente d’Azure, suivre ces liens pour en savoir plus sur les tâches de stockage plus complexes :

- Visitez le [blog de l’équipe de stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Pour plus d’informations, consultez également le [Centre pour développeurs PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

