---
title: "Delegowanie domeny do usługi Azure DNS | Microsoft Docs"
description: "Dowiedz się, jak zmienić delegowanie domeny i korzystać z serwerów nazw usługi Azure DNS do zapewniania hostingu domeny."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="7aedc-103">Delegowanie domeny do usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="7aedc-104">Usługa Azure DNS umożliwia hostowanie strefy DNS i zarządzanie rekordami DNS dla domeny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7aedc-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="7aedc-105">Aby zapytania DNS dla domeny miały dostęp do usługi Azure DNS, należy delegować domenę do usługi Azure DNS z domeny nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="7aedc-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="7aedc-106">Należy pamiętać, że usługa Azure DNS nie jest rejestratorem domen.</span><span class="sxs-lookup"><span data-stu-id="7aedc-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="7aedc-107">W tym artykule wyjaśniono, jak delegować domenę do usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="7aedc-108">W przypadku domen zakupionych u rejestratora domen rejestrator zaoferuje opcję skonfigurowania tych rekordów NS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="7aedc-109">Nie musisz być właścicielem domeny, aby utworzyć strefę DNS z tą nazwą domeny w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="7aedc-110">Musisz być jednak właścicielem domeny, aby skonfigurować delegowanie do usługi Azure DNS u rejestratora.</span><span class="sxs-lookup"><span data-stu-id="7aedc-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="7aedc-111">Załóżmy na przykład, że masz zakupioną domenę „contoso.net” i tworzysz strefę o nazwie „contoso.net” w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="7aedc-112">Jako właścicielowi domeny rejestrator oferuje Ci opcję skonfigurowania adresów serwerów nazw (czyli rekordów NS) dla domeny.</span><span class="sxs-lookup"><span data-stu-id="7aedc-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="7aedc-113">Rejestrator przechowuje te rekordy NS w domenie nadrzędnej (w tym przypadku „.net”).</span><span class="sxs-lookup"><span data-stu-id="7aedc-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="7aedc-114">Klienci na całym świecie mogą być kierowani do Twojej domeny w strefie usługi Azure DNS podczas próby rozpoznania rekordów DNS w strefie „contoso.net”.</span><span class="sxs-lookup"><span data-stu-id="7aedc-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="7aedc-115">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-115">Create a DNS zone</span></span>

