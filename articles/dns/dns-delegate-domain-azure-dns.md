---
title: aaaDelegate Twojego tooAzure domeny DNS | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toochange, delegowanie domeny i używanie usługi Azure DNS nazwy hosting domeny tooprovide serwerów."
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="6fdfb-103">Delegat tooAzure domeny DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="6fdfb-104">Usługa DNS platformy Azure pozwala toohost strefy DNS i zarządzanie nimi hello rekordy DNS dla domeny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="6fdfb-105">Aby zapytania DNS dotyczące tooreach domeny usługi Azure DNS, hello domena ma toobe delegowane z domeny nadrzędnej hello tooAzure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="6fdfb-106">Należy pamiętać, że usługi Azure DNS nie jest hello rejestratora domen.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="6fdfb-107">W tym artykule opisano sposób toodelegate Twojego tooAzure domeny DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="6fdfb-108">W przypadku domen zakupionych u rejestratora rejestratora oferuje hello opcja tooset tych rekordów NS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="6fdfb-109">Nie masz tooown toocreate domeny strefę DNS z tą nazwą domeny w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="6fdfb-110">Jednak należy tooown hello domeny tooset się hello tooAzure delegowania DNS w rejestrze hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="6fdfb-111">Załóżmy na przykład, zakupu domeny hello "contoso.net" i tworzysz strefę o nazwie hello "contoso.net" w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="6fdfb-112">Właściciel hello domeny hello rejestratora oferuje hello adresów serwerów nazw hello tooconfigure opcji (czyli rekordów hello NS) dla domeny.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="6fdfb-113">Rejestrator Hello przechowuje te rekordy NS w domenie nadrzędnej hello, w tym przypadku ".net".</span><span class="sxs-lookup"><span data-stu-id="6fdfb-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="6fdfb-114">Klienci na całym świecie hello można następnie ukierunkowanej tooyour domeny w strefie DNS platformy Azure, podczas próby tooresolve rekordów DNS w "contoso.net".</span><span class="sxs-lookup"><span data-stu-id="6fdfb-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="6fdfb-115">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-115">Create a DNS zone</span></span>

1. <span data-ttu-id="6fdfb-116">Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6fdfb-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="6fdfb-117">W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="6fdfb-119">Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="6fdfb-120">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-120">**Setting**</span></span> | <span data-ttu-id="6fdfb-121">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-121">**Value**</span></span> | <span data-ttu-id="6fdfb-122">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="6fdfb-123">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-123">**Name**</span></span>|<span data-ttu-id="6fdfb-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="6fdfb-124">contoso.net</span></span>|<span data-ttu-id="6fdfb-125">Nazwa Hello hello strefy DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="6fdfb-126">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-126">**Subscription**</span></span>|<span data-ttu-id="6fdfb-127">[Twoja subskrypcja]</span><span class="sxs-lookup"><span data-stu-id="6fdfb-127">[Your subscription]</span></span>|<span data-ttu-id="6fdfb-128">Wybierz bramę aplikacji hello toocreate subskrypcji w.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="6fdfb-129">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-129">**Resource group**</span></span>|<span data-ttu-id="6fdfb-130">**Utwórz nową:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="6fdfb-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="6fdfb-131">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-131">Create a resource group.</span></span> <span data-ttu-id="6fdfb-132">Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="6fdfb-133">więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="6fdfb-134">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-134">**Location**</span></span>|<span data-ttu-id="6fdfb-135">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="6fdfb-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="6fdfb-136">Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="6fdfb-137">Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="6fdfb-138">Pobieranie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="6fdfb-138">Retrieve name servers</span></span>

