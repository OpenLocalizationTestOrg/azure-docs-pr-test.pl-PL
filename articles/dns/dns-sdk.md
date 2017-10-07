---
title: "strefy DNS aaaCreate i zestawów rekordów w usłudze Azure DNS przy użyciu zestawu .NET SDK hello | Dokumentacja firmy Microsoft"
description: "Jak stref DNS toocreate zestawami rekordów i w usłudze Azure DNS za pomocą hello zestawu .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Tworzenie strefy DNS i zestawy rekordów przy użyciu zestawu .NET SDK hello

Można zautomatyzować operacje toocreate, usuwania lub aktualizacji strefy DNS, zestawów rekordów i rekordów przy użyciu zestawu SDK DNS z biblioteki .NET zarządzania DNS. Pełna projektu programu Visual Studio jest dostępny [tutaj.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Utwórz konto główne usługi

Zazwyczaj otrzymuje dostęp programistyczny tooAzure zasobów za pomocą dedykowanego konta, a nie poświadczenia użytkownika. Te dedykowanego konta są nazywane "nazwy głównej usługi" kont. toouse hello Azure DNS SDK przykładowy projekt, należy najpierw toocreate konta głównego usługi i przypisz go hello odpowiednie uprawnienia.

1. Postępuj zgodnie z [tych instrukcji](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate konto główne usługi (hello zestawu SDK usługi Azure DNS przykładowy projekt założono uwierzytelniania opartego na hasłach).
2. Utwórz grupę zasobów ([Oto jak](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Użyj Azure RBAC toogrant hello konto główne "Współautora strefę DNS" uprawnienia toohello grupy zasobów usługi ([Oto jak](../active-directory/role-based-access-control-configure.md).)
4. Jeśli używasz hello zestawu SDK usługi Azure DNS przykładowy projekt, Edytuj plik "program.cs" hello w następujący sposób:

   * Wstaw hello poprawne wartości dla identyfikatora dzierżawcy hello, clientId (znanej także jako identyfikator konta), klucz tajny (hasło konta głównego usługi) i identyfikator subskrypcji w kroku 1.
   * Wprowadź nazwę grupy zasobów hello wybranego w kroku 2.
   * Wprowadź nazwę strefy DNS.

## <a name="nuget-packages-and-namespace-declarations"></a>Pakiety NuGet i deklaracje przestrzeni nazw

toouse hello DNS platformy Azure .NET SDK, należy tooinstall hello **biblioteki zarządzania usługi Azure DNS** pakietu NuGet i inne wymagane pakiety platformy Azure.

1. W **programu Visual Studio**, otwórz projekt lub nowego projektu.
2. Przejdź za**narzędzia**  **>**  **Menedżera pakietów NuGet**  **>**  **Zarządzanie pakietami NuGet dla Rozwiązania...** .
3. Kliknij przycisk **Przeglądaj**, Włącz hello **Uwzględnij wersję wstępną** wyboru i wpisz **Microsoft.Azure.Management.Dns** w polu wyszukiwania hello.
4. Wybierz pakiet hello i kliknij przycisk **zainstalować** tooadd on tooyour projekt programu Visual Studio.
5. Powtórz proces hello powyżej tooalso hello Zainstaluj następujące pakiety: **Microsoft.Rest.ClientRuntime.Azure.Authentication** i **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Dodawanie deklaracji przestrzeni nazw

Dodaj następujące deklaracje przestrzeni nazw hello

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Inicjowanie klienta zarządzania hello DNS

Witaj *DnsManagementClient* zawiera hello metody i właściwości niezbędne do zarządzania strefy DNS i zestawy rekordów.  Witaj poniższy kod loguje konto główne usługi toohello i tworzy obiekt DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Utwórz lub zaktualizuj strefę DNS

toocreate strefę DNS, najpierw "Strefy" tworzony jest obiekt parametrów strefy DNS hello toocontain. Ponieważ strefy DNS nie są połączone tooa określonego regionu, too'global ustawiono lokalizacji hello ". W tym przykładzie [usługi Azure Resource Manager "tag"](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) jest także dodawane toohello strefy.

Utwórz tooactually lub strefy hello aktualizacji w usłudze Azure DNS, hello strefy obiekt zawierający parametry strefy hello jest przekazywany toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* metody.

> [!NOTE]
> DnsManagementClient obsługuje trzy tryby działania: synchroniczne ("CreateOrUpdate"), asynchroniczne ("CreateOrUpdateAsync"), lub asynchroniczne o odpowiedzi toohello HTTP dostępu (CreateOrUpdateWithHttpMessagesAsync).  Można wybrać dowolną z tych trybów, w zależności od potrzeb aplikacji.

Usługa DNS platformy Azure obsługuje optymistycznej współbieżności, nazywany [elementy etag](dns-getstarted-create-dnszone.md). W tym przykładzie określenie "*" dla nagłówka "If-None-Match" hello informuje toocreate usługi Azure DNS strefy DNS, jeśli już nie istnieje.  Wywołanie Hello kończy się niepowodzeniem, jeśli strefę o hello podanej nazwie już istnieje w hello danej grupy zasobów.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>Tworzenie zestawów rekordów DNS i rekordów

Rekordy DNS są zarządzane jako zestawu rekordów. Zestaw rekordów z hello takie same nazwy i rejestrowanie jest zestaw rekordów typu w strefie.  Nazwa zestawu rekordów Hello toohello względną nazwę strefy, nie hello w pełni kwalifikowana nazwa DNS.

zestaw rekordów toocreate lub aktualizacji, obiektu parametrów "Zestawu rekordów" jest utworzony i przekazano zbyt*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Zgodnie ze strefami DNS są dostępne trzy tryby działania: synchroniczne ("CreateOrUpdate"), asynchroniczne ("CreateOrUpdateAsync"), lub asynchroniczne o odpowiedzi toohello HTTP dostępu (CreateOrUpdateWithHttpMessagesAsync).

Podobnie jak w przypadku stref DNS, operacje na zestawów rekordów obejmuje obsługę optymistycznej współbieżności.  W tym przykładzie ponieważ "If-Match" i "If-None-Match" nie są określone, zestaw rekordów hello zawsze jest tworzony.  Tego wywołania spowoduje zastąpienie wszelkich istniejącego zestawu rekordów z hello takie same nazwy i zarejestrować typu w tej strefie DNS.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>Pobierz stref i zestawy rekordów

Witaj *DnsManagementClient.Zones.Get* i *DnsManagementClient.RecordSets.Get* metody pobrać odpowiednio poszczególnych stref i zestawy rekordów. Zestawy rekordów są identyfikowane przez ich typu, nazwy i hello strefy i grupie zasobów, które istnieją w. Strefy są identyfikowane przez ich nazwy i hello grupy zasobów, które istnieją w.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Aktualizowanie istniejącego zestawu rekordów

tooupdate istniejącego rekordu DNS należy ustawić, należy najpierw pobrać hello zestawu rekordów, a następnie Uaktualnij hello rekord Ustaw zawartość, a następnie prześlij hello zmianę.  W tym przykładzie określono hello "Tagu" z hello pobrać zestawu w parametrze "If-Match" hello rekordów. Wywołanie Hello kończy się niepowodzeniem, jeśli operacja współbieżna zmodyfikował hello rekord w hello międzyczasie.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Lista stref i zestawy rekordów

toolist strefy, użyj hello *DnsManagementClient.Zones.List...*  metod, które obsługują wyświetlanie listy wszystkich stref w danej grupy zasobów albo wszystkie strefy w zestawach rekordów toolist danej subskrypcji platformy Azure (za pośrednictwem grup zasobów.), użyj *DnsManagementClient.RecordSets.List...*  metody, które obsługują, albo listę wszystkich zestawów rekordów w strefie danego lub tylko tych zestawów rekordów określonego typu.

Należy pamiętać, podczas wyświetlania stref i zestawy rekordów, które powoduje może zostać podzielony na strony.  powitania po przykładzie pokazano, jak tooiterate stronach hello wyników. (Rozmiar sztucznie strony "2" jest używane tooforce stronicowania; w praktyce tego parametru należy pominąć i hello domyślny rozmiar strony używany).

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>Następne kroki

Pobierz hello [zestawu SDK usługi Azure DNS .NET przykładowy projekt](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), która obejmuje dodatkowe przykłady sposobu toouse hello SDK .NET usługi Azure DNS, wraz z przykładami dla innych typów rekordów DNS.
