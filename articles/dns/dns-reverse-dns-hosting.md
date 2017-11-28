---
title: "aaaHosting reverse DNS strefy wyszukiwania w usłudze Azure DNS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak strefy wyszukiwania DNS dla zakresy IP wstecznego hello toohost usługi Azure DNS toouse"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="51ae5-103">Hosting stref wyszukiwania wstecznego wyszukiwania DNS w usłudze Azure DNS</span><span class="sxs-lookup"><span data-stu-id="51ae5-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="51ae5-104">W tym artykule opisano, jak toohost hello wstecznego strefy wyszukiwania DNS dla przypisanego zakresy IP w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="51ae5-105">zakresy adresów IP Hello reprezentowany przez strefy wyszukiwania wstecznego hello musi być przypisany organizacji tooyour zwykle przez Usługodawcę internetowego.</span><span class="sxs-lookup"><span data-stu-id="51ae5-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="51ae5-106">tooconfigure reverse DNS dla tooyour przypisany adres IP należącą do Azure usługi Azure, zobacz [Konfigurowanie wyszukiwania wstecznego hello hello adresy IP przydzielone tooyour usługi Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="51ae5-107">Przed przeczytaniem tego artykułu, należy się zapoznać z tym [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="51ae5-108">W tym artykule przedstawiono hello kroki toocreate z pierwszą strefę DNS wyszukiwania wstecznego i rejestrowanie przy użyciu hello portalu Azure, programu Azure PowerShell, Azure CLI w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="51ae5-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="51ae5-109">Utwórz strefę wyszukiwania wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="51ae5-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="51ae5-110">Zaloguj się toohello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="51ae5-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="51ae5-111">W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy** > **sieci** >, a następnie kliknij przycisk **strefy DNS** tooopen hello **strefy DNS Utwórz**bloku.</span><span class="sxs-lookup"><span data-stu-id="51ae5-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Strefa DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="51ae5-113">Na powitania **strefy DNS Utwórz** bloku Nazwa strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="51ae5-114">Nazwa Hello strefy hello jest inaczej przystosowana do prefiksy IPv4 i IPv6.</span><span class="sxs-lookup"><span data-stu-id="51ae5-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="51ae5-115">Użyj instrukcji albo hello [IPV4](#ipv4) lub [IPv6](#ipv6) tooname strefy.</span><span class="sxs-lookup"><span data-stu-id="51ae5-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="51ae5-116">Po zakończeniu kliknij przycisk **Utwórz** toocreate hello strefy.</span><span class="sxs-lookup"><span data-stu-id="51ae5-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="51ae5-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="51ae5-117">IPv4</span></span>

<span data-ttu-id="51ae5-118">Nazwa strefy wyszukiwania wstecznego IPv4 Hello opiera się na zakres IP hello, który reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="51ae5-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="51ae5-119">Powinien on być zgodny z formatem hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="51ae5-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="51ae5-120">Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="51ae5-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="51ae5-121">Podczas tworzenia classless strefy wyszukiwania wstecznego DNS w usłudze Azure DNS, należy użyć łącznika (`-`) zamiast ukośnika ("/") w nazwie strefy hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="51ae5-122">Na przykład dla hello 192.0.2.128/26 zakres IP, należy użyć `128-26.2.0.192.in-addr.arpa` jako nazwa strefy hello zamiast `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="51ae5-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="51ae5-123">Wynika to z faktu, zarówno są obsługiwane przez hello standardy usługi DNS, nazwy zawierające ukośnik hello strefy DNS (`/`) znaków nie są obsługiwane w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="51ae5-124">Witaj poniższy przykład przedstawia sposób toocreate C klasy wstecznego strefę DNS o nazwie `2.0.192.in-addr.arpa` w usłudze Azure DNS za pomocą hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="51ae5-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="51ae5-126">Witaj, "Lokalizacja grupy zasobów" definiuje hello lokalizację dla grupy zasobów hello i nie ma wpływu na powitania strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="51ae5-127">Lokalizacja strefy DNS Hello jest zawsze "global" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="51ae5-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="51ae5-128">Witaj następujące przykłady przedstawiają sposób toocomplete to zadanie z programu Azure PowerShell i hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="51ae5-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="51ae5-130">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="51ae5-131">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="51ae5-132">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="51ae5-132">IPv6</span></span>

<span data-ttu-id="51ae5-133">Hello Nazwa strefy wyszukiwania wstecznego IPv6 powinny mieć hello następującej postaci: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="51ae5-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="51ae5-134">Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="51ae5-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="51ae5-135">Witaj poniższy przykład przedstawia sposób toocreate strefy IPv6 wstecznego wyszukiwania DNS o nazwie `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` w usłudze Azure DNS za pomocą hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="51ae5-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="51ae5-137">Witaj, "Lokalizacja grupy zasobów" definiuje hello lokalizację dla grupy zasobów hello i nie ma wpływu na powitania strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="51ae5-138">Lokalizacja strefy DNS Hello jest zawsze "global" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="51ae5-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="51ae5-139">Witaj następujące przykłady przedstawiają sposób toocomplete to zadanie z programu Azure PowerShell i hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="51ae5-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="51ae5-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="51ae5-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="51ae5-143">Delegowanie strefy wyszukiwania wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="51ae5-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="51ae5-144">Wytworzeniu strefy wyszukiwania wstecznego DNS, musisz zapewnić, że tej strefy hello jest delegowane ze strefy nadrzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="51ae5-145">Delegowanie DNS umożliwia hello DNS nazwa rozwiązania procesu toofind hello serwery nazw hostujące strefy wyszukiwania wstecznego DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="51ae5-146">Dzięki temu te nazwy serwerów tooanswer odwrotnej zapytania DNS dotyczące hello adresów IP z zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="51ae5-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="51ae5-147">Proces hello delegowanie strefy DNS dla strefy wyszukiwania do przodu, opisano w [delegować tooAzure Twojego domeny DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="51ae5-148">Delegowanie dla strefy wyszukiwania wstecznego działa hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="51ae5-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="51ae5-149">Jedyną różnicą Hello jest konieczność serwery nazw hello tooconfigure z hello usługodawcy internetowego, która opracowała zakresowi adresów IP, a nie rejestratora nazw domen.</span><span class="sxs-lookup"><span data-stu-id="51ae5-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="51ae5-150">Tworzenie rekordu PTR systemu DNS</span><span class="sxs-lookup"><span data-stu-id="51ae5-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="51ae5-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="51ae5-151">IPv4</span></span>

<span data-ttu-id="51ae5-152">Witaj poniższy przykład przeprowadzi Cię przez proces hello tworzenie rekordu PTR w strefy wyszukiwania wstecznego DNS w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="51ae5-153">Inne typy rekordów i istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="51ae5-154">U góry hello hello **strefy DNS** bloku, wybierz opcję **+ zestawu rekordów** tooopen hello **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="51ae5-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Strefa DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="51ae5-156">Na powitania **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="51ae5-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="51ae5-157">Wybierz **PTR** z rekordu hello "**typu**" menu.</span><span class="sxs-lookup"><span data-stu-id="51ae5-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="51ae5-158">Witaj Nazwa zestawu rekordów hello rekordu PTR musi toobe hello reszty hello adres IPv4 w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="51ae5-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="51ae5-159">W tym przykładzie hello pierwsze trzy oktety są już wypełnione jako część nazwy strefy hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="51ae5-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="51ae5-160">W związku z tym tylko hello ostatni oktet jest dostarczany w polu Nazwa hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="51ae5-161">Można na przykład, nazwę zestawu rekordów "**15**" dla zasobu, którego adres IP jest 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="51ae5-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="51ae5-162">W hello "**nazwy domeny**" Wprowadź hello pełną nazwę domeny (FQDN) przy użyciu protokołu IP hello zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="51ae5-163">Wybierz **OK** u dołu hello hello bloku toocreate hello DNS rekordu.</span><span class="sxs-lookup"><span data-stu-id="51ae5-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![Dodaj zestaw rekordów](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="51ae5-165">Witaj poniżej przedstawiono przykłady dotyczące toocomplete to zadanie z programu PowerShell i hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="51ae5-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="51ae5-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="51ae5-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="51ae5-169">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="51ae5-169">IPv6</span></span>

<span data-ttu-id="51ae5-170">Poniższy przykład Hello przeprowadzi Cię przez proces tworzenia nowego rekordu "PTR" hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="51ae5-171">Inne typy rekordów i istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="51ae5-172">U góry hello hello **bloku strefy DNS**, wybierz pozycję **+ zestawu rekordów** tooopen hello **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="51ae5-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="51ae5-174">Na powitania **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="51ae5-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="51ae5-175">Wybierz **PTR** z rekordu hello "**typu**" menu.</span><span class="sxs-lookup"><span data-stu-id="51ae5-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="51ae5-176">Witaj Nazwa zestawu rekordów hello rekordu PTR musi toobe hello reszty hello adres IPv6 w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="51ae5-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="51ae5-177">Nie może zawierać zero kompresji.</span><span class="sxs-lookup"><span data-stu-id="51ae5-177">It must not include any zero compression.</span></span> <span data-ttu-id="51ae5-178">W tym przykładzie hello pierwszych 64 bitów hello IPv6 są już wypełnione jako część nazwy strefy hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="51ae5-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="51ae5-179">W związku z tym hello ostatnie 64 bity są dostarczane w polu Nazwa hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="51ae5-180">Hello ostatniego 64-bitowy adres IP hello są wprowadzane w odwrotnej kolejności kropką jako ogranicznik hello między każdą liczbę szesnastkową.</span><span class="sxs-lookup"><span data-stu-id="51ae5-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="51ae5-181">Można na przykład, nazwę zestawu rekordów "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" dla zasobu, którego adres IP jest 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="51ae5-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="51ae5-182">W hello "**nazwy domeny**" Wprowadź hello pełną nazwę domeny (FQDN) przy użyciu protokołu IP hello zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="51ae5-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="51ae5-183">Wybierz **OK** u dołu hello hello bloku toocreate hello DNS rekordu.</span><span class="sxs-lookup"><span data-stu-id="51ae5-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![Dodawanie bloku zestawu rekordów](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="51ae5-185">Witaj poniżej przedstawiono przykłady dotyczące toocomplete to zadanie z programu PowerShell i hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="51ae5-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="51ae5-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="51ae5-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="51ae5-189">Wyświetlanie rekordów</span><span class="sxs-lookup"><span data-stu-id="51ae5-189">View Records</span></span>

<span data-ttu-id="51ae5-190">tooview hello rekordy, które zostały utworzone, przejdź tooyour strefę DNS w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="51ae5-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="51ae5-191">W hello obniżyć część hello **strefy DNS** bloku hello rekordów dla strefy DNS hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="51ae5-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="51ae5-192">Powinna zostać wyświetlona hello domyślne NS i SOA rekordy, które są tworzone w każdej strefie, oraz nowych rekordów, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="51ae5-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="51ae5-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="51ae5-193">IPv4</span></span>

<span data-ttu-id="51ae5-194">Blok strefy DNS, wyświetlanie rekordów IPv4 PTR:</span><span class="sxs-lookup"><span data-stu-id="51ae5-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="51ae5-196">Witaj następujące przykłady Pokaż jak tooview hello PTR rekordy przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="51ae5-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="51ae5-198">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="51ae5-199">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="51ae5-200">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="51ae5-200">IPv6</span></span>

<span data-ttu-id="51ae5-201">Blok strefy DNS, wyświetlanie rekordów IPv6 PTR:</span><span class="sxs-lookup"><span data-stu-id="51ae5-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="51ae5-203">Witaj poniżej przedstawiono przykłady jak tooview hello rekordy z programu PowerShell i hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="51ae5-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="51ae5-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51ae5-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="51ae5-205">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="51ae5-206">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="51ae5-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="51ae5-207">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="51ae5-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="51ae5-208">Stref wyszukiwania wstecznego wyszukiwania DNS może być obsługiwać Moje bloków IP przypisany usługodawcy internetowego w usłudze Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="51ae5-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="51ae5-209">Tak.</span><span class="sxs-lookup"><span data-stu-id="51ae5-209">Yes.</span></span> <span data-ttu-id="51ae5-210">Hosting hello stref wyszukiwania wstecznego (ARPA) do własnego zakresów IP w usłudze Azure DNS jest w pełni obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="51ae5-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="51ae5-211">Tworzenie strefy wyszukiwania wstecznego hello w usłudze Azure DNS, jak wyjaśniono w tym artykule, a następnie pracować z Usługodawcą zbyt[delegowanie strefy hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="51ae5-212">Następnie można zarządzać hello rekordów PTR dla każdego wyszukiwania wstecznego w hello sam sposób jak inne typy rekordów.</span><span class="sxs-lookup"><span data-stu-id="51ae5-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="51ae5-213">Jaka jest hosting moich kosztów strefy wstecznego wyszukiwania DNS?</span><span class="sxs-lookup"><span data-stu-id="51ae5-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="51ae5-214">Hosting hello strefy wyszukiwania wstecznego wyszukiwania DNS dla sieci bloku IP przypisany usługodawcy internetowego w usłudze Azure DNS jest rozliczana według [standardowe opłaty za usługę Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="51ae5-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="51ae5-215">Czy można udostępniać stref wyszukiwania wstecznego wyszukiwania DNS dla adresów IPv4 i IPv6 w usłudze Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="51ae5-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="51ae5-216">Tak.</span><span class="sxs-lookup"><span data-stu-id="51ae5-216">Yes.</span></span> <span data-ttu-id="51ae5-217">W tym artykule opisano sposób toocreate protokołów IPv4 i IPv6 reverse DNS strefy wyszukiwania w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="51ae5-218">Można zaimportować istniejący strefy wyszukiwania wstecznego DNS?</span><span class="sxs-lookup"><span data-stu-id="51ae5-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="51ae5-219">Tak.</span><span class="sxs-lookup"><span data-stu-id="51ae5-219">Yes.</span></span> <span data-ttu-id="51ae5-220">Można użyć hello Azure CLI tooimport istniejących stref DNS w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="51ae5-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="51ae5-221">Działa to zarówno dla strefy wyszukiwania do przodu i strefy wyszukiwania wstecznego.</span><span class="sxs-lookup"><span data-stu-id="51ae5-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="51ae5-222">Aby uzyskać więcej informacji, zobacz [importu i eksportu, używając pliku strefy DNS hello Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51ae5-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51ae5-223">Next steps</span></span>

<span data-ttu-id="51ae5-224">Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="51ae5-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="51ae5-225">Dowiedz się, jak za[Zarządzanie odwrotnej rekordy DNS dla usług Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="51ae5-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
