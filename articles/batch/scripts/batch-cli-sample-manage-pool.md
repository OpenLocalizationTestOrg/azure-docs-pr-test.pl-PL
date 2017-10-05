---
title: "Przykładowy skrypt Azure CLI — Zarządzanie pule w partii | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt Azure CLI — Zarządzanie pule w partii"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Zarządzanie pule partii zadań Azure z wiersza polecenia platformy Azure

Te skryptu przedstawia niektóre z narzędzi dostępnych w ramach wiersza polecenia platformy Azure, aby utworzyć i Zarządzaj pulami węzłów obliczeniowych w usługi partia zadań Azure.

> [!NOTE]
> Polecenia w tym przykładzie Tworzenie maszyn wirtualnych platformy Azure. Działających maszyn wirtualnych będą naliczane opłaty do Twojego konta. Aby zminimalizować tych opłat, Usuń maszyn wirtualnych po zakończeniu uruchamiania próbki. Zobacz [wyczyścić pule](#clean-up-pools).

Pule partii można skonfigurować na dwa sposoby z konfiguracji usługi w chmurze (tylko system Windows) lub konfiguracji maszyny wirtualnej (z systemem Windows i Linux). Przykładowe skrypty poniżej pokazano, jak utworzyć pule z obydwu konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj interfejs wiersza polecenia platformy Azure przy użyciu instrukcji w [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.
- Tworzenie konta usługi partia zadań, jeśli nie został wcześniej. Zobacz [Tworzenie konta usługi partia zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.
- Skonfigurować aplikację do uruchamiania z zadania uruchamiania, jeśli nie zostało to jeszcze zrobione. Zobacz [Dodawanie aplikacji do partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje pakietu aplikacji do platformy Azure.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Puli z skrypt przykładowy konfiguracji usługi chmury

[!code-azurecli[główne](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Zarządzaj pulami usługi w chmurze")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Puli z skrypt przykładowy konfiguracji maszyny wirtualnej

[!code-azurecli[główne](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Zarządzaj pulami maszyny wirtualnej")]

## <a name="clean-up-pools"></a>Oczyszczanie pul

Po uruchomieniu powyższy skrypt przykładowy należy uruchomić następujące polecenie, aby usunąć pule.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do tworzenia i modyfikowania pule partii.
Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.

| Polecenie | Uwagi |
|---|---|
| [AZ logowanie się na koncie usługi partia zadań](https://docs.microsoft.com/cli/azure/batch/account#login) | Uwierzytelnić konta usługi partia zadań.  |
| [Lista zbiorcza az partii aplikacji](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Lista dostępnych aplikacji w ramach konta usługi partia zadań.  |
| [Tworzenie puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#create) | Tworzenie puli maszyn wirtualnych.  |
| [zestaw puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#set) | Zaktualizuj właściwości puli.  |
| [Lista węzła — agent-jednostki SKU puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Agent dostępnego węzła listy jednostki SKU i informacje o obrazie.  |
| [Zmiana rozmiaru puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Zmień rozmiar liczba uruchomionych maszyn wirtualnych w określonej puli.  |
| [Pokaż puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#show) | Wyświetl właściwości puli.  |
| [Usuwanie puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Usuń określoną pulę.  |
| [Włączanie automatycznego skalowania puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Włącz automatyczne skalowanie w puli i zastosować formułę.  |
| [wyłączanie automatycznego skalowania puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Wyłącz automatyczne skalowanie w puli.  |
| [AZ partii węzła listy](https://docs.microsoft.com/cli/azure/batch/node#list) | Wyświetl listę wszystkich węźle obliczeń w określonej puli.  |
| [ponowny rozruch węzła partii az](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Ponowny rozruch węzła obliczeniowego określony.  |
| [Usuń węzeł partii az](https://docs.microsoft.com/cli/azure/batch/node#delete) | Usuń węzły wymienionych z określonej puli.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).

