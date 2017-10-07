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
# <a name="delegate-a-domain-tooazure-dns"></a>Delegat tooAzure domeny DNS

Usługa DNS platformy Azure pozwala toohost strefy DNS i zarządzanie nimi hello rekordy DNS dla domeny na platformie Azure. Aby zapytania DNS dotyczące tooreach domeny usługi Azure DNS, hello domena ma toobe delegowane z domeny nadrzędnej hello tooAzure DNS. Należy pamiętać, że usługi Azure DNS nie jest hello rejestratora domen. W tym artykule opisano sposób toodelegate Twojego tooAzure domeny DNS.

W przypadku domen zakupionych u rejestratora rejestratora oferuje hello opcja tooset tych rekordów NS. Nie masz tooown toocreate domeny strefę DNS z tą nazwą domeny w usłudze Azure DNS. Jednak należy tooown hello domeny tooset się hello tooAzure delegowania DNS w rejestrze hello.

Załóżmy na przykład, zakupu domeny hello "contoso.net" i tworzysz strefę o nazwie hello "contoso.net" w usłudze Azure DNS. Właściciel hello domeny hello rejestratora oferuje hello adresów serwerów nazw hello tooconfigure opcji (czyli rekordów hello NS) dla domeny. Rejestrator Hello przechowuje te rekordy NS w domenie nadrzędnej hello, w tym przypadku ".net". Klienci na całym świecie hello można następnie ukierunkowanej tooyour domeny w strefie DNS platformy Azure, podczas próby tooresolve rekordów DNS w "contoso.net".

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

1. Zaloguj się toohello portalu Azure
1. W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:

   | **Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|contoso.net|Nazwa Hello hello strefy DNS|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz bramę aplikacji hello toocreate subskrypcji w.|
   |**Grupa zasobów**|**Utwórz nową:** contosoRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

> [!NOTE]
> Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.

## <a name="retrieve-name-servers"></a>Pobieranie serwerów nazw

Aby móc delegować Twojej tooAzure DNS w strefie DNS, należy najpierw tooknow hello nazw serwerów nazw dla swojej strefy. Usługa Azure DNS przydziela serwery nazw z puli za każdym razem, gdy tworzona jest strefa.

1. Strefy DNS hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **contoso.net** strefę DNS w hello **wszystkie zasoby** bloku. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **contoso.net** w hello filtru według nazwy... Brama aplikacji w polu tooeasily dostępu hello. 

1. Serwery nazw hello należy pobrać z bloku strefy DNS hello. W tym przykładzie hello strefie "contoso.net" przypisano serwery nazw "ns1-01.azure-dns.com", "ns2-01.azure-DNS.NET", "ns3-01.azure-dns.org", i "ns4-01.azure-dns.info":

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw hello.  Serwer nazw hello toosee nazwy za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure, wystarczy tooretrieve tych rekordów.

Witaj następujące przykłady stanowią Ponadto kroki hello serwery nazw hello tooretrieve strefę w usłudze Azure DNS za pomocą programu PowerShell i interfejsu wiersza polecenia Azure.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Poniższy przykład Hello jest hello odpowiedzi.

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

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Poniższy przykład Hello jest hello odpowiedzi.

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

## <a name="delegate-hello-domain"></a>Delegat hello domeny

Strefy DNS hello jest tworzony, a masz serwery nazw hello, domena nadrzędna hello musi toobe zaktualizowane z serwerów nazw usługi Azure DNS hello. Każdy rejestrator ma swoje własne DNS zarządzania narzędzia toochange hello rekordy serwera nazw dla domeny. Na stronie zarządzania DNS rejestratora hello Edytuj rekordy NS hello i Zastąp rekordy NS hello hello te usługę Azure DNS.

Podczas delegowania tooAzure domeny DNS, należy użyć hello nazwy serwerów nazw udostępnionych przez usługę Azure DNS. Zalecane jest toouse wszystkie cztery nazw serwera, niezależnie od hello nazwę domeny. Delegowanie domeny nie wymaga hello name server name toouse hello tej samej domeny najwyższego poziomu jako domenę.

Nie należy używać "przyklej rekordów" toopoint toohello usługi Azure DNS nazwy serwera adresów IP, ponieważ te adresy IP mogą ulec zmianie w przyszłych. Delegowanie z wykorzystaniem nazw serwerów nazw we własnej strefie, niekiedy nazywanych „serwerami nazw znaczących”, nie jest obecnie obsługiwane w usłudze Azure DNS.

## <a name="verify-name-resolution-is-working"></a>Sprawdzanie prawidłowego rozpoznawania nazw

Po zakończeniu delegowania hello, można sprawdzić, czy rozpoznawanie nazw działa przy użyciu narzędzia, takiego jak "nslookup" hello tooquery rekord SOA dla swojej strefy (który jest tworzony automatycznie podczas tworzenia strefy hello).

Nie masz serwery toospecify hello Azure DNS, jeśli hello delegowanie zostało skonfigurowane prawidłowo, hello normalny proces rozpoznawania DNS znajdzie serwery nazw hello automatycznie.

```
nslookup -type=SOA contoso.com
```

