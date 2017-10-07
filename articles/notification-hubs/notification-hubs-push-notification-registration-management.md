---
title: "aaaRegistration zarządzania"
description: "W tym temacie wyjaśniono, jak tooregister urządzeniami przy użyciu usługi notification hubs w kolejności tooreceive powiadomienia wypychane."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Zarządzanie rejestracją
## <a name="overview"></a>Omówienie
W tym temacie wyjaśniono, jak tooregister urządzeniami przy użyciu usługi notification hubs w kolejności tooreceive powiadomienia wypychane. Hello tematu opisano rejestracji na wysokim poziomie, a następnie wprowadza hello dwa główne wzorców do rejestracji urządzeń: rejestrowanie na urządzeniu hello bezpośrednio toohello Centrum powiadomień i rejestrowanie za pomocą wewnętrznej bazy danych aplikacji. 

## <a name="what-is-device-registration"></a>Co to jest rejestracja urządzenia
Rejestracja urządzenia z Centrum powiadomień odbywa się przy użyciu **rejestracji** lub **instalacji**.

#### <a name="registrations"></a>Rejestracje
Rejestracja kojarzy powitalne obsługi usługi powiadomień platformy (PNS) dla urządzeń z tagami i prawdopodobnie szablonu. dojście systemu powiadomień platformy Hello można ChannelURI, token urządzenia lub identyfikator rejestracji usługi GCM. Tagi są używane tooroute powiadomienia toohello poprawny zestaw dojść urządzeń. Aby uzyskać więcej informacji, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md). Szablony są używane tooimplement na rejestracji przekształcenia. Aby uzyskać więcej informacji, zobacz [szablony](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Instalacje
Instalacja jest rozszerzonych właściwości powiązanych z rejestrację, która zawiera zbiór wypychania. Jest hello tooregistering najnowsze i najlepsze rozwiązania z urządzenia. Jednak nie jest obsługiwany przez klienta po stronie zestawu SDK programu .NET ([SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) jeszcze.  Oznacza to, w przypadku rejestracji powitania klienta urządzenia, konieczne będzie toouse hello [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx) podejścia toosupport instalacji. Jeśli używasz usługi wewnętrznej bazy danych powinno być możliwe toouse [SDK Centrum powiadomień dla wewnętrznej bazy danych operacji](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Witaj poniżej przedstawiono niektóre instalacje toousing podstawowych zalet:

* Tworzenie lub aktualizowanie instalacji jest w pełni idempotentności. Dlatego możesz ponowić próbę jej bez żadnych problemów dotyczących rejestracji duplikatów.
* model instalacji Hello umożliwia łatwe toodo poszczególnych wypchnięć - przeznaczonych dla określonego urządzenia. Tag systemu **"$InstallationId: [identyfikator installationId]"** jest automatycznie dodawany z każdej instalacji na podstawie rejestracji. Dlatego można wywołać wysyłania toothis tag tootarget określonego urządzenia bez konieczności toodo dodatkowy kod.
* Przy użyciu instalacji umożliwia również należy toodo rejestracji częściowej aktualizacji. Witaj częściowej aktualizacji instalacji zażądano za pomocą metody poprawki przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902). Jest to szczególnie przydatne, należy tagi tooupdate na powitania rejestracji. Nie masz toopull dół całej rejestracji hello i ponownie Wyślij wszystkie tagi poprzedniej hello ponownie.

Instalacja produktu może zawierać hello hello następujące właściwości. Aby uzyskać pełną listę, zobacz właściwości instalacji hello [utworzyć ani zastąpić instalacji z interfejsu API REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) lub [właściwości instalacji](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) dla hello.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



Jest ważne toonote, którego rejestracji i instalacje domyślnie nie wygaśnie.

Rejestracje i instalacji musi zawierać prawidłowe dojście systemu powiadomień platformy dla każdego urządzenia/kanału. Ponieważ dojść systemu powiadomień platformy można uzyskać tylko w aplikacji klienta na powitania urządzeniu, jeden wzorzec jest tooregister bezpośrednio na tym urządzeniu z powitania klienta aplikacji. Na powitania inne strony, zagadnienia dotyczące zabezpieczeń i logiki biznesowej związanych z tootags może wymagać toomanage rejestracji urządzeń w zaplecze aplikacji hello. 

#### <a name="templates"></a>Szablony
Jeśli chcesz, aby toouse [szablony](notification-hubs-templates-cross-platform-push-messages.md), instalacja urządzenia hello również przechowywać wszystkie szablony skojarzone z tym urządzeniem w formacie JSON formatu (Zobacz przykład powyżej). Witaj nazwy szablonów pomocy target różnych szablonów dla hello tego samego urządzenia.

Należy pamiętać, że nazwa każdego szablonu mapuje treści szablonu tooa i opcjonalny zestaw tagów. Ponadto każdej z platform może mieć właściwości dodatkowe szablonu. Dla Sklepu Windows (przy użyciu usługi WNS) i Windows Phone 8 (przy użyciu usługi MPNS) dodatkowych zestawu nagłówków może być częścią hello szablonu. W przypadku hello APN można ustawić tooeither właściwości wygaśnięcia stałą lub tooa wyrażenia szablonu. Aby uzyskać pełną listę, zobacz właściwości instalacji hello [Tworzenie lub Zastąp instalacji REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) tematu.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Dodatkowej Kafelki aplikacji do Sklepu Windows
Dla aplikacji ze Sklepu Windows klienta wysyłania powiadomień jest Kafelki toosecondary hello takie same jak wysyłanie ich toohello główną. Ta jest obsługiwana w przypadku instalacji. Należy zauważyć, że dodatkowej Kafelki różnych ChannelUri, które hello zestawu SDK w aplikacji klienta obsługuje przezroczysty.

używa słownika SecondaryTiles Hello hello tego samego TileId, który jest obiektem SecondaryTiles hello toocreate używane w aplikacji ze Sklepu Windows.
Zgodnie z hello ChannelUri podstawowego, ChannelUris dodatkowej Kafelki można zmienić w dowolnym momencie. W przypadku kolejności tookeep hello instalacji w Centrum powiadomień hello zaktualizowane hello urządzenia należy odświeżyć je z hello bieżącego ChannelUris hello dodatkowej kafelków.

## <a name="registration-management-from-hello-device"></a>Zarządzanie rejestrację z urządzenia hello
Podczas zarządzania rejestracji urządzeń z aplikacji klienta, hello wewnętrznej bazy danych tylko jest odpowiedzialny za wysyłanie powiadomień. Aplikacje klienta zachować dojść systemu powiadomień platformy się toodate i zarejestruj tagów. Witaj, na poniższej ilustracji przedstawiono ten wzorzec.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

urządzenie Hello najpierw pobiera powitalne systemu powiadomień platformy obsługi z hello systemu powiadomień platformy, a następnie rejestruje z Centrum powiadomień hello bezpośrednio. Po pomyślnym rejestracji hello zaplecza aplikacji hello można wysłać powiadomienia targeting tej rejestracji. Aby uzyskać więcej informacji o tym, jak toosend powiadomień, zobacz [routingu i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).
Należy pamiętać, że w takim przypadku użyjesz nasłuchiwał tylko tooaccess praw użytkownika usługi notification hubs z hello urządzenia. Aby uzyskać więcej informacji, zobacz [zabezpieczeń](notification-hubs-push-notification-security.md).

Rejestracja urządzenia hello jest hello najprostszą metodą, ale ma kilka wad.
Witaj pierwszy wadą jest to, że aplikacja kliencka tylko aktualizowania jego tagi, gdy aplikacja hello jest aktywna. Na przykład jeśli użytkownik ma dwa urządzenia zarejestrować zespoły toosport powiązane tagi, gdy hello pierwszego urządzenia rejestruje dodatkowe tagów (na przykład Seahawks), hello drugiego urządzenia nie otrzymają powiadomienia hello o hello Seahawks do aplikacji hello na powitania drugie urządzenie jest wykonywany po raz drugi. Ogólnie rzecz biorąc gdy tagi jest narażony na wielu urządzeniach, zarządzanie tagów z zaplecza hello jest pożądane opcji.
drugi zwrot zarządzania rejestracji z powitania klienta aplikacji Hello jest, ponieważ aplikacje mogą być zaatakowane, zabezpieczanie rejestracji hello tagi toospecific wymaga szczególną uwagę, zgodnie z objaśnieniem w hello sekcję "zabezpieczenia poziomu znacznika."

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Przykład kodu tooregister z Centrum powiadomień z urządzeniem przy użyciu instalacji
W tej chwili obsługiwane wyłącznie przy użyciu hello [interfejsu API REST centra powiadomień](https://msdn.microsoft.com/library/mt621153.aspx).

Umożliwia także metodę PATCH hello przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizowania hello instalacji.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Przykład kodu tooregister z Centrum powiadomień z urządzenia przy użyciu rejestracji
Te metody Utwórz lub zaktualizuj rejestracji dla urządzenia hello, na którym są one nazywane. Oznacza to, że w kolejności tooupdate hello dojścia lub hello tagów, musi zastąpić hello całego rejestracji. Należy pamiętać, że rejestracje przejściowe, więc powinien zawsze mieć niezawodnej magazynu z hello bieżącego tagi, które wymaga określonego urządzenia.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Zarządzanie rejestracji z poziomu zaplecza
Zarządzanie rejestracje z zaplecza hello wymaga zapisywania dodatkowy kod. Witaj aplikacji z urządzenia hello podać hello zaktualizowane zaplecza toohello dojście systemu powiadomień platformy w każdym uruchomieniu aplikacji hello (wraz z tagami i szablonów) i hello wewnętrznej bazy danych należy zaktualizować ta dojścia na powitania Centrum powiadomień. Witaj, na poniższej ilustracji przedstawiono ten projekt.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

Zalety Hello Zarządzanie rejestracje z zaplecza hello obejmują hello możliwości toomodify tagi tooregistrations nawet wtedy, gdy hello odpowiednich aplikacji na urządzeniu hello jest nieaktywny i tooauthenticate powitania klienta aplikacji przed dodaniem rejestracji tooits tagu.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Przykład kodu tooregister z Centrum powiadomień z zaplecza, przy użyciu instalacji
powitania klienta urządzenia nadal pobiera jego dojście systemu powiadomień platformy i właściwości instalacji w odpowiednich jak wcześniej, a następnie wywołania niestandardowego interfejsu API hello wewnętrznej bazy danych, można dokonać rejestracji hello i autoryzować znaczniki wewnętrznej bazy danych itp. hello można wykorzystać hello [SDK Centrum powiadomień dla operacje zaplecza](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Umożliwia także metodę PATCH hello przy użyciu hello [standard JSON poprawki](https://tools.ietf.org/html/rfc6902) aktualizowania hello instalacji.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Przykład kodu tooregister z Centrum powiadomień z urządzenia przy użyciu identyfikatora rejestracji
Z poziomu zaplecza aplikacji można wykonywać podstawowe operacje CRUDS rejestracji. Na przykład:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


Witaj wewnętrznej bazy danych musi obsługiwać współbieżności między aktualizacjami rejestracji. Usługa Service Bus udostępnia optymistyczne sterowanie współbieżnością zarządzania rejestracji. Na poziomie hello HTTP ten sposób jest implementowany z użyciem hello ETag na operacji zarządzania rejestracji. Ta funkcja służy niewidocznie SDKs firmy Microsoft, które zgłosić wyjątek, jeśli aktualizacji zostało odrzucone ze względów współbieżności. zaplecze aplikacji Hello jest odpowiedzialny za obsługę tych wyjątków i ponowienie próby hello aktualizacji, jeśli jest to wymagane.

