---
title: "wprowadzenie do usługi Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0 aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie pierwszą strefę DNS i rekordów przy użyciu hello Azure CLI w wersji 1.0."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Rozpoczynanie pracy z usługą Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure 1.0

> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-getstarted-cli.md)

W tym artykule przedstawiono toocreate kroki hello pierwszy strefy DNS i przy użyciu rekordu hello 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux. Można również wykonywać następujące czynności, za pomocą hello portalu Azure lub programu Azure PowerShell.

Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny. Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS. Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny. Poniżej opisano każdy z tych kroków.

W poniższych instrukcjach przyjęto został już zainstalowany i zalogowany tooAzure 1.0 interfejsu wiersza polecenia. Aby uzyskać pomoc, zobacz [jak toomanage DNS strefy przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Przed utworzeniem hello strefę DNS, grupy zasobów jest utworzyć strefę DNS hello toocontain. Oto Hello hello polecenia.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzony przy użyciu hello `azure network dns zone create` polecenia. toosee pomocy dla tego polecenia, wpisz `azure network dns zone create -h`.

Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*. Użyj toocreate przykład hello strefy DNS, podstawiając hello własne wartości.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Tworzenie rekordu DNS

toocreate rekord DNS, użyj hello `azure network dns record-set add-record` polecenia. Aby uzyskać pomoc, zobacz `azure network dns record-set add-record -h`.

Witaj poniższy przykład tworzy rekord z hello nazwie względnej "www" w strefie DNS "contoso.com" w grupie zasobów "MyResourceGroup" hello. Hello pełni kwalifikowana nazwa zestawu rekordów hello jest "www.contoso.com". Typ rekordu Hello jest "A", o adresie IP "1.2.3.4", a używana jest domyślna TTL 3600 sekund (1 godzina).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Dla innych typów rekordów do zestawów rekordów z więcej niż jeden rekord dla alternatywne wartości TTL i toomodify istniejące rekordy, zobacz [przy użyciu zestawów rekordów i rekordami DNS Zarządzanie hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Wyświetlanie rekordów

toolist hello rekordów DNS w strefie, użyj:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Aktualizowanie serwerów nazw

Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw. Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.

Witaj serwerów nazw dla strefy są podane przez hello `azure network dns zone show` polecenia:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny). Rejestrator zaoferuje tooset opcji hello hello serwery nazw dla domeny hello. Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów
 
toodelete wszystkie zasoby są tworzone w tym artykule, wykonaj powitania po kroku:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).

toolearn więcej na temat zarządzania strefami DNS w usłudze Azure DNS, zobacz [stref DNS zarządzania w usłudze Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-dnszones-cli-nodejs.md).

toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [zestawami rekordów i rekordami DNS zarządzania w usłudze Azure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0](dns-operations-recordsets-cli-nodejs.md).

