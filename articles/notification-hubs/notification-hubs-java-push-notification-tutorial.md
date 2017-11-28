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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="79f2e-103">Jak toouse usługi Notification Hubs za pomocą języka Java</span><span class="sxs-lookup"><span data-stu-id="79f2e-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="79f2e-104">W tym temacie opisano najważniejsze funkcje hello urzędnika hello nowych w pełni obsługiwane SDK Java Centrum powiadomień Azure.</span><span class="sxs-lookup"><span data-stu-id="79f2e-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="79f2e-105">Jest to projekt typu open source i można wyświetlić hello cały kod zestawu SDK w [zestawu Java SDK].</span><span class="sxs-lookup"><span data-stu-id="79f2e-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="79f2e-106">Ogólnie rzecz biorąc, są dostępne wszystkie funkcje usługi Notification Hubs zaplecza Java/PHP/Python/Ruby przy użyciu interfejsu REST Centrum powiadomień hello zgodnie z opisem w temacie MSDN hello [interfejsów API REST centra powiadomień](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="79f2e-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="79f2e-107">Zestaw SDK Java udostępnia cienką otoką w porównaniu z tych interfejsów REST w języku Java.</span><span class="sxs-lookup"><span data-stu-id="79f2e-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="79f2e-108">Witaj zestaw SDK obsługuje obecnie:</span><span class="sxs-lookup"><span data-stu-id="79f2e-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="79f2e-109">CRUD na centra powiadomień</span><span class="sxs-lookup"><span data-stu-id="79f2e-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="79f2e-110">CRUD rejestracji</span><span class="sxs-lookup"><span data-stu-id="79f2e-110">CRUD on Registrations</span></span>
* <span data-ttu-id="79f2e-111">Zarządzanie instalacji</span><span class="sxs-lookup"><span data-stu-id="79f2e-111">Installation Management</span></span>
* <span data-ttu-id="79f2e-112">Import/Eksport rejestracji</span><span class="sxs-lookup"><span data-stu-id="79f2e-112">Import/Export Registrations</span></span>
* <span data-ttu-id="79f2e-113">Wysyła regularnych</span><span class="sxs-lookup"><span data-stu-id="79f2e-113">Regular Sends</span></span>
* <span data-ttu-id="79f2e-114">Wysyła według harmonogramu</span><span class="sxs-lookup"><span data-stu-id="79f2e-114">Scheduled Sends</span></span>
* <span data-ttu-id="79f2e-115">Operacje asynchroniczne za pośrednictwem Java NIO</span><span class="sxs-lookup"><span data-stu-id="79f2e-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="79f2e-116">Obsługiwane platformy: APNS (iOS), usługi GCM (Android), usługi WNS (aplikacje ze Sklepu Windows), usługi MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android bez usług Google)</span><span class="sxs-lookup"><span data-stu-id="79f2e-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="79f2e-117">Użycie zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="79f2e-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="79f2e-118">Kompilowanie i kompilacji</span><span class="sxs-lookup"><span data-stu-id="79f2e-118">Compile and build</span></span>
<span data-ttu-id="79f2e-119">Użyj [Maven]</span><span class="sxs-lookup"><span data-stu-id="79f2e-119">Use [Maven]</span></span>

<span data-ttu-id="79f2e-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="79f2e-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="79f2e-121">Kod</span><span class="sxs-lookup"><span data-stu-id="79f2e-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="79f2e-122">CRUDs Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="79f2e-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="79f2e-123">**Utwórz NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="79f2e-124">**Tworzenie Centrum powiadomień:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="79f2e-125">LUB</span><span class="sxs-lookup"><span data-stu-id="79f2e-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="79f2e-126">**Pobierz Centrum powiadomień:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="79f2e-127">**Zaktualizuj Centrum powiadomień:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="79f2e-128">**Usunąć Centrum powiadomień:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="79f2e-129">CRUDs rejestracji</span><span class="sxs-lookup"><span data-stu-id="79f2e-129">Registration CRUDs</span></span>
<span data-ttu-id="79f2e-130">**Tworzenie klienta Centrum powiadomień:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="79f2e-131">**Utwórz rejestracji systemu Windows:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="79f2e-132">**Utwórz rejestracji systemu iOS:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="79f2e-133">Podobnie można utworzyć rejestracji dla systemu Android (GCM), Windows Phone (MPNS) i Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="79f2e-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="79f2e-134">**Tworzenie szablonu rejestracji:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="79f2e-135">**Tworzenie rejestracji za pomocą tworzyć registrationid + upsert wzorca**</span><span class="sxs-lookup"><span data-stu-id="79f2e-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="79f2e-136">Usuwa duplikaty powodu odpowiedzi tooany utracone jeśli identyfikatorów rejestracji są przechowywane na urządzeniu hello:</span><span class="sxs-lookup"><span data-stu-id="79f2e-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="79f2e-137">**Aktualizacja rejestracji:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="79f2e-138">**Usuwanie rejestracji:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="79f2e-139">**Rejestracje zapytania:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-139">**Query registrations:**</span></span>

