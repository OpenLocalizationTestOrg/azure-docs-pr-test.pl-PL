---
title: "Azure CLI 1.0 hello aaaManage rekordy DNS przy użyciu usługi Azure DNS | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="0cd41-104">Zarządzanie rekordami DNS w usłudze Azure DNS przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="0cd41-104">Manage DNS records in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cd41-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0cd41-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="0cd41-106">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0cd41-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="0cd41-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="0cd41-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="0cd41-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd41-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="0cd41-109">W tym artykule opisano, jak toomanage rekordy DNS dla strefy DNS przy użyciu hello Azure interfejsu wiersza polecenia (CLI), która jest dostępna dla systemu Windows, Mac i Linux między platformami.</span><span class="sxs-lookup"><span data-stu-id="0cd41-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0cd41-110">Można również zarządzać rekordami DNS przy użyciu [programu Azure PowerShell](dns-operations-recordsets.md) lub hello [portalu Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0cd41-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0cd41-111">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0cd41-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="0cd41-112">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0cd41-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0cd41-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0cd41-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="0cd41-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="0cd41-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="0cd41-115">Przykłady Hello w tym artykule założono, że masz już [zainstalowane hello Azure CLI 1.0, zalogowany i utworzyć strefę DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0cd41-115">hello examples in this article assume you have already [installed hello Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0cd41-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0cd41-116">Introduction</span></span>

<span data-ttu-id="0cd41-117">Przed utworzeniem rekordy DNS w usłudze Azure DNS, należy najpierw toounderstand jak usługi Azure DNS organizuje rekordy DNS w zestawach rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="0cd41-118">Aby uzyskać więcej informacji na temat rekordów DNS w usłudze Azure DNS, zobacz [Strefy i rekordy DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0cd41-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="0cd41-119">Tworzenie rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="0cd41-119">Create a DNS record</span></span>

<span data-ttu-id="0cd41-120">toocreate rekord DNS, użyj hello `azure network dns record-set add-record` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cd41-120">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="0cd41-121">Aby uzyskać pomoc, zobacz `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="0cd41-122">Podczas tworzenia rekordu, potrzebna jest nazwa grupy zasobów toospecify hello, nazwę strefy, nazwę, typ rekordu hello i hello szczegółów rekordu hello Trwa tworzenie zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="0cd41-123">Witaj podanej nazwy zestawu rekordów musi być *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy.</span><span class="sxs-lookup"><span data-stu-id="0cd41-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="0cd41-124">Jeśli jeszcze nie istnieje zestaw rekordów hello, to polecenie tworzy go.</span><span class="sxs-lookup"><span data-stu-id="0cd41-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="0cd41-125">Jeśli istnieje już zestaw rekordów hello, to polecenie adda hello rekordem toohello istniejącego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-125">If hello record set already exists, this command adda hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="0cd41-126">Jeśli jest tworzony nowy rekord, używany jest domyślny czas wygaśnięcia wynoszący 3600.</span><span class="sxs-lookup"><span data-stu-id="0cd41-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="0cd41-127">Aby uzyskać instrukcje dotyczące toouse różnych TTLs, zobacz temat [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0cd41-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0cd41-128">Witaj poniższym przykładzie jest tworzony rekord A o nazwie *www* w strefie hello *contoso.com* w grupie zasobów hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0cd41-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0cd41-129">Witaj adres IP hello jest rekord *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="0cd41-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="0cd41-130">toocreate rekord w wierzchołku strefy hello hello (w tym przypadku "contoso.com"), użyj hello Nazwa rekordu "@", wraz ze znakami cudzysłowu hello:</span><span class="sxs-lookup"><span data-stu-id="0cd41-130">toocreate a record in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="0cd41-131">Tworzenie zestawu rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="0cd41-131">Create a DNS record set</span></span>

<span data-ttu-id="0cd41-132">W hello powyżej przykłady, hello rekord DNS została albo dodano tooan istniejącego zestawu rekordów lub utworzono zestaw rekordów hello *niejawnie*.</span><span class="sxs-lookup"><span data-stu-id="0cd41-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="0cd41-133">Można również utworzyć zestaw rekordów hello *jawnie* przed dodaniem rejestruje tooit.</span><span class="sxs-lookup"><span data-stu-id="0cd41-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="0cd41-134">Usługa DNS platformy Azure obsługuje "empty" zestawów rekordów, które mogą działać jako tooreserve symbol zastępczy nazwy DNS przed utworzeniem rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="0cd41-135">Pusty zestawów rekordów są widoczne w hello Azure DNS kontrolować płaszczyzny, ale nie są wyświetlane na serwery hello Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="0cd41-136">Zestawy rekordów są tworzone przy użyciu hello `azure network dns record-set create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cd41-136">Record sets are created using hello `azure network dns record-set create` command.</span></span> <span data-ttu-id="0cd41-137">Aby uzyskać pomoc, zobacz `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="0cd41-138">Tworzenie rekordu hello jawnie ustaw umożliwia toospecify właściwości zestawu rekordów, takie jak hello [czasu wygaśnięcia (TTL, Time-To-Live)](dns-zones-records.md#time-to-live) i metadanych.</span><span class="sxs-lookup"><span data-stu-id="0cd41-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="0cd41-139">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="0cd41-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="0cd41-140">Witaj poniższym przykładzie jest tworzony rekord pusty ustawić TTL 60 sekund, przy użyciu hello `--ttl` parametr (forma krótka `-l`):</span><span class="sxs-lookup"><span data-stu-id="0cd41-140">hello following example creates an empty record set with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="0cd41-141">Hello poniższym przykładzie jest tworzony rekord z dwóch wpisów metadanych, "dział = not" i "środowiska produkcji =", za pomocą hello `--metadata` parametr (krótka wersja `-m`):</span><span class="sxs-lookup"><span data-stu-id="0cd41-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="0cd41-142">Posiadanie utworzony pusty zestaw rekordów, można dodawać rekordy przy użyciu `azure network dns record-set add-record` zgodnie z opisem w [Utwórz rekord DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="0cd41-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="0cd41-143">Tworzenie rekordów innych typów</span><span class="sxs-lookup"><span data-stu-id="0cd41-143">Create records of other types</span></span>

<span data-ttu-id="0cd41-144">Posiadanie widoczne szczegółowo jak rekordy toocreate "A", hello następujących przykładach pokazano, jak rekord toocreate innych typów rekordów obsługiwane przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="0cd41-145">Parametry Hello używane toospecify hello rekordu danych różnią się w zależności od typu hello hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="0cd41-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="0cd41-146">Na przykład dla rekordów typu "A", należy określić adres hello IPv4 z parametrem hello `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="0cd41-147">Witaj parametry dla poszczególnych typów rekordów mogą być wyświetlane przy użyciu `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-147">hello parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="0cd41-148">W każdym przypadku zostanie przedstawiony sposób toocreate pojedynczego rekordu.</span><span class="sxs-lookup"><span data-stu-id="0cd41-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="0cd41-149">rekord Hello jest dodany toohello istniejącego zestawu rekordów lub zestawu rekordów utworzone niejawnie.</span><span class="sxs-lookup"><span data-stu-id="0cd41-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="0cd41-150">Aby uzyskać więcej informacji na temat tworzenia zestawów rekordów i rekordu definiujący parametr jawnie, zobacz [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0cd41-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0cd41-151">Firma Microsoft nie dają toocreate przykład zestawu rekordów SOA, ponieważ SOAs są tworzone i usunąć z każdej strefy DNS i nie można utworzyć ani usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="0cd41-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="0cd41-152">Jednak [hello SOA można modyfikować, jak pokazano w przykładzie nowsze](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="0cd41-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="0cd41-153">Utwórz rekord AAAA</span><span class="sxs-lookup"><span data-stu-id="0cd41-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="0cd41-154">Utwórz rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="0cd41-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="0cd41-155">Standardy usługi DNS Hello nie zezwalają na rekordy CNAME w wierzchołku hello strefy (`-Name "@"`), ani akceptują zestawów rekordów zawierających więcej niż jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="0cd41-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="0cd41-156">Aby uzyskać więcej informacji, zobacz [rekordy CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="0cd41-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="0cd41-157">Utwórz rekord MX</span><span class="sxs-lookup"><span data-stu-id="0cd41-157">Create an MX record</span></span>

<span data-ttu-id="0cd41-158">W tym przykładzie używamy nazwy zestawu rekordów hello "@" hello toocreate rekord MX w wierzchołku strefy hello (w tym przypadku "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="0cd41-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="0cd41-159">Tworzenie rekordów NS</span><span class="sxs-lookup"><span data-stu-id="0cd41-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="0cd41-160">Utwórz rekord PTR</span><span class="sxs-lookup"><span data-stu-id="0cd41-160">Create a PTR record</span></span>

<span data-ttu-id="0cd41-161">W takim przypadku "Mój-arpa-zone.com" reprezentuje hello strefy ARPA reprezentujący zakresowi adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0cd41-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="0cd41-162">Każdy rekord PTR ustawione w tej strefie odpowiada tooan adres IP zakresu tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0cd41-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="0cd41-163">Nazwa rekordu Hello "10" jest Witaj oktet ostatniego adresu IP hello tego zakresu IP reprezentowany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="0cd41-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="0cd41-164">Tworzenie rekordów SRV</span><span class="sxs-lookup"><span data-stu-id="0cd41-164">Create an SRV record</span></span>

<span data-ttu-id="0cd41-165">Podczas tworzenia [zestawu rekordów SRV](dns-zones-records.md#srv-records), określ hello  *\_usługi* i  *\_protokołu* w hello nazwy zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="0cd41-166">Nie istnieje żadne tooinclude potrzeby "@" w hello nazwy zestawu rekordów podczas tworzenia rekordów SRV zestawu w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="0cd41-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="0cd41-167">Utwórz rekord TXT</span><span class="sxs-lookup"><span data-stu-id="0cd41-167">Create a TXT record</span></span>

<span data-ttu-id="0cd41-168">Witaj poniższy przykład przedstawia sposób rejestrowania toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="0cd41-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="0cd41-169">Aby uzyskać więcej informacji na temat hello maksymalna długość ciągu obsługiwane w rekordach TXT, zobacz [rekordów TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="0cd41-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="0cd41-170">Pobierz zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-170">Get a record set</span></span>

<span data-ttu-id="0cd41-171">Użyj istniejącego zestawu rekordów, tooretrieve `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-171">tooretrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="0cd41-172">Aby uzyskać pomoc, zobacz `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="0cd41-173">Podczas tworzenia rekordu lub zestawu rekordów, rekord hello określić nazwy musi być *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy.</span><span class="sxs-lookup"><span data-stu-id="0cd41-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="0cd41-174">Należy również typ rekordu hello toospecify, hello strefie zawierającej rekord hello ustawić i hello grupę zasobów, zawierającą hello strefy.</span><span class="sxs-lookup"><span data-stu-id="0cd41-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="0cd41-175">Witaj poniższy przykład pobiera rekordu hello *www* a typu ze strefy *contoso.com* w grupie zasobów *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0cd41-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="0cd41-176">Lista zestawów rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-176">List record sets</span></span>

<span data-ttu-id="0cd41-177">Wyświetl listę wszystkich rekordów w strefie DNS przy użyciu hello `azure network dns record-set list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cd41-177">You can list all records in a DNS zone by using hello `azure network dns record-set list` command.</span></span> <span data-ttu-id="0cd41-178">Aby uzyskać pomoc, zobacz `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="0cd41-179">W tym przykładzie zwraca zestawy wszystkich rekordów w strefie hello *contoso.com*, w grupie zasobów *MyResourceGroup*, niezależnie od tego, czy nazwa lub typ rekordu:</span><span class="sxs-lookup"><span data-stu-id="0cd41-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="0cd41-180">W tym przykładzie zwraca wszystkie zestawy rekordów zgodne hello danego typu rekordu (w tym przypadku rekordy ""):</span><span class="sxs-lookup"><span data-stu-id="0cd41-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="0cd41-181">Dodawanie rekordów tooan istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="0cd41-182">Można użyć `azure network dns record-set add-record` zarówno zestaw rekordów w nowym rekordzie toocreate lub zestaw rekordów istniejącego rekordu tooan tooadd.</span><span class="sxs-lookup"><span data-stu-id="0cd41-182">You can use `azure network dns record-set add-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="0cd41-183">Aby uzyskać więcej informacji, zobacz [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.</span><span class="sxs-lookup"><span data-stu-id="0cd41-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="0cd41-184">Usuń rekord z istniejącego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="0cd41-185">tooremove DNS rekordów z istniejącego zestawu rekordów, użyj `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-185">tooremove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="0cd41-186">Aby uzyskać pomoc, zobacz `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="0cd41-187">To polecenie usuwa rekord DNS z zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="0cd41-188">Usunięcie ostatniego rekordu hello w zestawie rekordów jest samego zestawu rekordów hello **nie** usunięte.</span><span class="sxs-lookup"><span data-stu-id="0cd41-188">If hello last record in a record set is deleted, hello record set itself is **not** deleted.</span></span> <span data-ttu-id="0cd41-189">Zamiast tego zostanie pozostawiony pusty zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="0cd41-190">rekord hello toodelete Ustaw zamiast tego zobacz [Usuń zestaw rekordów](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="0cd41-190">toodelete hello record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="0cd41-191">Należy toospecify hello toobe rekordów usunięte i hello strefy należy ją usunąć, używając hello takich samych parametrach co podczas tworzenia rekordów przy użyciu `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-191">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="0cd41-192">Te parametry są opisane w [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.</span><span class="sxs-lookup"><span data-stu-id="0cd41-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="0cd41-193">To polecenie wyświetla monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="0cd41-193">This command prompts for confirmation.</span></span> <span data-ttu-id="0cd41-194">Ten monit można pomijać przy użyciu hello `--quiet` przełącznika (forma krótka `-q`).</span><span class="sxs-lookup"><span data-stu-id="0cd41-194">This prompt can be suppressed using hello `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="0cd41-195">powitania po usuwaniu przykład Witaj rekord z wartością "1.2.3.4" z rekordu hello ustawić nazwane *www* w strefie hello *contoso.com*, w grupie zasobów hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0cd41-195">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0cd41-196">monit o potwierdzenie Hello jest pomijane.</span><span class="sxs-lookup"><span data-stu-id="0cd41-196">hello confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="0cd41-197">Modyfikowanie istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-197">Modify an existing record set</span></span>

<span data-ttu-id="0cd41-198">Każdy zestaw rekordów zawiera [czas wygaśnięcia (TTL)](dns-zones-records.md#time-to-live), [metadanych](dns-zones-records.md#tags-and-metadata)i rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="0cd41-199">Witaj poniższe sekcje zawierają opis sposobu toomodify tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="0cd41-199">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="0cd41-200">toomodify rekord A, AAAA, MX, NS, PTR, SRV i TXT</span><span class="sxs-lookup"><span data-stu-id="0cd41-200">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="0cd41-201">toomodify istniejący rekord z typu A, AAAA, MX, NS, PTR, SRV i TXT, należy najpierw dodać nowego rekordu, a następnie usuń hello istniejącego rekordu.</span><span class="sxs-lookup"><span data-stu-id="0cd41-201">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="0cd41-202">Aby uzyskać szczegółowe informacje na temat toodelete i dodać rekordy, zobacz hello wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="0cd41-202">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="0cd41-203">Witaj poniższy przykład pokazuje, jak toomodify rekord "A", z tooIP 1.2.3.4 adres IP adresów 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="0cd41-203">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="0cd41-204">toomodify rekord CNAME</span><span class="sxs-lookup"><span data-stu-id="0cd41-204">toomodify a CNAME record</span></span>

<span data-ttu-id="0cd41-205">Użyj toomodify rekord CNAME `azure network dns record-set add-record` tooadd hello nową wartość rekordu.</span><span class="sxs-lookup"><span data-stu-id="0cd41-205">toomodify a CNAME record, use `azure network dns record-set add-record` tooadd hello new record value.</span></span> <span data-ttu-id="0cd41-206">W odróżnieniu od innych typów rekordów zestawu rekordów CNAME może zawierać tylko jeden rekord.</span><span class="sxs-lookup"><span data-stu-id="0cd41-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="0cd41-207">W związku z tym jest hello istniejącego rekordu *zastąpione* po hello nowy rekord został dodany i nie wymaga toobe usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="0cd41-207">Therefore, hello existing record is *replaced* when hello new record is added, and does not need toobe deleted separately.</span></span>  <span data-ttu-id="0cd41-208">Użytkownik będzie zostanie wyświetlony monit o tooaccept tego zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="0cd41-208">You will be prompted tooaccept this replacement.</span></span>

<span data-ttu-id="0cd41-209">Witaj przykład modyfikuje zestawu rekordów CNAME hello *www* w strefie hello *contoso.com*, w grupie zasobów *MyResourceGroup*, toopoint za "www.fabrikam.net" zamiast jego Istniejąca wartość:</span><span class="sxs-lookup"><span data-stu-id="0cd41-209">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="0cd41-210">toomodify rekord SOA</span><span class="sxs-lookup"><span data-stu-id="0cd41-210">toomodify an SOA record</span></span>

<span data-ttu-id="0cd41-211">Użyj `azure network dns record-set set-soa-record` toomodify hello SOA dla danej strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-211">Use `azure network dns record-set set-soa-record` toomodify hello SOA for a given DNS zone.</span></span> <span data-ttu-id="0cd41-212">Aby uzyskać pomoc, zobacz `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="0cd41-213">Witaj poniższy przykład przedstawia sposób rejestrowania właściwość tooset hello "e-mail" hello SOA strefy hello *contoso.com* w grupie zasobów hello *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0cd41-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="0cd41-214">toomodify NS rekordów w wierzchołku strefy hello</span><span class="sxs-lookup"><span data-stu-id="0cd41-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="0cd41-215">zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="0cd41-216">Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.</span><span class="sxs-lookup"><span data-stu-id="0cd41-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="0cd41-217">Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="0cd41-218">Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="0cd41-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="0cd41-219">Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="0cd41-220">Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="0cd41-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="0cd41-221">Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="0cd41-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="0cd41-222">Witaj poniższy przykład przedstawia tooadd rekordów NS toohello dodatkowe nazwy serwera konfiguracji na wierzchołku strefy hello:</span><span class="sxs-lookup"><span data-stu-id="0cd41-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="0cd41-223">Ustaw hello toomodify TTL istniejącego rekordu</span><span class="sxs-lookup"><span data-stu-id="0cd41-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="0cd41-224">Ustaw hello toomodify TTL istniejącego rekordu, użyj `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-224">toomodify hello TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="0cd41-225">Aby uzyskać pomoc, zobacz `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="0cd41-226">Witaj poniższy przykład pokazuje, jak toomodify zestawu rekordów TTL, w tym przypadku too60 sekund:</span><span class="sxs-lookup"><span data-stu-id="0cd41-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="0cd41-227">metadane hello toomodify istniejącego zestawu rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="0cd41-228">[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="0cd41-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="0cd41-229">Ustaw toomodify hello metadane istniejącego rekordu, użyj `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-229">toomodify hello metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="0cd41-230">Aby uzyskać pomoc, zobacz `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="0cd41-231">Hello poniższy przykład przedstawia sposób toomodify, zestaw rekordów, o dwa wpisy metadanych, "dział = not" i "środowiska produkcji =", przy użyciu hello `--metadata` parametr (krótka wersja `-m`).</span><span class="sxs-lookup"><span data-stu-id="0cd41-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="0cd41-232">Należy zauważyć, że metadane *zastąpione* przez wartości hello podane.</span><span class="sxs-lookup"><span data-stu-id="0cd41-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="0cd41-233">Usuń zestaw rekordów</span><span class="sxs-lookup"><span data-stu-id="0cd41-233">Delete a record set</span></span>

<span data-ttu-id="0cd41-234">Zestawy rekordów można usunąć za pomocą hello `azure network dns record-set delete` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cd41-234">Record sets can be deleted by using hello `azure network dns record-set delete` command.</span></span> <span data-ttu-id="0cd41-235">Aby uzyskać pomoc, zobacz `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="0cd41-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="0cd41-236">Usunięcie zestawu rekordów spowoduje również usunięcie wszystkich rekordów w zestawie rekordów hello.</span><span class="sxs-lookup"><span data-stu-id="0cd41-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd41-237">Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="0cd41-237">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="0cd41-238">Te są tworzone automatycznie podczas hello strefy został utworzony i są usuwane automatycznie po usunięciu hello strefy.</span><span class="sxs-lookup"><span data-stu-id="0cd41-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="0cd41-239">Witaj poniższy przykład powoduje usunięcie zestawu o nazwie rekordów hello *www* a typu ze strefy hello *contoso.com* w grupie zasobów *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0cd41-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="0cd41-240">Jesteś operację usuwania hello zostanie wyświetlony monit o tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0cd41-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="0cd41-241">toosuppress ten monit, użyj hello `--quiet` przełącznika (forma krótka `-q`).</span><span class="sxs-lookup"><span data-stu-id="0cd41-241">toosuppress this prompt, use hello `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cd41-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0cd41-242">Next steps</span></span>

<span data-ttu-id="0cd41-243">Dowiedz się więcej o [strefy i rekordy w usłudze Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0cd41-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="0cd41-244">Dowiedz się, jak za[ochrony strefy i rekordy](dns-protect-zones-recordsets.md) przy użyciu usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0cd41-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
