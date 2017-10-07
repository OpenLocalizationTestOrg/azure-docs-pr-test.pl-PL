---
title: "toouse aaaHow usługi Notification Hubs z językiem Java"
description: "Dowiedz się, jak toouse usługi Azure Notification Hubs z zaplecza Java."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>Jak toouse usługi Notification Hubs za pomocą języka Java
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

W tym temacie opisano najważniejsze funkcje hello urzędnika hello nowych w pełni obsługiwane SDK Java Centrum powiadomień Azure. Jest to projekt typu open source i można wyświetlić hello cały kod zestawu SDK w [zestawu Java SDK]. 

Ogólnie rzecz biorąc, są dostępne wszystkie funkcje usługi Notification Hubs zaplecza Java/PHP/Python/Ruby przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx). Zestaw SDK Java udostępnia cienką otoką w porównaniu z tych interfejsów REST w języku Java. 

Witaj zestaw SDK obsługuje obecnie:

* CRUD na centra powiadomień 
* CRUD rejestracji
* Zarządzanie instalacji
* Import/Eksport rejestracji
* Wysyła regularnych
* Wysyła według harmonogramu
* Operacje asynchroniczne za pośrednictwem Java NIO
* Obsługiwane platformy: APNS (iOS), usługi GCM (Android), usługi WNS (aplikacje ze Sklepu Windows), usługi MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android bez usług Google) 

## <a name="sdk-usage"></a>Użycie zestawu SDK
### <a name="compile-and-build"></a>Kompilowanie i kompilacji
Użyj [Maven]

toobuild:

    mvn package

## <a name="code"></a>Kod
### <a name="notification-hub-cruds"></a>CRUDs Centrum powiadomień
**Utwórz NamespaceManager:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**Tworzenie Centrum powiadomień:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 LUB

    hub = new NotificationHub("connection string", "hubname");

**Pobierz Centrum powiadomień:**

    hub = namespaceManager.getNotificationHub("hubname");

**Zaktualizuj Centrum powiadomień:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**Usunąć Centrum powiadomień:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>CRUDs rejestracji
**Tworzenie klienta Centrum powiadomień:**

    hub = new NotificationHub("connection string", "hubname");

**Utwórz rejestracji systemu Windows:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**Utwórz rejestracji systemu iOS:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

Podobnie można utworzyć rejestracji dla systemu Android (GCM), Windows Phone (MPNS) i Kindle Fire (ADM).

**Tworzenie szablonu rejestracji:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**Tworzenie rejestracji za pomocą tworzyć registrationid + upsert wzorca**

Usuwa duplikaty powodu odpowiedzi tooany utracone jeśli identyfikatorów rejestracji są przechowywane na urządzeniu hello:

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**Aktualizacja rejestracji:**

    hub.updateRegistration(reg);

**Usuwanie rejestracji:**

    hub.deleteRegistration(regid);

**Rejestracje zapytania:**

* **Pobierz pojedynczy rejestracji:**
  
    hub.getRegistration(regid);
* **Pobieranie wszystkich rejestracji w Centrum:**
  
    hub.getRegistrations();
* **Pobierz rejestracje z tagiem:**
  
    hub.getRegistrationsByTag("myTag");
* **Uzyskać rejestracji za pomocą kanału:**
  
    hub.getRegistrationsByChannel("devicetoken");

Wszystkie zapytania kolekcji obsługuje tokenów $top i kontynuacji.

### <a name="installation-api-usage"></a>Użycie instalacji interfejsu API
Instalacja interfejsu API jest alternatywny mechanizm zarządzania rejestracji. Obsługa wielu rejestracji, które nie jest prosta i mogą łatwo zrobić nieprawidłowo lub Niewydajne, a nie jest teraz możliwe toouse obiektu jednej instalacji. Instalacja zawiera wszystkie elementy potrzebne: push kanał (token urządzenia), tagi, szablony, dodatkowej kafelków (w przypadku usługi WNS i APNS). Nie trzeba już toocall hello usługi tooget identyfikator — tylko generowania identyfikatora GUID lub innego identyfikatora, zachowaj go na urządzeniu i wysyłania tooyour wewnętrznej bazy danych wraz z kanału wypychanych (token urządzenia). Witaj wewnętrznej bazy danych należy wykonywać tylko jednego wywołania: CreateOrUpdateInstallation, jest całkowicie idempotentności, więc możesz wolnego tooretry w razie potrzeby.

Jako przykład Amazon Kindle Fire wygląda następująco:

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Jeśli chcesz, aby tooupdate go: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