* <span data-ttu-id="79f2e-140">**Pobierz pojedynczy rejestracji:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="79f2e-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="79f2e-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="79f2e-142">**Pobieranie wszystkich rejestracji w Centrum:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="79f2e-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="79f2e-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="79f2e-144">**Pobierz rejestracje z tagiem:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="79f2e-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="79f2e-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="79f2e-146">**Uzyskać rejestracji za pomocą kanału:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="79f2e-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="79f2e-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="79f2e-148">Wszystkie zapytania kolekcji obsługuje tokenów $top i kontynuacji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="79f2e-149">Użycie instalacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="79f2e-149">Installation API usage</span></span>
<span data-ttu-id="79f2e-150">Instalacja interfejsu API jest alternatywny mechanizm zarządzania rejestracji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="79f2e-151">Obsługa wielu rejestracji, które nie jest prosta i mogą łatwo zrobić nieprawidłowo lub Niewydajne, a nie jest teraz możliwe toouse obiektu jednej instalacji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="79f2e-152">Instalacja zawiera wszystkie elementy potrzebne: push kanał (token urządzenia), tagi, szablony, dodatkowej kafelków (w przypadku usługi WNS i APNS).</span><span class="sxs-lookup"><span data-stu-id="79f2e-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="79f2e-153">Nie trzeba już toocall hello usługi tooget identyfikator — tylko generowania identyfikatora GUID lub innego identyfikatora, zachowaj go na urządzeniu i wysyłania tooyour wewnętrznej bazy danych wraz z kanału wypychanych (token urządzenia).</span><span class="sxs-lookup"><span data-stu-id="79f2e-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="79f2e-154">Witaj wewnętrznej bazy danych należy wykonywać tylko jednego wywołania: CreateOrUpdateInstallation, jest całkowicie idempotentności, więc możesz wolnego tooretry w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="79f2e-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="79f2e-155">Jako przykład Amazon Kindle Fire wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="79f2e-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="79f2e-156">Jeśli chcesz, aby tooupdate go:</span><span class="sxs-lookup"><span data-stu-id="79f2e-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="79f2e-157">Scenariusze zaawansowane zostały możliwości częściowej aktualizacji, dzięki czemu toomodify tylko określonej właściwości obiektu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="79f2e-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="79f2e-158">Zasadniczo częściowej aktualizacji jest podzbiorem operacje JSON poprawki, które można uruchomić dla obiekt instalacji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="79f2e-159">Usuń instalacji:</span><span class="sxs-lookup"><span data-stu-id="79f2e-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="79f2e-160">CreateOrUpdate, poprawki i Delete są ostatecznie zgodne z Get.</span><span class="sxs-lookup"><span data-stu-id="79f2e-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="79f2e-161">Żądana operacja tylko przechodzi kolejki system toohello podczas wywołania hello i będą wykonywane w tle.</span><span class="sxs-lookup"><span data-stu-id="79f2e-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="79f2e-162">Należy pamiętać, że Get nie jest przeznaczony dla scenariusza głównego środowiska uruchomieniowego, ale tylko dla debugowania i rozwiązywania problemów, ściśle jest ograniczany przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="79f2e-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="79f2e-163">Przepływ wysyłania dla instalacji jest hello taki sam jak dla rejestracji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="79f2e-164">Właśnie dodaliśmy toohello powiadomień tootarget opcji Instalacja - Użyj tylko tag "InstallationId: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="79f2e-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="79f2e-165">W przypadku powyższych wyglądałyby tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="79f2e-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="79f2e-166">Dla jednego z kilku szablonów:</span><span class="sxs-lookup"><span data-stu-id="79f2e-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="79f2e-167">Zaplanuj powiadomienia (dostępne do warstwy standardowa)</span><span class="sxs-lookup"><span data-stu-id="79f2e-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="79f2e-168">Witaj takie same, jak regularne send, ale jeden dodatkowy parametr - samych parametrach scheduledTime jago dostarczenia powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="79f2e-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="79f2e-169">Usługa akceptuje dowolnego punktu czas między teraz + 5 minut, a teraz + 7 dni.</span><span class="sxs-lookup"><span data-stu-id="79f2e-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="79f2e-170">**Harmonogram powiadomień macierzystego systemu Windows:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="79f2e-171">Import/Eksport (dostępne do warstwy standardowa)</span><span class="sxs-lookup"><span data-stu-id="79f2e-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="79f2e-172">Czasami jest wymagane tooperform operacji zbiorczej przed rejestracji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="79f2e-173">Zazwyczaj jest do integracji z innego systemu lub po prostu ogromną poprawka toosay aktualizacji hello tagi.</span><span class="sxs-lookup"><span data-stu-id="79f2e-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="79f2e-174">Zdecydowanie nie zaleca toouse przepływu Get lub zaktualizowania jeśli mamy mówimy więc o tysiące rejestracji.</span><span class="sxs-lookup"><span data-stu-id="79f2e-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="79f2e-175">Możliwość importu/eksportu jest zaprojektowana toocover hello scenariusz.</span><span class="sxs-lookup"><span data-stu-id="79f2e-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="79f2e-176">Zasadniczo musisz podać kontener obiektów blob toosome dostępu na koncie magazynu jako źródła przychodzących danych oraz lokalizację dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="79f2e-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="79f2e-177">**Prześlij zadanie eksportu:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="79f2e-178">**Prześlij zadanie importu:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="79f2e-179">**Zaczekaj, aż pracę:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="79f2e-180">**Pobierz wszystkie zadania:**</span><span class="sxs-lookup"><span data-stu-id="79f2e-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="79f2e-181">**Identyfikator URI przy użyciu podpisu sygnatury dostępu Współdzielonego:** jest adres URL hello niektóre pliku blob lub kontenera obiektów blob oraz zestaw parametrów, takich jak uprawnienia i czas wygaśnięcia plus podpisu wszystkie elementy utworzone za pomocą klucza sygnatury dostępu Współdzielonego dla konta.</span><span class="sxs-lookup"><span data-stu-id="79f2e-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="79f2e-182">Zestawu SDK Java usługi Magazyn Azure ma rozbudowane możliwości, takie jak tworzenie takie identyfikatory URI.</span><span class="sxs-lookup"><span data-stu-id="79f2e-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="79f2e-183">Jako alternatywne prosty może zająć przyjrzeć się klasy testu ImportExportE2E (z lokalizacji github hello), która ma bardzo podstawowe i compact implementację algorytmu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="79f2e-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="79f2e-184">Wysyłanie powiadomień</span><span class="sxs-lookup"><span data-stu-id="79f2e-184">Send Notifications</span></span>
<span data-ttu-id="79f2e-185">Obiekt powiadomienia Hello jest po prostu treść z nagłówkami, niektóre metody narzędziowe ułatwić tworzenie obiektów hello macierzystego i szablonu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="79f2e-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="79f2e-186">**Sklep Windows i Windows Phone 8.1 (z systemem innym niż platformy Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="79f2e-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="79f2e-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="79f2e-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="79f2e-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="79f2e-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="79f2e-189">**Windows Phone 8.0 i 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="79f2e-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="79f2e-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="79f2e-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="79f2e-191">**Wyślij tooTags**</span><span class="sxs-lookup"><span data-stu-id="79f2e-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="79f2e-192">**Wyślij tootag wyrażenia**</span><span class="sxs-lookup"><span data-stu-id="79f2e-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="79f2e-193">**Wyślij powiadomienie szablonu**</span><span class="sxs-lookup"><span data-stu-id="79f2e-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="79f2e-194">Uruchamianie kodu języka Java teraz powinna generować powiadomienia znajdujących się na urządzeniu docelowym.</span><span class="sxs-lookup"><span data-stu-id="79f2e-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="79f2e-195"><a name="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="79f2e-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="79f2e-196">W tym temacie firma Microsoft pokazano, jak toocreate proste Java REST klienta dla usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="79f2e-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="79f2e-197">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="79f2e-197">From here you can:</span></span>

