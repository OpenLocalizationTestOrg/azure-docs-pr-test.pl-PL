---
title: "aaaManage DNS strefy w usłudze Azure DNS - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS używa interfejsu wiersza polecenia platformy Azure w wersji 2.0. W tym artykule przedstawiono sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Jak toomanage strefy DNS w usłudze Azure DNS przy użyciu hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)


Ten przewodnik przedstawia, jak toomanage serwery DNS strefy za pomocą wieloplatformowych hello Azure CLI, która jest dostępna dla systemu Windows, Mac i Linux. Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub hello portalu Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.

## <a name="introduction"></a>Wprowadzenie

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Konfigurowanie interfejsu wiersza polecenia platformy Azure 2.0 dla usługi Azure DNS

### <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.

* Subskrypcja platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).

* Zainstaluj najnowszą wersję hello hello Azure CLI 2.0, dostępne dla systemu Windows, Linux lub MAC. Więcej informacji znajduje się w temacie [instalacji hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Zaloguj się tooyour konto platformy Azure

Otwórz okno konsoli i uwierzytelnij się przy użyciu swoich poświadczeń. Aby uzyskać więcej informacji, zapoznaj się z dziennikiem w tooAzure z hello wiersza polecenia platformy Azure

```
az login
```

### <a name="select-hello-subscription"></a>Wybierz subskrypcję hello

Sprawdź subskrypcje hello hello konta.

```
az account list
```

Wybierz z toouse Twojej subskrypcji platformy Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.

Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Uzyskiwanie pomocy

Wszystkie polecenia 2.0 interfejsu wiersza polecenia dotyczące tooAzure DNS rozpoczynać `az network dns`. Pomoc jest dostępna dla każdego polecenia za pomocą hello `--help` opcji (forma krótka `-h`).  Na przykład:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Strefa DNS jest tworzony przy użyciu hello `az network dns zone create` polecenia. Aby uzyskać pomoc, zobacz `az network dns zone create -h`.

Witaj poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w hello grupy zasobów o nazwie *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate strefy DNS przy użyciu tagów

Hello poniższy przykład przedstawia sposób toocreate DNS strefy przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *project = demo* i *env = test*, za pomocą hello `--tags` parametr (forma krótka `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Pobierz strefę DNS

Użyj tooretrieve strefę DNS `az network dns zone show`. Aby uzyskać pomoc, zobacz `az network dns zone show --help`.

Witaj poniższy przykład zwraca strefę DNS hello *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Poniższy przykład Hello jest hello odpowiedzi.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Należy pamiętać, że rekordy DNS nie są zwracane przez `az network dns zone show`. toolist rekordy DNS, użyj `az network dns record-set list`.


## <a name="list-dns-zones"></a>Lista stref DNS

tooenumerate stref DNS, użyj `az network dns zone list`. Aby uzyskać pomoc, zobacz `az network dns zone list --help`.

Określanie grupy zasobów hello wyświetla tylko tych stref w grupie zasobów hello:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Pominięcie hello grupa zasobów zawiera listę wszystkich stref w subskrypcji hello:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Zaktualizuj strefę DNS

Zmiany tooa zasobów strefy DNS będzie możliwe przy użyciu `az network dns zone update`. Aby uzyskać pomoc, zobacz `az network dns zone update --help`.

To polecenie nie powoduje aktualizacji hello zestawów rekordów DNS w strefie hello (zobacz [jak rekordy DNS tooManage](dns-operations-recordsets-cli.md)). Jest tylko tooupdate używanych właściwości zasobu strefy hello, sama. Te właściwości są obecnie ograniczone toohello [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) hello strefy zasobu.

Witaj poniższy przykład przedstawia sposób tooupdate hello znaczniki strefy DNS. znaczniki istniejących Hello są zastępowane przez hello wybrana.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Można usunąć strefy DNS przy użyciu `az network dns zone delete`. Aby uzyskać pomoc, zobacz `az network dns zone delete --help`.

> [!NOTE]
> Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie hello. Tej operacji nie można cofnąć. Strefa DNS hello jest używany, usługi przy użyciu strefy hello zakończy się niepowodzeniem po usunięciu hello strefy.
>
>Zobacz tooprotect przed usunięciem strefy przypadkowemu [jak tooprotect DNS strefy i rejestruje](dns-protect-zones-recordsets.md).

To polecenie wyświetla monit o potwierdzenie. opcjonalne Hello `--yes` przełącznik pomija tego wiersza.

Witaj poniższy przykład przedstawia sposób toodelete hello strefy *contoso.com* z grupy zasobów *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli.md) w strefie DNS.

Dowiedz się, jak za[delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).