Scenariusze zaawansowane zostały możliwości częściowej aktualizacji, dzięki czemu toomodify tylko określonej właściwości obiektu instalacji hello. Zasadniczo częściowej aktualizacji jest podzbiorem operacje JSON poprawki, które można uruchomić dla obiekt instalacji.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

Usuń instalacji:

    hub.deleteInstallation(installation.getInstallationId());

CreateOrUpdate, poprawki i Delete są ostatecznie zgodne z Get. Żądana operacja tylko przechodzi kolejki system toohello podczas wywołania hello i będą wykonywane w tle. Należy pamiętać, że Get nie jest przeznaczony dla scenariusza głównego środowiska uruchomieniowego, ale tylko dla debugowania i rozwiązywania problemów, ściśle jest ograniczany przez usługę hello.

Przepływ wysyłania dla instalacji jest hello taki sam jak dla rejestracji. Właśnie dodaliśmy toohello powiadomień tootarget opcji Instalacja - Użyj tylko tag "InstallationId: {desired-id}". W przypadku powyższych wyglądałyby tak jak poniżej:

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

Dla jednego z kilku szablonów:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>Zaplanuj powiadomienia (dostępne do warstwy standardowa)
Witaj takie same, jak regularne send, ale jeden dodatkowy parametr - samych parametrach scheduledTime jago dostarczenia powiadomienia. Usługa akceptuje dowolnego punktu czas między teraz + 5 minut, a teraz + 7 dni.

**Harmonogram powiadomień macierzystego systemu Windows:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>Import/Eksport (dostępne do warstwy standardowa)
Czasami jest wymagane tooperform operacji zbiorczej przed rejestracji. Zazwyczaj jest do integracji z innego systemu lub po prostu ogromną poprawka toosay aktualizacji hello tagi. Zdecydowanie nie zaleca toouse przepływu Get lub zaktualizowania jeśli mamy mówimy więc o tysiące rejestracji. Możliwość importu/eksportu jest zaprojektowana toocover hello scenariusz. Zasadniczo musisz podać kontener obiektów blob toosome dostępu na koncie magazynu jako źródła przychodzących danych oraz lokalizację dla danych wyjściowych.

**Prześlij zadanie eksportu:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**Prześlij zadanie importu:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**Zaczekaj, aż pracę:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**Pobierz wszystkie zadania:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**Identyfikator URI przy użyciu podpisu sygnatury dostępu Współdzielonego:** jest adres URL hello niektóre pliku blob lub kontenera obiektów blob oraz zestaw parametrów, takich jak uprawnienia i czas wygaśnięcia plus podpisu wszystkie elementy utworzone za pomocą klucza sygnatury dostępu Współdzielonego dla konta. Zestawu SDK Java usługi Magazyn Azure ma rozbudowane możliwości, takie jak tworzenie takie identyfikatory URI. Jako alternatywne prosty może zająć przyjrzeć się klasy testu ImportExportE2E (z lokalizacji github hello), która ma bardzo podstawowe i compact implementację algorytmu podpisywania.

### <a name="send-notifications"></a>Wysyłanie powiadomień
Obiekt powiadomienia Hello jest po prostu treść z nagłówkami, niektóre metody narzędziowe ułatwić tworzenie obiektów hello macierzystego i szablonu powiadomienia.

* **Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Windows Phone 8.0 i 8.1 Silverlight**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **Wyślij tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Wyślij tootag wyrażenia**       
  
        hub.sendNotification(n, "foo && ! bar");
* **Wyślij powiadomienie szablonu**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

Uruchamianie kodu języka Java teraz powinna generować powiadomienia znajdujących się na urządzeniu docelowym.

## <a name="next-steps"></a>Następne kroki
W tym temacie firma Microsoft pokazano, jak toocreate proste Java REST klienta dla usługi Notification Hubs. W tym miejscu można wykonywać następujące czynności:

* Pobierz pełną hello [zestawu Java SDK], zawierającą hello cały kod zestawu SDK. 
* Odtwarzanie z hello próbek:
  * [Rozpoczynanie pracy z usługą Notification Hubs]
  * [Wysyłanie najważniejszych wiadomości]
  * [Wysyłanie najważniejszych zlokalizowanych wiadomości]
  * [Wyślij powiadomienia użytkowników tooauthenticated]
  * [Wysyłanie powiadomień i platform tooauthenticated użytkowników]

[zestawu Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Rozpoczynanie pracy z usługą Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Wysyłanie najważniejszych wiadomości]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Wysyłanie najważniejszych zlokalizowanych wiadomości]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Wyślij powiadomienia użytkowników tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Wysyłanie powiadomień i platform tooauthenticated użytkowników]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

