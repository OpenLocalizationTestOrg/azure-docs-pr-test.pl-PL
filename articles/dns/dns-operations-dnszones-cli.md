---
title: "Zarządzanie strefami DNS w usłudze Azure DNS - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Możesz zarządzać stref DNS używa interfejsu wiersza polecenia platformy Azure w wersji 2.0. W tym artykule pokazano, jak aktualizowanie, usuwanie i tworzenie stref DNS w usłudze Azure DNS."
services: dns
documentationcenter: na
author: KumudD
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: kumud
ms.openlocfilehash: 2042d9c2864a4f8da474e0df38882414bfe3417e
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a>Jak zarządzać stref DNS w usłudze Azure DNS za pomocą 2.0 interfejsu wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [Program PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)


W tym przewodniku pokazano, jak zarządzać stref DNS przy użyciu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux. Można również zarządzać stref DNS przy użyciu [programu Azure PowerShell](dns-operations-dnszones.md) lub w portalu Azure.

## <a name="introduction"></a>Wprowadzenie

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Konfigurowanie interfejsu wiersza polecenia platformy Azure 2.0 dla usługi Azure DNS

### <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem konfiguracji sprawdź, czy dysponujesz następującymi elementami:

* Subskrypcja platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).

* Zainstaluj najnowszą wersję 2.0 interfejsu wiersza polecenia Azure, dostępne dla systemu Windows, Linux lub MAC. Więcej informacji znajduje się w temacie [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

### <a name="sign-in-to-your-azure-account"></a>Zaloguj się do swojego konta platformy Azure

Otwórz okno konsoli i uwierzytelnij się przy użyciu swoich poświadczeń. Aby uzyskać więcej informacji, zobacz Log in to Azure from the Azure CLI (Logowanie do platformy Azure z poziomu interfejsu wiersza polecenia platformy Azure).

```
az login
```

### <a name="select-the-subscription"></a>Wybierz subskrypcję

Sprawdź subskrypcje dostępne na koncie.

```
az account list
```

Wybierz subskrypcję platformy Azure do użycia.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Będzie ona używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów. Ponieważ jednak wszystkie zasoby DNS są globalne, a nie regionalne, wybór lokalizacji grupy zasobów nie ma wpływu na usługę Azure DNS.

Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Uzyskiwanie pomocy

Wszystkie polecenia interfejsu wiersza polecenia 2.0 odnoszących się do usługi Azure DNS rozpoczynać `az network dns`. Pomoc jest dostępna dla każdego polecenia za pomocą `--help` opcji (forma krótka `-h`).  Na przykład:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

Do tworzenia strefy DNS służy polecenie `az network dns zone create`. Aby uzyskać pomoc, zobacz `az network dns zone create -h`.

Poniższy przykład tworzy strefę DNS o nazwie *contoso.com* w grupie zasobów o nazwie *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a>Aby utworzyć strefę DNS za pomocą tagów

Poniższy przykład przedstawia sposób tworzenia strefy DNS przy użyciu dwóch [znaczniki usługi Azure Resource Manager](dns-zones-records.md#tags), *projektu = demo* i *env = test*, za pomocą `--tags` parametr (forma krótka `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Pobierz strefę DNS

Aby uzyskać dostęp do strefy DNS, należy użyć `az network dns zone show`. Aby uzyskać pomoc, zobacz `az network dns zone show --help`.

Poniższy przykład zwraca strefę DNS *contoso.com* i skojarzonych danych z grupy zasobów *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Odpowiedzią jest poniższy przykład.

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

Należy pamiętać, że rekordy DNS nie są zwracane przez `az network dns zone show`. Aby wyświetlić listę rekordów DNS, użyj `az network dns record-set list`.


## <a name="list-dns-zones"></a>Lista stref DNS

Aby wyliczyć stref DNS, należy użyć `az network dns zone list`. Aby uzyskać pomoc, zobacz `az network dns zone list --help`.

Określenie grupy zasobów zawiera tylko tych stref w grupie zasobów:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Pominięcie grupa zasobów zawiera listę wszystkich stref w subskrypcji:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Zaktualizuj strefę DNS

Można wprowadzać zmiany do zasobu strefy DNS przy użyciu `az network dns zone update`. Aby uzyskać pomoc, zobacz `az network dns zone update --help`.

To polecenie nie powoduje aktualizacji zestawów rekordów DNS w strefie (zobacz [jak rekordy DNS zarządzanie](dns-operations-recordsets-cli.md)). Jest używane wyłącznie do właściwości zasobu strefy samej aktualizacji. Te właściwości są obecnie ograniczone do [usługi Azure Resource Manager "tagi"](dns-zones-records.md#tags) dla zasobu strefy.

Poniższy przykład przedstawia sposób aktualizowania elementów tag w strefie DNS. Istniejące znaczniki zostały zastąpione przez określona wartość.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Można usunąć strefy DNS przy użyciu `az network dns zone delete`. Aby uzyskać pomoc, zobacz `az network dns zone delete --help`.

> [!NOTE]
> Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów DNS w strefie. Tej operacji nie można cofnąć. Strefa DNS jest używana, usług za pomocą strefie zakończy się niepowodzeniem po usunięciu strefy.
>
>Aby chronić przed usunięciem strefy przypadkowe, zobacz [jak chronić strefy DNS i rekordy](dns-protect-zones-recordsets.md).

To polecenie wyświetla monit o potwierdzenie. Opcjonalny `--yes` przełącznik pomija tego wiersza.

Poniższy przykład przedstawia sposób usunięcia strefy *contoso.com* z grupy zasobów *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się, jak [zarządzać zestawów rekordów i rekordami](dns-getstarted-create-recordset-cli.md) w strefie DNS.

Dowiedz się, jak [Delegowanie domeny do usługi Azure DNS](dns-domain-delegation.md).

