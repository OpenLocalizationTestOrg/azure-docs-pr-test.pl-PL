<span data-ttu-id="41993-101">W tej sekcji należy zaktualizować kodu w Twojej istniejącego projektu zaplecza Mobile Apps toosend powiadomień wypychanych za każdym razem, gdy zostanie dodany nowy element.</span><span class="sxs-lookup"><span data-stu-id="41993-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="41993-102">Jest to obsługiwane przez hello [szablonu](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) funkcji usługi Azure Notification Hubs, włączanie wypchnięć między platformami.</span><span class="sxs-lookup"><span data-stu-id="41993-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="41993-103">Witaj różnych klientów są rejestrowane dla powiadomień wypychanych przy użyciu szablonów i pojedynczego wypychania uniwersalnych można uzyskać tooall platform klientów.</span><span class="sxs-lookup"><span data-stu-id="41993-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="41993-104">Wybierz jedną z procedur przedstawionych hello, odpowiadający danemu typowi projektu zaplecza&mdash;albo [zaplecza .NET](#dotnet) lub [zaplecza Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="41993-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="41993-105"><a name="dotnet"></a>Projektu zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="41993-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="41993-106">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="41993-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="41993-107">Wyszukaj `Microsoft.Azure.NotificationHubs`, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="41993-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="41993-108">Spowoduje to zainstalowanie hello biblioteki centra powiadomień do wysyłania powiadomień z sieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="41993-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="41993-109">W projekcie powitania serwera Otwórz **kontrolerów** > **TodoItemController.cs**i dodaj następujące hello instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="41993-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="41993-110">W hello **PostTodoItem** metody, Dodaj hello następującego kodu po wywołaniu hello zbyt**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="41993-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="41993-111">To wysyła powiadomienie szablonu, który zawiera element hello. Tekst, gdy znajduje się nowy element.</span><span class="sxs-lookup"><span data-stu-id="41993-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="41993-112">Ponownie opublikować hello na serwerze project Server.</span><span class="sxs-lookup"><span data-stu-id="41993-112">Republish hello server project.</span></span>

### <span data-ttu-id="41993-113"><a name="nodejs"></a>Projektu zaplecza node.js</span><span class="sxs-lookup"><span data-stu-id="41993-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="41993-114">Jeśli jeszcze tego nie zrobiono, [pobrać projektu zaplecza szybkiego startu hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), lub użyj else hello [edytora online w portalu Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="41993-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="41993-115">Zastąp istniejący kod hello w todoitem.js hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="41993-115">Replace hello existing code in todoitem.js with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="41993-116">To wysyła powiadomienie szablon zawierający item.text powitania po wstawieniu nowego elementu.</span><span class="sxs-lookup"><span data-stu-id="41993-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="41993-117">Podczas edytowania pliku hello na komputerze lokalnym, należy ponownie opublikować hello na serwerze project Server.</span><span class="sxs-lookup"><span data-stu-id="41993-117">When editing hello file on your local computer, republish hello server project.</span></span>
