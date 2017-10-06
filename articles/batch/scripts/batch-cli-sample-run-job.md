---
title: "Przykładowy skrypt interfejsu wiersza polecenia - uruchamiania zadania z instancją aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - uruchamiania zadania z partii"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Uruchomione zadania w partii zadań Azure z wiersza polecenia platformy Azure

Ten skrypt tworzy zadanie wsadowe i dodaje szereg zadań toohello zadania. Ponadto przedstawiono sposób toomonitor zadania i jego zadań. Na koniec pokazuje, jak tooquery hello usługa partia zadań wydajnie uzyskać informacji o zadaniach hello zadania.

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.
- Tworzenie konta usługi partia zadań, jeśli nie został wcześniej. Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.
- Jeśli nie zostało to jeszcze zrobione, należy skonfigurować toorun aplikacji z zadania uruchamiania. Zobacz [Dodawanie tooAzure aplikacji partii zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje tooAzure pakietu aplikacji.
- Skonfiguruj pulę, na które hello zadania. Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) przykładowego skryptu, który powoduje utworzenie puli z konfiguracji usługi chmury lub konfiguracji maszyny wirtualnej.

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Oczyszczanie zadania

Po uruchomieniu hello powyżej przykładowy skrypt uruchom następujące polecenie tooremove hello zadania i wszystkie jego zadań podrzędnych. Należy zauważyć, że pula hello będzie toobe usunąć oddzielnie. Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](./batch-cli-sample-manage-pool.md) Aby uzyskać więcej informacji na temat tworzenia i usuwania pule.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń w trybie wsadowym i zadania. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [AZ logowanie się na koncie usługi partia zadań](https://docs.microsoft.com/cli/azure/batch/account#login) | Uwierzytelnić konta usługi partia zadań.  |
| [Utwórz zadanie wsadowe az](https://docs.microsoft.com/cli/azure/batch/job#create) | Tworzy zadanie wsadowe.  |
| [Ustaw zadanie wsadowe az](https://docs.microsoft.com/cli/azure/batch/job#set) | Aktualizuje właściwości zadania wsadowego.  |
| [Pokaż zadania wsadowego az](https://docs.microsoft.com/cli/azure/batch/job#show) | Pobiera szczegóły określone zadanie wsadowe.  |
| [Utwórz zadanie wsadowe az](https://docs.microsoft.com/cli/azure/batch/task#create) | Dodaje toohello zadań określony zadania wsadowego.  |
| [Pokaż zadania wsadowego az](https://docs.microsoft.com/cli/azure/batch/task#show) | Pobiera hello szczegółów zadania z hello określone zadanie wsadowe.  |
| [Lista zadań wsadowych az](https://docs.microsoft.com/cli/azure/batch/task#list) | Zawiera listę zadań hello skojarzone z hello określonego zadania.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).
