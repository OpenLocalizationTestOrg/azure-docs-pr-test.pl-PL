---
title: "aaaSending powiadomień wypychanych przy użyciu usługi Azure Notification Hubs na Windows Phone | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak powiadomienia toopush usługi Azure Notification Hubs toouse tooa Windows Phone 8 lub Windows Phone 8.1 Silverlight aplikacji."
services: notification-hubs
documentationcenter: windows
keywords: powiadomienie wypychane, powiadomienia wypychane, wypychanie w systemie windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Wysyłanie powiadomień wypychanych do urządzeń z systemem Windows Phone przy użyciu usługi Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse push aplikacji Windows Phone 8 lub Windows Phone 8.1 Silverlight tooa powiadomienia. Jeśli ma być przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), zapoznaj się toohello [uniwersalnych systemu Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) wersji.
W tym samouczku utworzysz pustą aplikację systemu Windows Phone 8, która odbiera powiadomienia wypychane przy użyciu hello usługi powiadomień wypychanych firmy Microsoft (MPNS). Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.

> [!NOTE]
> Hello zestaw SDK usługi Notification Hubs Windows Phone nie obsługuje używania hello Push powiadomienia usługi WNS (Windows) dla aplikacji Windows Phone 8.1 Silverlight. toouse WNS (zamiast usługi MPNS) z aplikacjami systemu Windows Phone 8.1 Silverlight, należy wykonać hello [Notification Hubs — Samouczek Windows Phone Silverlight], który używa interfejsów API REST.
> 
> 

Hello samouczku został omówiony Prosty scenariusz emisji hello przy użyciu usługi Notification Hubs.

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* Program [Visual Studio 2012 Express for Windows Phone] lub nowsza wersja.

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Windows Phone 8.

## <a name="create-your-notification-hub"></a>Tworzenie centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Kliknij przycisk hello <b>usługi powiadomień</b> sekcji (w ramach <i>ustawienia</i>), kliknij <b>Windows Phone (MPNS)</b> , a następnie kliknij przycisk hello <b>Włącz nieuwierzytelnione wypychanie </b> pole wyboru.</p>
</li>
</ol>

&emsp;&emsp;![Portal Azure — włączanie nieuwierzytelnionych powiadomień wypychanych](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

Koncentrator jest teraz utworzony i skonfigurowany toosend nieuwierzytelnionych powiadomień dla Windows Phone.

> [!NOTE]
> W tym samouczku używana jest usługa MPNS w trybie nieuwierzytelnionym. Trybie nieuwierzytelnionym usługi MPNS występują ograniczenia na wysłanie tooeach kanału powiadomień. Usługa Notification Hubs obsługuje [tryb uwierzytelniony usługi MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) pozwala tooupload certyfikatu.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Łączenie aplikacji toohello Centrum powiadomień
1. W programie Visual Studio utwórz nową aplikację dla systemu Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    W programie Visual Studio 2013 Update 2 lub nowszym zamiast tego utwórz aplikację platformy Silverlight dla systemu Windows Phone.
   
    ![Visual Studio — Nowy projekt — Pusta aplikacja — Windows Phone Silverlight][11]
2. W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
   
    Spowoduje to wyświetlenie hello **Zarządzaj pakietami NuGet** okno dialogowe.
3. Wyszukaj `WindowsAzure.Messaging.Managed` i kliknij przycisk **zainstalować**, a następnie zaakceptuj warunki użytkowania hello.
   
    ![Visual Studio — menedżer pakietów NuGet][20]
   
    To spowoduje pobranie, instaluje i dodaje odwołanie do biblioteki Azure Messaging toohello dla systemu Windows za pomocą hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pakietu WindowsAzure.Messaging.Managed NuGet</a>.
4. Otwórz plik hello App.xaml.cs i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Dodaj następującego kodu u góry hello hello **Application_Launching** metody w pliku App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Witaj wartość **MyPushChannel** jest indeks, który jest używany toolookup istniejącego kanału w hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) kolekcji. Jeśli nie istnieje, utwórz nowy wpis o tej nazwie.
   > 
   > 
   
    Upewnij się, że nazwa hello tooinsert parametrów połączenia koncentratora i hello wywoływana **DefaultListenSharedAccessSignature** uzyskane w poprzedniej sekcji hello.
    Ten kod pobiera identyfikator URI kanału hello aplikacji hello z usługi MPNS, a następnie rejestruje ten identyfikator URI kanału w Centrum powiadomień. Gwarantuje również tego kanału hello. identyfikator URI jest rejestrowany w Centrum powiadomień, które każda aplikacja hello czasu jest uruchamiana.
   
   > [!NOTE]
   > W tym samouczku wysyła urządzenia toohello wyskakujące powiadomienie. W przypadku wysyłania powiadomienia na kafelku należy zamiast tego wywołać hello **BindToShellTile** metody w kanale hello. toosupport powiadomienia zarówno wyskakujące i kafelka, wywołać metodę **BindToShellTile** i **BindToShellToast**.
   > 
   > 
