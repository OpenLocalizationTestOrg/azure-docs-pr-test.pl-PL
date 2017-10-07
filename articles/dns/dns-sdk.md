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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="bc303-103">Tworzenie strefy DNS i zestawy rekordów przy użyciu zestawu .NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="bc303-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="bc303-104">Można zautomatyzować operacje toocreate, usuwania lub aktualizacji strefy DNS, zestawów rekordów i rekordów przy użyciu zestawu SDK DNS z biblioteki .NET zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="bc303-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="bc303-105">Pełna projektu programu Visual Studio jest dostępny [tutaj.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="bc303-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="bc303-106">Utwórz konto główne usługi</span><span class="sxs-lookup"><span data-stu-id="bc303-106">Create a service principal account</span></span>

<span data-ttu-id="bc303-107">Zazwyczaj otrzymuje dostęp programistyczny tooAzure zasobów za pomocą dedykowanego konta, a nie poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc303-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="bc303-108">Te dedykowanego konta są nazywane "nazwy głównej usługi" kont.</span><span class="sxs-lookup"><span data-stu-id="bc303-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="bc303-109">toouse hello Azure DNS SDK przykładowy projekt, należy najpierw toocreate konta głównego usługi i przypisz go hello odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="bc303-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="bc303-110">Postępuj zgodnie z [tych instrukcji](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate konto główne usługi (hello zestawu SDK usługi Azure DNS przykładowy projekt założono uwierzytelniania opartego na hasłach).</span><span class="sxs-lookup"><span data-stu-id="bc303-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="bc303-111">Utwórz grupę zasobów ([Oto jak](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="bc303-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="bc303-112">Użyj Azure RBAC toogrant hello konto główne "Współautora strefę DNS" uprawnienia toohello grupy zasobów usługi ([Oto jak](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="bc303-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="bc303-113">Jeśli używasz hello zestawu SDK usługi Azure DNS przykładowy projekt, Edytuj plik "program.cs" hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bc303-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="bc303-114">Wstaw hello poprawne wartości dla identyfikatora dzierżawcy hello, clientId (znanej także jako identyfikator konta), klucz tajny (hasło konta głównego usługi) i identyfikator subskrypcji w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="bc303-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="bc303-115">Wprowadź nazwę grupy zasobów hello wybranego w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="bc303-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="bc303-116">Wprowadź nazwę strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="bc303-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="bc303-117">Pakiety NuGet i deklaracje przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="bc303-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="bc303-118">toouse hello DNS platformy Azure .NET SDK, należy tooinstall hello **biblioteki zarządzania usługi Azure DNS** pakietu NuGet i inne wymagane pakiety platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bc303-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="bc303-119">W **programu Visual Studio**, otwórz projekt lub nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="bc303-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="bc303-120">Przejdź za**narzędzia**  **>**  **Menedżera pakietów NuGet**  **>**  **Zarządzanie pakietami NuGet dla Rozwiązania...** .</span><span class="sxs-lookup"><span data-stu-id="bc303-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="bc303-121">Kliknij przycisk **Przeglądaj**, Włącz hello **Uwzględnij wersję wstępną** wyboru i wpisz **Microsoft.Azure.Management.Dns** w polu wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="bc303-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="bc303-122">Wybierz pakiet hello i kliknij przycisk **zainstalować** tooadd on tooyour projekt programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc303-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="bc303-123">Powtórz proces hello powyżej tooalso hello Zainstaluj następujące pakiety: **Microsoft.Rest.ClientRuntime.Azure.Authentication** i **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="bc303-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="bc303-124">Dodawanie deklaracji przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="bc303-124">Add namespace declarations</span></span>

<span data-ttu-id="bc303-125">Dodaj następujące deklaracje przestrzeni nazw hello</span><span class="sxs-lookup"><span data-stu-id="bc303-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="bc303-126">Inicjowanie klienta zarządzania hello DNS</span><span class="sxs-lookup"><span data-stu-id="bc303-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="bc303-127">Witaj *DnsManagementClient* zawiera hello metody i właściwości niezbędne do zarządzania strefy DNS i zestawy rekordów.</span><span class="sxs-lookup"><span data-stu-id="bc303-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="bc303-128">Witaj poniższy kod loguje konto główne usługi toohello i tworzy obiekt DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="bc303-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="bc303-129">Utwórz lub zaktualizuj strefę DNS</span><span class="sxs-lookup"><span data-stu-id="bc303-129">Create or update a DNS zone</span></span>

<span data-ttu-id="bc303-130">toocreate strefę DNS, najpierw "Strefy" tworzony jest obiekt parametrów strefy DNS hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="bc303-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="bc303-131">Ponieważ strefy DNS nie są połączone tooa określonego regionu, too'global ustawiono lokalizacji hello ".</span><span class="sxs-lookup"><span data-stu-id="bc303-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="bc303-132">W tym przykładzie [usługi Azure Resource Manager "tag"](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) jest także dodawane toohello strefy.</span><span class="sxs-lookup"><span data-stu-id="bc303-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="bc303-133">Utwórz tooactually lub strefy hello aktualizacji w usłudze Azure DNS, hello strefy obiekt zawierający parametry strefy hello jest przekazywany toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* metody.</span><span class="sxs-lookup"><span data-stu-id="bc303-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="bc303-134">DnsManagementClient obsługuje trzy tryby działania: synchroniczne ("CreateOrUpdate"), asynchroniczne ("CreateOrUpdateAsync"), lub asynchroniczne o odpowiedzi toohello HTTP dostępu (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="bc303-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="bc303-135">Można wybrać dowolną z tych trybów, w zależności od potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc303-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="bc303-136">Usługa DNS platformy Azure obsługuje optymistycznej współbieżności, nazywany [elementy etag](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="bc303-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="bc303-137">W tym przykładzie określenie "*" dla nagłówka "If-None-Match" hello informuje toocreate usługi Azure DNS strefy DNS, jeśli już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bc303-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="bc303-138">Wywołanie Hello kończy się niepowodzeniem, jeśli strefę o hello podanej nazwie już istnieje w hello danej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bc303-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

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

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="bc303-139">Tworzenie zestawów rekordów DNS i rekordów</span><span class="sxs-lookup"><span data-stu-id="bc303-139">Create DNS record sets and records</span></span>

<span data-ttu-id="bc303-140">Rekordy DNS są zarządzane jako zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="bc303-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="bc303-141">Zestaw rekordów z hello takie same nazwy i rejestrowanie jest zestaw rekordów typu w strefie.</span><span class="sxs-lookup"><span data-stu-id="bc303-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="bc303-142">Nazwa zestawu rekordów Hello toohello względną nazwę strefy, nie hello w pełni kwalifikowana nazwa DNS.</span><span class="sxs-lookup"><span data-stu-id="bc303-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="bc303-143">zestaw rekordów toocreate lub aktualizacji, obiektu parametrów "Zestawu rekordów" jest utworzony i przekazano zbyt*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="bc303-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="bc303-144">Zgodnie ze strefami DNS są dostępne trzy tryby działania: synchroniczne ("CreateOrUpdate"), asynchroniczne ("CreateOrUpdateAsync"), lub asynchroniczne o odpowiedzi toohello HTTP dostępu (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="bc303-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="bc303-145">Podobnie jak w przypadku stref DNS, operacje na zestawów rekordów obejmuje obsługę optymistycznej współbieżności.</span><span class="sxs-lookup"><span data-stu-id="bc303-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="bc303-146">W tym przykładzie ponieważ "If-Match" i "If-None-Match" nie są określone, zestaw rekordów hello zawsze jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="bc303-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="bc303-147">Tego wywołania spowoduje zastąpienie wszelkich istniejącego zestawu rekordów z hello takie same nazwy i zarejestrować typu w tej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="bc303-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

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

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="bc303-148">Pobierz stref i zestawy rekordów</span><span class="sxs-lookup"><span data-stu-id="bc303-148">Get zones and record sets</span></span>

<span data-ttu-id="bc303-149">Witaj *DnsManagementClient.Zones.Get* i *DnsManagementClient.RecordSets.Get* metody pobrać odpowiednio poszczególnych stref i zestawy rekordów.</span><span class="sxs-lookup"><span data-stu-id="bc303-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="bc303-150">Zestawy rekordów są identyfikowane przez ich typu, nazwy i hello strefy i grupie zasobów, które istnieją w.</span><span class="sxs-lookup"><span data-stu-id="bc303-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="bc303-151">Strefy są identyfikowane przez ich nazwy i hello grupy zasobów, które istnieją w.</span><span class="sxs-lookup"><span data-stu-id="bc303-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="bc303-152">Aktualizowanie istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="bc303-152">Update an existing record set</span></span>

<span data-ttu-id="bc303-153">tooupdate istniejącego rekordu DNS należy ustawić, należy najpierw pobrać hello zestawu rekordów, a następnie Uaktualnij hello rekord Ustaw zawartość, a następnie prześlij hello zmianę.</span><span class="sxs-lookup"><span data-stu-id="bc303-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="bc303-154">W tym przykładzie określono hello "Tagu" z hello pobrać zestawu w parametrze "If-Match" hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="bc303-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="bc303-155">Wywołanie Hello kończy się niepowodzeniem, jeśli operacja współbieżna zmodyfikował hello rekord w hello międzyczasie.</span><span class="sxs-lookup"><span data-stu-id="bc303-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="bc303-156">Lista stref i zestawy rekordów</span><span class="sxs-lookup"><span data-stu-id="bc303-156">List zones and record sets</span></span>

<span data-ttu-id="bc303-157">toolist strefy, użyj hello *DnsManagementClient.Zones.List...*  metod, które obsługują wyświetlanie listy wszystkich stref w danej grupy zasobów albo wszystkie strefy w zestawach rekordów toolist danej subskrypcji platformy Azure (za pośrednictwem grup zasobów.), użyj *DnsManagementClient.RecordSets.List...*  metody, które obsługują, albo listę wszystkich zestawów rekordów w strefie danego lub tylko tych zestawów rekordów określonego typu.</span><span class="sxs-lookup"><span data-stu-id="bc303-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="bc303-158">Należy pamiętać, podczas wyświetlania stref i zestawy rekordów, które powoduje może zostać podzielony na strony.</span><span class="sxs-lookup"><span data-stu-id="bc303-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="bc303-159">powitania po przykładzie pokazano, jak tooiterate stronach hello wyników.</span><span class="sxs-lookup"><span data-stu-id="bc303-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="bc303-160">(Rozmiar sztucznie strony "2" jest używane tooforce stronicowania; w praktyce tego parametru należy pominąć i hello domyślny rozmiar strony używany).</span><span class="sxs-lookup"><span data-stu-id="bc303-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bc303-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc303-161">Next steps</span></span>

<span data-ttu-id="bc303-162">Pobierz hello [zestawu SDK usługi Azure DNS .NET przykładowy projekt](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), która obejmuje dodatkowe przykłady sposobu toouse hello SDK .NET usługi Azure DNS, wraz z przykładami dla innych typów rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="bc303-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
