---
title: "aaaManage DNS strefy w usłudze Azure DNS - PowerShell | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu programu Azure Powershell. W tym artykule opisano sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>Jak toomanage stref DNS przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)

W tym artykule opisano, jak toomanage serwery DNS strefy przy użyciu programu Azure PowerShell. Można również zarządzać stref DNS przy użyciu wieloplatformowych hello [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub hello portalu Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzona przy użyciu hello `New-AzureRmDnsZone` polecenia cmdlet.

Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Pobierz strefę DNS

tooretrieve strefy DNS, użyj hello `Get-AzureRmDnsZone` polecenia cmdlet. Ta operacja zwraca obiekt odpowiadającą tooan istniejących strefę w usłudze Azure DNS strefy DNS. Witaj obiekt zawiera dane dotyczące hello strefy (na przykład hello liczba zestawów rekordów), ale nie zawiera zestawów rekordów hello sami (zobacz `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Lista stref DNS

Pomijając hello nazwę strefy z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w grupie zasobów. Ta operacja zwraca tablicę obiektów stref.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Pomijając hello Nazwa strefy i hello Nazwa grupy zasobów z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w hello subskrypcji platformy Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Zaktualizuj strefę DNS

Zmienia tooa zasobów strefy DNS może się przy użyciu `Set-AzureRmDnsZone`. To polecenie cmdlet nie zaktualizować hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets.md)). Ma ona używana tylko właściwości tooupdate zasób strefy hello samej siebie. właściwości strefy zapisywalny Hello są obecnie ograniczone toohello [usługi Azure Resource Manager "tagów" dla zasobu strefy hello](dns-zones-records.md#tags).

Użyj jednej z następujących dwóch sposobów tooupdate hello strefę DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Określ strefę hello przy użyciu hello strefy nazwy i grupie zasobów

Takie podejście zastępuje istniejące znaczniki strefy hello hello wartości.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Określ strefę hello przy użyciu obiektu $zone

Takie podejście pobiera hello istniejący obiekt strefy, modyfikuje hello tagów, a następnie zatwierdza zmiany hello. W ten sposób istniejące znaczniki będzie możliwe.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Korzystając z `Set-AzureRmDnsZone` z obiektem $zone [sprawdza Etag](dns-zones-records.md#etags) służą tooensure równoległe zmiany nie zostaną zastąpione. Można opcjonalnie hello `-Overwrite` przełącznika toosuppress kontrole.

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Można usunąć strefy DNS przy użyciu hello `Remove-AzureRmDnsZone` polecenia cmdlet.

> [!NOTE]
> Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello. Tej operacji nie można cofnąć. Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.
>
>Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).


Użyj jednej z następujących dwóch sposobów toodelete hello strefę DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Określ strefę hello przy użyciu nazwy strefy hello i nazwa grupy zasobów

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Określ strefę hello przy użyciu obiektu $zone

Można określić toobe strefy hello usunąć przy użyciu `$zone` obiektu zwróconego przez `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Obiekt strefy Hello również mogą być przetwarzane potokowo zamiast przekazywana jako parametr:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Jak `Set-AzureRmDnsZone`, określając hello strefy przy użyciu `$zone` obiektu umożliwia Etag sprawdza tooensure równoległe zmiany nie zostaną usunięte. Użyj hello `-Overwrite` przełącznika toosuppress kontrole.

## <a name="confirmation-prompts"></a>Monituje o potwierdzenie

Witaj `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, i `Remove-AzureRmDnsZone` o potwierdzenie obsługuje wszystkie polecenia cmdlet.

Zarówno `New-AzureRmDnsZone` i `Set-AzureRmDnsZone` monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej. Powodu toohello potencjalnie duże znaczenie usunięcia strefę DNS hello `Remove-AzureRmDnsZone` polecenie cmdlet monituje o potwierdzenie, jeśli hello `$ConfirmPreference` PowerShell zmienna ma żadnej wartości innych niż `None`.

Ponieważ hello wartości domyślnej dla `$ConfirmPreference` jest `High`, tylko `Remove-AzureRmDnsZone` monituje o potwierdzenie domyślnie.

Można zastąpić bieżący hello `$ConfirmPreference` ustawienie za pomocą hello `-Confirm` parametru. Jeśli określisz `-Confirm` lub `-Confirm:$True` , hello polecenie cmdlet monituje o potwierdzenie przed go uruchamia. Jeśli określisz `-Confirm:$False` , hello polecenie cmdlet monituje o potwierdzenie.

Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-operations-recordsets.md) w strefie DNS.
<br>
Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).
<br>
Przejrzyj hello [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).

