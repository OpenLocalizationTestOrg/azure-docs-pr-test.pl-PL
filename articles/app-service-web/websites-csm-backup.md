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
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a>Korzystanie z interfejsu REST do tworzenia kopii zapasowych aplikacji w usłudze App Service i przywracania ich
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [Interfejs API REST](websites-csm-backup.md)
> 
> 

[Usługi aplikacji — aplikacje](https://azure.microsoft.com/services/app-service/web/) utworzeniem kopii zapasowej jako obiekty BLOB w magazynie Azure. Tworzenie kopii zapasowej może również zawierać aplikacji baz danych. Jeśli aplikacja zostanie kiedykolwiek przypadkowo usunięty lub aplikacja musi zostać przywrócony do poprzedniej wersji, można go przywrócić z dowolnego z poprzedniej kopii zapasowej. Kopie zapasowe można zrobić w dowolnym momencie na żądanie lub kopie zapasowe mogą być planowane w odpowiednich odstępach czasu.

W tym artykule opisano sposób wykonywania kopii zapasowej i przywracanie aplikacji za pomocą żądań interfejsu API RESTful. Jeśli chcesz utworzyć i zarządzać kopiami zapasowymi aplikacji graficznie za pośrednictwem portalu Azure, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Wprowadzenie
Do wysyłania żądań REST, musisz wiedzieć o aplikacji **nazwa**, **grupy zasobów**, i **identyfikator subskrypcji**. Te informacje można znaleźć, klikając swoją aplikację przy użyciu **usługi aplikacji** bloku [portalu Azure](https://portal.azure.com). Przykłady w tym artykule, firma Microsoft Konfigurowanie witryny sieci Web **backuprestoreapiexamples.azurewebsites.net**. On znajduje się w grupie zasobów WestUS-Web — domyślnej i działa w przypadku subskrypcji o identyfikatorze 00001111-2222-3333-4444-555566667777.

![Informacje o przykładowej witryny internetowej][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Kopia zapasowa i przywracanie interfejsu API REST
Teraz omówimy kilka przykładów sposobu wykonywania kopii zapasowej i przywracanie aplikacji za pomocą interfejsu API REST. Każdy przykład zawiera adres URL i HTTP treści żądania. Przykładowy adres URL zawiera symbole zastępcze ujęte w nawiasy klamrowe, takich jak {identyfikator subskrypcji}. Zastąp symbole zastępcze odpowiednich informacji dla aplikacji. Odwołania w tym miejscu jest wyjaśnienie każdego symbolu zastępczego, która jest wyświetlana w adresach URL.

* Identyfikator subskrypcji — identyfikator subskrypcji platformy Azure, zawierającej aplikację
* Nazwa grupy zasobów-— Nazwa grupy zasobów zawierającej aplikację
* Nazwa — Nazwa aplikacji
* Identyfikator kopii zapasowej — identyfikator aplikacji kopii zapasowej

Aby uzyskać pełną dokumentację interfejsu API, w tym kilka opcjonalnych parametrów, które można dołączyć do żądania HTTP, zobacz [Eksploratora zasobów Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Kopia zapasowa aplikację na żądanie
Aby natychmiast wykonać kopię zapasową aplikacji, Wyślij **POST** żądanie **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Kopia zapasowa /**.

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**

Należy podać obiekt JSON w treści żądania, aby określić konto magazynu, które będzie używany do przechowywania kopii zapasowej. Obiekt JSON musi mieć właściwość o nazwie **storageAccountUrl**, który posiada [adres URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) udzielanie dostępu zapisu do kontenera magazynu Azure, który przechowuje kopii zapasowej obiektu blob. Jeśli chcesz utworzyć kopię zapasową baz danych, należy również podać listę zawierającą nazwy, typy i parametry połączenia do wykonania kopii zapasowej bazy danych.

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

Kopia zapasowa aplikacji rozpocznie się natychmiast po odebraniu żądania. Proces tworzenia kopii zapasowej może potrwać bardzo długo. Odpowiedź HTTP zawiera identyfikator, którego można użyć w innego żądania, aby wyświetlić stan kopii zapasowej. Oto przykład treści odpowiedzi HTTP do tworzenia kopii zapasowej żądanie.

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
> Komunikaty o błędach można znaleźć we właściwości dziennika odpowiedzi HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Harmonogram automatycznego tworzenia kopii zapasowych
Oprócz tworzenia kopii zapasowej aplikacji na żądanie, można również zaplanować kopię zapasową, aby automatycznie.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Konfigurowanie nowego harmonogramu automatycznego tworzenia kopii zapasowej
Aby skonfigurować harmonogram tworzenia kopii zapasowych, Wyślij **PUT** żądanie **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/ Kopia zapasowa**.

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**

Treść żądania musi mieć obiekt JSON, który określa konfiguracji kopii zapasowej. Oto przykład z wymaganymi parametrami.

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

Ten przykład konfiguruje aplikację do automatycznego wykonania kopii zapasowej co siedem dni. Parametry **frequencyInterval** i **frequencyUnit** wspólnie określają, jak często kopie zapasowe są wykonywane. Prawidłowymi wartościami dla **frequencyUnit** są **godzina** i **dzień**. Na przykład aby utworzyć kopię zapasową aplikacji co 12 godzin, ustaw frequencyInterval 12 i frequencyUnit na godzinę.

Starych kopii zapasowych zostaną automatycznie usunięte z konta magazynu. Można określić wiek kopie zapasowe mogą być przez ustawienie **retentionPeriodInDays** parametru. Jeśli chcesz zawsze mieć co najmniej jedną kopię zapasową zapisano, niezależnie od tego, ile lat ustawiana jest **keepAtLeastOneBackup** na wartość true.

### <a name="get-the-automatic-backup-schedule"></a>Pobierz harmonogramu automatycznego tworzenia kopii zapasowej
Aby uzyskać konfiguracji kopii zapasowej aplikacji, Wyślij **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites / {Nazwa} / config / / kopii zapasowej listy**.

Adres URL witryny przykład jest **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a>Pobierz stan kopii zapasowej
W zależności od tego, jak duże jest aplikacja kopii zapasowej może zająć trochę czasu, aby zakończyć. Tworzenie kopii zapasowych może również zakończyć się niepowodzeniem, limit czasu lub częściowo powiodła się. Aby wyświetlić stan kopii zapasowych wszystkich aplikacji, należy wysłać **UZYSKAĆ** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / {Nazwa} / kopii zapasowych**.

Aby wyświetlić stan określonej kopii zapasowej, Wyślij żądanie GET do adresu URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}** .

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

Treść odpowiedzi zawiera obiekt JSON, podobnie jak w tym przykładzie.

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

Stan kopii zapasowej jest typ wyliczeniowy. Oto co możliwe stany.

* 0 — W toku: kopia zapasowa została uruchomiona, ale nie została jeszcze zakończona.
* 1 — Błąd: tworzenie kopii zapasowej nie powiodło się.
* 2 – Powodzenie: kopia zapasowa została wykonana pomyślnie.
* 3 — upłynął limit czasu: Tworzenie kopii zapasowej nie zostało zakończone w czasie i została anulowana.
* 4 — Utworzono: żądanie kopii zapasowej znajduje się w kolejce, ale nie zostało jeszcze uruchomione.
* 5 – Pominięto: kopia zapasowa nie była wykonywana, ponieważ harmonogram wyzwolił zbyt wiele kopii zapasowych.
* 6 — Częściowe powodzenie: tworzenie kopii zapasowej powiodło się, ale nie utworzono kopii zapasowych niektórych plików, ponieważ nie można było ich odczytać. Przyczyną jest zazwyczaj blokada na wyłączność nałożona na pliki.
* 7 — Usuwanie w toku: zażądano usunięcia kopii zapasowej, ale nie została ona jeszcze usunięta.
* 8 — Błąd usuwania: nie można usunąć kopii zapasowej. Przyczyną może być wygaśnięcie adresu URL sygnatury dostępu współdzielonego użytego do utworzenia kopii zapasowej.
* 9 — Usunięto: kopia zapasowa została usunięta pomyślnie.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Przywracanie z kopii zapasowej aplikacji
Jeśli aplikacja została usunięta lub jeśli chcesz przywrócić do poprzedniej wersji aplikacji, można przywrócić z kopii zapasowej aplikacji. Aby wywołać operację przywracania, Wyślij **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups / {backup-id} / restore**.

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**

W treści żądania Wyślij obiekt JSON, który zawiera właściwości dla operacji przywracania. Poniżej przedstawiono przykład zawierający wszystkie wymagane właściwości:

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

### <a name="restore-to-a-new-app"></a>Przywróć w nowej aplikacji
Czasami możesz utworzyć nową aplikację po przywróceniu kopii zapasowej, zamiast zastępowanie istniejących aplikacji. Aby to zrobić, należy zmienić adres URL żądania, aby wskazywał nową aplikację, aby utworzyć i zmienić **zastąpić** właściwości w formacie JSON do **false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Usuwanie kopii zapasowej aplikacji
Jeśli chcesz usunąć kopii zapasowej, Wyślij **usunąć** żądania na adres URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites / /backups/ {backup-id} {nazwa}**.

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Zarządzanie adres URL SAS kopii zapasowej
Usługa aplikacji Azure podejmie próbę usunięcia kopii zapasowej z usługi Azure Storage przy użyciu adresu URL SAS, podany podczas tworzenia kopii zapasowej. Jeśli ten adres URL SAS nie jest już prawidłowe, tworzenie kopii zapasowej nie można usunąć za pomocą interfejsu API REST. Jednak możesz zaktualizować adres URL SAS skojarzone z kopii zapasowej, wysyłając **POST** żądania na adres URL **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Oto, co adres URL wygląda naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/list**

W treści żądania Wyślij obiekt JSON, który zawiera nowy adres URL SAS. Oto przykład.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Ze względów bezpieczeństwa adres URL SAS skojarzone z kopii zapasowej nie są zwracane podczas wysyłania żądania GET do określonej kopii zapasowej. Jeśli chcesz wyświetlić adres URL SAS skojarzone z kopii zapasowej, wysłanie żądania POST do tego samego adresu URL powyżej. Uwzględnij pusty obiekt JSON w treści żądania. Odpowiedź z serwera zawiera wszystkie informacje o możliwość tworzenia kopii zapasowych, w tym jego adres URL SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