6. W Eksploratorze rozwiązań rozwiń **właściwości**, otwórz hello `WMAppManifest.xml` plików, kliknij hello **możliwości** karcie i upewnij się, że hello **ID_CAP_PUSH_NOTIFICATION** jest zaznaczona.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Naciśnij klawisz hello `F5` aplikacji hello toorun klucza.
   
    W aplikacji hello zostanie wyświetlony komunikat rejestracji.
8. Aplikacja hello Zamknij.  
   
   > [!NOTE]
   > tooreceive wyskakujące powiadomienia wypychane, aplikacja hello nie może być uruchomiona na pierwszym planie hello.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Wysyłanie powiadomień wypychanych z poziomu zaplecza
Można wysyłać powiadomienia wypychane przy użyciu usługi Notification Hubs z poziomu dowolnego zaplecza za pośrednictwem publicznego hello <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfejsu REST</a>. W tym samouczku powiadomienia wypychane są wysyłane przy użyciu aplikacji konsolowej programu .NET. 

Przykład sposobu toosend powiadomień wypychanych z zaplecza ASP.NET WebAPI zintegrowanego z usługą Notification Hubs, zobacz [Azure Notification Hubs Powiadom użytkowników z zaplecza programu .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Przykład sposobu hello toosend powiadomień wypychanych przy użyciu [interfejsów API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), zapoznaj się z [jak toouse usługi Notification Hubs za pomocą języka Java](notification-hubs-java-push-notification-tutorial.md) i [jak toouse usługi Notification Hubs za pomocą języka PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Rozwiązanie powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** i **nowy projekt...** , a następnie w obszarze **Visual C#**, kliknij przycisk **Windows** i **aplikacji konsoli**i kliknij przycisk **OK**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Spowoduje to dodanie nowego Visual C# console application toohello rozwiązania. Można to również zrobić w oddzielnym rozwiązaniu.
2. Kliknij pozycję **Narzędzia**, kliknij pozycję **Menedżer pakietów biblioteki**, a następnie kliknij pozycję **Konsola menedżera pakietów**.
   
    Spowoduje to wyświetlenie konsoli Menedżera pakietów hello.
3. W hello **Konsola Menedżera pakietów** okna, zestaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
4. Otwórz hello `Program.cs` i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
5. W hello `Program` klasy, Dodaj hello następujące metody:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Upewnij się, że hello tooreplace `<hub name>` symbol zastępczy nazwą hello hello Centrum powiadomień wyświetlaną w portalu hello. Ponadto Zastąp symbol zastępczy parametrów połączenia hello hello parametry połączenia o nazwie **DefaultFullSharedAccessSignature** uzyskanymi w sekcji hello "Konfigurowanie Centrum powiadomień".
   
   > [!NOTE]
   > Upewnij się, że użyto parametrów połączenia hello z **pełne** dostępu nie **nasłuchiwania** dostępu. Parametry połączenia Hello dostępu do nasłuchiwania nie mają powiadomień wypychanych toosend uprawnienia.
   > 
   > 
6. Dodaj powitania po wierszu w Twojej `Main` metody:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Z programu Windows Phone uruchomionym emulatorem projekt aplikacji hello zamknięte, ustaw konsoli aplikacji jako hello domyślny projekt startowy, a następnie naciśnij klawisz hello `F5` aplikacji hello toorun klucza.
   
    Otrzymasz wyskakujące powiadomienie wypychane. Naciśnięcie baneru wyskakującego powiadomienia spowoduje hello ładuje aplikacji hello.

Wszystkie możliwe ładunki hello można znaleźć w hello [wykazu powiadomień wyskakujących] i [wykazu kafelków] tematów w witrynie MSDN.

## <a name="next-steps"></a>Następne kroki
W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzenia Windows Phone 8. 

W kolejności tootarget określonych użytkowników, zapoznaj się toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka. 

Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. 

Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[wykazu powiadomień wyskakujących]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[wykazu kafelków]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs — Samouczek Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

