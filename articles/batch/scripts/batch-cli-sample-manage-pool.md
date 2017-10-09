---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Zarządzanie pule w partii | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Zarządzanie pule partii zadań Azure z wiersza polecenia platformy Azure

Te skrypt przedstawiono niektóre hello narzędzi dostępnych w ramach hello toocreate wiersza polecenia platformy Azure i Zarządzanie pulami węzłów obliczeniowych w hello usługi partia zadań Azure.

> [!NOTE]
> polecenia Hello w tym przykładzie Tworzenie maszyn wirtualnych platformy Azure. Działających maszyn wirtualnych będą naliczane opłaty tooyour konta. toominimize tych opłat, Usuń hello maszyn wirtualnych, po zakończeniu uruchomionych próbki hello. Zobacz [wyczyścić pule](#clean-up-pools).

Pule partii można skonfigurować na dwa sposoby z konfiguracji usługi w chmurze (tylko system Windows) lub konfiguracji maszyny wirtualnej (z systemem Windows i Linux). Przykładowe skrypty Hello poniżej pokazują, jak toocreate puli z obydwu konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.
- Tworzenie konta usługi partia zadań, jeśli nie został wcześniej. Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.
- Jeśli nie zostało to jeszcze zrobione, należy skonfigurować toorun aplikacji z zadania uruchamiania. Zobacz [Dodawanie tooAzure aplikacji partii zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje tooAzure pakietu aplikacji.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Puli z skrypt przykładowy konfiguracji usługi chmury

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Puli z skrypt przykładowy konfiguracji maszyny wirtualnej

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Oczyszczanie pul

Po uruchomieniu hello powyżej przykładowy skrypt należy uruchomić hello następujące polecenia toodelete hello pule.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń i manipulowania pule partii.
Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [AZ logowanie się na koncie usługi partia zadań](https://docs.microsoft.com/cli/azure/batch/account#login) | Uwierzytelnić konta usługi partia zadań.  |
| [Lista zbiorcza az partii aplikacji](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Lista dostępnych aplikacji hello w hello konta usługi partia zadań.  |
| [Tworzenie puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#create) | Tworzenie puli maszyn wirtualnych.  |
| [zestaw puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#set) | Zaktualizuj właściwości puli.  |
| [Lista węzła — agent-jednostki SKU puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Agent dostępnego węzła listy jednostki SKU i informacje o obrazie.  |
| [Zmiana rozmiaru puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Podana liczba hello zmiany rozmiaru działających maszyn wirtualnych w hello puli.  |
| [Pokaż puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#show) | Wyświetl właściwości hello puli.  |
| [Usuwanie puli partii az](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Usuń hello określonej puli.  |
| [Włączanie automatycznego skalowania puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Włącz automatyczne skalowanie w puli i zastosować formułę.  |
| [wyłączanie automatycznego skalowania puli partii az](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Wyłącz automatyczne skalowanie w puli.  |
| [AZ partii węzła listy](https://docs.microsoft.com/cli/azure/batch/node#list) | Lista wszystkich hello węźle obliczeń w hello określonej puli.  |
| [ponowny rozruch węzła partii az](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Ponowny rozruch węzła obliczeniowego określonego hello.  |
| [Usuń węzeł partii az](https://docs.microsoft.com/cli/azure/batch/node#delete) | Usuń węzły hello wymienione z hello określone puli.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).