1. <span data-ttu-id="7aedc-116">Logowanie się do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7aedc-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="7aedc-117">W menu Centrum kliknij pozycję **Nowa > Sieć >** , a następnie kliknij pozycję **Strefa DNS**, aby otworzyć blok Tworzenie strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="7aedc-119">W bloku **Tworzenie strefy DNS** wprowadź następujące wartości, a następnie kliknij pozycję **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="7aedc-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="7aedc-120">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="7aedc-120">**Setting**</span></span> | <span data-ttu-id="7aedc-121">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="7aedc-121">**Value**</span></span> | <span data-ttu-id="7aedc-122">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="7aedc-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7aedc-123">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="7aedc-123">**Name**</span></span>|<span data-ttu-id="7aedc-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="7aedc-124">contoso.net</span></span>|<span data-ttu-id="7aedc-125">Nazwa strefy DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="7aedc-126">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="7aedc-126">**Subscription**</span></span>|<span data-ttu-id="7aedc-127">[Twoja subskrypcja]</span><span class="sxs-lookup"><span data-stu-id="7aedc-127">[Your subscription]</span></span>|<span data-ttu-id="7aedc-128">Wybierz subskrypcję, w której chcesz utworzyć bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7aedc-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="7aedc-129">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="7aedc-129">**Resource group**</span></span>|<span data-ttu-id="7aedc-130">**Utwórz nową:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="7aedc-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="7aedc-131">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7aedc-131">Create a resource group.</span></span> <span data-ttu-id="7aedc-132">Nazwa grupy zasobów musi być unikatowa w obrębie wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7aedc-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="7aedc-133">Aby dowiedzieć się więcej na temat grup zasobów, zapoznaj się z artykułem [Omówienie usługi Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7aedc-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7aedc-134">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="7aedc-134">**Location**</span></span>|<span data-ttu-id="7aedc-135">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="7aedc-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7aedc-136">Ustawienie Grupa zasobów dotyczy lokalizacji grupy zasobów i nie ma wpływu na strefę DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="7aedc-137">Lokalizacja strefy DNS jest zawsze „globalna” i nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="7aedc-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="7aedc-138">Pobieranie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="7aedc-138">Retrieve name servers</span></span>

<span data-ttu-id="7aedc-139">Aby móc delegować swoją strefę DNS do usługi Azure DNS, musisz najpierw znać nazwy serwerów nazw dla swojej strefy.</span><span class="sxs-lookup"><span data-stu-id="7aedc-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="7aedc-140">Usługa Azure DNS przydziela serwery nazw z puli za każdym razem, gdy tworzona jest strefa.</span><span class="sxs-lookup"><span data-stu-id="7aedc-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="7aedc-141">Gdy utworzysz strefę DNS, w okienku **Ulubione** witryny Azure Portal kliknij pozycję **Wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7aedc-142">W bloku **Wszystkie zasoby** kliknij strefę DNS **contoso.net**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="7aedc-143">Jeśli wybrana subskrypcja zawiera kilka zasobów, możesz wpisać **contoso.net** w polu Filtruj według nazwy...,</span><span class="sxs-lookup"><span data-stu-id="7aedc-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="7aedc-144">aby łatwo uzyskać dostęp do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7aedc-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="7aedc-145">W bloku Strefa DNS pobierz serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="7aedc-146">W tym przykładzie strefie „contoso.net” przypisano serwery nazw „ns1-01.azure-dns.com”, „ns2-01.azure-dns.net”, „ns3-01.azure-dns.org” i „ns4-01.azure-dns.info”:</span><span class="sxs-lookup"><span data-stu-id="7aedc-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="7aedc-148">Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="7aedc-149">Aby wyświetlić nazwy serwerów nazw za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure, musisz po prostu pobrać te rekordy.</span><span class="sxs-lookup"><span data-stu-id="7aedc-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="7aedc-150">W poniższych przykładach udostępniono również instrukcje pobierania serwerów nazw dla strefy w usłudze Azure DNS przy użyciu programu PowerShell i interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7aedc-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="7aedc-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7aedc-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="7aedc-152">Odpowiedzią jest poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7aedc-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="7aedc-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7aedc-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="7aedc-154">Odpowiedzią jest poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7aedc-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="7aedc-155">Delegowanie domeny</span><span class="sxs-lookup"><span data-stu-id="7aedc-155">Delegate the domain</span></span>

<span data-ttu-id="7aedc-156">Po utworzeniu strefy DNS i pobraniu serwerów nazw domena nadrzędna powinna zostać zaktualizowana przy użyciu informacji o serwerach nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="7aedc-157">Każdy rejestrator ma swoje własne narzędzia do zarządzania systemem DNS służące do zmiany rekordów serwerów nazw dla domeny.</span><span class="sxs-lookup"><span data-stu-id="7aedc-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="7aedc-158">Na stronie zarządzania systemem DNS rejestratora edytuj rekordy NS i zastąp je rekordami utworzonymi przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="7aedc-159">Podczas delegowania domeny do usługi Azure DNS należy użyć nazw serwerów nazw udostępnionych przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="7aedc-160">Zaleca się używanie wszystkich czterech nazw serwerów nazw, niezależnie od nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="7aedc-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="7aedc-161">Delegowanie domeny nie wymaga, aby nazwa serwera nazw korzystała z tej samej domeny najwyższego poziomu, co domena użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7aedc-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="7aedc-162">Nie należy używać rekordów sklejki do wskazywania adresów IP serwerów nazw usługi Azure DNS, ponieważ te adresy IP mogą ulec zmianie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="7aedc-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="7aedc-163">Delegowanie z wykorzystaniem nazw serwerów nazw we własnej strefie, niekiedy nazywanych „serwerami nazw znaczących”, nie jest obecnie obsługiwane w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="7aedc-164">Sprawdzanie prawidłowego rozpoznawania nazw</span><span class="sxs-lookup"><span data-stu-id="7aedc-164">Verify name resolution is working</span></span>

<span data-ttu-id="7aedc-165">Po zakończeniu delegowania możesz sprawdzić, czy rozpoznawanie nazw działa, uruchamiając zapytanie o rekord SOA dla swojej strefy (który również jest tworzony automatycznie podczas tworzenia strefy) za pomocą narzędzia takiego jak „nslookup”.</span><span class="sxs-lookup"><span data-stu-id="7aedc-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="7aedc-166">Nie musisz określać serwerów nazw usługi Azure DNS, jeśli delegowanie zostało skonfigurowane prawidłowo, ponieważ normalny proces rozpoznawania nazw DNS znajdzie serwery nazw automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7aedc-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="7aedc-167">Poniżej zamieszczono przykładową odpowiedź na poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="7aedc-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="7aedc-168">Delegowanie domen podrzędnych w usłudze Azure DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="7aedc-169">Jeśli chcesz skonfigurować oddzielną strefę podrzędną, możesz delegować domenę podrzędną w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="7aedc-170">Załóżmy na przykład, że po skonfigurowaniu i delegowaniu domeny „contoso.net” w usłudze Azure DNS chcesz skonfigurować oddzielną strefę podrzędną „partners.contoso.net”.</span><span class="sxs-lookup"><span data-stu-id="7aedc-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="7aedc-171">Utwórz strefę podrzędną „partners.contoso.net” w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="7aedc-172">Wyszukaj autorytatywne rekordy NS w strefie podrzędnej, aby uzyskać serwery nazw hostujące strefę podrzędną w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="7aedc-173">Deleguj strefę podrzędną przez skonfigurowanie rekordów NS w strefie nadrzędnej wskazującej strefę podrzędną.</span><span class="sxs-lookup"><span data-stu-id="7aedc-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="7aedc-174">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-174">Create a DNS zone</span></span>

1. <span data-ttu-id="7aedc-175">Logowanie się do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7aedc-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="7aedc-176">W menu Centrum kliknij pozycję **Nowa > Sieć >** , a następnie kliknij pozycję **Strefa DNS**, aby otworzyć blok Tworzenie strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="7aedc-178">W bloku **Tworzenie strefy DNS** wprowadź następujące wartości, a następnie kliknij pozycję **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="7aedc-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="7aedc-179">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="7aedc-179">**Setting**</span></span> | <span data-ttu-id="7aedc-180">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="7aedc-180">**Value**</span></span> | <span data-ttu-id="7aedc-181">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="7aedc-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7aedc-182">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="7aedc-182">**Name**</span></span>|<span data-ttu-id="7aedc-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="7aedc-183">partners.contoso.net</span></span>|<span data-ttu-id="7aedc-184">Nazwa strefy DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="7aedc-185">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="7aedc-185">**Subscription**</span></span>|<span data-ttu-id="7aedc-186">[Twoja subskrypcja]</span><span class="sxs-lookup"><span data-stu-id="7aedc-186">[Your subscription]</span></span>|<span data-ttu-id="7aedc-187">Wybierz subskrypcję, w której chcesz utworzyć bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7aedc-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="7aedc-188">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="7aedc-188">**Resource group**</span></span>|<span data-ttu-id="7aedc-189">**Użyj istniejącej:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="7aedc-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="7aedc-190">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7aedc-190">Create a resource group.</span></span> <span data-ttu-id="7aedc-191">Nazwa grupy zasobów musi być unikatowa w obrębie wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7aedc-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="7aedc-192">Aby dowiedzieć się więcej na temat grup zasobów, zapoznaj się z artykułem [Omówienie usługi Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7aedc-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7aedc-193">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="7aedc-193">**Location**</span></span>|<span data-ttu-id="7aedc-194">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="7aedc-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7aedc-195">Ustawienie Grupa zasobów dotyczy lokalizacji grupy zasobów i nie ma wpływu na strefę DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="7aedc-196">Lokalizacja strefy DNS jest zawsze „globalna” i nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="7aedc-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="7aedc-197">Pobieranie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="7aedc-197">Retrieve name servers</span></span>

1. <span data-ttu-id="7aedc-198">Gdy utworzysz strefę DNS, w okienku **Ulubione** witryny Azure Portal kliknij pozycję **Wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7aedc-199">W bloku **Wszystkie zasoby** kliknij strefę DNS **partners.contoso.net**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="7aedc-200">Jeśli wybrana subskrypcja zawiera kilka zasobów, możesz wpisać **partners.contoso.net** w polu Filtruj według nazwy...,</span><span class="sxs-lookup"><span data-stu-id="7aedc-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="7aedc-201">aby łatwo uzyskać dostęp do strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="7aedc-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="7aedc-202">W bloku Strefa DNS pobierz serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="7aedc-203">W tym przykładzie strefie „contoso.net” przypisano serwery nazw „ns1-01.azure-dns.com”, „ns2-01.azure-dns.net”, „ns3-01.azure-dns.org” i „ns4-01.azure-dns.info”:</span><span class="sxs-lookup"><span data-stu-id="7aedc-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="7aedc-205">Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="7aedc-206">Aby wyświetlić nazwy serwerów nazw za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure, musisz po prostu pobrać te rekordy.</span><span class="sxs-lookup"><span data-stu-id="7aedc-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="7aedc-207">Tworzenie rekordu serwera nazw w strefie nadrzędnej</span><span class="sxs-lookup"><span data-stu-id="7aedc-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="7aedc-208">W witrynie Azure Portal przejdź do strefy DNS **contoso.net**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="7aedc-209">Kliknij pozycję **+ Zestaw rekordów**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="7aedc-210">W bloku **Dodaj zestaw rekordów** wprowadź następujące wartości, a następnie kliknij przycisk **OK**:</span><span class="sxs-lookup"><span data-stu-id="7aedc-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="7aedc-211">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="7aedc-211">**Setting**</span></span> | <span data-ttu-id="7aedc-212">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="7aedc-212">**Value**</span></span> | <span data-ttu-id="7aedc-213">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="7aedc-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7aedc-214">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="7aedc-214">**Name**</span></span>|<span data-ttu-id="7aedc-215">partners</span><span class="sxs-lookup"><span data-stu-id="7aedc-215">partners</span></span>|<span data-ttu-id="7aedc-216">Nazwa podrzędnej strefy DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="7aedc-217">**Typ**</span><span class="sxs-lookup"><span data-stu-id="7aedc-217">**Type**</span></span>|<span data-ttu-id="7aedc-218">NS</span><span class="sxs-lookup"><span data-stu-id="7aedc-218">NS</span></span>|<span data-ttu-id="7aedc-219">Użyj wartości NS w przypadku rekordów serwera nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="7aedc-220">**Czas wygaśnięcia**</span><span class="sxs-lookup"><span data-stu-id="7aedc-220">**TTL**</span></span>|<span data-ttu-id="7aedc-221">1</span><span class="sxs-lookup"><span data-stu-id="7aedc-221">1</span></span>|<span data-ttu-id="7aedc-222">Czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="7aedc-222">Time to live.</span></span>|
   |<span data-ttu-id="7aedc-223">**Jednostka czasu wygaśnięcia**</span><span class="sxs-lookup"><span data-stu-id="7aedc-223">**TTL unit**</span></span>|<span data-ttu-id="7aedc-224">Godziny</span><span class="sxs-lookup"><span data-stu-id="7aedc-224">Hours</span></span>|<span data-ttu-id="7aedc-225">Ustawia jednostkę czasu wygaśnięcia na godziny</span><span class="sxs-lookup"><span data-stu-id="7aedc-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="7aedc-226">**SERWER NAZW**</span><span class="sxs-lookup"><span data-stu-id="7aedc-226">**NAME SERVER**</span></span>|<span data-ttu-id="7aedc-227">{serwery nazw ze strefy partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="7aedc-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="7aedc-228">Wprowadź wszystkie 4 serwery nazw ze strefy partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="7aedc-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="7aedc-230">Delegowanie domen podrzędnych w usłudze Azure DNS za pomocą innych narzędzi</span><span class="sxs-lookup"><span data-stu-id="7aedc-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="7aedc-231">Poniższe przykłady zawierają instrukcje delegowania domen podrzędnych w usłudze Azure DNS przy użyciu programu PowerShell i interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7aedc-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="7aedc-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7aedc-232">PowerShell</span></span>

<span data-ttu-id="7aedc-233">W poniższym przykładzie programu PowerShell pokazano, jak to działa.</span><span class="sxs-lookup"><span data-stu-id="7aedc-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="7aedc-234">Te same czynności można wykonać w witrynie Azure Portal lub międzyplatformowym interfejsie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7aedc-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="7aedc-235">Użyj polecenia `nslookup` w celu sprawdzenia poprawności skonfigurowania wszystkich elementów przez wyszukanie rekordu SOA strefy podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="7aedc-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="7aedc-236">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7aedc-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="7aedc-237">Z danych wyjściowych pobierz serwery nazw dla strefy `partners.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="7aedc-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="7aedc-238">Utwórz zestaw rekordów i rekordy NS dla poszczególnych serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="7aedc-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="7aedc-239">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="7aedc-239">Delete all resources</span></span>

<span data-ttu-id="7aedc-240">Aby usunąć wszystkie zasoby utworzone w tym artykule, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7aedc-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="7aedc-241">W okienku **Ulubione** witryny Azure Portal kliknij pozycję **Wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7aedc-242">W bloku Wszystkie zasoby kliknij grupę zasobów **contosorg**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="7aedc-243">Jeśli wybrana subskrypcja zawiera kilka zasobów, możesz wpisać **contosorg** w polu **Filtruj według nazwy...**,</span><span class="sxs-lookup"><span data-stu-id="7aedc-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="7aedc-244">aby łatwo uzyskać dostęp do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7aedc-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="7aedc-245">W bloku **contosorg** kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="7aedc-246">Portal wymaga wpisania nazwy grupy zasobów w celu potwierdzenia zamiaru jej usunięcia.</span><span class="sxs-lookup"><span data-stu-id="7aedc-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="7aedc-247">Wpisz nazwę grupy zasobów *contosorg*, po czym kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="7aedc-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="7aedc-248">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w niej zawartych, dlatego zawsze należy sprawdzić zawartość grupy zasobów przed jej usunięciem.</span><span class="sxs-lookup"><span data-stu-id="7aedc-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="7aedc-249">Portal usuwa wszystkie zasoby zawarte w grupie zasobów, a następnie usuwa tę grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7aedc-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="7aedc-250">Ten proces trwa kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7aedc-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7aedc-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7aedc-251">Next steps</span></span>

[<span data-ttu-id="7aedc-252">Zarządzanie strefami DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="7aedc-253">Zarządzanie rekordami DNS</span><span class="sxs-lookup"><span data-stu-id="7aedc-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
