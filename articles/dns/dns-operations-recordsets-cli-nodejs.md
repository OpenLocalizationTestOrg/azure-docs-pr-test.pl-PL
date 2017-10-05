---
title: "Zarządzanie rekordami DNS w usłudze Azure DNS przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Zarządzanie zestawów rekordów DNS i rekordy w usłudze Azure DNS, gdy hosting domeny w usłudze Azure DNS. Wszystkie polecenia interfejsu wiersza polecenia 1.0 dla operacji na zestawów rekordów i rekordów."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="807d0-104">Zarządzanie rekordami DNS w usłudze Azure DNS przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="807d0-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="807d0-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="807d0-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="807d0-106">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="807d0-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="807d0-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="807d0-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="807d0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="807d0-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="807d0-109">W tym artykule przedstawiono sposób zarządzania rekordy DNS dla strefy DNS przy użyciu wielu platform Azure interfejsu wiersza polecenia (CLI), która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="807d0-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="807d0-110">Można również zarządzać rekordami DNS przy użyciu [programu Azure PowerShell](dns-operations-recordsets.md) lub [portalu Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="807d0-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="807d0-111">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="807d0-111">CLI versions to complete the task</span></span>

<span data-ttu-id="807d0-112">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="807d0-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="807d0-113">[Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-recordsets-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="807d0-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="807d0-114">[Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-recordsets-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="807d0-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="807d0-115">Przykłady w tym artykule założono, że masz już [zainstalowane 1.0 interfejsu wiersza polecenia Azure, zalogowany i utworzyć strefę DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="807d0-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="807d0-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="807d0-116">Introduction</span></span>

<span data-ttu-id="807d0-117">Przed utworzeniem rekordów DNS w usłudze Azure DNS należy najpierw zrozumieć, w jaki sposób usługa Azure DNS organizuje rekordy DNS w zestawy rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="807d0-118">Aby uzyskać więcej informacji na temat rekordów DNS w usłudze Azure DNS, zobacz [Strefy i rekordy DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="807d0-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="807d0-119">Tworzenie rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="807d0-119">Create a DNS record</span></span>

<span data-ttu-id="807d0-120">Aby utworzyć rekord DNS, użyj polecenia `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="807d0-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="807d0-121">Aby uzyskać pomoc, zobacz `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="807d0-122">Podczas tworzenia rekordu należy określić nazwę grupy zasobów, nazwę strefy, nazwę zestawu rekordów, typ rekordu oraz szczegóły tworzonego rekordu.</span><span class="sxs-lookup"><span data-stu-id="807d0-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="807d0-123">Podana nazwa zestawu rekordów musi być *względną* nazwy, co oznacza należy wykluczyć Nazwa strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="807d0-124">Jeśli zestaw rekordów jeszcze nie istnieje, to polecenie utworzy go dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="807d0-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="807d0-125">Jeśli istnieje już zestaw rekordów, to polecenie adda przez użytkownika do istniejącego rekordu zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="807d0-126">Jeśli jest tworzony nowy rekord, używany jest domyślny czas wygaśnięcia wynoszący 3600.</span><span class="sxs-lookup"><span data-stu-id="807d0-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="807d0-127">Aby uzyskać instrukcje dotyczące sposobu używania różnych TTLs, zobacz [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="807d0-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="807d0-128">Poniższy przykład tworzy rekord A o nazwie *www* w strefie *contoso.com* w grupie zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="807d0-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="807d0-129">Adres IP rekordu A to *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="807d0-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="807d0-130">Aby utworzyć rekord w wierzchołku strefy (w tym przypadku "contoso.com"), użyj nazwy rekordu "@", wraz z cudzysłowami:</span><span class="sxs-lookup"><span data-stu-id="807d0-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="807d0-131">Tworzenie zestawu rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="807d0-131">Create a DNS record set</span></span>

<span data-ttu-id="807d0-132">W powyższych przykładach rekord DNS albo został dodany do istniejącego zestawu rekordów lub zestawu rekordów została utworzona *niejawnie*.</span><span class="sxs-lookup"><span data-stu-id="807d0-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="807d0-133">Można również utworzyć zestaw rekordów *jawnie* przed dodaniem do niej rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="807d0-134">Usługa DNS platformy Azure obsługuje "empty" zestawów rekordów, które mogą działać jako symbol zastępczy do zarezerwowania nazwy DNS przed utworzeniem rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="807d0-135">Pusty zestawów rekordów są widoczne w płaszczyźnie kontroli usługi Azure DNS, ale nie są wyświetlane na serwery nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="807d0-136">Zestawy rekordów są tworzone przy użyciu `azure network dns record-set create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="807d0-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="807d0-137">Aby uzyskać pomoc, zobacz `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="807d0-138">Tworzenie rekordu jawnie ustaw służy do określenia, takie jak właściwości zestawu rekordów [czasu wygaśnięcia (TTL, Time-To-Live)](dns-zones-records.md#time-to-live) i metadanych.</span><span class="sxs-lookup"><span data-stu-id="807d0-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="807d0-139">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) można skojarzyć dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="807d0-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="807d0-140">Poniższy przykład tworzy rekord pusty ustawić TTL 60 sekund, przy użyciu `--ttl` parametr (forma krótka `-l`):</span><span class="sxs-lookup"><span data-stu-id="807d0-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="807d0-141">W poniższym przykładzie jest tworzony rekord z dwóch wpisów metadanych, "dział = not" i "środowiska produkcji =", za pomocą `--metadata` parametru (krótka wersja `-m`):</span><span class="sxs-lookup"><span data-stu-id="807d0-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="807d0-142">Posiadanie utworzony pusty zestaw rekordów, można dodawać rekordy przy użyciu `azure network dns record-set add-record` zgodnie z opisem w [Utwórz rekord DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="807d0-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="807d0-143">Tworzenie rekordów innych typów</span><span class="sxs-lookup"><span data-stu-id="807d0-143">Create records of other types</span></span>

<span data-ttu-id="807d0-144">O przedstawiono szczegółowo sposób utworzyć rekordy "", następujące przykłady przedstawiają sposób tworzenia rekordu innych typów rekordów obsługiwane przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="807d0-145">Parametry używane do określenia danych rekordu różnią się w zależności od typu rekordu.</span><span class="sxs-lookup"><span data-stu-id="807d0-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="807d0-146">Na przykład w przypadku rekordu typu „A” należy podać adres IPv4 przy użyciu parametru `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="807d0-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="807d0-147">Parametry dla poszczególnych typów rekordów mogą być wyświetlane przy użyciu `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="807d0-148">W każdym przypadku zostanie przedstawiony sposób jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="807d0-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="807d0-149">Rekord jest dodawana do istniejącego zestawu rekordów lub niejawnie utworzyć zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="807d0-150">Aby uzyskać więcej informacji na temat tworzenia zestawów rekordów i rekordu definiujący parametr jawnie, zobacz [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="807d0-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="807d0-151">Firma Microsoft nie dają przykład można utworzyć zestawu rekordów SOA, ponieważ SOAs są tworzone i usunąć z każdej strefy DNS i nie można utworzyć ani usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="807d0-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="807d0-152">Jednak [SOA można modyfikować, jak pokazano w przykładzie nowsze](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="807d0-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="807d0-153">Utwórz rekord AAAA</span><span class="sxs-lookup"><span data-stu-id="807d0-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="807d0-154">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="807d0-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="807d0-155">Standardy usługi DNS nie zezwalają na rekordy CNAME w wierzchołku strefy (`-Name "@"`), ani akceptują zestawów rekordów zawierających więcej niż jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="807d0-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="807d0-156">Aby uzyskać więcej informacji, zobacz [rekordy CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="807d0-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="807d0-157">Utwórz rekord MX</span><span class="sxs-lookup"><span data-stu-id="807d0-157">Create an MX record</span></span>

<span data-ttu-id="807d0-158">W tym przykładzie używamy nazwy zestawu rekordów „@”, aby utworzyć rekord MX w wierzchołku strefy (w tym przypadku „contoso.com”).</span><span class="sxs-lookup"><span data-stu-id="807d0-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="807d0-159">Tworzenie rekordów NS</span><span class="sxs-lookup"><span data-stu-id="807d0-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="807d0-160">Utwórz rekord PTR</span><span class="sxs-lookup"><span data-stu-id="807d0-160">Create a PTR record</span></span>

<span data-ttu-id="807d0-161">W takim przypadku "Mój-arpa-zone.com" reprezentuje strefy ARPA reprezentujący zakresowi adresów IP.</span><span class="sxs-lookup"><span data-stu-id="807d0-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="807d0-162">Każdy rekord PTR w tej strefie odnosi się do adresu IP w tym zakresie adresów IP.</span><span class="sxs-lookup"><span data-stu-id="807d0-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="807d0-163">Nazwa rekordu "10" nie jest ostatni oktet adresu IP w zakresie adresów IP, to reprezentowany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="807d0-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="807d0-164">Tworzenie rekordów SRV</span><span class="sxs-lookup"><span data-stu-id="807d0-164">Create an SRV record</span></span>

<span data-ttu-id="807d0-165">Podczas tworzenia [zestawu rekordów SRV](dns-zones-records.md#srv-records), określ  *\_usługi* i  *\_protokołu* w nazwie zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="807d0-166">Nie istnieje potrzeba do uwzględnienia "@" w nazwie zestawu rekordów, podczas tworzenia rekordów SRV zestawu w wierzchołku strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="807d0-167">Utwórz rekord TXT</span><span class="sxs-lookup"><span data-stu-id="807d0-167">Create a TXT record</span></span>

<span data-ttu-id="807d0-168">Poniższy przykład pokazuje, jak utworzyć rekord TXT.</span><span class="sxs-lookup"><span data-stu-id="807d0-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="807d0-169">Aby uzyskać więcej informacji na temat maksymalną długość ciągu obsługiwane w rekordach TXT, zobacz [rekordów TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="807d0-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="807d0-170">Pobierz zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-170">Get a record set</span></span>

<span data-ttu-id="807d0-171">Aby uzyskać dostęp do istniejącego zestawu rekordów, użyj `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="807d0-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="807d0-172">Aby uzyskać pomoc, zobacz `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="807d0-173">Jak podczas tworzenia rekordu lub zestawu rekordów, musi być podana nazwa zestawu rekordów *względną* nazwy, co oznacza należy wykluczyć Nazwa strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="807d0-174">Należy również określić typ rekordu strefy zawierającej zestawu rekordów i grupę zasobów, zawierającą strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="807d0-175">Poniższy przykład pobiera rekordu *www* a typu ze strefy *contoso.com* w grupie zasobów *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="807d0-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="807d0-176">Lista zestawów rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-176">List record sets</span></span>

<span data-ttu-id="807d0-177">Wyświetl listę wszystkich rekordów w strefie DNS przy użyciu `azure network dns record-set list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="807d0-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="807d0-178">Aby uzyskać pomoc, zobacz `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="807d0-179">W tym przykładzie zwraca zestawy wszystkich rekordów w strefie *contoso.com*, w grupie zasobów *MyResourceGroup*, niezależnie od tego, czy nazwa lub typ rekordu:</span><span class="sxs-lookup"><span data-stu-id="807d0-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="807d0-180">W tym przykładzie zwraca wszystkie zestawy rekordów zgodne podanego typu rekordu (w tym przypadku rekordy ""):</span><span class="sxs-lookup"><span data-stu-id="807d0-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="807d0-181">Dodaj rekord do istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-181">Add a record to an existing record set</span></span>

<span data-ttu-id="807d0-182">Można użyć `azure network dns record-set add-record` zarówno tworzenie rekordu w zestawie rekordów lub można dodać rekordu do istniejącego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="807d0-183">Aby uzyskać więcej informacji, zobacz [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.</span><span class="sxs-lookup"><span data-stu-id="807d0-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="807d0-184">Usuń rekord z istniejącego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="807d0-185">Aby usunąć rekord DNS z istniejącego zestawu rekordów, użyj `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="807d0-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="807d0-186">Aby uzyskać pomoc, zobacz `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="807d0-187">To polecenie usuwa rekord DNS z zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="807d0-188">Usunięcie ostatniego rekordu w zestawie rekordów jest samego zestawu rekordów **nie** usunięte.</span><span class="sxs-lookup"><span data-stu-id="807d0-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="807d0-189">Zamiast tego zostanie pozostawiony pusty zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="807d0-190">Aby usunąć rekord, ustaw zamiast tego, zobacz [Usuń zestaw rekordów](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="807d0-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="807d0-191">Należy określić usunięcie rekordu i strefy należy ją usunąć, przy użyciu takich samych parametrach co przy tworzeniu przy użyciu rekordu `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="807d0-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="807d0-192">Te parametry są opisane w [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.</span><span class="sxs-lookup"><span data-stu-id="807d0-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="807d0-193">To polecenie wyświetla monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="807d0-193">This command prompts for confirmation.</span></span> <span data-ttu-id="807d0-194">Ten monit można pomijać przy użyciu `--quiet` przełącznika (forma krótka `-q`).</span><span class="sxs-lookup"><span data-stu-id="807d0-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="807d0-195">Poniższy przykład umożliwia usunięcie rekordu A o wartości "1.2.3.4" z rekordu ustawić nazwane *www* w strefie *contoso.com*, w grupie zasobów *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="807d0-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="807d0-196">Nie jest wyświetlany monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="807d0-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="807d0-197">Modyfikowanie istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-197">Modify an existing record set</span></span>

<span data-ttu-id="807d0-198">Każdy zestaw rekordów zawiera [czas wygaśnięcia (TTL)](dns-zones-records.md#time-to-live), [metadanych](dns-zones-records.md#tags-and-metadata)i rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="807d0-199">W poniższych sekcjach opisano sposób modyfikowania każdej z tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="807d0-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="807d0-200">Aby zmodyfikować rekord A, AAAA, MX, NS, PTR, SRV i TXT</span><span class="sxs-lookup"><span data-stu-id="807d0-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="807d0-201">Aby zmodyfikować istniejący rekord z typu A, AAAA, MX, NS, PTR, SRV i TXT, należy najpierw dodać nowy rekord i następnie usunąć istniejącego rekordu.</span><span class="sxs-lookup"><span data-stu-id="807d0-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="807d0-202">Aby uzyskać szczegółowe instrukcje na temat usunąć i dodać rekordy Zobacz wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="807d0-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="807d0-203">Poniższy przykład przedstawia sposób zmodyfikować rekord "", z adresu IP 1.2.3.4 adres IP 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="807d0-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="807d0-204">Aby zmodyfikować rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="807d0-204">To modify a CNAME record</span></span>

<span data-ttu-id="807d0-205">Aby zmodyfikować rekord zasobu CNAME, użyj `azure network dns record-set add-record` nową wartość rekordu.</span><span class="sxs-lookup"><span data-stu-id="807d0-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="807d0-206">W odróżnieniu od innych typów rekordów zestawu rekordów CNAME może zawierać tylko jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="807d0-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="807d0-207">W związku z tym jest istniejący rekord *zastąpione* po dodaniu nowego rekordu i nie trzeba usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="807d0-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="807d0-208">Pojawi się monit zaakceptować tego zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="807d0-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="807d0-209">Przykład modyfikuje zestawu rekordów CNAME *www* w strefie *contoso.com*, w grupie zasobów *MyResourceGroup*, aby wskazywał "www.fabrikam.net" zamiast jego istniejącej wartości:</span><span class="sxs-lookup"><span data-stu-id="807d0-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="807d0-210">Aby zmodyfikować rekord SOA</span><span class="sxs-lookup"><span data-stu-id="807d0-210">To modify an SOA record</span></span>

<span data-ttu-id="807d0-211">Użyj `azure network dns record-set set-soa-record` do modyfikowania SOA dla danej strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="807d0-212">Aby uzyskać pomoc, zobacz `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="807d0-213">Poniższy przykład przedstawia sposób ustawiania właściwości "e-mail" rekord SOA strefy *contoso.com* w grupie zasobów *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="807d0-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="807d0-214">Aby zmodyfikować rekordy NS w wierzchołku strefy</span><span class="sxs-lookup"><span data-stu-id="807d0-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="807d0-215">Zestaw w wierzchołku strefy rekordów NS jest tworzony automatycznie w każdej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="807d0-216">Zawiera ona nazwy serwerów nazw usługi Azure DNS, które są przypisane do strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="807d0-217">Możesz dodać dodatkowe serwery do tego rekordu NS ustawiona, do obsługi wspólnej hostingu domen z więcej niż jednego dostawcy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="807d0-218">Można również zmodyfikować TTL i metadanych dla tego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="807d0-219">Jednak nie można usunąć ani zmodyfikować wstępnie wypełnione serwerów nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="807d0-220">Należy pamiętać, że dotyczy to tylko zestawu w wierzchołku strefy rekordów NS.</span><span class="sxs-lookup"><span data-stu-id="807d0-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="807d0-221">Innymi zestawami rekordów NS w strefie (tak jak delegowania strefy podrzędnej) można modyfikować bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="807d0-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="807d0-222">Poniższy przykład pokazuje, jak dodać serwer dodatkowe nazwy do zestawu w wierzchołku strefy rekordów NS:</span><span class="sxs-lookup"><span data-stu-id="807d0-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="807d0-223">Aby zmodyfikować TTL z istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="807d0-224">Aby zmodyfikować TTL z istniejącego zestawu rekordów, użyj `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="807d0-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="807d0-225">Aby uzyskać pomoc, zobacz `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="807d0-226">Poniższy przykład przedstawia sposób modyfikowania zestawu rekordów TTL, w tym przypadku do 60 sekund:</span><span class="sxs-lookup"><span data-stu-id="807d0-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="807d0-227">Aby zmodyfikować metadane istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="807d0-228">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) można skojarzyć dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="807d0-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="807d0-229">Aby zmodyfikować metadane istniejącego zestawu rekordów, użyj `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="807d0-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="807d0-230">Aby uzyskać pomoc, zobacz `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="807d0-231">Poniższy przykład przedstawia sposób modyfikowania rekordów dwa wpisy metadanych, "dział = not" i "środowiska produkcji =", za pomocą `--metadata` parametru (krótka wersja `-m`).</span><span class="sxs-lookup"><span data-stu-id="807d0-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="807d0-232">Należy zauważyć, że metadane *zastąpione* przez podane wartości.</span><span class="sxs-lookup"><span data-stu-id="807d0-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="807d0-233">Usuń zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="807d0-233">Delete a record set</span></span>

<span data-ttu-id="807d0-234">Zestawy rekordów można usunąć za pomocą `azure network dns record-set delete` polecenia.</span><span class="sxs-lookup"><span data-stu-id="807d0-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="807d0-235">Aby uzyskać pomoc, zobacz `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="807d0-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="807d0-236">Usunięcie zestawu rekordów spowoduje również usunięcie wszystkich rekordów w zestawie rekordów.</span><span class="sxs-lookup"><span data-stu-id="807d0-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="807d0-237">Nie można usunąć SOA i zestawy rekordów NS w wierzchołku strefy (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="807d0-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="807d0-238">Te są tworzone automatycznie podczas strefy został utworzony i są usuwane automatycznie po usunięciu strefy.</span><span class="sxs-lookup"><span data-stu-id="807d0-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="807d0-239">Poniższy przykład powoduje usunięcie zestawu o nazwie rekordów *www* a typu ze strefy *contoso.com* w grupie zasobów *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="807d0-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="807d0-240">Monit o potwierdzenie operacji usuwania.</span><span class="sxs-lookup"><span data-stu-id="807d0-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="807d0-241">Aby pominąć ten monit, użyj `--quiet` przełącznika (forma krótka `-q`).</span><span class="sxs-lookup"><span data-stu-id="807d0-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="807d0-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="807d0-242">Next steps</span></span>

<span data-ttu-id="807d0-243">Dowiedz się więcej o [strefy i rekordy w usłudze Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="807d0-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="807d0-244">Dowiedz się, jak [ochrony strefy i rekordy](dns-protect-zones-recordsets.md) przy użyciu usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="807d0-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
