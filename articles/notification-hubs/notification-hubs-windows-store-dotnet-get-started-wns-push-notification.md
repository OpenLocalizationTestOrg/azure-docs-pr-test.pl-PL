---
title: "wprowadzenie do usługi Azure Notification Hubs dla systemu Windows Universal platformy aplikacji aaaGet | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs toopush powiadomienia tooa aplikacji platformy uniwersalnej systemu Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Rozpoczynanie pracy z usługą Azure Notification Hubs dla aplikacji platformy uniwersalnej systemu Windows
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa Windows platformy Uniwersalnej aplikacji.

W tym samouczku utworzysz pustą aplikację Sklepu Windows, która odbiera powiadomienia wypychane przy użyciu hello wypychania powiadomienia usługi WNS (Windows). Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.

## <a name="before-you-begin"></a>Przed rozpoczęciem
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* Program [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) lub nowszy
* [Zainstalowane narzędzia do programowania aplikacji uniwersalnych systemu Windows](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Aktywne konto platformy Azure <br/>Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Aktywne konto Sklepu Windows

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji platformy uniwersalnej systemu Windows.

## <a name="register-your-app-for-hello-windows-store"></a>Rejestrowanie aplikacji dla Sklepu Windows hello
toosend aplikacji tooUWP powiadomienia wypychane, należy skojarzyć z toohello aplikacji Sklepu Windows. Następnie należy skonfigurować Twoje toointegrate Centrum powiadomień z usługą WNS.

1. Jeśli nie zarejestrowano jeszcze aplikacji, przejdź toohello [Centrum deweloperów systemu Windows](https://dev.windows.com/overview), zaloguj się przy użyciu konta Microsoft, a następnie kliknij przycisk **Utwórz nową aplikację**.

2. Wpisz nazwę aplikacji i kliknij pozycję **Rezerwuj nazwę aplikacji**. Spowoduje to utworzenie nowej rejestracji aplikacji w Sklepie Windows.

3. W programie Visual Studio Utwórz nowy projekt Visual C# aplikacji ze sklepu za pomocą uniwersalnych systemu Windows hello **pusta aplikacja** szablon i kliknij przycisk **OK**.

4. Zaakceptuj ustawienia domyślne powitania dla docelowej hello i minimalną platformy wersji.

5. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows hello, kliknij przycisk **magazynu**, a następnie kliknij przycisk **Skojarz aplikację ze sklepu hello...** . hello **kojarzenie aplikacji ze Sklepu Windows hello** zostanie wyświetlony Kreator.

6. W Kreatorze hello Zaloguj się przy użyciu konta Microsoft.

7. Kliknij aplikację hello zarejestrowaną w kroku 2, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**. Spowoduje to dodanie manifest aplikacji toohello informacji o rejestracji Sklepu Windows hello wymagane.

8. Wstecz na powitania [Centrum deweloperów systemu Windows](http://dev.windows.com/overview) dla nowej aplikacji kliknij pozycję **usług**, kliknij przycisk **powiadomienia wypychane**, a następnie kliknij przycisk **WNS/MPNS**.

9. Kliknij pozycję **Nowe powiadomienie**.

10. Kliknij szablon **Puste (wyskakujące)**, a następnie kliknij przycisk **OK**.

11. Wprowadź **Nazwę** powiadomienia i komunikat **Kontekst** wizualizacji. Następnie kliknij pozycję **Zapisz jako wersję roboczą**.

12. Przejdź toohello [portalu rejestracji aplikacji](http://apps.dev.microsoft.com) i zaloguj się.

13. Kliknij nazwę swojej aplikacji. Zanotuj hello **klucz tajny aplikacji** hasło i hello **identyfikator zabezpieczeń (SID) pakietu** znajduje się w hello **Sklepu Windows** ustawienia platformy.

     > [AZURE.WARNING]
    klucz tajny aplikacji Hello i identyfikatora SID pakietu są ważnymi poświadczeniami zabezpieczeń. Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją.

## <a name="configure-your-notification-hub"></a>Konfigurowanie centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Wybierz hello <b>usługi powiadomień</b> opcja i hello <b>systemu Windows (WNS)</b> opcji. Następnie wprowadź hello <b>klucz tajny aplikacji</b> hasło w hello <b>klucz zabezpieczeń</b> pola. Wprowadź użytkownika <b>identyfikatora SID pakietu</b> wartość uzyskane z usługi WNS w poprzedniej sekcji hello, a następnie kliknij przycisk <b>zapisać</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Centrum powiadomień jest teraz skonfigurowany toowork z usługą WNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia.

## <a name="connect-your-app-toohello-notification-hub"></a>Łączenie aplikacji toohello Centrum powiadomień
1. W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
   
    Spowoduje to wyświetlenie hello **Zarządzaj pakietami NuGet** okno dialogowe.
2. Wyszukaj `WindowsAzure.Messaging.Managed` i kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.
   
    ![][20]
   
    To spowoduje pobranie, instaluje i dodaje odwołanie do biblioteki Azure Messaging toohello dla systemu Windows za pomocą hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pakietu WindowsAzure.Messaging.Managed NuGet</a>.
3. Otwórz plik projektu App.xaml.cs hello i dodaj następujące hello `using` instrukcje. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Również w pliku App.xaml.cs Dodaj następujące hello **InitNotificationsAsync** toohello definicję metody **aplikacji** klasy:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Ten kod pobiera identyfikator URI kanału hello aplikacji hello z usługi WNS, a następnie rejestruje ten identyfikator URI kanału w Centrum powiadomień.
   
   > [!NOTE]
   > Upewnij się, że tooreplace hello symbolu zastępczego "Twoje hub name" nazwą hello hello Centrum powiadomień wyświetlaną w portalu Azure hello. Również Zastąp symbol zastępczy parametrów połączenia hello hello **DefaultListenSharedAccessSignature** ciąg połączenia, który został uzyskany z hello **zasady dostępu** strony w Centrum powiadomień poprzedniej sekcji.
   > 
   > 
5. U góry hello hello **OnLaunched** obsługi zdarzeń w pliku App.xaml.cs Dodaj hello następujące nowe toohello wywołania **InitNotificationsAsync** metody:
   
        InitNotificationsAsync();
   
    Gwarantuje to tego kanału hello. identyfikator URI jest rejestrowany w Centrum powiadomień, które każda aplikacja hello czasu jest uruchamiana.
6. Naciśnij klawisz hello **F5** aplikacji hello toorun klucza. Podręczne okno dialogowe, który zawiera klucz rejestracji hello jest wyświetlany.

Aplikacja jest teraz gotowy tooreceive wyskakujące powiadomienia.

## <a name="send-notifications"></a>Wysyłanie powiadomień
Możesz szybko przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [Azure Portal](https://portal.azure.com/) przy użyciu hello **wysyłanie testowe** znajdującego się na powitania Centrum powiadomień, jak pokazano na poniższym zrzucie ekranu hello.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki. Umożliwia także hello interfejsu API REST bezpośrednio toosend powiadomień wiadomości, jeśli biblioteka nie jest dostępna dla sieci wewnętrznej. 

W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK. Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET. Jednak po podejścia hello może służyć do wysyłania powiadomień:

* **Interfejs REST**: powiadomienia mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplikacje mobilne platformy Azure**: na przykład jak toosend powiadomienia z aplikacji mobilnej Azure, który jest zintegrowany z usługą Notification Hubs, zobacz [Dodawanie powiadomień wypychanych do aplikacji mobilnej](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: przykład sposobu toosend powiadomienia za pomocą hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Opcjonalnie) Wysyłanie powiadomień z poziomu aplikacji konsolowej
toosend powiadomienia za pomocą aplikacji konsoli .NET, wykonaj następujące kroki. 

1. Rozwiązanie powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** i **nowy projekt...** , a następnie w obszarze **Visual C#**, kliknij przycisk **Windows** i **aplikacji konsoli**i kliknij przycisk **OK**.
   
    Spowoduje to dodanie nowego Visual C# console application toohello rozwiązania. Można to również zrobić w oddzielnym rozwiązaniu.

2. W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.
   
    Spowoduje to wyświetlenie konsoli Menedżera pakietów hello w programie Visual Studio.
3. W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Otwórz plik Program.cs hello i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
5. W hello **Program** klasy, Dodaj hello następujące metody:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Upewnij się, że używasz hello parametry połączenia, które ma **pełne** dostępu nie **nasłuchiwania** dostępu. Parametry połączenia Hello dostępu do nasłuchiwania nie mają uprawnień toosend powiadomienia.
   > 
   > 
6. Dodaj następujące wiersze w hello hello **Main** metody:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Kliknij prawym przyciskiem myszy projekt aplikacji hello konsoli w programie Visual Studio, a następnie kliknij przycisk **Ustaw jako projekt startowy** tooset go jako projekt startowy hello. Następnie naciśnij klawisz hello **F5** aplikacji hello toorun klucza.
   
    Otrzymasz wyskakujące powiadomienie na wszystkich zarejestrowanych urządzeniach. Kliknięcie lub naciśnięcie hello baneru wyskakującego powiadomienia spowoduje załadowanie aplikacji hello.

Wszystkie hello obsługiwane ładunki można znaleźć w hello [wykazu powiadomień wyskakujących], [wykazu kafelków], i [omówienia znaczków] tematów w witrynie MSDN.

## <a name="next-steps"></a>Następne kroki
W tym prostym przykładzie wysłano wyemitowane powiadomienia tooall urządzeń z systemem Windows za pomocą portalu hello lub aplikacji konsoli. Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku. Przedstawiono w nim sposób toosend powiadomień z zaplecza ASP.NET za pomocą tagów tootarget określonych użytkowników.

Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zobacz [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. 

toolearn więcej ogólnych informacji o usłudze Notification Hubs, zobacz [wskazówki dotyczące usługi Notification Hubs](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[wykazu powiadomień wyskakujących]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[wykazu kafelków]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[omówienia znaczków]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
