---
title: "aaaAdd wypychania powiadomień tooyour Windows platformy Uniwersalnej aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure App Service Mobile Apps i usługi Azure Notification Hubs toosend wypychanie powiadomień tooyour Windows platformy Uniwersalnej aplikacji."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Dodawanie aplikacji dla systemu Windows tooyour powiadomień wypychanych
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku, możesz dodać toohello powiadomień wypychanych [szybki start systemu Windows](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Rejestrowanie aplikacji dla usługi powiadomień wypychanych
Możesz toosubmit Twojego toohello aplikacji Sklepu Windows, a następnie skonfiguruj toointegrate projektu z serwera z wypychania toosend powiadomienia usługi WNS (Windows).

1. W programie Visual Studio Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji platformy uniwersalnej systemu Windows hello, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepu hello...** .

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. W Kreatorze powitania kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.
3. Po rejestracji aplikacji hello jest hello został pomyślnie utworzony, wybierz nową nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**. Spowoduje to dodanie manifest aplikacji toohello informacji o rejestracji Sklepu Windows hello wymagane.  
4. Przejdź toohello [Centrum deweloperów systemu Windows](https://dev.windows.com/en-us/overview), logowanie przy użyciu konta Microsoft, kliknij przycisk hello nowej rejestracji aplikacji w **Moje aplikacje**, następnie rozwiń węzeł **usług**  >  **Powiadomienia wypychane**.
5. W hello **powiadomienia wypychane** kliknij przycisk **witryna usług Live** w obszarze **Microsoft Azure Mobile Services**.
6. Hello strony rejestracji, zanotuj wartości hello na **klucze tajne aplikacji** i hello **identyfikatora SID pakietu**, który można następnie użyje tooconfigure zaplecza aplikacji mobilnej.

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > klucz tajny powitania klienta i identyfikatora SID pakietu są ważnymi poświadczeniami zabezpieczeń. Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją. Witaj **identyfikator aplikacji** jest używany z hello tajny tooconfigure Account Microsoft uwierzytelniania.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Konfigurowanie powiadomień wypychanych toosend hello w wewnętrznej bazie danych
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Zaktualizuj powiadomień wypychanych toosend serwera hello
Użyj poniższej procedury hello, odpowiadający danemu typowi projektu zaplecza&mdash;albo [zaplecza .NET](#dotnet) lub [zaplecza Node.js](#nodejs).

### <a name="dotnet"></a>Projektu zaplecza .NET
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj Microsoft.Azure.NotificationHubs, a następnie kliknij przycisk **zainstalować**. Spowoduje to zainstalowanie biblioteki klienta usługi Notification Hubs hello.
2. Rozwiń węzeł **kontrolerów**, otwórz TodoItemController.cs i dodać hello następujące instrukcje using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. W hello **PostTodoItem** metody, Dodaj hello następującego kodu po wywołaniu hello zbyt**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Ten kod informuje toosend Centrum powiadomień hello powiadomienie wypychane po Wstawianie nowego elementu.
4. Ponownie opublikować hello na serwerze project Server.

### <a name="nodejs"></a>Projektu zaplecza node.js
1. Jeśli jeszcze tego nie zrobiono, [pobieranie projektu Szybki Start hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) lub w przeciwnym razie użyj hello [edytora online w portalu Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Zastąp hello istniejący kod w pliku todoitem.js hello hello następujące czynności:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
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

    To wysyła wyskakujących powiadomień WNS zawierający item.text powitania po wstawieniu nowe zadanie do wykonania.
3. Podczas edytowania pliku hello na komputerze lokalnym, należy ponownie opublikować hello na serwerze project Server.

## <a id="update-app"></a>Dodaj aplikację tooyour powiadomień wypychanych
Następnie zarejestrować dla powiadomień wypychanych przy uruchamianiu aplikacji. Podczas uwierzytelniania jest jeszcze włączone, upewnij się, że hello zalogowaniu się użytkownika przed podjęciem próby tooregister dla powiadomień wypychanych.

1. Otwórz hello **App.xaml.cs** pliku projektu i dodaj następujące hello `using` instrukcji:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. W hello tego samego pliku, należy dodać następujące hello **InitNotificationsAsync** toohello definicję metody **aplikacji** klasy:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Ten kod pobiera hello ChannelURI dla aplikacji hello z usługi WNS, a następnie rejestruje ten ChannelURI w aplikacji mobilnej usługi aplikacji.
3. U góry hello hello **OnLaunched** obsługi zdarzeń w **App.xaml.cs**, Dodaj hello **async** definicję metody toohello modyfikator i dodaj następujące hello wywołanie Nowetoohello **InitNotificationsAsync** metody hello poniższy przykład:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Gwarantuje to tego hello krótkim okresie ChannelURI jest zarejestrowana na każdym razem, gdy aplikacja hello jest uruchomiona.
4. Ponownie skompiluj projekt aplikacji platformy uniwersalnej systemu Windows. Aplikacja jest teraz gotowy tooreceive wyskakujące powiadomienia.

## <a id="test"></a>Testowych powiadomień wypychanych w aplikacji
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Następne kroki
Dowiedz się więcej na temat powiadomień wypychanych:

* [Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Szablony umożliwiają wypchnięć wieloplatformowych toosend elastyczność i wypchnięć zlokalizowane. Dowiedz się, jak szablony tooregister.
* [Diagnozowanie problemów powiadomień wypychanych](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach. W tym temacie pokazano, jak tooanalyze i ustalenie potrzebnej głównego hello. Przyczyna niepowodzenia powiadomień wypychanych.

Należy rozważyć kontynuować tooone hello następujące samouczki:

* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.
* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej. Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
