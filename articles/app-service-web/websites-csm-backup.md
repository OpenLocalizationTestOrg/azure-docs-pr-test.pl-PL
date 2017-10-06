---
title: "aaaUse REST tooback zapasowej i przywracania usługi aplikacji — aplikacje"
description: "Dowiedz się, jak toouse interfejsu API RESTful wywołuje tooback i przywracanie aplikacji w usłudze Azure App Service"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="b22b9-103">Użyj REST tooback i przywracania usługi aplikacji — aplikacje</span><span class="sxs-lookup"><span data-stu-id="b22b9-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b22b9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b22b9-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="b22b9-105">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="b22b9-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="b22b9-106">[Usługi aplikacji — aplikacje](https://azure.microsoft.com/services/app-service/web/) utworzeniem kopii zapasowej jako obiekty BLOB w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="b22b9-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="b22b9-107">Kopia zapasowa Hello może również zawierać aplikacji hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="b22b9-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="b22b9-108">Jeśli aplikacja hello jest kiedykolwiek przypadkowo usunięty lub jeśli toobe potrzeb aplikacji hello przywrócony tooa poprzedniej wersji, można go przywrócić z dowolnego z poprzedniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="b22b9-109">Kopie zapasowe można zrobić w dowolnym momencie na żądanie lub kopie zapasowe mogą być planowane w odpowiednich odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="b22b9-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="b22b9-110">W tym artykule opisano, jak toobackup i przywracania żądania aplikacji za pomocą interfejsu API RESTful.</span><span class="sxs-lookup"><span data-stu-id="b22b9-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="b22b9-111">Jeśli chcesz toocreate i zarządzanie kopiami zapasowymi aplikacji graficznie za pośrednictwem hello portalu Azure, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="b22b9-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="b22b9-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b22b9-112">Getting Started</span></span>
<span data-ttu-id="b22b9-113">żąda toosend REST, należy tooknow aplikacji **nazwa**, **grupy zasobów**, i **identyfikator subskrypcji**. Te informacje można znaleźć, klikając aplikacji w hello **usługi aplikacji** bloku hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b22b9-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b22b9-114">Hello przykłady w tym artykule, firma Microsoft Konfigurowanie witryny sieci Web hello **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="b22b9-115">On znajduje się w grupie zasobów domyślna-Web-WestUS hello i działa w przypadku subskrypcji z hello identyfikator 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="b22b9-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informacje o przykładowej witryny internetowej][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="b22b9-117">Kopia zapasowa i przywracanie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b22b9-117">Backup and restore REST API</span></span>
<span data-ttu-id="b22b9-118">Teraz omówimy kilka przykładów sposobu toouse hello toobackup interfejsu API REST i przywrócić aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b22b9-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="b22b9-119">Każdy przykład zawiera adres URL i HTTP treści żądania.</span><span class="sxs-lookup"><span data-stu-id="b22b9-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="b22b9-120">adres URL przykładowych Hello zawiera symbole zastępcze ujęte w nawiasy klamrowe, takich jak {identyfikator subskrypcji}.</span><span class="sxs-lookup"><span data-stu-id="b22b9-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="b22b9-121">Zastąp symbole zastępcze hello hello odpowiednich informacji o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b22b9-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="b22b9-122">Odwołania w tym miejscu jest wyjaśnienie każdego symbolu zastępczego w hello adresy URL.</span><span class="sxs-lookup"><span data-stu-id="b22b9-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="b22b9-123">Identyfikator subskrypcji — identyfikator zawierającego aplikacji hello hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b22b9-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="b22b9-124">Nazwa grupy zasobów-— Nazwa hello zasobów grupy zawierające hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="b22b9-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="b22b9-125">Nazwa — Nazwa aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b22b9-125">name – Name of hello app</span></span>
* <span data-ttu-id="b22b9-126">Identyfikator kopii zapasowej — identyfikator aplikacji hello tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="b22b9-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="b22b9-127">Hello pełną dokumentację interfejsu API hello, kilka opcjonalnych parametrów, które można uwzględnić w żądaniu hello HTTP, w tym temacie hello [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b22b9-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="b22b9-128">Kopia zapasowa aplikację na żądanie</span><span class="sxs-lookup"><span data-stu-id="b22b9-128">Backup an app on demand</span></span>
<span data-ttu-id="b22b9-129">tooback zapasowej aplikacji bezpośrednio, Wyślij **POST** żądania zbyt**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Kopia zapasowa /**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="b22b9-130">Oto, jak naszym przykładzie witryny sieci Web wygląda hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b22b9-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="b22b9-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**</span><span class="sxs-lookup"><span data-stu-id="b22b9-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="b22b9-132">Podaj obiekt JSON w treści hello toospecify z żądania, które toostore toouse konta magazynu hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="b22b9-133">Obiekt JSON Hello musi mieć właściwość o nazwie **storageAccountUrl**, który posiada [adres URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) udzielanie zapisu toohello usługi Azure Storage kontener, który zawiera hello blob kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="b22b9-134">Jeśli chcesz tooback zapasową baz danych, należy również podać listę zawierającą nazwy hello, typy i parametry połączenia z hello toobe baz danych kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="b22b9-135">Kopię zapasową aplikacji hello rozpocznie się natychmiast po odebraniu żądania hello.</span><span class="sxs-lookup"><span data-stu-id="b22b9-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="b22b9-136">proces tworzenia kopii zapasowej Hello może potrwać toocomplete dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="b22b9-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="b22b9-137">Witaj odpowiedzi HTTP zawiera identyfikator, którego można używać w inny stan żądania toosee hello hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="b22b9-138">Oto przykład treści żądania tworzenia kopii zapasowej tooour odpowiedzi HTTP hello hello.</span><span class="sxs-lookup"><span data-stu-id="b22b9-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="b22b9-139">Komunikaty o błędach można znaleźć we właściwości dziennika hello hello odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="b22b9-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="b22b9-140">Harmonogram automatycznego tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="b22b9-140">Schedule automatic backups</span></span>
<span data-ttu-id="b22b9-141">W przypadku dodawania toobacking się aplikację na żądanie można również zaplanować toohappen kopii zapasowej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b22b9-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="b22b9-142">Konfigurowanie nowego harmonogramu automatycznego tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="b22b9-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="b22b9-143">Wyślij tooset harmonogram tworzenia kopii zapasowej, **PUT** żądania zbyt**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="b22b9-144">Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b22b9-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="b22b9-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**</span><span class="sxs-lookup"><span data-stu-id="b22b9-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="b22b9-146">Treść żądania Hello musi mieć obiekt JSON, który określa hello konfiguracji kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="b22b9-147">Oto przykład parametrami hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="b22b9-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="b22b9-148">Ten przykład konfiguruje toobe aplikacji hello automatycznie do kopii zapasowej co siedem dni.</span><span class="sxs-lookup"><span data-stu-id="b22b9-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="b22b9-149">Witaj parametry **frequencyInterval** i **frequencyUnit** wspólnie określają, jak często hello kopie zapasowe są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="b22b9-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="b22b9-150">Prawidłowymi wartościami dla **frequencyUnit** są **godzina** i **dzień**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="b22b9-151">Na przykład tooback zapasowej aplikacji co 12 godzin, ustaw frequencyInterval too12 i frequencyUnit toohour.</span><span class="sxs-lookup"><span data-stu-id="b22b9-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="b22b9-152">Starych kopii zapasowych zostaną automatycznie usunięte z hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b22b9-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="b22b9-153">Można kontrolować wiek hello kopie zapasowe mogą być przez ustawienie hello **retentionPeriodInDays** parametru.</span><span class="sxs-lookup"><span data-stu-id="b22b9-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="b22b9-154">Jeśli chcesz tooalways ma co najmniej jedną kopię zapasową zapisano, niezależnie od tego, ile lat ustawiana jest **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="b22b9-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="b22b9-155">Pobierz hello automatycznego harmonogramu tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="b22b9-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="b22b9-156">tooget aplikacji kopii zapasowej konfiguracji, Wyślij **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / {nazwa} / config/tworzenia kopii zapasowej/listy**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="b22b9-157">adres URL witryny przykład Hello jest **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="b22b9-158">Pobierz stan hello kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="b22b9-158">Get hello status of a backup</span></span>
<span data-ttu-id="b22b9-159">W zależności od wielkości aplikacji hello jest, kopia zapasowa może potrwać pewien czas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b22b9-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="b22b9-160">Tworzenie kopii zapasowych może również zakończyć się niepowodzeniem, limit czasu lub częściowo powiodła się.</span><span class="sxs-lookup"><span data-stu-id="b22b9-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="b22b9-161">Wyślij toosee hello stanu kopii zapasowych wszystkich aplikacji, **UZYSKAĆ** toohello adres URL żądania **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="b22b9-162">Stan hello toosee określonej kopii zapasowej, Wyślij adres URL toohello żądania GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { Kopia zapasowa id}**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="b22b9-163">Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b22b9-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="b22b9-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="b22b9-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="b22b9-165">treść odpowiedzi Hello zawiera podobny przykład toothis JSON obiektu.</span><span class="sxs-lookup"><span data-stu-id="b22b9-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="b22b9-166">Stan Hello kopii zapasowej jest typ wyliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="b22b9-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="b22b9-167">Oto co możliwe stany.</span><span class="sxs-lookup"><span data-stu-id="b22b9-167">Here is every possible state.</span></span>

* <span data-ttu-id="b22b9-168">0 — w toku: hello kopia zapasowa została uruchomiona, ale nie zostało jeszcze zakończone.</span><span class="sxs-lookup"><span data-stu-id="b22b9-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="b22b9-169">1 – nie powiodło się: hello kopii zapasowej nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b22b9-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="b22b9-170">2 — Powodzenie: hello pomyślnie wykonano kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="b22b9-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="b22b9-171">3 — upłynął limit czasu: hello kopii zapasowej nie zostało zakończone w czasie i została anulowana.</span><span class="sxs-lookup"><span data-stu-id="b22b9-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="b22b9-172">4 — utworzone: hello żądania tworzenia kopii zapasowej znajduje się w kolejce, ale nie została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="b22b9-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="b22b9-173">5 — pominięto: hello kopii zapasowej nie kontynuować powodu harmonogram tooa wyzwalania zbyt wiele kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="b22b9-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="b22b9-174">6 — PartiallySucceeded: hello kopii zapasowej zakończyło się pomyślnie, ale niektóre pliki nie zostały kopii zapasowej, ponieważ nie można odczytać.</span><span class="sxs-lookup"><span data-stu-id="b22b9-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="b22b9-175">Zazwyczaj dzieje się tak, ponieważ w trybie wyłączności została umieszczona na powitania plików.</span><span class="sxs-lookup"><span data-stu-id="b22b9-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="b22b9-176">7 — DeleteInProgress: hello kopia zapasowa została żądanego toobe usunięte, ale jeszcze nie zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="b22b9-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="b22b9-177">8 – DeleteFailed: nie można usunąć hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="b22b9-178">Taka sytuacja może wystąpić, ponieważ wygasła hello adres URL SAS, które były używane toocreate hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="b22b9-179">9 — usunięte: hello kopii zapasowej zostało pomyślnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="b22b9-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="b22b9-180">Przywracanie z kopii zapasowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b22b9-180">Restore an app from a backup</span></span>
<span data-ttu-id="b22b9-181">Jeśli aplikacja została usunięta lub ma toorevert aplikacji tooa poprzedniej wersji, można przywrócić z kopii zapasowej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b22b9-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="b22b9-182">Wyślij tooinvoke przywracania, **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Tworzenie kopii zapasowych / {backup-id} / restore**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="b22b9-183">Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b22b9-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="b22b9-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="b22b9-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="b22b9-185">W treści żądania hello Wyślij obiekt JSON, który zawiera właściwości hello hello operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="b22b9-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="b22b9-186">Poniżej przedstawiono przykład zawierający wszystkie wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="b22b9-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="b22b9-187">Przywróć tooa nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b22b9-187">Restore tooa new app</span></span>
<span data-ttu-id="b22b9-188">Czasami może być toocreate nowej aplikacji, podczas przywracania kopii zapasowej, zamiast zastępowanie istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b22b9-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="b22b9-189">toodo tego, zmień hello żądanie adresu URL toopoint toohello nową aplikację toocreate, a następnie zmień hello **zastąpić** właściwości w hello JSON za**false**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="b22b9-190">Usuwanie kopii zapasowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b22b9-190">Delete an app backup</span></span>
<span data-ttu-id="b22b9-191">Jeśli chcesz toodelete kopii zapasowej, Wyślij **usunąć** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / /backups/ {backup-id} {nazwa}**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="b22b9-192">Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b22b9-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="b22b9-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="b22b9-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="b22b9-194">Zarządzanie adres URL SAS kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="b22b9-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="b22b9-195">Usługa aplikacji Azure podejmie toodelete kopii zapasowej z usługi Azure Storage za pomocą hello podany podczas tworzenia kopii zapasowej hello adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="b22b9-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="b22b9-196">Jeśli ten adres URL SAS nie jest już prawidłowe, hello kopii zapasowej nie można usunąć za pomocą hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b22b9-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="b22b9-197">Jednak możesz zaktualizować adres URL SAS skojarzone z kopii zapasowej, wysyłając hello **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="b22b9-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="b22b9-198">Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b22b9-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="b22b9-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="b22b9-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="b22b9-200">W treści żądania hello Wyślij obiekt JSON, który zawiera hello nowy adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="b22b9-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="b22b9-201">Oto przykład.</span><span class="sxs-lookup"><span data-stu-id="b22b9-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="b22b9-202">Ze względów bezpieczeństwa adres URL SAS skojarzone z kopią zapasową powitalne nie są zwracane podczas wysyłania żądania GET do określonej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b22b9-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="b22b9-203">Jeśli hello tooview adres URL SAS skojarzone z kopii zapasowej, należy wysłać toohello żądania POST powyżej tego samego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b22b9-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="b22b9-204">Uwzględnij pusty obiekt JSON w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="b22b9-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="b22b9-205">Hello odpowiedzi z serwera hello zawiera wszystkie informacje możliwość tworzenia kopii zapasowych, łącznie z jej adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="b22b9-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
