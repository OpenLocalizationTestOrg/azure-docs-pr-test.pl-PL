---
title: "powiązanie funkcji tabeli zewnętrznej aaaAzure (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Przy użyciu powiązań zewnętrznych tabeli w funkcji Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Powiązanie funkcji tabeli zewnętrznej Azure (wersja zapoznawcza)
W tym artykule przedstawiono sposób dane tabelaryczne toomanipulate na dostawców w modelu SaaS (np. Sharepoint, Dynamics) w funkcji z powiązaniami wbudowanych. Środowisko Azure Functions obsługuje powiązań wejściowych i wyjściowych tabel zewnętrznych.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>Połączenia interfejsu API

Powiązania tabeli wykorzystać zewnętrznych tooauthenticate połączenia interfejsu API z 3 SaaS dostawców. 

Podczas przypisywania powiązanie możesz utworzyć nowe połączenie interfejsu API lub użyć istniejącego połączenia interfejsu API w hello tej samej grupie zasobów

### <a name="supported-api-connections-tables"></a>Połączeń obsługiwanych interfejsu API (tabeli) s

|Łącznik|Wyzwalacz|Dane wejściowe|Dane wyjściowe|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 dla operacji](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Arkusze Google](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 dla Finanse](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Baza danych Oracle](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Wspólne usługi danych](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> Połączenia zewnętrzne tabeli można również w [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

### <a name="creating-an-api-connection-step-by-step"></a>Tworzenie połączenia interfejsu API: krok po kroku

1. Utwórz funkcję > funkcji niestandardowej ![Tworzenie funkcji niestandardowej](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Scenariusz `Experimental`  >  `ExternalTable-CSharp` szablonu > Utwórz nowy `External Table connection` 
 ![wybierz tabelę wejściowego szablonu](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Wybierz dostawcę SaaS > Wybierz/utworzyć połączenie ![SaaS skonfigurować połączenia](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Wybierz połączenie z interfejsem API > Utwórz funkcję hello ![Tworzenie tabeli w funkcji](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Wybierz`Integrate` > `External Table`
    1. Skonfiguruj toouse połączenia hello tabeli docelowej. Te ustawienia będą bardzo między dostawców w modelu SaaS. Są one konspektu poniżej w [ustawienia źródła danych](#datasourcesettings)
![Konfigurowanie tabeli](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Sposób użycia

W tym przykładzie łączy tooa tabeli o nazwie "Skontaktuj się z" z kolumnami Identyfikator, nazwisko i imię. Kod Hello listy jednostkami kontaktowymi hello w tabeli hello i dzienniki hello imiona i nazwiska.

### <a name="bindings"></a>Powiązania
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId`może być puste dla powiązania tabeli.

`ConnectionAppSettingsKey`Określa ustawienie aplikacji hello zawierający parametry połączenia hello interfejsu API. Witaj ustawienia aplikacji jest tworzona automatycznie podczas dodawania interfejsu API połączenia w hello integracji interfejsu użytkownika.

Łącznik tabelarycznych zawiera zestawy danych, a każdy zestaw danych zawiera tabele. Nazwa Hello hello domyślny zestaw danych to "domyślny". Poniżej wymieniono tytułów Hello zestawu danych i tabeli w różnych dostawców SaaS:

|Łącznik|Zestaw danych|Tabela|
|:-----|:---|:---| 
|**SharePoint**|Lokacji|Listy programu SharePoint
|**SQL**|Database (Baza danych)|Tabela 
|**Arkusz Google**|Arkusz kalkulacyjny|Arkusza 
|**Excel**|Plik programu Excel|Arkusza 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Użycie w języku C# #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
##Ustawienia źródła danych

### <a name="sql-server"></a>Oprogramowanie SQL Server

Witaj toocreate skryptu i wypełniania tabeli Kontakt hello znajduje się poniżej. dataSetName jest "domyślny".

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Arkusze Google
W Google Docs, należy utworzyć arkusz kalkulacyjny w arkuszu o nazwie `Contact`. Łącznik Hello nie można użyć nazwy wyświetlanej arkusza kalkulacyjnego hello. Wewnętrzna nazwa Hello (pogrubione) wymaga toobe używane jako dataSetName, na przykład: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  dodać nazwy kolumn hello `Id`, `LastName`, `FirstName` toohello pierwszy wiersz, a następnie wypełnij dane na kolejne wiersze.

### <a name="salesforce"></a>SalesForce
dataSetName jest "domyślny".

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
