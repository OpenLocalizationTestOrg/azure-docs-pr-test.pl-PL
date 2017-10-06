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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Użyj REST tooback i przywracania usługi aplikacji — aplikacje
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [Interfejs API REST](websites-csm-backup.md)
> 
> 

[Usługi aplikacji — aplikacje](https://azure.microsoft.com/services/app-service/web/) utworzeniem kopii zapasowej jako obiekty BLOB w magazynie Azure. Kopia zapasowa Hello może również zawierać aplikacji hello baz danych. Jeśli aplikacja hello jest kiedykolwiek przypadkowo usunięty lub jeśli toobe potrzeb aplikacji hello przywrócony tooa poprzedniej wersji, można go przywrócić z dowolnego z poprzedniej kopii zapasowej. Kopie zapasowe można zrobić w dowolnym momencie na żądanie lub kopie zapasowe mogą być planowane w odpowiednich odstępach czasu.

W tym artykule opisano, jak toobackup i przywracania żądania aplikacji za pomocą interfejsu API RESTful. Jeśli chcesz toocreate i zarządzanie kopiami zapasowymi aplikacji graficznie za pośrednictwem hello portalu Azure, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Wprowadzenie
żąda toosend REST, należy tooknow aplikacji **nazwa**, **grupy zasobów**, i **identyfikator subskrypcji**. Te informacje można znaleźć, klikając aplikacji w hello **usługi aplikacji** bloku hello [portalu Azure](https://portal.azure.com). Hello przykłady w tym artykule, firma Microsoft Konfigurowanie witryny sieci Web hello **backuprestoreapiexamples.azurewebsites.net**. On znajduje się w grupie zasobów domyślna-Web-WestUS hello i działa w przypadku subskrypcji z hello identyfikator 00001111-2222-3333-4444-555566667777.

![Informacje o przykładowej witryny internetowej][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Kopia zapasowa i przywracanie interfejsu API REST
Teraz omówimy kilka przykładów sposobu toouse hello toobackup interfejsu API REST i przywrócić aplikacji. Każdy przykład zawiera adres URL i HTTP treści żądania. adres URL przykładowych Hello zawiera symbole zastępcze ujęte w nawiasy klamrowe, takich jak {identyfikator subskrypcji}. Zastąp symbole zastępcze hello hello odpowiednich informacji o aplikacji. Odwołania w tym miejscu jest wyjaśnienie każdego symbolu zastępczego w hello adresy URL.

* Identyfikator subskrypcji — identyfikator zawierającego aplikacji hello hello subskrypcji platformy Azure
* Nazwa grupy zasobów-— Nazwa hello zasobów grupy zawierające hello aplikacji
* Nazwa — Nazwa aplikacji hello
* Identyfikator kopii zapasowej — identyfikator aplikacji hello tworzenia kopii zapasowej

Hello pełną dokumentację interfejsu API hello, kilka opcjonalnych parametrów, które można uwzględnić w żądaniu hello HTTP, w tym temacie hello [Eksploratora zasobów Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Kopia zapasowa aplikację na żądanie
tooback zapasowej aplikacji bezpośrednio, Wyślij **POST** żądania zbyt**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Kopia zapasowa /**.

Oto, jak naszym przykładzie witryny sieci Web wygląda hello adresu URL. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**

Podaj obiekt JSON w treści hello toospecify z żądania, które toostore toouse konta magazynu hello kopii zapasowej. Obiekt JSON Hello musi mieć właściwość o nazwie **storageAccountUrl**, który posiada [adres URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) udzielanie zapisu toohello usługi Azure Storage kontener, który zawiera hello blob kopii zapasowej. Jeśli chcesz tooback zapasową baz danych, należy również podać listę zawierającą nazwy hello, typy i parametry połączenia z hello toobe baz danych kopii zapasowej.

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

Kopię zapasową aplikacji hello rozpocznie się natychmiast po odebraniu żądania hello. proces tworzenia kopii zapasowej Hello może potrwać toocomplete dużo czasu. Witaj odpowiedzi HTTP zawiera identyfikator, którego można używać w inny stan żądania toosee hello hello kopii zapasowej. Oto przykład treści żądania tworzenia kopii zapasowej tooour odpowiedzi HTTP hello hello.

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
> Komunikaty o błędach można znaleźć we właściwości dziennika hello hello odpowiedzi HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Harmonogram automatycznego tworzenia kopii zapasowych
W przypadku dodawania toobacking się aplikację na żądanie można również zaplanować toohappen kopii zapasowej automatycznie.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Konfigurowanie nowego harmonogramu automatycznego tworzenia kopii zapasowej
Wyślij tooset harmonogram tworzenia kopii zapasowej, **PUT** żądania zbyt**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / tworzenia kopii zapasowej**.

Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**

Treść żądania Hello musi mieć obiekt JSON, który określa hello konfiguracji kopii zapasowej. Oto przykład parametrami hello wymagane.

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

Ten przykład konfiguruje toobe aplikacji hello automatycznie do kopii zapasowej co siedem dni. Witaj parametry **frequencyInterval** i **frequencyUnit** wspólnie określają, jak często hello kopie zapasowe są wykonywane. Prawidłowymi wartościami dla **frequencyUnit** są **godzina** i **dzień**. Na przykład tooback zapasowej aplikacji co 12 godzin, ustaw frequencyInterval too12 i frequencyUnit toohour.

Starych kopii zapasowych zostaną automatycznie usunięte z hello konta magazynu. Można kontrolować wiek hello kopie zapasowe mogą być przez ustawienie hello **retentionPeriodInDays** parametru. Jeśli chcesz tooalways ma co najmniej jedną kopię zapasową zapisano, niezależnie od tego, ile lat ustawiana jest **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Pobierz hello automatycznego harmonogramu tworzenia kopii zapasowych
tooget aplikacji kopii zapasowej konfiguracji, Wyślij **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / {nazwa} / config/tworzenia kopii zapasowej/listy**.

adres URL witryny przykład Hello jest **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Pobierz stan hello kopii zapasowej
W zależności od wielkości aplikacji hello jest, kopia zapasowa może potrwać pewien czas toocomplete. Tworzenie kopii zapasowych może również zakończyć się niepowodzeniem, limit czasu lub częściowo powiodła się. Wyślij toosee hello stanu kopii zapasowych wszystkich aplikacji, **UZYSKAĆ** toohello adres URL żądania **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} /providers/ Microsoft.Web/sites/{name}/backups**.

Stan hello toosee określonej kopii zapasowej, Wyślij adres URL toohello żądania GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { Kopia zapasowa id}**.

Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

treść odpowiedzi Hello zawiera podobny przykład toothis JSON obiektu.

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

Stan Hello kopii zapasowej jest typ wyliczeniowy. Oto co możliwe stany.

* 0 — w toku: hello kopia zapasowa została uruchomiona, ale nie zostało jeszcze zakończone.
* 1 – nie powiodło się: hello kopii zapasowej nie powiodło się.
* 2 — Powodzenie: hello pomyślnie wykonano kopię zapasową.
* 3 — upłynął limit czasu: hello kopii zapasowej nie zostało zakończone w czasie i została anulowana.
* 4 — utworzone: hello żądania tworzenia kopii zapasowej znajduje się w kolejce, ale nie została uruchomiona.
* 5 — pominięto: hello kopii zapasowej nie kontynuować powodu harmonogram tooa wyzwalania zbyt wiele kopii zapasowych.
* 6 — PartiallySucceeded: hello kopii zapasowej zakończyło się pomyślnie, ale niektóre pliki nie zostały kopii zapasowej, ponieważ nie można odczytać. Zazwyczaj dzieje się tak, ponieważ w trybie wyłączności została umieszczona na powitania plików.
* 7 — DeleteInProgress: hello kopia zapasowa została żądanego toobe usunięte, ale jeszcze nie zostały usunięte.
* 8 – DeleteFailed: nie można usunąć hello kopii zapasowej. Taka sytuacja może wystąpić, ponieważ wygasła hello adres URL SAS, które były używane toocreate hello tworzenia kopii zapasowej.
* 9 — usunięte: hello kopii zapasowej zostało pomyślnie usunięte.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Przywracanie z kopii zapasowej aplikacji
Jeśli aplikacja została usunięta lub ma toorevert aplikacji tooa poprzedniej wersji, można przywrócić z kopii zapasowej aplikacji hello. Wyślij tooinvoke przywracania, **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Tworzenie kopii zapasowych / {backup-id} / restore**.

Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**

W treści żądania hello Wyślij obiekt JSON, który zawiera właściwości hello hello operacji przywracania. Poniżej przedstawiono przykład zawierający wszystkie wymagane właściwości:

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

### <a name="restore-tooa-new-app"></a>Przywróć tooa nowej aplikacji
Czasami może być toocreate nowej aplikacji, podczas przywracania kopii zapasowej, zamiast zastępowanie istniejących aplikacji. toodo tego, zmień hello żądanie adresu URL toopoint toohello nową aplikację toocreate, a następnie zmień hello **zastąpić** właściwości w hello JSON za**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Usuwanie kopii zapasowej aplikacji
Jeśli chcesz toodelete kopii zapasowej, Wyślij **usunąć** toohello adres URL żądania **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ Lokacje / /backups/ {backup-id} {nazwa}**.

Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Zarządzanie adres URL SAS kopii zapasowej
Usługa aplikacji Azure podejmie toodelete kopii zapasowej z usługi Azure Storage za pomocą hello podany podczas tworzenia kopii zapasowej hello adres URL SAS. Jeśli ten adres URL SAS nie jest już prawidłowe, hello kopii zapasowej nie można usunąć za pomocą hello interfejsu API REST. Jednak możesz zaktualizować adres URL SAS skojarzone z kopii zapasowej, wysyłając hello **POST** toohello adres URL żądania **https://management.azure.com/subscriptions/ {identyfikator subskrypcji} /resourceGroups/ {— Nazwa grupy zasobów-} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Oto, jak wygląda adres URL hello naszym przykładzie witryny sieci Web. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/Providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/list**

W treści żądania hello Wyślij obiekt JSON, który zawiera hello nowy adres URL SAS. Oto przykład.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Ze względów bezpieczeństwa adres URL SAS skojarzone z kopią zapasową powitalne nie są zwracane podczas wysyłania żądania GET do określonej kopii zapasowej. Jeśli hello tooview adres URL SAS skojarzone z kopii zapasowej, należy wysłać toohello żądania POST powyżej tego samego adresu URL. Uwzględnij pusty obiekt JSON w treści żądania hello. Hello odpowiedzi z serwera hello zawiera wszystkie informacje możliwość tworzenia kopii zapasowych, łącznie z jej adres URL SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
