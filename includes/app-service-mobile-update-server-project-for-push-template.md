<span data-ttu-id="d44d0-101">W tej sekcji zaktualizuj kod w istniejących projektu zaplecza aplikacji mobilnej do wysyłania powiadomień wypychanych za każdym razem, gdy zostanie dodany nowy element.</span><span class="sxs-lookup"><span data-stu-id="d44d0-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="d44d0-102">Jest to obsługiwane przez [szablonu](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funkcji usługi Azure Notification Hubs, włączanie wypchnięć między platformami.</span><span class="sxs-lookup"><span data-stu-id="d44d0-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="d44d0-103">Różnych klientów są zarejestrowane dla powiadomień wypychanych przy użyciu szablonów i jednego wypychania uniwersalnych może uzyskać dostęp do wszystkich platform klienta.</span><span class="sxs-lookup"><span data-stu-id="d44d0-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="d44d0-104">Wybierz jedną z następujących procedur, które jest zgodny z typem projektu zaplecza&mdash;albo [zaplecza .NET](#dotnet) lub [zaplecza Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="d44d0-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="d44d0-105"><a name="dotnet"></a>Projektu zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="d44d0-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="d44d0-106">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d44d0-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="d44d0-107">Wyszukaj `Microsoft.Azure.NotificationHubs`, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="d44d0-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="d44d0-108">Spowoduje to zainstalowanie biblioteki centra powiadomień do wysyłania powiadomień z sieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="d44d0-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="d44d0-109">Otwórz projekt serwera **kontrolerów** > **TodoItemController.cs**i dodaj następujące instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="d44d0-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="d44d0-110">W **PostTodoItem** metody, Dodaj następujący kod po wywołaniu **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="d44d0-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="d44d0-111">To wysyła powiadomienie szablonu, który zawiera element. Tekst, gdy znajduje się nowy element.</span><span class="sxs-lookup"><span data-stu-id="d44d0-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="d44d0-112">Ponownie opublikować projekt serwera.</span><span class="sxs-lookup"><span data-stu-id="d44d0-112">Republish the server project.</span></span>

### <span data-ttu-id="d44d0-113"><a name="nodejs"></a>Projektu zaplecza node.js</span><span class="sxs-lookup"><span data-stu-id="d44d0-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="d44d0-114">Jeśli jeszcze tego nie zrobiono, [projektu zaplecza Szybki Start Pobierz](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), lub użyj innego [edytora online w portalu Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="d44d0-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="d44d0-115">Zastąp istniejący kod w todoitem.js następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d44d0-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="d44d0-116">To wysyła powiadomienie szablon zawierający item.text po wstawieniu nowego elementu.</span><span class="sxs-lookup"><span data-stu-id="d44d0-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="d44d0-117">Podczas edytowania pliku na komputerze lokalnym, należy ponownie opublikować projekt serwera.</span><span class="sxs-lookup"><span data-stu-id="d44d0-117">When editing the file on your local computer, republish the server project.</span></span>
