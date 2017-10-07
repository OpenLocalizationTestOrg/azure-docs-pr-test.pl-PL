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
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Zarządzanie rekordami DNS i zestawy rekordów w usłudze Azure DNS przy użyciu programu Azure PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

W tym artykule opisano, jak rekordy toomanage DNS dla strefy DNS przy użyciu programu Azure PowerShell. Rekordy DNS można też zarządzać za pomocą wielu platform hello [interfejsu wiersza polecenia Azure](dns-operations-recordsets-cli.md) lub hello [portalu Azure](dns-operations-recordsets-portal.md).

Przykłady Hello w tym artykule założono, że masz już [zainstalowany program Azure PowerShell, zalogowany i utworzyć strefę DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Wprowadzenie

Przed utworzeniem rekordy DNS w usłudze Azure DNS, należy najpierw toounderstand jak usługi Azure DNS organizuje rekordy DNS w zestawach rekordów DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Aby uzyskać więcej informacji na temat rekordów DNS w usłudze Azure DNS, zobacz [Strefy i rekordy DNS](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Utwórz nowy rekord DNS

Jeśli Twoje nowy rekord ma hello takie same nazwy i wpisać jako istniejącego rekordu, należy za[ją dodać toohello istniejącego zestawu rekordów](#add-a-record-to-an-existing-record-set). Twój nowy rekord ma inną tooall nazwę i typ istniejących rekordów, należy najpierw toocreate zestawu rekordów. 

### <a name="create-a-records-in-a-new-record-set"></a>Utwórz rekordy "" w zestawie rekordów

Tworzenie zestawów rekordów przy użyciu hello `New-AzureRmDnsRecordSet` polecenia cmdlet. Podczas tworzenia zestawu rekordów, należy nazwy zestawu rekordów hello toospecify, hello strefy, czas hello toolive (TTL), typ rekordu hello i toobe rekordów hello utworzony.

Parametry Hello w celu dodania zestawu rekordów tooa rekordów różnią się zależnie od typu hello hello zestawu rekordów. Na przykład podczas korzystania z zestawu rekordów typu "A", potrzebujesz adresu IP hello toospecify za pomocą parametru hello `-IPv4Address`. Inne parametry są używane dla innych typów rekordów. Zobacz [typu rekordu dodatkowe przykłady](#additional-record-type-examples) szczegółowe informacje.

Witaj poniższy przykład tworzy hello nazwie względnej "www" w strefie DNS "contoso.com" hello rekordów. Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com". Typ rekordu Hello jest "A", a hello TTL jest 3600 sekund. Witaj zestaw rekordów zawiera jeden rekord o adresie IP "1.2.3.4".

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

zestaw rekordów toocreate na powitania wierzchołku i strefy (w tym przypadku "contoso.com"), użyj nazwy zestawu rekordów hello "@" (bez cudzysłowów):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Toocreate zestaw rekordów, zawierający więcej niż jeden rekord, należy najpierw utworzyć lokalnej tablicy i dodać rekordy hello, a następnie przekazać tablicy hello zbyt`New-AzureRmDnsRecordSet` w następujący sposób:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość. Hello poniższy przykład przedstawia sposób toocreate, zestaw rekordów, o dwa wpisy metadanych, "dział = not" i "środowiska produkcji =".

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

Usługa DNS platformy Azure obsługuje również "empty" zestawów rekordów, które mogą działać jako tooreserve symbol zastępczy nazwy DNS przed utworzeniem rekordów DNS. Pusty zestawów rekordów są widoczne w płaszczyźnie kontroli usługi Azure DNS hello, ale są wyświetlane na serwery hello Azure DNS. Witaj poniższy przykład tworzy pusty zestaw rekordów:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Tworzenie rekordów innych typów

Posiadanie widoczne szczegółowo jak rekordy toocreate "A", hello następujących przykładach pokazano, jak rekordy toocreate innych zarejestrować typy są obsługiwane przez usługę Azure DNS.

W każdym przypadku zostanie przedstawiony sposób toocreate rekord zestaw zawierający pojedynczy rekord. Witaj wcześniejszych przykłady rekordy "" może być dostosowane toocreate zestawów rekordów innych typów zawierający wiele rekordów z metadanymi, lub ustawia toocreate pusty rekord.

Firma Microsoft nie dają toocreate przykład zestawu rekordów SOA, ponieważ SOAs są tworzone i usunąć z każdej strefy DNS i nie można utworzyć ani usunąć oddzielnie. Jednak [hello SOA można modyfikować, jak pokazano w przykładzie nowsze](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów AAAA z pojedynczym rekordem

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów CNAME z pojedynczym rekordem

> [!NOTE]
> Standardy usługi DNS Hello nie zezwalają na rekordy CNAME w wierzchołku hello strefy (`-Name '@'`), ani akceptują zestawów rekordów zawierających więcej niż jeden rekord.
> 
> Aby uzyskać więcej informacji, zobacz [rekordy CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów MX z pojedynczym rekordem

W tym przykładzie używamy nazwy zestawu rekordów hello "@" rekordu toocreate MX w wierzchołku strefy hello (w tym przypadku "contoso.com").


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów NS z pojedynczym rekordem

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów PTR z pojedynczym rekordem

W takim przypadku "Mój-arpa-zone.com" reprezentuje hello strefy wyszukiwania wstecznego ARPA reprezentujący zakresowi adresów IP. Każdy rekord PTR ustawione w tej strefie odpowiada tooan adres IP zakresu tego adresu IP. Nazwa rekordu Hello "10" jest Witaj oktet ostatniego adresu IP hello tego zakresu IP reprezentowany przez ten rekord.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów SRV z pojedynczym rekordem

Podczas tworzenia [zestawu rekordów SRV](dns-zones-records.md#srv-records), określ hello * \_usługi* i * \_protokołu* w hello nazwy zestawu rekordów. Nie istnieje żadne tooinclude potrzeby "@" w hello nazwy zestawu rekordów podczas tworzenia rekordów SRV zestawu w wierzchołku strefy hello.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Tworzenie zestawu rekordów TXT z pojedynczym rekordem

Witaj poniższy przykład przedstawia sposób rejestrowania toocreate TXT. Aby uzyskać więcej informacji na temat hello maksymalna długość ciągu obsługiwane w rekordach TXT, zobacz [rekordów TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Pobierz zestaw rekordów

Użyj istniejącego zestawu rekordów, tooretrieve `Get-AzureRmDnsRecordSet`. To polecenie cmdlet zwraca obiekt reprezentujący rekord hello w usłudze Azure DNS.

Jak `New-AzureRmDnsRecordSet`, musi być podana nazwa zestawu rekordów hello *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy. Należy również typ rekordu hello toospecify i strefy hello zawierającej hello zestawu rekordów.

Witaj poniższy przykład przedstawia sposób tooretrieve zestaw rekordów. W tym przykładzie strefie hello jest określona za pomocą hello `-ZoneName` i `-ResourceGroupName` parametrów.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Alternatywnie można również określić strefy hello przy użyciu obiektu strefy przekazywane przy użyciu hello `-Zone` parametru.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Lista zestawów rekordów

Można również użyć `Get-AzureRmDnsZone` zestawy toolist rekordów w strefie, pomijając hello `-Name` i/lub `-RecordType` parametrów.

Witaj poniższy przykład zwraca zestawy wszystkich rekordów w strefie hello:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Witaj poniższym przykładzie pokazano, jak rejestrować wszystkie zestawy danego typu mogą być pobierane przez określenie typu rekordu hello podczas pominięcie rekordu hello Nazwa zestawu:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

zestawy wszystkich rekordów o podanej nazwie, tooretrieve różnych typów rekordów, należy tooretrieve wszystkie zestawy rekordów i następnie filtr hello wyniki:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

W wszystkich hello powyżej przykłady, hello strefa może być określona za pomocą hello `-ZoneName` i `-ResourceGroupName`parametrów (jak pokazano), lub za pośrednictwem obiektu strefy:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Dodawanie rekordów tooan istniejącego zestawu rekordów

tooadd istniejącego rekordu rekordów tooan ustawić, wykonaj następujące trzy kroki hello:

1. Pobierz hello istniejącego zestawu rekordów

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Dodaj hello nowych rekordów toohello lokalnego zestawu rekordów. Jest to operacja offline.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Zatwierdź hello zmiany wstecz toohello usługa Azure DNS. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Przy użyciu `Set-AzureRmDnsRecordSet` *zastępuje* hello istniejącego zestawu rekordów w usłudze Azure DNS (i wszystkich rekordów zawiera) z zestawu rekordów hello określony. [Element etag kontroli](dns-zones-records.md#etags) są używane tooensure równoległe zmiany nie zostaną zastąpione. Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.

Ta sekwencja operacji można też *przetwarzana potokowo*, co oznacza przekazać obiekt zestawu rekordów hello za pomocą potoku hello zamiast przekazaniem go jako parametr:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Witaj powyższych przykładach konfiguracji tooadd istniejącego rekordu "" tooan rekordów typu "A". Podobne sekwencja operacji jest używane tooadd rekordów toorecord zestawy innych typów, zastępując hello `-Ipv4Address` parametr `Add-AzureRmDnsRecordConfig` z innym typem rekordu tooeach określonych parametrów. Witaj parametry dla poszczególnych typów rekordów są hello takie same jak w przypadku hello `New-AzureRmDnsRecordConfig` polecenia cmdlet, jak pokazano w [typu rekordu dodatkowe przykłady](#additional-record-type-examples) powyżej.

Zestawy rekordów typu "CNAME" lub "SOA" nie może zawierać więcej niż jeden rekord. To ograniczenie wynika z hello standardy usługi DNS. Nie jest to ograniczenie usługi Azure DNS.

## <a name="remove-a-record-from-an-existing-record-set"></a>Usuń rekord z istniejącego zestawu rekordów

Hello tooremove procesu rekord na podstawie zestawu rekordów jest podobne tooadd procesu toohello istniejących rekordów tooan zestawu rekordów:

1. Pobierz hello istniejącego zestawu rekordów

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Usuń rekord hello z obiektu zestawu rekordów lokalne powitania. Jest to operacja offline. Hello rekordu, który jest usuwana musi być identyczna z istniejącym rekordem we wszystkich parametrów.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Zatwierdź hello zmiany wstecz toohello usługa Azure DNS. Użyj hello opcjonalne `-Overwrite` przełącznika toosuppress [sprawdza Etag](dns-zones-records.md#etags) równoczesnych zmian.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Przy użyciu hello powyżej sekwencji tooremove hello ostatni rekord z zestawu rekordów nie powoduje usunięcia hello zestawu rekordów, a nie wydostaje pusty zestaw rekordów. Zobacz tooremove całkowicie, zestaw rekordów [Usuń zestaw rekordów](#delete-a-record-set).

Podobnie tooadding rekordów tooa zestawu rekordów, sekwencja hello tooremove operacje, w których zestaw rekordów mogą również być przekazywane w potoku:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Różnych typów rekordów są obsługiwane, przekazując odpowiednie parametry typu hello zbyt`Remove-AzureRmDnsRecordSet`. Witaj parametry dla poszczególnych typów rekordów są hello takie same jak w przypadku hello `New-AzureRmDnsRecordConfig` polecenia cmdlet, jak pokazano w [typu rekordu dodatkowe przykłady](#additional-record-type-examples) powyżej.


## <a name="modify-an-existing-record-set"></a>Modyfikowanie istniejącego zestawu rekordów

kroki Hello modyfikowania istniejącego zestawu rekordów są podobne kroki toohello, które należy wykonać podczas dodawania lub usuwania rekordów z zestawu rekordów:

1. Pobrać hello istniejącego rekordu skonfigurowane przy użyciu `Get-AzureRmDnsRecordSet`.
2. Modyfikowanie obiektu lokalnego zestawu rekordów hello przez:
    * Dodawanie lub usuwanie rekordów
    * Zmiana parametrów hello istniejących rekordów
    * Zmiana rekordu hello Ustaw metadanych i czas toolive (TTL)
3. Zatwierdź zmiany przy użyciu hello `Set-AzureRmDnsRecordSet` polecenia cmdlet. To *zastępuje* hello istniejącego zestawu rekordów w usłudze Azure DNS z zestawu rekordów hello określony.

Korzystając z `Set-AzureRmDnsRecordSet`, [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną zastąpione. Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>Ustaw tooupdate rekordu w istniejącego rekordu

W tym przykładzie zmienimy hello adresu IP istniejącego rekordu "":

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify rekord SOA

Nie można dodać lub usunąć rekordy hello automatycznie utworzony rekord SOA na wierzchołku strefy hello (`-Name "@"`, w tym znaki cudzysłowu). Jednak można zmodyfikować jego dowolne parametry hello w hello rekord SOA (z wyjątkiem "Host") i czas wygaśnięcia zestawu rekordów hello.

powitania po przykładzie pokazano, jak toochange hello *E-mail* właściwości hello rekord SOA:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS rekordów w wierzchołku strefy hello

zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS. Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.

Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS. Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów. Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.

Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello. Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.

Witaj poniższy przykład przedstawia tooadd rekordów NS toohello dodatkowe nazwy serwera konfiguracji na wierzchołku strefy hello:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>metadane zestawu rekordów toomodify

[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.

Witaj poniższym przykładzie pokazano, jak ustawić toomodify hello metadane istniejącego rekordu:

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


## <a name="delete-a-record-set"></a>Usuń zestaw rekordów

Zestawy rekordów można usunąć za pomocą hello `Remove-AzureRmDnsRecordSet` polecenia cmdlet. Usunięcie zestawu rekordów spowoduje również usunięcie wszystkich rekordów w zestawie rekordów hello.

> [!NOTE]
> Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (`-Name '@'`).  Usługa Azure DNS utworzenia są automatycznie hello strefy został utworzony i usunie je automatycznie po usunięciu hello strefy.

Witaj poniższy przykład przedstawia sposób toodelete zestaw rekordów. W tym przykładzie nazwa zestawu rekordów hello, zestaw rekordów typu nazwa strefy i grupy zasobów są każdego określonego jawnie.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Możesz też zestawu rekordów hello może zostać określony przez nazwę i typ i hello strefy określonej za pomocą obiektu:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Trzecia opcja można określić samego zestawu rekordów hello przy użyciu obiektu zestaw rekordów:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Po określeniu zestawu rekordów hello toobe usunięte za pomocą obiektu zestawu rekordów, [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną usunięte. Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.

obiekt zestawu rekordów Hello również mogą być przetwarzane potokowo zamiast przekazywana jako parametr:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Monituje o potwierdzenie

Witaj `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, i `Remove-AzureRmDnsRecordSet` o potwierdzenie obsługuje wszystkie polecenia cmdlet.

Każde polecenie cmdlet monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej. Ponieważ hello wartości domyślnej dla `$ConfirmPreference` jest `High`, monity nie są podane, używając hello domyślnych ustawień programu PowerShell.

Można zastąpić bieżący hello `$ConfirmPreference` ustawienie za pomocą hello `-Confirm` parametru. Jeśli określisz `-Confirm` lub `-Confirm:$True` , hello polecenie cmdlet monituje o potwierdzenie przed go uruchamia. Jeśli określisz `-Confirm:$False` , hello polecenie cmdlet monituje o potwierdzenie. 

Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [strefy i rekordy w usłudze Azure DNS](dns-zones-records.md).
<br>
Dowiedz się, jak za[ochrony strefy i rekordy](dns-protect-zones-recordsets.md) przy użyciu usługi Azure DNS.
<br>
Przejrzyj hello [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).
