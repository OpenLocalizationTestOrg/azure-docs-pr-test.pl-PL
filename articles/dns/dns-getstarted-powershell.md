---
title: "wprowadzenie do usługi Azure DNS przy użyciu programu PowerShell aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie nimi z pierwszą strefę DNS oraz rejestrowania przy użyciu programu PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Rozpoczynanie pracy z usługą Azure DNS przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-getstarted-cli.md)

W tym artykule przedstawiono hello kroki toocreate z pierwszą strefę DNS i rejestrowanie przy użyciu programu Azure PowerShell. Można również wykonywać te czynności przy użyciu portalu Azure hello lub hello wiersza polecenia platformy Azure i platform.

Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny. Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS. Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny. Poniżej opisano każdy z tych kroków.

W poniższych instrukcjach przyjęto został już zainstalowany i zalogowany tooAzure środowiska PowerShell. Aby uzyskać pomoc, zobacz [jak toomanage DNS strefy przy użyciu programu PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Przed utworzeniem hello strefę DNS, grupy zasobów jest utworzyć strefę DNS hello toocontain. Oto Hello hello polecenia.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzona przy użyciu hello `New-AzureRmDnsZone` polecenia cmdlet. Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*. Użyj toocreate przykład hello strefy DNS, podstawiając hello własne wartości.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Tworzenie rekordu DNS

Tworzenie zestawów rekordów przy użyciu hello `New-AzureRmDnsRecordSet` polecenia cmdlet. Witaj poniższy przykład tworzy rekord z hello nazwie względnej "www" w strefie DNS "contoso.com" w grupie zasobów "MyResourceGroup" hello. Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com". Typ rekordu Hello jest "A", o adresie IP "1.2.3.4", a hello TTL jest 3600 sekund.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Dla innych typów rekordów do zestawów rekordów z więcej niż jeden rekord, a istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu programu Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Wyświetlanie rekordów

toolist hello rekordów DNS w strefie, użyj:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Aktualizowanie serwerów nazw

Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw. Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.

Witaj serwerów nazw dla strefy są podane przez hello `Get-AzureRmDnsZone` polecenia cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny). Rejestrator zaoferuje tooset opcji hello hello serwery nazw dla domeny hello. Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule, wykonaj powitania po kroku:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).

toolearn więcej na temat zarządzania strefami DNS w usłudze Azure DNS, zobacz [stref DNS zarządzania w usłudze Azure DNS przy użyciu programu PowerShell](dns-operations-dnszones.md).

toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [zestawami rekordów i rekordami DNS zarządzania w usłudze Azure DNS przy użyciu programu PowerShell](dns-operations-recordsets.md).

