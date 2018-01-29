---
title: "Zarządzanie strefami DNS w usłudze Azure DNS - PowerShell | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu programu Azure Powershell. W tym artykule opisano sposób aktualizowanie, usuwanie i tworzenie stref DNS w usłudze Azure DNS"
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
ms.date: 09/22/2016
ms.author: gwallace
ms.openlocfilehash: 3f28e70bb6ef46f53375d256a520db40fcb71ad0
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a>Jak zarządzać stref DNS przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [Program PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)

W tym artykule przedstawiono sposób zarządzania stref DNS przy użyciu programu Azure PowerShell. Można również zarządzać stref DNS przy użyciu wielu platform [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub w portalu Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzona za pomocą polecenia cmdlet `New-AzureRmDnsZone`.

Poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w grupie zasobów o nazwie *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Poniższy przykład przedstawia sposób tworzenia strefy DNS przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

Usługa Azure DNS teraz obsługuje również prywatnej stref DNS (obecnie w wersji zapoznawczej).  Na przykład sposobu tworzenia prywatnej strefy DNS Zobacz [wprowadzenie do usługi Azure DNS strefy prywatnej przy użyciu programu PowerShell](./private-dns-getstarted-powershell.md).

## <a name="get-a-dns-zone"></a>Pobierz strefę DNS

Aby uzyskać dostęp do strefy DNS, należy użyć `Get-AzureRmDnsZone` polecenia cmdlet. Ta operacja zwraca obiekt strefy DNS odpowiadającej istniejącej strefy w usłudze Azure DNS. Obiekt zawiera dane dotyczące strefy (na przykład liczba zestawów rekordów), ale nie zawiera zestawów rekordów, same (zobacz `Get-AzureRmDnsRecordSet`).

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

Pomijając nazwę strefy z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w grupie zasobów. Ta operacja zwraca tablicę obiektów stref.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Pomijając zarówno nazwę strefy, jak i nazwę grupy zasobów z `Get-AzureRmDnsZone`, można wyliczyć wszystkich stref w subskrypcji platformy Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Zaktualizuj strefę DNS

Można wprowadzać zmiany do zasobu strefy DNS przy użyciu `Set-AzureRmDnsZone`. To polecenie cmdlet nie zaktualizować zestawów rekordów DNS w strefie (zobacz [jak rekordy DNS zarządzanie](dns-operations-recordsets.md)). Jest używane wyłącznie do właściwości zasobu strefy samej aktualizacji. Właściwości strefy zapisu są obecnie ograniczone do [usługi Azure Resource Manager "tagów" dla zasobu strefy](dns-zones-records.md#tags).

Użyj jednej z dwóch sposobów do aktualizacji strefy DNS:

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a>Określ strefę za pomocą grupy strefy nazwy i zasobów

Ta metoda zastępuje istniejące znaczniki strefy podane wartości.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a>Określ strefę za pomocą obiektu $zone

Takie podejście pobiera istniejący obiekt strefy, modyfikuje tagi, a następnie zatwierdza zmiany. W ten sposób istniejące znaczniki będzie możliwe.

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Korzystając z `Set-AzureRmDnsZone` z obiektem $zone [sprawdza Etag](dns-zones-records.md#etags) są używane do zapewnienia równoległe zmiany nie zostaną zastąpione. Można użyć opcjonalnego `-Overwrite` przełącznik, aby pominąć kontrole.

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Można usunąć strefy DNS przy użyciu `Remove-AzureRmDnsZone` polecenia cmdlet.

> [!NOTE]
> Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie. Tej operacji nie można cofnąć. Strefa DNS jest używana, usług za pomocą strefie zakończy się niepowodzeniem po usunięciu strefy.
>
>Aby chronić przed usunięciem strefy przypadkowe, zobacz [jak chronić strefy DNS i rekordy](dns-protect-zones-recordsets.md).


Użyj jednej z dwóch sposobów można usunąć strefy DNS:

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a>Określ strefę przy użyciu nazwy strefy i nazwy grupy zasobów

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a>Określ strefę za pomocą obiektu $zone

Można określić strefy, które mają zostać usunięte przy użyciu `$zone` obiektu zwróconego przez `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Obiekt strefy może również być przekazywane w potoku zamiast przekazywana jako parametr:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Jak `Set-AzureRmDnsZone`, określając przy użyciu strefy `$zone` obiektu umożliwia Etag kontroli w celu zapewnienia, równoległe zmiany nie zostaną usunięte. Użyj `-Overwrite` przełącznik, aby pominąć kontrole.

## <a name="confirmation-prompts"></a>Monituje o potwierdzenie

`New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, I `Remove-AzureRmDnsZone` o potwierdzenie obsługuje wszystkie polecenia cmdlet.

Zarówno `New-AzureRmDnsZone` i `Set-AzureRmDnsZone` monituje o potwierdzenie, jeśli `$ConfirmPreference` PowerShell preferencji Zmienna ma wartość `Medium` lub niższej. Z powodu potencjalnie duże znaczenie usunięcia strefę DNS `Remove-AzureRmDnsZone` polecenie cmdlet monituje o potwierdzenie, jeśli `$ConfirmPreference` PowerShell zmienna ma żadnej wartości innych niż `None`.

Ponieważ domyślna wartość `$ConfirmPreference` jest `High`, tylko `Remove-AzureRmDnsZone` monituje o potwierdzenie domyślnie.

Można zastąpić bieżącą `$ConfirmPreference` ustawienie przy użyciu `-Confirm` parametru. Jeśli określisz `-Confirm` lub `-Confirm:$True` , polecenie cmdlet monituje o potwierdzenie przed go uruchamia. Jeśli określisz `-Confirm:$False` , polecenie cmdlet monituje o potwierdzenie.

Aby uzyskać więcej informacji na temat `-Confirm` i `$ConfirmPreference`, zobacz [o zmiennych preferencji](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się, jak [zarządzać zestawów rekordów i rekordami](dns-operations-recordsets.md) w strefie DNS.
<br>
Dowiedz się, jak [Delegowanie domeny do usługi Azure DNS](dns-domain-delegation.md).
<br>
Przegląd [dokumentacji programu PowerShell usługi Azure DNS](/powershell/module/azurerm.dns).

