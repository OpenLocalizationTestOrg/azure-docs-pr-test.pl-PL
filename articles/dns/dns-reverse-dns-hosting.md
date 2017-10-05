---
title: "Obsługującego Odwróć stref DNS wyszukiwania w usłudze Azure DNS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Azure DNS do obsługi stref wyszukiwania wstecznego wyszukiwania DNS dla zakresy IP"
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="3dcce-103">Hosting stref wyszukiwania wstecznego wyszukiwania DNS w usłudze Azure DNS</span><span class="sxs-lookup"><span data-stu-id="3dcce-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="3dcce-104">W tym artykule wyjaśniono, jak udostępniać stref wyszukiwania wstecznego wyszukiwania DNS dla przypisane zakresy IP w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="3dcce-105">Zakresy IP reprezentowany przez strefy wyszukiwania wstecznego musi być przypisany do organizacji, zazwyczaj przez Usługodawcę internetowego.</span><span class="sxs-lookup"><span data-stu-id="3dcce-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="3dcce-106">Aby skonfigurować wstecznego DNS dla adresu IP należącą do Azure przypisane do usługi Azure, zobacz [skonfigurować wyszukiwanie wsteczne adresy IP przydzielone do usługi Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="3dcce-107">Przed przeczytaniem tego artykułu, należy się zapoznać z tym [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="3dcce-108">W tym artykule przedstawiono kroki, aby utworzyć Twojego pierwszego wyszukiwania wstecznego strefy DNS i rekordów przy użyciu portalu Azure, programu Azure PowerShell, Azure CLI w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcce-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="3dcce-109">Utwórz strefę wyszukiwania wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="3dcce-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="3dcce-110">Zaloguj się do [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="3dcce-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="3dcce-111">W menu centralnym kliknij przycisk, a następnie kliknij przycisk **nowy** > **sieci** >, a następnie kliknij przycisk **strefy DNS** otworzyć **strefy DNS Utwórz** blok.</span><span class="sxs-lookup"><span data-stu-id="3dcce-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Strefa DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="3dcce-113">Na **strefy DNS Utwórz** bloku Nazwa strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="3dcce-114">Nazwa strefy, co jest inaczej dla prefiksy IPv4 i IPv6.</span><span class="sxs-lookup"><span data-stu-id="3dcce-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="3dcce-115">Użyj instrukcji dla [IPV4](#ipv4) lub [IPv6](#ipv6) nazwę strefy.</span><span class="sxs-lookup"><span data-stu-id="3dcce-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="3dcce-116">Po zakończeniu kliknij przycisk **Utwórz** można utworzyć strefy.</span><span class="sxs-lookup"><span data-stu-id="3dcce-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="3dcce-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="3dcce-117">IPv4</span></span>

<span data-ttu-id="3dcce-118">Nazwa strefy wyszukiwania wstecznego IPv4 opiera się na zakres IP, który reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="3dcce-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="3dcce-119">Powinna być w następującym formacie: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="3dcce-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="3dcce-120">Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="3dcce-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="3dcce-121">Podczas tworzenia classless strefy wyszukiwania wstecznego DNS w usłudze Azure DNS, należy użyć łącznika (`-`) zamiast ukośnika ("/") w nazwie strefy.</span><span class="sxs-lookup"><span data-stu-id="3dcce-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="3dcce-122">Na przykład dla 192.0.2.128/26 zakres IP, należy użyć `128-26.2.0.192.in-addr.arpa` jako nazwa strefy zamiast `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="3dcce-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="3dcce-123">Wynika to z faktu, zarówno są obsługiwane w standardach DNS, nazwy zawierające ukośnik strefy DNS (`/`) znaków nie są obsługiwane w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="3dcce-124">Poniższy przykład przedstawia sposób tworzenia strefy DNS wyszukiwania wstecznego "Klasa C" o nazwie `2.0.192.in-addr.arpa` w usłudze Azure DNS za pomocą portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="3dcce-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="3dcce-126">Lokalizacja grupy zasobów określa lokalizację dla grupy zasobów, a nie ma wpływu na strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="3dcce-127">Lokalizacja strefy DNS jest zawsze "global" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="3dcce-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="3dcce-128">Następujące przykłady przedstawiają sposób wykonania tego zadania z programu Azure PowerShell i interfejsu wiersza polecenia Azure:</span><span class="sxs-lookup"><span data-stu-id="3dcce-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="3dcce-130">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="3dcce-131">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="3dcce-132">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="3dcce-132">IPv6</span></span>

<span data-ttu-id="3dcce-133">Nazwa strefy wyszukiwania wstecznego IPv6, powinna być w następującym formacie: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="3dcce-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="3dcce-134">Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="3dcce-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="3dcce-135">Poniższy przykład przedstawia sposób tworzenia IPv6 strefy wyszukiwania wstecznego DNS wyszukiwania o nazwie `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` w usłudze Azure DNS za pomocą portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="3dcce-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="3dcce-137">Lokalizacja grupy zasobów określa lokalizację dla grupy zasobów, a nie ma wpływu na strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="3dcce-138">Lokalizacja strefy DNS jest zawsze "global" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="3dcce-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="3dcce-139">Następujące przykłady przedstawiają sposób wykonania tego zadania z programu Azure PowerShell i interfejsu wiersza polecenia Azure:</span><span class="sxs-lookup"><span data-stu-id="3dcce-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="3dcce-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="3dcce-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="3dcce-143">Delegowanie strefy wyszukiwania wstecznego DNS</span><span class="sxs-lookup"><span data-stu-id="3dcce-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="3dcce-144">Wytworzeniu strefy wyszukiwania wstecznego DNS, należy upewnić się czy strefy delegowane ze strefy nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="3dcce-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="3dcce-145">Delegowanie DNS umożliwia proces rozpoznawania nazw DNS znaleźć serwery nazw hostujące strefy wyszukiwania wstecznego DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="3dcce-146">Dzięki temu te serwery nazw do odpowiedzi DNS zapytań wstecznych dla adresów IP z zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="3dcce-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="3dcce-147">Proces delegowanie strefy DNS dla strefy wyszukiwania do przodu, opisano w [Delegowanie domeny do usługi Azure DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="3dcce-148">Delegowanie dla strefy wyszukiwania wstecznego działa tak samo.</span><span class="sxs-lookup"><span data-stu-id="3dcce-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="3dcce-149">Jedyna różnica polega na tym, że należy skonfigurować serwery nazw z usługodawcą Internetowym, która opracowała zakresowi adresów IP, a nie rejestratora nazw domen.</span><span class="sxs-lookup"><span data-stu-id="3dcce-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="3dcce-150">Tworzenie rekordu PTR systemu DNS</span><span class="sxs-lookup"><span data-stu-id="3dcce-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="3dcce-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="3dcce-151">IPv4</span></span>

<span data-ttu-id="3dcce-152">Poniższy przykład przeprowadzi Cię przez proces tworzenia rekordu PTR w strefy wyszukiwania wstecznego DNS w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="3dcce-153">Aby uzyskać informacje o innych typach rekordów oraz sposobie modyfikowania istniejących rekordów, zobacz [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md) (Zarządzanie rekordami i zestawami rekordów DNS przy użyciu witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="3dcce-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="3dcce-154">W górnej części bloku **Strefa DNS** wybierz pozycję **+ Zestaw rekordów**, aby otworzyć blok **Dodawanie zestawu rekordów**.</span><span class="sxs-lookup"><span data-stu-id="3dcce-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Strefa DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="3dcce-156">Na **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="3dcce-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="3dcce-157">Wybierz **PTR** z rekordu "**typu**" menu.</span><span class="sxs-lookup"><span data-stu-id="3dcce-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="3dcce-158">Nazwa zestawu dla rekordu PTR rekordów należy pozostałą część adresu IPv4 w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3dcce-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="3dcce-159">W tym przykładzie pierwsze trzy oktety są już wypełnione jako część nazwy strefy (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="3dcce-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="3dcce-160">W związku z tym tylko ostatni oktet jest dostarczany w polu Nazwa.</span><span class="sxs-lookup"><span data-stu-id="3dcce-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="3dcce-161">Można na przykład, nazwę zestawu rekordów "**15**" dla zasobu, którego adres IP jest 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="3dcce-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="3dcce-162">W "**nazwy domeny**" Wprowadź w pełni kwalifikowaną nazwę (FQDN) przy użyciu adresu IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="3dcce-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="3dcce-163">Kliknij przycisk **OK** na dole bloku, aby utworzyć rekord DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![Dodaj zestaw rekordów](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="3dcce-165">Poniżej przedstawiono przykłady dotyczące sposobu wykonania tego zadania ze środowiska PowerShell i AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="3dcce-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="3dcce-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="3dcce-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="3dcce-169">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="3dcce-169">IPv6</span></span>

<span data-ttu-id="3dcce-170">Poniższy przykład przeprowadzi Cię przez proces tworzenia nowego rekordu "PTR".</span><span class="sxs-lookup"><span data-stu-id="3dcce-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="3dcce-171">Aby uzyskać informacje o innych typach rekordów oraz sposobie modyfikowania istniejących rekordów, zobacz [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md) (Zarządzanie rekordami i zestawami rekordów DNS przy użyciu witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="3dcce-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="3dcce-172">W górnej części **bloku strefy DNS**, wybierz pozycję **+ zestawu rekordów** otworzyć **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="3dcce-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="3dcce-174">Na **dodać zestaw rekordów** bloku.</span><span class="sxs-lookup"><span data-stu-id="3dcce-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="3dcce-175">Wybierz **PTR** z rekordu "**typu**" menu.</span><span class="sxs-lookup"><span data-stu-id="3dcce-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="3dcce-176">Nazwa zestawu dla rekordu PTR rekordów należy pozostałą część adresu IPv6 w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3dcce-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="3dcce-177">Nie może zawierać zero kompresji.</span><span class="sxs-lookup"><span data-stu-id="3dcce-177">It must not include any zero compression.</span></span> <span data-ttu-id="3dcce-178">W tym przykładzie pierwsze 64-bitowy IPv6 są już wypełnione jako część nazwy strefy (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="3dcce-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="3dcce-179">W związku z tym ostatnie 64 bity są dostarczane w polu Nazwa.</span><span class="sxs-lookup"><span data-stu-id="3dcce-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="3dcce-180">Ostatnie 64 bity adresu IP są wprowadzane w odwrotnej kolejności kropką jako separator każdą liczbę szesnastkową.</span><span class="sxs-lookup"><span data-stu-id="3dcce-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="3dcce-181">Można na przykład, nazwę zestawu rekordów "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" dla zasobu, którego adres IP jest 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="3dcce-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="3dcce-182">W "**nazwy domeny**" Wprowadź w pełni kwalifikowaną nazwę (FQDN) przy użyciu adresu IP zasobu.</span><span class="sxs-lookup"><span data-stu-id="3dcce-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="3dcce-183">Kliknij przycisk **OK** na dole bloku, aby utworzyć rekord DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![Dodawanie bloku zestawu rekordów](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="3dcce-185">Poniżej przedstawiono przykłady dotyczące sposobu wykonania tego zadania ze środowiska PowerShell i AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="3dcce-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="3dcce-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="3dcce-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="3dcce-189">Wyświetlanie rekordów</span><span class="sxs-lookup"><span data-stu-id="3dcce-189">View Records</span></span>

<span data-ttu-id="3dcce-190">Aby wyświetlić utworzone rekordy, przejdź do strefy DNS w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcce-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="3dcce-191">W dolnej części **strefy DNS** bloku widać rekordów dla strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="3dcce-192">Powinny zostać wyświetlone domyślne rekordy NS i SOA tworzone w każdej strefie oraz wszystkie nowo utworzone rekordy.</span><span class="sxs-lookup"><span data-stu-id="3dcce-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="3dcce-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="3dcce-193">IPv4</span></span>

<span data-ttu-id="3dcce-194">Blok strefy DNS, wyświetlanie rekordów IPv4 PTR:</span><span class="sxs-lookup"><span data-stu-id="3dcce-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="3dcce-196">Poniższe przykłady przedstawiają sposób wyświetlania rekordów PTR przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure:</span><span class="sxs-lookup"><span data-stu-id="3dcce-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="3dcce-198">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="3dcce-199">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="3dcce-200">Protokół IPv6</span><span class="sxs-lookup"><span data-stu-id="3dcce-200">IPv6</span></span>

<span data-ttu-id="3dcce-201">Blok strefy DNS, wyświetlanie rekordów IPv6 PTR:</span><span class="sxs-lookup"><span data-stu-id="3dcce-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="3dcce-203">Poniżej przedstawiono przykłady dotyczące wyświetlania rekordów z programu PowerShell i AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="3dcce-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3dcce-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dcce-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="3dcce-205">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="3dcce-206">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3dcce-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="3dcce-207">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3dcce-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="3dcce-208">Stref wyszukiwania wstecznego wyszukiwania DNS może być obsługiwać Moje bloków IP przypisany usługodawcy internetowego w usłudze Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="3dcce-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="3dcce-209">Tak.</span><span class="sxs-lookup"><span data-stu-id="3dcce-209">Yes.</span></span> <span data-ttu-id="3dcce-210">Hosting stref wyszukiwania wstecznego (ARPA) do własnego zakresów IP w usłudze Azure DNS jest w pełni obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="3dcce-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="3dcce-211">Tworzenie strefy wyszukiwania wstecznego w usłudze Azure DNS, jak wyjaśniono w tym artykule, a następnie pracować z usługodawcą Internetowym w celu [delegowanie strefy](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="3dcce-212">Następnie można zarządzać rekordów PTR dla każdego wyszukiwania wstecznego w taki sam sposób jak inne typy rekordów.</span><span class="sxs-lookup"><span data-stu-id="3dcce-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="3dcce-213">Jaka jest hosting moich kosztów strefy wstecznego wyszukiwania DNS?</span><span class="sxs-lookup"><span data-stu-id="3dcce-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="3dcce-214">Hosting strefy wyszukiwania wstecznego wyszukiwania DNS dla sieci bloku IP przypisany usługodawcy internetowego w usłudze Azure DNS jest rozliczana według [standardowe opłaty za usługę Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="3dcce-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="3dcce-215">Czy można udostępniać stref wyszukiwania wstecznego wyszukiwania DNS dla adresów IPv4 i IPv6 w usłudze Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="3dcce-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="3dcce-216">Tak.</span><span class="sxs-lookup"><span data-stu-id="3dcce-216">Yes.</span></span> <span data-ttu-id="3dcce-217">W tym artykule opisano sposób tworzenia protokołów IPv4 i IPv6 stref wyszukiwania wstecznego DNS wyszukiwania w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="3dcce-218">Można zaimportować istniejący strefy wyszukiwania wstecznego DNS?</span><span class="sxs-lookup"><span data-stu-id="3dcce-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="3dcce-219">Tak.</span><span class="sxs-lookup"><span data-stu-id="3dcce-219">Yes.</span></span> <span data-ttu-id="3dcce-220">Interfejsu wiersza polecenia Azure umożliwia importowanie istniejących stref DNS w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3dcce-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="3dcce-221">Działa to zarówno dla strefy wyszukiwania do przodu i strefy wyszukiwania wstecznego.</span><span class="sxs-lookup"><span data-stu-id="3dcce-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="3dcce-222">Aby uzyskać więcej informacji, zobacz [importowanie i eksportowanie pliku strefy DNS przy użyciu interfejsu wiersza polecenia Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dcce-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3dcce-223">Next steps</span></span>

<span data-ttu-id="3dcce-224">Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="3dcce-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="3dcce-225">Dowiedz się, jak [Zarządzanie odwrotnej rekordy DNS dla usług Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="3dcce-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
