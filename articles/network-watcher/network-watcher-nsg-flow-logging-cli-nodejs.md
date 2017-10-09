---
title: "aaaManage przepływ grupy zabezpieczeń sieci dzienniki z obserwatora sieciowego Azure - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage przepływu grupy zabezpieczeń sieci loguje obserwatora sieciowego Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a>Konfigurowanie dzienniki przepływu grupy zabezpieczeń sieci przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [Interfejs API REST](network-watcher-nsg-flow-logging-rest.md)

Dzienniki przepływu sieciowej grupy zabezpieczeń są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci. Te dzienniki przepływu są zapisywane w formacie json i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.

W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux. Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.

## <a name="register-insights-provider"></a>Zarejestruj dostawcę usługi Insights

Aby przepływ hello pomyślnie, rejestrowanie toowork **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana. Jeśli nie masz pewności, czy hello **elemencie Microsoft.Insights** dostawca jest zarejestrowany, uruchom hello poniższy skrypt.

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a>Dzienniki przepływu włączyć grupy zabezpieczeń sieci

Dzienniki przepływu tooenable polecenia Hello jest pokazywana w hello poniższy przykład:

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a>Dzienniki przepływu wyłączyć grupy zabezpieczeń sieci

Następujące przykładowe toodisable przepływu dzienniki hello użycia:

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a>Pobierz dziennik przepływu

Witaj lokalizacji magazynu dziennika przepływu jest definiowany podczas tworzenia. Tooaccess wygodne narzędzie, te konta magazynu tooa Dzienniki zapisane przepływu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/

Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Informacje o strukturze hello hello dziennika można znaleźć [dziennika przepływu grupy zabezpieczeń sieci — omówienie](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Dowiedz się, jak za[wizualizacji NSG przepływu dzienników przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
