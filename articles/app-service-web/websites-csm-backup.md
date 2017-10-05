---
title: "Korzystanie z interfejsu REST do tworzenia kopii zapasowych aplikacji w usłudze App Service i przywracania ich"
description: "Dowiedz się, jak użyć interfejsu API RESTful kopii zapasowej i przywracanie aplikacji w usłudze Azure App Service"
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
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="bf314-103">Korzystanie z interfejsu REST do tworzenia kopii zapasowych aplikacji w usłudze App Service i przywracania ich</span><span class="sxs-lookup"><span data-stu-id="bf314-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf314-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf314-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="bf314-105">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="bf314-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="bf314-106">[Usługi aplikacji — aplikacje](https://azure.microsoft.com/services/app-service/web/) utworzeniem kopii zapasowej jako obiekty BLOB w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="bf314-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="bf314-107">Tworzenie kopii zapasowej może również zawierać aplikacji baz danych.</span><span class="sxs-lookup"><span data-stu-id="bf314-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="bf314-108">Jeśli aplikacja zostanie kiedykolwiek przypadkowo usunięty lub aplikacja musi zostać przywrócony do poprzedniej wersji, można go przywrócić z dowolnego z poprzedniej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="bf314-109">Kopie zapasowe można zrobić w dowolnym momencie na żądanie lub kopie zapasowe mogą być planowane w odpowiednich odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="bf314-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="bf314-110">W tym artykule opisano sposób wykonywania kopii zapasowej i przywracanie aplikacji za pomocą żądań interfejsu API RESTful.</span><span class="sxs-lookup"><span data-stu-id="bf314-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="bf314-111">Jeśli chcesz utworzyć i zarządzać kopiami zapasowymi aplikacji graficznie za pośrednictwem portalu Azure, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="bf314-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="bf314-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="bf314-112">Getting Started</span></span>
<span data-ttu-id="bf314-113">Do wysyłania żądań REST, musisz wiedzieć o aplikacji **nazwa**, **grupy zasobów**, i **identyfikator subskrypcji**. Te informacje można znaleźć, klikając swoją aplikację przy użyciu **usługi aplikacji** bloku [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf314-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bf314-114">Przykłady w tym artykule, firma Microsoft Konfigurowanie witryny sieci Web **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="bf314-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="bf314-115">On znajduje się w grupie zasobów WestUS-Web — domyślnej i działa w przypadku subskrypcji o identyfikatorze 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="bf314-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informacje o przykładowej witryny internetowej][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="bf314-117">Kopia zapasowa i przywracanie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="bf314-117">Backup and restore REST API</span></span>
<span data-ttu-id="bf314-118">Teraz omówimy kilka przykładów sposobu wykonywania kopii zapasowej i przywracanie aplikacji za pomocą interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bf314-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="bf314-119">Każdy przykład zawiera adres URL i HTTP treści żądania.</span><span class="sxs-lookup"><span data-stu-id="bf314-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="bf314-120">Przykładowy adres URL zawiera symbole zastępcze ujęte w nawiasy klamrowe, takich jak {identyfikator subskrypcji}.</span><span class="sxs-lookup"><span data-stu-id="bf314-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="bf314-121">Zastąp symbole zastępcze odpowiednich informacji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf314-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="bf314-122">Odwołania w tym miejscu jest wyjaśnienie każdego symbolu zastępczego, która jest wyświetlana w adresach URL.</span><span class="sxs-lookup"><span data-stu-id="bf314-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="bf314-123">Identyfikator subskrypcji — identyfikator subskrypcji platformy Azure, zawierającej aplikację</span><span class="sxs-lookup"><span data-stu-id="bf314-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="bf314-124">Nazwa grupy zasobów-— Nazwa grupy zasobów zawierającej aplikację</span><span class="sxs-lookup"><span data-stu-id="bf314-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="bf314-125">Nazwa — Nazwa aplikacji</span><span class="sxs-lookup"><span data-stu-id="bf314-125">name – Name of the app</span></span>
* <span data-ttu-id="bf314-126">Identyfikator kopii zapasowej — identyfikator aplikacji kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bf314-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="bf314-127">Aby uzyskać pełną dokumentację interfejsu API, w tym kilka opcjonalnych parametrów, które można dołączyć do żądania HTTP, zobacz [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf314-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="bf314-128">Kopia zapasowa aplikację na żądanie</span><span class="sxs-lookup"><span data-stu-id="bf314-128">Backup an app on demand</span></span>
<span data-ttu-id="bf314-129">Aby natychmiast wykonać kopię zapasową aplikacji, Wyślij **POST** żądanie **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Kopia zapasowa /**.</span><span class="sxs-lookup"><span data-stu-id="bf314-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="bf314-130">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="bf314-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**</span><span class="sxs-lookup"><span data-stu-id="bf314-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="bf314-132">Należy podać obiekt JSON w treści żądania, aby określić konto magazynu, które będzie używany do przechowywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="bf314-133">Obiekt JSON musi mieć właściwość o nazwie **storageAccountUrl**, który posiada [adres URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) udzielanie dostępu zapisu do kontenera magazynu Azure, który przechowuje kopii zapasowej obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bf314-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="bf314-134">Jeśli chcesz utworzyć kopię zapasową baz danych, należy również podać listę zawierającą nazwy, typy i parametry połączenia do wykonania kopii zapasowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bf314-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

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

<span data-ttu-id="bf314-135">Kopia zapasowa aplikacji rozpocznie się natychmiast po odebraniu żądania.</span><span class="sxs-lookup"><span data-stu-id="bf314-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="bf314-136">Proces tworzenia kopii zapasowej może potrwać bardzo długo.</span><span class="sxs-lookup"><span data-stu-id="bf314-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="bf314-137">Odpowiedź HTTP zawiera identyfikator, którego można użyć w innego żądania, aby wyświetlić stan kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="bf314-138">Oto przykład treści odpowiedzi HTTP do tworzenia kopii zapasowej żądanie.</span><span class="sxs-lookup"><span data-stu-id="bf314-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

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
> <span data-ttu-id="bf314-139">Komunikaty o błędach można znaleźć we właściwości dziennika odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf314-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="bf314-140">Harmonogram automatycznego tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="bf314-140">Schedule automatic backups</span></span>
<span data-ttu-id="bf314-141">Oprócz tworzenia kopii zapasowej aplikacji na żądanie, można również zaplanować kopię zapasową, aby automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bf314-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="bf314-142">Konfigurowanie nowego harmonogramu automatycznego tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bf314-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="bf314-143">Aby skonfigurować harmonogram tworzenia kopii zapasowych, Wyślij **PUT** żądanie **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/ Kopia zapasowa**.</span><span class="sxs-lookup"><span data-stu-id="bf314-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="bf314-144">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="bf314-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**</span><span class="sxs-lookup"><span data-stu-id="bf314-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="bf314-146">Treść żądania musi mieć obiekt JSON, który określa konfiguracji kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="bf314-147">Oto przykład z wymaganymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="bf314-147">Here is an example with all the required parameters.</span></span>

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
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="bf314-148">Ten przykład konfiguruje aplikację do automatycznego wykonania kopii zapasowej co siedem dni.</span><span class="sxs-lookup"><span data-stu-id="bf314-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="bf314-149">Parametry **frequencyInterval** i **frequencyUnit** wspólnie określają, jak często kopie zapasowe są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="bf314-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="bf314-150">Prawidłowymi wartościami dla **frequencyUnit** są **godzina** i **dzień**.</span><span class="sxs-lookup"><span data-stu-id="bf314-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="bf314-151">Na przykład aby utworzyć kopię zapasową aplikacji co 12 godzin, ustaw frequencyInterval 12 i frequencyUnit na godzinę.</span><span class="sxs-lookup"><span data-stu-id="bf314-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="bf314-152">Starych kopii zapasowych zostaną automatycznie usunięte z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bf314-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="bf314-153">Można określić wiek kopie zapasowe mogą być przez ustawienie **retentionPeriodInDays** parametru.</span><span class="sxs-lookup"><span data-stu-id="bf314-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="bf314-154">Jeśli chcesz zawsze mieć co najmniej jedną kopię zapasową zapisano, niezależnie od tego, ile lat ustawiana jest **keepAtLeastOneBackup** na wartość true.</span><span class="sxs-lookup"><span data-stu-id="bf314-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="bf314-155">Pobierz harmonogramu automatycznego tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bf314-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="bf314-156">Aby uzyskać konfiguracji kopii zapasowej aplikacji, Wyślij **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites / {Nazwa} / config / / kopii zapasowej listy**.</span><span class="sxs-lookup"><span data-stu-id="bf314-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="bf314-157">Adres URL witryny przykład jest **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="bf314-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="bf314-158">Pobierz stan kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bf314-158">Get the status of a backup</span></span>
<span data-ttu-id="bf314-159">W zależności od tego, jak duże jest aplikacja kopii zapasowej może zająć trochę czasu, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="bf314-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="bf314-160">Tworzenie kopii zapasowych może również zakończyć się niepowodzeniem, limit czasu lub częściowo powiodła się.</span><span class="sxs-lookup"><span data-stu-id="bf314-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="bf314-161">Aby wyświetlić stan kopii zapasowych wszystkich aplikacji, należy wysłać **UZYSKAĆ** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / {Nazwa} / kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="bf314-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="bf314-162">Aby wyświetlić stan określonej kopii zapasowej, Wyślij żądanie GET do adresu URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}** .</span><span class="sxs-lookup"><span data-stu-id="bf314-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="bf314-163">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="bf314-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="bf314-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="bf314-165">Treść odpowiedzi zawiera obiekt JSON, podobnie jak w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bf314-165">The response body contains a JSON object similar to this example.</span></span>

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

<span data-ttu-id="bf314-166">Stan kopii zapasowej jest typ wyliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="bf314-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="bf314-167">Oto co możliwe stany.</span><span class="sxs-lookup"><span data-stu-id="bf314-167">Here is every possible state.</span></span>

* <span data-ttu-id="bf314-168">0 — W toku: kopia zapasowa została uruchomiona, ale nie została jeszcze zakończona.</span><span class="sxs-lookup"><span data-stu-id="bf314-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="bf314-169">1 — Błąd: tworzenie kopii zapasowej nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="bf314-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="bf314-170">2 – Powodzenie: kopia zapasowa została wykonana pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bf314-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="bf314-171">3 — upłynął limit czasu: Tworzenie kopii zapasowej nie zostało zakończone w czasie i została anulowana.</span><span class="sxs-lookup"><span data-stu-id="bf314-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="bf314-172">4 — Utworzono: żądanie kopii zapasowej znajduje się w kolejce, ale nie zostało jeszcze uruchomione.</span><span class="sxs-lookup"><span data-stu-id="bf314-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="bf314-173">5 – Pominięto: kopia zapasowa nie była wykonywana, ponieważ harmonogram wyzwolił zbyt wiele kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bf314-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="bf314-174">6 — Częściowe powodzenie: tworzenie kopii zapasowej powiodło się, ale nie utworzono kopii zapasowych niektórych plików, ponieważ nie można było ich odczytać.</span><span class="sxs-lookup"><span data-stu-id="bf314-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="bf314-175">Przyczyną jest zazwyczaj blokada na wyłączność nałożona na pliki.</span><span class="sxs-lookup"><span data-stu-id="bf314-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="bf314-176">7 — Usuwanie w toku: zażądano usunięcia kopii zapasowej, ale nie została ona jeszcze usunięta.</span><span class="sxs-lookup"><span data-stu-id="bf314-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="bf314-177">8 — Błąd usuwania: nie można usunąć kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="bf314-178">Przyczyną może być wygaśnięcie adresu URL sygnatury dostępu współdzielonego użytego do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="bf314-179">9 — Usunięto: kopia zapasowa została usunięta pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="bf314-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="bf314-180">Przywracanie z kopii zapasowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bf314-180">Restore an app from a backup</span></span>
<span data-ttu-id="bf314-181">Jeśli aplikacja została usunięta lub jeśli chcesz przywrócić do poprzedniej wersji aplikacji, można przywrócić z kopii zapasowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf314-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="bf314-182">Aby wywołać operację przywracania, Wyślij **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups / {backup-id} / restore**.</span><span class="sxs-lookup"><span data-stu-id="bf314-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="bf314-183">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="bf314-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="bf314-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="bf314-185">W treści żądania Wyślij obiekt JSON, który zawiera właściwości dla operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="bf314-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="bf314-186">Poniżej przedstawiono przykład zawierający wszystkie wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="bf314-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="bf314-187">Przywróć w nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bf314-187">Restore to a new app</span></span>
<span data-ttu-id="bf314-188">Czasami możesz utworzyć nową aplikację po przywróceniu kopii zapasowej, zamiast zastępowanie istniejących aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf314-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="bf314-189">Aby to zrobić, należy zmienić adres URL żądania, aby wskazywał nową aplikację, aby utworzyć i zmienić **zastąpić** właściwości w formacie JSON do **false**.</span><span class="sxs-lookup"><span data-stu-id="bf314-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="bf314-190">Usuwanie kopii zapasowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bf314-190">Delete an app backup</span></span>
<span data-ttu-id="bf314-191">Jeśli chcesz usunąć kopii zapasowej, Wyślij **usunąć** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites / /backups/ {backup-id} {nazwa}**.</span><span class="sxs-lookup"><span data-stu-id="bf314-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="bf314-192">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="bf314-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="bf314-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="bf314-194">Zarządzanie adres URL SAS kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="bf314-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="bf314-195">Usługa aplikacji Azure podejmie próbę usunięcia kopii zapasowej z usługi Azure Storage przy użyciu adresu URL SAS, podany podczas tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="bf314-196">Jeśli ten adres URL SAS nie jest już prawidłowe, tworzenie kopii zapasowej nie można usunąć za pomocą interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bf314-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="bf314-197">Jednak możesz zaktualizować adres URL SAS skojarzone z kopii zapasowej, wysyłając **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="bf314-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="bf314-198">Oto, co adres URL wygląda naszym przykładzie witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bf314-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="bf314-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="bf314-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="bf314-200">W treści żądania Wyślij obiekt JSON, który zawiera nowy adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="bf314-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="bf314-201">Oto przykład.</span><span class="sxs-lookup"><span data-stu-id="bf314-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="bf314-202">Ze względów bezpieczeństwa adres URL SAS skojarzone z kopii zapasowej nie są zwracane podczas wysyłania żądania GET do określonej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="bf314-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="bf314-203">Jeśli chcesz wyświetlić adres URL SAS skojarzone z kopii zapasowej, wysłanie żądania POST do tego samego adresu URL powyżej.</span><span class="sxs-lookup"><span data-stu-id="bf314-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="bf314-204">Uwzględnij pusty obiekt JSON w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="bf314-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="bf314-205">Odpowiedź z serwera zawiera wszystkie informacje o możliwość tworzenia kopii zapasowych, w tym jego adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="bf314-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
