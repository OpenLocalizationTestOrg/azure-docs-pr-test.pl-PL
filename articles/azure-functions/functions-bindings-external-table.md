---
title: "Powiązanie funkcji tabeli zewnętrznej Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="82ea3-103">Powiązanie funkcji tabeli zewnętrznej Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="82ea3-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="82ea3-104">W tym artykule przedstawiono sposób manipulować danymi tabelarycznego na dostawców w modelu SaaS (np. Sharepoint, Dynamics) w funkcji z powiązaniami wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="82ea3-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="82ea3-105">Środowisko Azure Functions obsługuje powiązań wejściowych i wyjściowych tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="82ea3-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="82ea3-106">Połączenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="82ea3-106">API Connections</span></span>

<span data-ttu-id="82ea3-107">Powiązania tabeli korzystać z połączeń zewnętrznych interfejsu API do uwierzytelniania za pomocą 3 SaaS dostawców.</span><span class="sxs-lookup"><span data-stu-id="82ea3-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="82ea3-108">Podczas przypisywania powiązanie możesz utworzyć nowe połączenie interfejsu API lub użyć istniejącego połączenia interfejsu API w tej samej grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="82ea3-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="82ea3-109">Połączeń obsługiwanych interfejsu API (tabeli) s</span><span class="sxs-lookup"><span data-stu-id="82ea3-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="82ea3-110">Łącznik</span><span class="sxs-lookup"><span data-stu-id="82ea3-110">Connector</span></span>|<span data-ttu-id="82ea3-111">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="82ea3-111">Trigger</span></span>|<span data-ttu-id="82ea3-112">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="82ea3-112">Input</span></span>|<span data-ttu-id="82ea3-113">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="82ea3-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="82ea3-114">DB2</span><span class="sxs-lookup"><span data-stu-id="82ea3-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="82ea3-115">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-115">x</span></span>|<span data-ttu-id="82ea3-116">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-116">x</span></span>
|[<span data-ttu-id="82ea3-117">Dynamics 365 dla operacji</span><span class="sxs-lookup"><span data-stu-id="82ea3-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="82ea3-118">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-118">x</span></span>|<span data-ttu-id="82ea3-119">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-119">x</span></span>
|[<span data-ttu-id="82ea3-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="82ea3-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="82ea3-121">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-121">x</span></span>|<span data-ttu-id="82ea3-122">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-122">x</span></span>
|[<span data-ttu-id="82ea3-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="82ea3-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="82ea3-124">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-124">x</span></span>|<span data-ttu-id="82ea3-125">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-125">x</span></span>
|[<span data-ttu-id="82ea3-126">Arkusze Google</span><span class="sxs-lookup"><span data-stu-id="82ea3-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="82ea3-127">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-127">x</span></span>|<span data-ttu-id="82ea3-128">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-128">x</span></span>
|[<span data-ttu-id="82ea3-129">Informix</span><span class="sxs-lookup"><span data-stu-id="82ea3-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="82ea3-130">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-130">x</span></span>|<span data-ttu-id="82ea3-131">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-131">x</span></span>
|[<span data-ttu-id="82ea3-132">Dynamics 365 dla Finanse</span><span class="sxs-lookup"><span data-stu-id="82ea3-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="82ea3-133">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-133">x</span></span>|<span data-ttu-id="82ea3-134">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-134">x</span></span>
|[<span data-ttu-id="82ea3-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="82ea3-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="82ea3-136">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-136">x</span></span>|<span data-ttu-id="82ea3-137">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-137">x</span></span>
|[<span data-ttu-id="82ea3-138">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="82ea3-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="82ea3-139">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-139">x</span></span>|<span data-ttu-id="82ea3-140">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-140">x</span></span>
|[<span data-ttu-id="82ea3-141">Wspólne usługi danych</span><span class="sxs-lookup"><span data-stu-id="82ea3-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="82ea3-142">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-142">x</span></span>|<span data-ttu-id="82ea3-143">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-143">x</span></span>
|[<span data-ttu-id="82ea3-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="82ea3-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="82ea3-145">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-145">x</span></span>|<span data-ttu-id="82ea3-146">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-146">x</span></span>
|[<span data-ttu-id="82ea3-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="82ea3-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="82ea3-148">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-148">x</span></span>|<span data-ttu-id="82ea3-149">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-149">x</span></span>
|[<span data-ttu-id="82ea3-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="82ea3-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="82ea3-151">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-151">x</span></span>|<span data-ttu-id="82ea3-152">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-152">x</span></span>
|[<span data-ttu-id="82ea3-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="82ea3-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="82ea3-154">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-154">x</span></span>|<span data-ttu-id="82ea3-155">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-155">x</span></span>
|<span data-ttu-id="82ea3-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="82ea3-156">UserVoice</span></span>||<span data-ttu-id="82ea3-157">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-157">x</span></span>|<span data-ttu-id="82ea3-158">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-158">x</span></span>
|<span data-ttu-id="82ea3-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="82ea3-159">Zendesk</span></span>||<span data-ttu-id="82ea3-160">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-160">x</span></span>|<span data-ttu-id="82ea3-161">x</span><span class="sxs-lookup"><span data-stu-id="82ea3-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="82ea3-162">Połączenia zewnętrzne tabeli można również w [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="82ea3-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="82ea3-163">Tworzenie połączenia interfejsu API: krok po kroku</span><span class="sxs-lookup"><span data-stu-id="82ea3-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="82ea3-164">Utwórz funkcję > funkcji niestandardowej ![Tworzenie funkcji niestandardowej](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="82ea3-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="82ea3-165">Scenariusz `Experimental`  >  `ExternalTable-CSharp` szablonu > Utwórz nowy `External Table connection` 
 ![wybierz tabelę wejściowego szablonu](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="82ea3-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="82ea3-166">Wybierz dostawcę SaaS > Wybierz/utworzyć połączenie ![SaaS skonfigurować połączenia](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="82ea3-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="82ea3-167">Wybierz połączenie z interfejsem API > Utwórz funkcję ![Tworzenie tabeli w funkcji](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="82ea3-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="82ea3-168">Wybierz`Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="82ea3-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="82ea3-169">Skonfiguruj połączenie z tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="82ea3-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="82ea3-170">Te ustawienia będą bardzo między dostawców w modelu SaaS.</span><span class="sxs-lookup"><span data-stu-id="82ea3-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="82ea3-171">Są one konspektu poniżej w [ustawienia źródła danych](#datasourcesettings)
![Konfigurowanie tabeli](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="82ea3-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="82ea3-172">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="82ea3-172">Usage</span></span>

<span data-ttu-id="82ea3-173">W tym przykładzie łączy do tabeli z kolumnami Identyfikator, nazwisko i imię o nazwie "Skontaktuj się z".</span><span class="sxs-lookup"><span data-stu-id="82ea3-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="82ea3-174">Kod wyświetla jednostkami kontaktowymi w tabeli i dzienniki imiona i nazwiska.</span><span class="sxs-lookup"><span data-stu-id="82ea3-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="82ea3-175">Powiązania</span><span class="sxs-lookup"><span data-stu-id="82ea3-175">Bindings</span></span>
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
<span data-ttu-id="82ea3-176">`entityId`może być puste dla powiązania tabeli.</span><span class="sxs-lookup"><span data-stu-id="82ea3-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="82ea3-177">`ConnectionAppSettingsKey`Określa ustawienie aplikacji, które są przechowywane w parametrach połączenia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="82ea3-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="82ea3-178">Ustawienia aplikacji jest tworzona automatycznie podczas dodawania połączenia interfejsu API w integracji interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="82ea3-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="82ea3-179">Łącznik tabelarycznych zawiera zestawy danych, a każdy zestaw danych zawiera tabele.</span><span class="sxs-lookup"><span data-stu-id="82ea3-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="82ea3-180">Nazwa domyślnego zestawu danych to "domyślny".</span><span class="sxs-lookup"><span data-stu-id="82ea3-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="82ea3-181">Poniżej wymieniono tytułów dla zestawu danych i tabeli w różnych dostawców SaaS:</span><span class="sxs-lookup"><span data-stu-id="82ea3-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="82ea3-182">Łącznik</span><span class="sxs-lookup"><span data-stu-id="82ea3-182">Connector</span></span>|<span data-ttu-id="82ea3-183">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="82ea3-183">Dataset</span></span>|<span data-ttu-id="82ea3-184">Tabela</span><span class="sxs-lookup"><span data-stu-id="82ea3-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="82ea3-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="82ea3-185">**SharePoint**</span></span>|<span data-ttu-id="82ea3-186">Lokacji</span><span class="sxs-lookup"><span data-stu-id="82ea3-186">Site</span></span>|<span data-ttu-id="82ea3-187">Listy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="82ea3-187">SharePoint List</span></span>
|<span data-ttu-id="82ea3-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="82ea3-188">**SQL**</span></span>|<span data-ttu-id="82ea3-189">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="82ea3-189">Database</span></span>|<span data-ttu-id="82ea3-190">Tabela</span><span class="sxs-lookup"><span data-stu-id="82ea3-190">Table</span></span> 
|<span data-ttu-id="82ea3-191">**Arkusz Google**</span><span class="sxs-lookup"><span data-stu-id="82ea3-191">**Google Sheet**</span></span>|<span data-ttu-id="82ea3-192">Arkusz kalkulacyjny</span><span class="sxs-lookup"><span data-stu-id="82ea3-192">Spreadsheet</span></span>|<span data-ttu-id="82ea3-193">Arkusza</span><span class="sxs-lookup"><span data-stu-id="82ea3-193">Worksheet</span></span> 
|<span data-ttu-id="82ea3-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="82ea3-194">**Excel**</span></span>|<span data-ttu-id="82ea3-195">Plik programu Excel</span><span class="sxs-lookup"><span data-stu-id="82ea3-195">Excel file</span></span>|<span data-ttu-id="82ea3-196">Arkusza</span><span class="sxs-lookup"><span data-stu-id="82ea3-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="82ea3-197">Użycie w języku C#</span><span class="sxs-lookup"><span data-stu-id="82ea3-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
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

<span data-ttu-id="82ea3-198"><!--
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
##Ustawienia źródła danych</span><span class="sxs-lookup"><span data-stu-id="82ea3-198"><!--
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
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="82ea3-199">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="82ea3-199">SQL Server</span></span>

<span data-ttu-id="82ea3-200">Skrypt do tworzenia i wypełniania tabeli Kontakt jest niższa.</span><span class="sxs-lookup"><span data-stu-id="82ea3-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="82ea3-201">dataSetName jest "domyślny".</span><span class="sxs-lookup"><span data-stu-id="82ea3-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="82ea3-202">Arkusze Google</span><span class="sxs-lookup"><span data-stu-id="82ea3-202">Google Sheets</span></span>
<span data-ttu-id="82ea3-203">W Google Docs, należy utworzyć arkusz kalkulacyjny w arkuszu o nazwie `Contact`.</span><span class="sxs-lookup"><span data-stu-id="82ea3-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="82ea3-204">Łącznik nie można użyć Nazwa wyświetlana arkusza kalkulacyjnego.</span><span class="sxs-lookup"><span data-stu-id="82ea3-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="82ea3-205">Potrzeb wewnętrzna nazwa (pogrubione) ma być używany jako dataSetName, na przykład: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  dodać nazwy kolumn `Id`, `LastName`, `FirstName` do pierwszego wiersza, następnie wypełnij dane na kolejne wiersze.</span><span class="sxs-lookup"><span data-stu-id="82ea3-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="82ea3-206">SalesForce</span><span class="sxs-lookup"><span data-stu-id="82ea3-206">Salesforce</span></span>
<span data-ttu-id="82ea3-207">dataSetName jest "domyślny".</span><span class="sxs-lookup"><span data-stu-id="82ea3-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="82ea3-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82ea3-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