* <span data-ttu-id="79f2e-198">Pobierz pełną hello [zestawu Java SDK], zawierającą hello cały kod zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="79f2e-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="79f2e-199">Odtwarzanie z hello próbek:</span><span class="sxs-lookup"><span data-stu-id="79f2e-199">Play with hello samples:</span></span>
  * <span data-ttu-id="79f2e-200">[Rozpoczynanie pracy z usługą Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="79f2e-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="79f2e-201">[Wysyłanie najważniejszych wiadomości]</span><span class="sxs-lookup"><span data-stu-id="79f2e-201">[Send breaking news]</span></span>
  * <span data-ttu-id="79f2e-202">[Wysyłanie najważniejszych zlokalizowanych wiadomości]</span><span class="sxs-lookup"><span data-stu-id="79f2e-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="79f2e-203">[Wyślij powiadomienia użytkowników tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="79f2e-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="79f2e-204">[Wysyłanie powiadomień i platform tooauthenticated użytkowników]</span><span class="sxs-lookup"><span data-stu-id="79f2e-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[zestawu Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Rozpoczynanie pracy z usługą Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Wysyłanie najważniejszych wiadomości]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Wysyłanie najważniejszych zlokalizowanych wiadomości]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Wyślij powiadomienia użytkowników tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Wysyłanie powiadomień i platform tooauthenticated użytkowników]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