Witaj poniżej znajduje się przykład odpowiedzi z hello poprzedzających polecenia:

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

## <a name="delegate-sub-domains-in-azure-dns"></a>Delegowanie domen podrzędnych w usłudze Azure DNS

Jeśli chcesz tooset się oddzielną strefę podrzędną, możesz delegować domenę podrzędną w usłudze Azure DNS. Na przykład po skonfigurowaniu i delegowanego "contoso.net" w usłudze Azure DNS, załóżmy, że chcesz tooset się oddzielną strefę podrzędną, "partners.contoso.net".

1. Tworzenie strefy podrzędnej hello "partners.contoso.net" w usłudze Azure DNS.
2. Wyszukiwanie hello autorytatywne rekordy NS w hello podrzędnych strefy tooobtain hello serwery nazw hostujące strefę podrzędną hello w usłudze Azure DNS.
3. Delegowanie strefy podrzędnej hello przez skonfigurowanie rekordów NS w strefie nadrzędnej hello wskazującej strefę podrzędną toohello.

### <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

1. Zaloguj się toohello portalu Azure
1. W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.

    ![Strefa DNS](./media/dns-domain-delegation/dns.png)

1. Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:

   | **Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|partners.contoso.net|Nazwa Hello hello strefy DNS|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz bramę aplikacji hello toocreate subskrypcji w.|
   |**Grupa zasobów**|**Użyj istniejącej:** contosoRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

> [!NOTE]
> Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.

### <a name="retrieve-name-servers"></a>Pobieranie serwerów nazw

1. Strefy DNS hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **partners.contoso.net** strefę DNS w hello **wszystkie zasoby** bloku. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **partners.contoso.net** w hello filtru według nazwy... Witaj strefy DNS pole tooeasily dostępu.

1. Serwery nazw hello należy pobrać z bloku strefy DNS hello. W tym przykładzie hello strefie "contoso.net" przypisano serwery nazw "ns1-01.azure-dns.com", "ns2-01.azure-DNS.NET", "ns3-01.azure-dns.org", i "ns4-01.azure-dns.info":

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Usługa Azure DNS automatycznie tworzy autorytatywne rekordy NS w strefie zawierającej przypisane serwery nazw hello.  Serwer nazw hello toosee nazwy za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia Azure, wystarczy tooretrieve tych rekordów.

### <a name="create-name-server-record-in-parent-zone"></a>Tworzenie rekordu serwera nazw w strefie nadrzędnej

1. Przejdź toohello **contoso.net** strefę DNS w hello portalu Azure.
1. Kliknij pozycję **+ Zestaw rekordów**.
1. Na powitania **dodać zestaw rekordów** bloku, wprowadź następujące wartości hello, a następnie kliknij przycisk **OK**:

   | **Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|partners|Witaj Nazwa strefy DNS podrzędnych hello|
   |**Typ**|NS|Użyj wartości NS w przypadku rekordów serwera nazw.|
   |**Czas wygaśnięcia**|1|Czas toolive.|
   |**Jednostka czasu wygaśnięcia**|Godziny|Ustawia toohours toolive jednostkę czasu|
   |**SERWER NAZW**|{serwery nazw ze strefy partners.contoso.net}|Wprowadź wszystkie 4 serwerów nazw hello ze strefy partners.contoso.net. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Delegowanie domen podrzędnych w usłudze Azure DNS za pomocą innych narzędzi

Witaj poniższe przykłady zapewniają kroki hello toodelegate domenami podrzędnymi w usłudze Azure DNS za pomocą programu PowerShell i interfejsu wiersza polecenia:

#### <a name="powershell"></a>PowerShell

Poniższy przykład PowerShell Hello pokazano, jak to działa. Witaj, te same kroki można wykonać za pomocą portalu Azure hello lub za pośrednictwem hello wiersza polecenia platformy Azure i platform.

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

Użyj `nslookup` tooverify, że wszystko jest poprawnie skonfigurowane, wyszukiwanie hello rekord SOA strefy podrzędnej hello.

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

#### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Pobrać hello serwerów nazw dla hello `partners.contoso.net` strefy z hello danych wyjściowych.

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

Utwórz hello zestawu rekordów i rekordy NS dla każdego serwera nazw.

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

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:

1. W portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **contosorg** grupa zasobów w hello wszystkich bloku zasobów. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **contosorg** w hello **filtrować według nazwy...** Grupa zasobów pole tooeasily dostępu hello.
1. W hello **contosorg** bloku, kliknij przycisk hello **usunąć** przycisku.
1. Witaj portal wymaga nazwy hello tootype tooconfirm grupy zasobów hello, które mają toodelete go. Typ *contosorg* hello Nazwa grupy zasobów, klikając **usunąć**. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów hello, więc zawsze tooconfirm się, że zawartość hello grupy zasobów przed jego usunięciem. Hello portal usuwa wszystkie zasoby zawarte w grupie zasobów hello, a następnie usuwa samej grupy zasobów hello. Ten proces trwa kilka minut.

## <a name="next-steps"></a>Następne kroki

[Zarządzanie strefami DNS](dns-operations-dnszones.md)

[Zarządzanie rekordami DNS](dns-operations-recordsets.md)
