---
title: "rejestruje aaaManage DNS w usłudze Azure DNS przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Zarządzanie zestawów rekordów DNS i rekordy w usłudze Azure DNS, gdy hosting domeny w usłudze Azure DNS. Wszystkie polecenia programu PowerShell dla operacji na zestawów rekordów i rekordów."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="397c7-104">Zarządzanie rekordami DNS i zestawy rekordów w usłudze Azure DNS przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="397c7-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="397c7-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="397c7-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="397c7-106">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="397c7-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="397c7-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="397c7-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="397c7-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="397c7-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="397c7-109">W tym artykule opisano, jak rekordy toomanage DNS dla strefy DNS przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="397c7-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="397c7-110">Rekordy DNS można też zarządzać za pomocą wielu platform hello [interfejsu wiersza polecenia Azure](dns-operations-recordsets-cli.md) lub hello [portalu Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="397c7-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="397c7-111">Przykłady Hello w tym artykule założono, że masz już [zainstalowany program Azure PowerShell, zalogowany i utworzyć strefę DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="397c7-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="397c7-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="397c7-112">Introduction</span></span>

<span data-ttu-id="397c7-113">Przed utworzeniem rekordy DNS w usłudze Azure DNS, należy najpierw toounderstand jak usługi Azure DNS organizuje rekordy DNS w zestawach rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="397c7-114">Aby uzyskać więcej informacji na temat rekordów DNS w usłudze Azure DNS, zobacz [Strefy i rekordy DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="397c7-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="397c7-115">Utwórz nowy rekord DNS</span><span class="sxs-lookup"><span data-stu-id="397c7-115">Create a new DNS record</span></span>

<span data-ttu-id="397c7-116">Jeśli Twoje nowy rekord ma hello takie same nazwy i wpisać jako istniejącego rekordu, należy za[ją dodać toohello istniejącego zestawu rekordów](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="397c7-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="397c7-117">Twój nowy rekord ma inną tooall nazwę i typ istniejących rekordów, należy najpierw toocreate zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="397c7-118">Utwórz rekordy "" w zestawie rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="397c7-119">Tworzenie zestawów rekordów przy użyciu hello `New-AzureRmDnsRecordSet` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="397c7-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="397c7-120">Podczas tworzenia zestawu rekordów, należy nazwy zestawu rekordów hello toospecify, hello strefy, czas hello toolive (TTL), typ rekordu hello i toobe rekordów hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="397c7-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="397c7-121">Parametry Hello w celu dodania zestawu rekordów tooa rekordów różnią się zależnie od typu hello hello zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="397c7-122">Na przykład podczas korzystania z zestawu rekordów typu "A", potrzebujesz adresu IP hello toospecify za pomocą parametru hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="397c7-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="397c7-123">Inne parametry są używane dla innych typów rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="397c7-124">Zobacz [typu rekordu dodatkowe przykłady](#additional-record-type-examples) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="397c7-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="397c7-125">Witaj poniższy przykład tworzy hello nazwie względnej "www" w strefie DNS "contoso.com" hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="397c7-126">Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="397c7-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="397c7-127">Typ rekordu Hello jest "A", a hello TTL jest 3600 sekund.</span><span class="sxs-lookup"><span data-stu-id="397c7-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="397c7-128">Witaj zestaw rekordów zawiera jeden rekord o adresie IP "1.2.3.4".</span><span class="sxs-lookup"><span data-stu-id="397c7-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="397c7-129">zestaw rekordów toocreate na powitania wierzchołku i strefy (w tym przypadku "contoso.com"), użyj nazwy zestawu rekordów hello "@" (bez cudzysłowów):</span><span class="sxs-lookup"><span data-stu-id="397c7-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="397c7-130">Toocreate zestaw rekordów, zawierający więcej niż jeden rekord, należy najpierw utworzyć lokalnej tablicy i dodać rekordy hello, a następnie przekazać tablicy hello zbyt`New-AzureRmDnsRecordSet` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="397c7-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="397c7-131">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="397c7-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="397c7-132">Hello poniższy przykład przedstawia sposób toocreate, zestaw rekordów, o dwa wpisy metadanych, "dział = not" i "środowiska produkcji =".</span><span class="sxs-lookup"><span data-stu-id="397c7-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="397c7-133">Usługa DNS platformy Azure obsługuje również "empty" zestawów rekordów, które mogą działać jako tooreserve symbol zastępczy nazwy DNS przed utworzeniem rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="397c7-134">Pusty zestawów rekordów są widoczne w płaszczyźnie kontroli usługi Azure DNS hello, ale są wyświetlane na serwery hello Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="397c7-135">Witaj poniższy przykład tworzy pusty zestaw rekordów:</span><span class="sxs-lookup"><span data-stu-id="397c7-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="397c7-136">Tworzenie rekordów innych typów</span><span class="sxs-lookup"><span data-stu-id="397c7-136">Create records of other types</span></span>

<span data-ttu-id="397c7-137">Posiadanie widoczne szczegółowo jak rekordy toocreate "A", hello następujących przykładach pokazano, jak rekordy toocreate innych zarejestrować typy są obsługiwane przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="397c7-138">W każdym przypadku zostanie przedstawiony sposób toocreate rekord zestaw zawierający pojedynczy rekord.</span><span class="sxs-lookup"><span data-stu-id="397c7-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="397c7-139">Witaj wcześniejszych przykłady rekordy "" może być dostosowane toocreate zestawów rekordów innych typów zawierający wiele rekordów z metadanymi, lub ustawia toocreate pusty rekord.</span><span class="sxs-lookup"><span data-stu-id="397c7-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="397c7-140">Firma Microsoft nie dają toocreate przykład zestawu rekordów SOA, ponieważ SOAs są tworzone i usunąć z każdej strefy DNS i nie można utworzyć ani usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="397c7-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="397c7-141">Jednak [hello SOA można modyfikować, jak pokazano w przykładzie nowsze](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="397c7-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="397c7-142">Tworzenie zestawu rekordów AAAA z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="397c7-143">Tworzenie zestawu rekordów CNAME z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="397c7-144">Standardy usługi DNS Hello nie zezwalają na rekordy CNAME w wierzchołku hello strefy (`-Name '@'`), ani akceptują zestawów rekordów zawierających więcej niż jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="397c7-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="397c7-145">Aby uzyskać więcej informacji, zobacz [rekordy CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="397c7-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="397c7-146">Tworzenie zestawu rekordów MX z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="397c7-147">W tym przykładzie używamy nazwy zestawu rekordów hello "@" rekordu toocreate MX w wierzchołku strefy hello (w tym przypadku "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="397c7-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="397c7-148">Tworzenie zestawu rekordów NS z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="397c7-149">Tworzenie zestawu rekordów PTR z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="397c7-150">W takim przypadku "Mój-arpa-zone.com" reprezentuje hello strefy wyszukiwania wstecznego ARPA reprezentujący zakresowi adresów IP.</span><span class="sxs-lookup"><span data-stu-id="397c7-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="397c7-151">Każdy rekord PTR ustawione w tej strefie odpowiada tooan adres IP zakresu tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="397c7-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="397c7-152">Nazwa rekordu Hello "10" jest Witaj oktet ostatniego adresu IP hello tego zakresu IP reprezentowany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="397c7-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="397c7-153">Tworzenie zestawu rekordów SRV z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="397c7-154">Podczas tworzenia [zestawu rekordów SRV](dns-zones-records.md#srv-records), określ hello * \_usługi* i * \_protokołu* w hello nazwy zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="397c7-155">Nie istnieje żadne tooinclude potrzeby "@" w hello nazwy zestawu rekordów podczas tworzenia rekordów SRV zestawu w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="397c7-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="397c7-156">Tworzenie zestawu rekordów TXT z pojedynczym rekordem</span><span class="sxs-lookup"><span data-stu-id="397c7-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="397c7-157">Witaj poniższy przykład przedstawia sposób rejestrowania toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="397c7-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="397c7-158">Aby uzyskać więcej informacji na temat hello maksymalna długość ciągu obsługiwane w rekordach TXT, zobacz [rekordów TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="397c7-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="397c7-159">Pobierz zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-159">Get a record set</span></span>

<span data-ttu-id="397c7-160">Użyj istniejącego zestawu rekordów, tooretrieve `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="397c7-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="397c7-161">To polecenie cmdlet zwraca obiekt reprezentujący rekord hello w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="397c7-162">Jak `New-AzureRmDnsRecordSet`, musi być podana nazwa zestawu rekordów hello *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy.</span><span class="sxs-lookup"><span data-stu-id="397c7-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="397c7-163">Należy również typ rekordu hello toospecify i strefy hello zawierającej hello zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="397c7-164">Witaj poniższy przykład przedstawia sposób tooretrieve zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="397c7-165">W tym przykładzie strefie hello jest określona za pomocą hello `-ZoneName` i `-ResourceGroupName` parametrów.</span><span class="sxs-lookup"><span data-stu-id="397c7-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="397c7-166">Alternatywnie można również określić strefy hello przy użyciu obiektu strefy przekazywane przy użyciu hello `-Zone` parametru.</span><span class="sxs-lookup"><span data-stu-id="397c7-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="397c7-167">Lista zestawów rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-167">List record sets</span></span>

<span data-ttu-id="397c7-168">Można również użyć `Get-AzureRmDnsZone` zestawy toolist rekordów w strefie, pomijając hello `-Name` i/lub `-RecordType` parametrów.</span><span class="sxs-lookup"><span data-stu-id="397c7-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="397c7-169">Witaj poniższy przykład zwraca zestawy wszystkich rekordów w strefie hello:</span><span class="sxs-lookup"><span data-stu-id="397c7-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="397c7-170">Witaj poniższym przykładzie pokazano, jak rejestrować wszystkie zestawy danego typu mogą być pobierane przez określenie typu rekordu hello podczas pominięcie rekordu hello Nazwa zestawu:</span><span class="sxs-lookup"><span data-stu-id="397c7-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="397c7-171">zestawy wszystkich rekordów o podanej nazwie, tooretrieve różnych typów rekordów, należy tooretrieve wszystkie zestawy rekordów i następnie filtr hello wyniki:</span><span class="sxs-lookup"><span data-stu-id="397c7-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="397c7-172">W wszystkich hello powyżej przykłady, hello strefa może być określona za pomocą hello `-ZoneName` i `-ResourceGroupName`parametrów (jak pokazano), lub za pośrednictwem obiektu strefy:</span><span class="sxs-lookup"><span data-stu-id="397c7-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="397c7-173">Dodawanie rekordów tooan istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="397c7-174">tooadd istniejącego rekordu rekordów tooan ustawić, wykonaj następujące trzy kroki hello:</span><span class="sxs-lookup"><span data-stu-id="397c7-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="397c7-175">Pobierz hello istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="397c7-176">Dodaj hello nowych rekordów toohello lokalnego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="397c7-177">Jest to operacja offline.</span><span class="sxs-lookup"><span data-stu-id="397c7-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="397c7-178">Zatwierdź hello zmiany wstecz toohello usługa Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="397c7-179">Przy użyciu `Set-AzureRmDnsRecordSet` *zastępuje* hello istniejącego zestawu rekordów w usłudze Azure DNS (i wszystkich rekordów zawiera) z zestawu rekordów hello określony.</span><span class="sxs-lookup"><span data-stu-id="397c7-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="397c7-180">[Element etag kontroli](dns-zones-records.md#etags) są używane tooensure równoległe zmiany nie zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="397c7-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="397c7-181">Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.</span><span class="sxs-lookup"><span data-stu-id="397c7-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="397c7-182">Ta sekwencja operacji można też *przetwarzana potokowo*, co oznacza przekazać obiekt zestawu rekordów hello za pomocą potoku hello zamiast przekazaniem go jako parametr:</span><span class="sxs-lookup"><span data-stu-id="397c7-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="397c7-183">Witaj powyższych przykładach konfiguracji tooadd istniejącego rekordu "" tooan rekordów typu "A".</span><span class="sxs-lookup"><span data-stu-id="397c7-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="397c7-184">Podobne sekwencja operacji jest używane tooadd rekordów toorecord zestawy innych typów, zastępując hello `-Ipv4Address` parametr `Add-AzureRmDnsRecordConfig` z innym typem rekordu tooeach określonych parametrów.</span><span class="sxs-lookup"><span data-stu-id="397c7-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="397c7-185">Witaj parametry dla poszczególnych typów rekordów są hello takie same jak w przypadku hello `New-AzureRmDnsRecordConfig` polecenia cmdlet, jak pokazano w [typu rekordu dodatkowe przykłady](#additional-record-type-examples) powyżej.</span><span class="sxs-lookup"><span data-stu-id="397c7-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="397c7-186">Zestawy rekordów typu "CNAME" lub "SOA" nie może zawierać więcej niż jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="397c7-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="397c7-187">To ograniczenie wynika z hello standardy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="397c7-188">Nie jest to ograniczenie usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="397c7-189">Usuń rekord z istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="397c7-190">Hello tooremove procesu rekord na podstawie zestawu rekordów jest podobne tooadd procesu toohello istniejących rekordów tooan zestawu rekordów:</span><span class="sxs-lookup"><span data-stu-id="397c7-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="397c7-191">Pobierz hello istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="397c7-192">Usuń rekord hello z obiektu zestawu rekordów lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="397c7-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="397c7-193">Jest to operacja offline.</span><span class="sxs-lookup"><span data-stu-id="397c7-193">This is an off-line operation.</span></span> <span data-ttu-id="397c7-194">Hello rekordu, który jest usuwana musi być identyczna z istniejącym rekordem we wszystkich parametrów.</span><span class="sxs-lookup"><span data-stu-id="397c7-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="397c7-195">Zatwierdź hello zmiany wstecz toohello usługa Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="397c7-196">Użyj hello opcjonalne `-Overwrite` przełącznika toosuppress [sprawdza Etag](dns-zones-records.md#etags) równoczesnych zmian.</span><span class="sxs-lookup"><span data-stu-id="397c7-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="397c7-197">Przy użyciu hello powyżej sekwencji tooremove hello ostatni rekord z zestawu rekordów nie powoduje usunięcia hello zestawu rekordów, a nie wydostaje pusty zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="397c7-198">Zobacz tooremove całkowicie, zestaw rekordów [Usuń zestaw rekordów](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="397c7-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="397c7-199">Podobnie tooadding rekordów tooa zestawu rekordów, sekwencja hello tooremove operacje, w których zestaw rekordów mogą również być przekazywane w potoku:</span><span class="sxs-lookup"><span data-stu-id="397c7-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="397c7-200">Różnych typów rekordów są obsługiwane, przekazując odpowiednie parametry typu hello zbyt`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="397c7-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="397c7-201">Witaj parametry dla poszczególnych typów rekordów są hello takie same jak w przypadku hello `New-AzureRmDnsRecordConfig` polecenia cmdlet, jak pokazano w [typu rekordu dodatkowe przykłady](#additional-record-type-examples) powyżej.</span><span class="sxs-lookup"><span data-stu-id="397c7-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="397c7-202">Modyfikowanie istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-202">Modify an existing record set</span></span>

<span data-ttu-id="397c7-203">kroki Hello modyfikowania istniejącego zestawu rekordów są podobne kroki toohello, które należy wykonać podczas dodawania lub usuwania rekordów z zestawu rekordów:</span><span class="sxs-lookup"><span data-stu-id="397c7-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="397c7-204">Pobrać hello istniejącego rekordu skonfigurowane przy użyciu `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="397c7-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="397c7-205">Modyfikowanie obiektu lokalnego zestawu rekordów hello przez:</span><span class="sxs-lookup"><span data-stu-id="397c7-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="397c7-206">Dodawanie lub usuwanie rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-206">Adding or removing records</span></span>
    * <span data-ttu-id="397c7-207">Zmiana parametrów hello istniejących rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="397c7-208">Zmiana rekordu hello Ustaw metadanych i czas toolive (TTL)</span><span class="sxs-lookup"><span data-stu-id="397c7-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="397c7-209">Zatwierdź zmiany przy użyciu hello `Set-AzureRmDnsRecordSet` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="397c7-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="397c7-210">To *zastępuje* hello istniejącego zestawu rekordów w usłudze Azure DNS z zestawu rekordów hello określony.</span><span class="sxs-lookup"><span data-stu-id="397c7-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="397c7-211">Korzystając z `Set-AzureRmDnsRecordSet`, [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="397c7-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="397c7-212">Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.</span><span class="sxs-lookup"><span data-stu-id="397c7-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="397c7-213">Ustaw tooupdate rekordu w istniejącego rekordu</span><span class="sxs-lookup"><span data-stu-id="397c7-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="397c7-214">W tym przykładzie zmienimy hello adresu IP istniejącego rekordu "":</span><span class="sxs-lookup"><span data-stu-id="397c7-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="397c7-215">toomodify rekord SOA</span><span class="sxs-lookup"><span data-stu-id="397c7-215">toomodify an SOA record</span></span>

<span data-ttu-id="397c7-216">Nie można dodać lub usunąć rekordy hello automatycznie utworzony rekord SOA na wierzchołku strefy hello (`-Name "@"`, w tym znaki cudzysłowu).</span><span class="sxs-lookup"><span data-stu-id="397c7-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="397c7-217">Jednak można zmodyfikować jego dowolne parametry hello w hello rekord SOA (z wyjątkiem "Host") i czas wygaśnięcia zestawu rekordów hello.</span><span class="sxs-lookup"><span data-stu-id="397c7-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="397c7-218">powitania po przykładzie pokazano, jak toochange hello *E-mail* właściwości hello rekord SOA:</span><span class="sxs-lookup"><span data-stu-id="397c7-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="397c7-219">toomodify NS rekordów w wierzchołku strefy hello</span><span class="sxs-lookup"><span data-stu-id="397c7-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="397c7-220">zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="397c7-221">Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.</span><span class="sxs-lookup"><span data-stu-id="397c7-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="397c7-222">Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="397c7-223">Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="397c7-224">Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="397c7-225">Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="397c7-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="397c7-226">Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="397c7-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="397c7-227">Witaj poniższy przykład przedstawia tooadd rekordów NS toohello dodatkowe nazwy serwera konfiguracji na wierzchołku strefy hello:</span><span class="sxs-lookup"><span data-stu-id="397c7-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="397c7-228">metadane zestawu rekordów toomodify</span><span class="sxs-lookup"><span data-stu-id="397c7-228">toomodify record set metadata</span></span>

<span data-ttu-id="397c7-229">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="397c7-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="397c7-230">Witaj poniższym przykładzie pokazano, jak ustawić toomodify hello metadane istniejącego rekordu:</span><span class="sxs-lookup"><span data-stu-id="397c7-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="397c7-231">Usuń zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="397c7-231">Delete a record set</span></span>

<span data-ttu-id="397c7-232">Zestawy rekordów można usunąć za pomocą hello `Remove-AzureRmDnsRecordSet` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="397c7-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="397c7-233">Usunięcie zestawu rekordów spowoduje również usunięcie wszystkich rekordów w zestawie rekordów hello.</span><span class="sxs-lookup"><span data-stu-id="397c7-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="397c7-234">Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="397c7-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="397c7-235">Usługa Azure DNS utworzenia są automatycznie hello strefy został utworzony i usunie je automatycznie po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="397c7-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="397c7-236">Witaj poniższy przykład przedstawia sposób toodelete zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="397c7-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="397c7-237">W tym przykładzie nazwa zestawu rekordów hello, zestaw rekordów typu nazwa strefy i grupy zasobów są każdego określonego jawnie.</span><span class="sxs-lookup"><span data-stu-id="397c7-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="397c7-238">Możesz też zestawu rekordów hello może zostać określony przez nazwę i typ i hello strefy określonej za pomocą obiektu:</span><span class="sxs-lookup"><span data-stu-id="397c7-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="397c7-239">Trzecia opcja można określić samego zestawu rekordów hello przy użyciu obiektu zestaw rekordów:</span><span class="sxs-lookup"><span data-stu-id="397c7-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="397c7-240">Po określeniu zestawu rekordów hello toobe usunięte za pomocą obiektu zestawu rekordów, [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="397c7-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="397c7-241">Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.</span><span class="sxs-lookup"><span data-stu-id="397c7-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="397c7-242">obiekt zestawu rekordów Hello również mogą być przetwarzane potokowo zamiast przekazywana jako parametr:</span><span class="sxs-lookup"><span data-stu-id="397c7-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="397c7-243">Monituje o potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="397c7-243">Confirmation prompts</span></span>

<span data-ttu-id="397c7-244">Witaj `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, i `Remove-AzureRmDnsRecordSet` o potwierdzenie obsługuje wszystkie polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="397c7-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="397c7-245">Każde polecenie cmdlet monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej.</span><span class="sxs-lookup"><span data-stu-id="397c7-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="397c7-246">Ponieważ hello wartości domyślnej dla `$ConfirmPreference` jest `High`, monity nie są podane, używając hello domyślnych ustawień programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="397c7-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="397c7-247">Można zastąpić bieżący hello `$ConfirmPreference` ustawienie za pomocą hello `-Confirm` parametru.</span><span class="sxs-lookup"><span data-stu-id="397c7-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="397c7-248">Jeśli określisz `-Confirm` lub `-Confirm:$True` , hello polecenie cmdlet monituje o potwierdzenie przed go uruchamia.</span><span class="sxs-lookup"><span data-stu-id="397c7-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="397c7-249">Jeśli określisz `-Confirm:$False` , hello polecenie cmdlet monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="397c7-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="397c7-250">Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="397c7-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="397c7-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="397c7-251">Next steps</span></span>

<span data-ttu-id="397c7-252">Dowiedz się więcej o [strefy i rekordy w usłudze Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="397c7-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="397c7-253">Dowiedz się, jak za[ochrony strefy i rekordy](dns-protect-zones-recordsets.md) przy użyciu usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="397c7-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="397c7-254">Przejrzyj hello [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="397c7-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