<span data-ttu-id="6fdfb-139">Aby móc delegować Twojej tooAzure DNS w strefie DNS, należy najpierw tooknow hello nazw serwerów nazw dla swojej strefy.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="6fdfb-140">Usługa Azure DNS przydziela serwery nazw z puli za każdym razem, gdy tworzona jest strefa.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="6fdfb-141">Strefy DNS hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="6fdfb-142">Kliknij przycisk hello **contoso.net** strefę DNS w hello **wszystkie zasoby** bloku.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="6fdfb-143">Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **contoso.net** w hello filtru według nazwy...</span><span class="sxs-lookup"><span data-stu-id="6fdfb-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="6fdfb-144">Brama aplikacji w polu tooeasily dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="6fdfb-145">Serwery nazw hello należy pobrać z bloku strefy DNS hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="6fdfb-146">W tym przykładzie hello strefie "contoso.net" przypisano serwery nazw "ns1-01.azure-dns.com", "ns2-01.azure-DNS.NET", "ns3-01.azure-dns.org", i "ns4-01.azure-dns.info":</span><span class="sxs-lookup"><span data-stu-id="6fdfb-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="6fdfb-148">Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="6fdfb-149">Serwer nazw hello toosee nazwy za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure, wystarczy tooretrieve tych rekordów.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="6fdfb-150">Witaj następujące przykłady stanowią Ponadto kroki hello serwery nazw hello tooretrieve strefę w usłudze Azure DNS za pomocą programu PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="6fdfb-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fdfb-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="6fdfb-152">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="6fdfb-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6fdfb-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="6fdfb-154">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="6fdfb-155">Delegat hello domeny</span><span class="sxs-lookup"><span data-stu-id="6fdfb-155">Delegate hello domain</span></span>

<span data-ttu-id="6fdfb-156">Strefy DNS hello jest tworzony, a masz serwery nazw hello, domena nadrzędna hello musi toobe zaktualizowane z serwerów nazw usługi Azure DNS hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="6fdfb-157">Każdy rejestrator ma swoje własne DNS zarządzania narzędzia toochange hello rekordy serwera nazw dla domeny.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="6fdfb-158">Na stronie zarządzania DNS rejestratora hello Edytuj rekordy NS hello i Zastąp rekordy NS hello hello te usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="6fdfb-159">Podczas delegowania tooAzure domeny DNS, należy użyć hello nazwy serwerów nazw udostępnionych przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="6fdfb-160">Zalecane jest toouse wszystkie cztery nazw serwera, niezależnie od hello nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="6fdfb-161">Delegowanie domeny nie wymaga hello name server name toouse hello tej samej domeny najwyższego poziomu jako domenę.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="6fdfb-162">Nie należy używać "przyklej rekordów" toopoint toohello usługi Azure DNS nazwy serwera adresów IP, ponieważ te adresy IP mogą ulec zmianie w przyszłych.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="6fdfb-163">Delegowanie z wykorzystaniem nazw serwerów nazw we własnej strefie, niekiedy nazywanych „serwerami nazw znaczących”, nie jest obecnie obsługiwane w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="6fdfb-164">Sprawdzanie prawidłowego rozpoznawania nazw</span><span class="sxs-lookup"><span data-stu-id="6fdfb-164">Verify name resolution is working</span></span>

<span data-ttu-id="6fdfb-165">Po zakończeniu delegowania hello, można sprawdzić, czy rozpoznawanie nazw działa przy użyciu narzędzia, takiego jak "nslookup" hello tooquery rekord SOA dla swojej strefy (który jest tworzony automatycznie podczas tworzenia strefy hello).</span><span class="sxs-lookup"><span data-stu-id="6fdfb-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="6fdfb-166">Nie masz serwery toospecify hello Azure DNS, jeśli hello delegowanie zostało skonfigurowane prawidłowo, hello normalny proces rozpoznawania DNS znajdzie serwery nazw hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="6fdfb-167">Witaj poniżej znajduje się przykład odpowiedzi z hello poprzedzających polecenia:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="6fdfb-168">Delegowanie domen podrzędnych w usłudze Azure DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="6fdfb-169">Jeśli chcesz tooset się oddzielną strefę podrzędną, możesz delegować domenę podrzędną w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="6fdfb-170">Na przykład po skonfigurowaniu i delegowanego "contoso.net" w usłudze Azure DNS, załóżmy, że chcesz tooset się oddzielną strefę podrzędną, "partners.contoso.net".</span><span class="sxs-lookup"><span data-stu-id="6fdfb-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="6fdfb-171">Tworzenie strefy podrzędnej hello "partners.contoso.net" w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="6fdfb-172">Wyszukiwanie hello autorytatywne rekordy NS w hello podrzędnych strefy tooobtain hello serwery nazw hostujące strefę podrzędną hello w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="6fdfb-173">Delegowanie strefy podrzędnej hello przez skonfigurowanie rekordów NS w strefie nadrzędnej hello wskazującej strefę podrzędną toohello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="6fdfb-174">Tworzenie strefy DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-174">Create a DNS zone</span></span>

