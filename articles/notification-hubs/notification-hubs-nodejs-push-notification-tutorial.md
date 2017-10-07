---
title: "aaaSending powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js"
description: "Dowiedz się, jak toosend usługi Notification Hubs toouse powiadomień wypychanych z poziomu aplikacji Node.js."
keywords: powiadomienia wypychane, wypychanie notifications,node.js wypychania, wypychanych systemu ios
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Omówienie
> [!IMPORTANT]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

W tym przewodniku opisano sposób toosend powiadomienia wypychane za pomocą hello usługi Azure Notification hubs bezpośrednio z poziomu aplikacji Node.js. 

omówione scenariusze Hello obejmują, wysyłanie tooapplications powiadomień wypychanych na powitania następujące platformy:

* Android
* iOS
* Windows Phone
* Platforma uniwersalna systemu Windows 

Aby uzyskać więcej informacji dotyczących usługi notification hubs, zobacz hello [następne kroki](#next) sekcji.

## <a name="what-are-notification-hubs"></a>Co to jest Notification Hubs?
Centra powiadomień Azure zapewnia infrastrukturę łatwy w użyciu, obejmującego wiele platform, skalowalna wysyłania urządzeń toomobile powiadomień wypychanych. Aby uzyskać szczegółowe informacje na powitania infrastrukturę usług, zobacz hello [usługi Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) strony.

## <a name="create-a-nodejs-application"></a>Tworzenie aplikacji Node.js
pierwszym krokiem Hello w tym samouczku jest tworzenie nowej aplikacji Node.js puste. Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie tooAzure aplikacji Node.js witryny sieci Web][nodejswebsite], [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell lub [witryny sieci Web za pomocą programu WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Konfigurowanie centrów powiadomień tooUse Twoja aplikacja
toouse usługi Azure Notification Hubs, należy toodownload i użyj hello Node.js [pakiet azure](https://www.npmjs.com/package/azure), który zawiera zestaw wbudowanych pomocnika bibliotek, które komunikują się z usługami REST powiadomień wypychanych hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Linux) i przejdź do folderu toohello, w którym utworzono pusta aplikacja .
2. Typ **azure sb instalacji narzędzia npm** w oknie polecenia hello.
3. Możesz ręcznie uruchomić hello **ls** lub **dir** tooverify polecenia który **węzła\_modułów** folder został utworzony. W tym folderze, Znajdź hello **azure** pakiet, który zawiera biblioteki hello należy tooaccess hello Centrum powiadomień.

> [!NOTE]
> Dowiedz się więcej na temat instalowania NPM na powitania oficjalne [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Moduł hello importu
Za pomocą edytora tekstu, Dodaj powitania od góry toohello hello **server.js** pliku aplikacji hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Nawiązanie połączenia Centrum powiadomień Azure
Witaj **NotificationHubService** obiektu umożliwia pracę z usługą notification hubs. Witaj poniższy kod tworzy **NotificationHubService** obiektu o nazwie Centrum nofication hello **hubname**. Dodać u góry hello hello **server.js** pliku po hello instrukcji tooimport hello azure modułu:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Witaj połączenia **connectionstring** wartość można uzyskać z hello [Azure Portal] , wykonując następujące kroki hello:

1. W okienku nawigacji po lewej stronie powitania kliknij **Przeglądaj**.
2. Wybierz **usługi Notification Hubs**i następnie znajdź hello mają toouse hello próbki. Może się odwoływać toohello [samouczka systemu Windows wprowadzenie magazynu](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu nowego centrum powiadomień.
3. Wybierz **ustawienia**.
4. Polecenie **zasady dostępu**. Zostanie wyświetlone parametry połączenia udostępnionego i pełny dostęp.

![Portal Azure — centra powiadomień](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Można również pobrać hello ciągu połączenia za pomocą hello **Get-AzureSbNamespace** udostępniane przez polecenia cmdlet [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello **Pokaż przestrzeni nazw azure sb** z Witaj [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Architektura ogólna
Witaj **NotificationHubService** obiekt udostępnia następujące wystąpienia obiektu wysyłania urządzeń toospecific powiadomień wypychanych i aplikacji hello:

* **Android** -Użyj hello **GcmService** obiektu, który jest dostępny na **notificationHubService.gcm**
* **iOS** -Użyj hello **ApnsService** obiektu, który jest dostępny pod **notificationHubService.apns**
* **Windows Phone** -Użyj hello **MpnsService** obiektu, który jest dostępny na **notificationHubService.mpns**
* **Platforma uniwersalna systemu Windows** -Użyj hello **WnsService** obiektu, który jest dostępny na **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Porady: wysyłanie wypychania powiadomień tooAndroid aplikacji
Hello **GcmService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooAndroid aplikacji. Witaj **wysyłania** metoda przyjmuje hello następujące parametry:

* **Tagi** — Witaj identyfikator tagu. Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.
* **Ładunek** — Witaj JSON lub nieprzetworzony ciąg ładunek komunikatu.
* **Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.

Aby uzyskać więcej informacji na format ładunku hello, zobacz hello **ładunku** sekcji hello [Implementowanie serwera GCM](http://developer.android.com/google/gcm/server.html#payload) dokumentu.

Witaj poniższy kod używa hello **GcmService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend tooall powiadomień wypychanych zarejestrowany klientów.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Porady: wysyłanie wypychania powiadomień tooiOS aplikacji
Takie same jak w przypadku aplikacji systemu Android opisane powyżej, hello **ApnsService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooiOS aplikacji. Witaj **wysyłania** metoda przyjmuje hello następujące parametry:

* **Tagi** — Witaj identyfikator tagu. Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.
* **Ładunek** — Witaj JSON komunikatu lub string ładunku.
* **Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.

Format ładunku hello więcej informacji, zobacz hello **ładunek powiadomienia** sekcji hello [lokalnych i wypychanych Podręcznik programowania powiadomień](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) dokumentu.

Witaj poniższy kod używa hello **ApnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend alert komunikatu tooall klientów:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Porady: wysyłanie wypychanych aplikacji Phone tooWindows powiadomienia
Witaj **MpnsService** udostępnia obiekt **wysyłania** metody, które mogą być tooWindows powiadomień wypychanych toosend używanych aplikacji telefonicznej. Witaj **wysyłania** metoda przyjmuje hello następujące parametry:

* **Tagi** — Witaj identyfikator tagu. Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.
* **Ładunek** — Witaj ładunek XML wiadomości.
* **TargetName**  -  `toast` dla wyskakujące powiadomienia. `token`Kafelek powiadomień.
* **NotificationClass** — Witaj priorytet hello powiadomień. Zobacz hello **elementów nagłówka HTTP** sekcji hello [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) dokumentu prawidłowe wartości.
* **Opcje** — opcjonalne nagłówki żądań.
* **Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.

Lista prawidłową **TargetName**, **NotificationClass** i opcje nagłówka wyewidencjonowania hello [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) strony.

Witaj następującego przykładowego kodu używa hello **MpnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend wyskakujące powiadomienie wypychane:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Porady: wysyłanie aplikacji platformy systemu Windows (UWP) tooUniversal powiadomień wypychanych
Witaj **WnsService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooUniversal platformy Windows aplikacji.  Witaj **wysyłania** metoda przyjmuje hello następujące parametry:

* **Tagi** — Witaj identyfikator tagu. Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane klientów tooall zarejestrowany.
* **Ładunek** -ładunek komunikatu hello XML.
* **Typ** — Witaj typu powiadomienia.
* **Opcje** — opcjonalne nagłówki żądań.
* **Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.

Aby uzyskać listę prawidłowych typów i nagłówków żądań, zobacz [nagłówki żądań i odpowiedzi usługi powiadomień wypychanych](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Witaj poniższy kod używa hello **WnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend w aplikacji platformy uniwersalnej systemu Windows tooa powiadomienie wyskakujące wypychania:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Następne kroki
Zezwalaj na Hello przykładowe fragmenty kodu powyżej możesz tooeasily kompilacji usługi infrastruktury toodeliver wypychania powiadomień tooa szerokiej gamy urządzeń. Teraz, kiedy znasz już podstawy hello przy użyciu usługi Notification Hubs za pomocą języka node.js, wykonaj te toolearn łącza więcej informacji na temat sposobu można rozszerzyć te dodatkowe możliwości.

* Zobacz odwołanie MSDN hello [usługi Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Odwiedź hello [zestawu Azure SDK dla węzła] repozytorium w usłudze GitHub więcej przykładów i szczegóły implementacji.

[zestawu Azure SDK dla węzła]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[witryny sieci Web za pomocą programu WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
