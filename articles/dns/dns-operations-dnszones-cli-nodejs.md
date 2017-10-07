---
title: "aaaManage DNS strefy w usłudze Azure DNS - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0. W tym artykule przedstawiono sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Jak toomanage strefy DNS w usłudze Azure DNS przy użyciu hello Azure CLI w wersji 1.0

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)

Ten przewodnik przedstawia, jak toomanage serwery DNS strefy za pomocą wieloplatformowych hello Azure CLI 1.0, która jest dostępna dla systemu Windows, Mac i Linux. Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub hello portalu Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.

## <a name="introduction"></a>Wprowadzenie

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Uzyskiwanie pomocy

Wszystkie polecenia 1.0 interfejsu wiersza polecenia dotyczące tooAzure DNS rozpoczynać `azure network dns`. Pomoc jest dostępna dla każdego polecenia za pomocą hello `--help` opcji (forma krótka `-h`).  Na przykład:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzony przy użyciu hello `azure network dns zone create` polecenia. Aby uzyskać pomoc, zobacz `azure network dns zone create -h`.

Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate strefy DNS przy użyciu tagów

Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*, za pomocą hello `--tags` parametr (forma krótka `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Pobierz strefę DNS

Użyj tooretrieve strefę DNS `azure network dns zone show`. Aby uzyskać pomoc, zobacz `azure network dns zone show -h`.

Witaj poniższy przykład zwraca strefę DNS hello *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Poniższy przykład Hello jest hello odpowiedzi.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Należy pamiętać, że rekordy DNS nie są zwracane przez `azure network dns zone show`. toolist rekordy DNS, użyj `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Lista stref DNS

tooenumerate stref DNS, użyj `azure network dns zone list`. Aby uzyskać pomoc, zobacz `azure network dns zone list -h`.

Określanie grupy zasobów hello wyświetla tylko tych stref w grupie zasobów hello:

```azurecli
azure network dns zone list MyResourceGroup
```

Pominięcie hello grupa zasobów zawiera listę wszystkich stref w subskrypcji hello:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Zaktualizuj strefę DNS

Zmiany tooa zasobów strefy DNS będzie możliwe przy użyciu `azure network dns zone set`. Aby uzyskać pomoc, zobacz `azure network dns zone set -h`.

To polecenie nie powoduje aktualizacji hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets-cli-nodejs.md)). Jest tylko tooupdate używanych właściwości zasobu strefy hello, sama. Te właściwości są obecnie ograniczone toohello [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) hello strefy zasobu.

Witaj poniższy przykład przedstawia sposób tooupdate hello znaczniki strefy DNS. znaczniki istniejących Hello są zastępowane przez hello wybrana.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Można usunąć strefy DNS przy użyciu `azure network dns zone delete`. Aby uzyskać pomoc, zobacz `azure network dns zone delete -h`.

> [!NOTE]
> Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello. Tej operacji nie można cofnąć. Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.
>
>Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).

To polecenie wyświetla monit o potwierdzenie. opcjonalne Hello `--quiet` przełącznika (forma krótka `-q`) pomija tego wiersza.

Witaj poniższy przykład przedstawia sposób toodelete hello strefy *contoso.com* z grupy zasobów *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli-nodejs.md) w strefie DNS.

Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).