1. <span data-ttu-id="6fdfb-175">Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6fdfb-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="6fdfb-176">W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="6fdfb-178">Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="6fdfb-179">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-179">**Setting**</span></span> | <span data-ttu-id="6fdfb-180">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-180">**Value**</span></span> | <span data-ttu-id="6fdfb-181">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="6fdfb-182">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-182">**Name**</span></span>|<span data-ttu-id="6fdfb-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="6fdfb-183">partners.contoso.net</span></span>|<span data-ttu-id="6fdfb-184">Nazwa Hello hello strefy DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="6fdfb-185">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-185">**Subscription**</span></span>|<span data-ttu-id="6fdfb-186">[Twoja subskrypcja]</span><span class="sxs-lookup"><span data-stu-id="6fdfb-186">[Your subscription]</span></span>|<span data-ttu-id="6fdfb-187">Wybierz bramę aplikacji hello toocreate subskrypcji w.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="6fdfb-188">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-188">**Resource group**</span></span>|<span data-ttu-id="6fdfb-189">**Użyj istniejącej:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="6fdfb-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="6fdfb-190">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-190">Create a resource group.</span></span> <span data-ttu-id="6fdfb-191">Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="6fdfb-192">więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="6fdfb-193">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-193">**Location**</span></span>|<span data-ttu-id="6fdfb-194">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="6fdfb-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="6fdfb-195">Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="6fdfb-196">Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="6fdfb-197">Pobieranie serwerów nazw</span><span class="sxs-lookup"><span data-stu-id="6fdfb-197">Retrieve name servers</span></span>

1. <span data-ttu-id="6fdfb-198">Strefy DNS hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="6fdfb-199">Kliknij przycisk hello **partners.contoso.net** strefę DNS w hello **wszystkie zasoby** bloku.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="6fdfb-200">Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **partners.contoso.net** w hello filtru według nazwy...</span><span class="sxs-lookup"><span data-stu-id="6fdfb-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="6fdfb-201">Witaj strefy DNS pole tooeasily dostępu.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="6fdfb-202">Serwery nazw hello należy pobrać z bloku strefy DNS hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="6fdfb-203">W tym przykładzie hello strefie "contoso.net" przypisano serwery nazw "ns1-01.azure-dns.com", "ns2-01.azure-DNS.NET", "ns3-01.azure-dns.org", i "ns4-01.azure-dns.info":</span><span class="sxs-lookup"><span data-stu-id="6fdfb-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="6fdfb-205">Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="6fdfb-206">Serwer nazw hello toosee nazwy za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure, wystarczy tooretrieve tych rekordów.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="6fdfb-207">Tworzenie rekordu serwera nazw w strefie nadrzędnej</span><span class="sxs-lookup"><span data-stu-id="6fdfb-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="6fdfb-208">Przejdź toohello **contoso.net** strefę DNS w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="6fdfb-209">Kliknij pozycję **+ Zestaw rekordów**.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="6fdfb-210">Na powitania **dodać zestaw rekordów** bloku, wprowadź następujące wartości hello, a następnie kliknij przycisk **OK**:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="6fdfb-211">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-211">**Setting**</span></span> | <span data-ttu-id="6fdfb-212">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-212">**Value**</span></span> | <span data-ttu-id="6fdfb-213">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="6fdfb-214">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-214">**Name**</span></span>|<span data-ttu-id="6fdfb-215">partners</span><span class="sxs-lookup"><span data-stu-id="6fdfb-215">partners</span></span>|<span data-ttu-id="6fdfb-216">Witaj Nazwa strefy DNS podrzędnych hello</span><span class="sxs-lookup"><span data-stu-id="6fdfb-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="6fdfb-217">**Typ**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-217">**Type**</span></span>|<span data-ttu-id="6fdfb-218">NS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-218">NS</span></span>|<span data-ttu-id="6fdfb-219">Użyj wartości NS w przypadku rekordów serwera nazw.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="6fdfb-220">**Czas wygaśnięcia**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-220">**TTL**</span></span>|<span data-ttu-id="6fdfb-221">1</span><span class="sxs-lookup"><span data-stu-id="6fdfb-221">1</span></span>|<span data-ttu-id="6fdfb-222">Czas toolive.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-222">Time toolive.</span></span>|
   |<span data-ttu-id="6fdfb-223">**Jednostka czasu wygaśnięcia**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-223">**TTL unit**</span></span>|<span data-ttu-id="6fdfb-224">Godziny</span><span class="sxs-lookup"><span data-stu-id="6fdfb-224">Hours</span></span>|<span data-ttu-id="6fdfb-225">Ustawia toohours toolive jednostkę czasu</span><span class="sxs-lookup"><span data-stu-id="6fdfb-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="6fdfb-226">**SERWER NAZW**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-226">**NAME SERVER**</span></span>|<span data-ttu-id="6fdfb-227">{serwery nazw ze strefy partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="6fdfb-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="6fdfb-228">Wprowadź wszystkie 4 serwerów nazw hello ze strefy partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="6fdfb-230">Delegowanie domen podrzędnych w usłudze Azure DNS za pomocą innych narzędzi</span><span class="sxs-lookup"><span data-stu-id="6fdfb-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="6fdfb-231">Witaj poniższe przykłady zapewniają kroki hello toodelegate domenami podrzędnymi w usłudze Azure DNS za pomocą programu PowerShell i interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="6fdfb-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fdfb-232">PowerShell</span></span>

<span data-ttu-id="6fdfb-233">Poniższy przykład PowerShell Hello pokazano, jak to działa.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="6fdfb-234">Witaj, te same kroki można wykonać za pomocą portalu Azure hello lub za pośrednictwem hello wiersza polecenia platformy Azure i platform.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="6fdfb-235">Użyj `nslookup` tooverify, że wszystko jest poprawnie skonfigurowane, wyszukiwanie hello rekord SOA strefy podrzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="6fdfb-236">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6fdfb-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="6fdfb-237">Pobrać hello serwerów nazw dla hello `partners.contoso.net` strefy z hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="6fdfb-238">Utwórz hello zestawu rekordów i rekordy NS dla każdego serwera nazw.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="6fdfb-239">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="6fdfb-239">Delete all resources</span></span>

<span data-ttu-id="6fdfb-240">toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6fdfb-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="6fdfb-241">W portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="6fdfb-242">Kliknij przycisk hello **contosorg** grupa zasobów w hello wszystkich bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="6fdfb-243">Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **contosorg** w hello **filtrować według nazwy...**</span><span class="sxs-lookup"><span data-stu-id="6fdfb-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="6fdfb-244">Grupa zasobów pole tooeasily dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="6fdfb-245">W hello **contosorg** bloku, kliknij przycisk hello **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="6fdfb-246">Witaj portal wymaga nazwy hello tootype tooconfirm grupy zasobów hello, które mają toodelete go.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="6fdfb-247">Typ *contosorg* hello Nazwa grupy zasobów, klikając **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="6fdfb-248">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów hello, więc zawsze tooconfirm się, że zawartość hello grupy zasobów przed jego usunięciem.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="6fdfb-249">Hello portal usuwa wszystkie zasoby zawarte w grupie zasobów hello, a następnie usuwa samej grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="6fdfb-250">Ten proces trwa kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6fdfb-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fdfb-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6fdfb-251">Next steps</span></span>

[<span data-ttu-id="6fdfb-252">Zarządzanie strefami DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="6fdfb-253">Zarządzanie rekordami DNS</span><span class="sxs-lookup"><span data-stu-id="6fdfb-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
