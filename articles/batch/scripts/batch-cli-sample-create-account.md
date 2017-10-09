---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz konto wsadowe | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie konta usługi partia zadań"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Tworzenie konta usługi partia zadań z hello wiersza polecenia platformy Azure

Ten skrypt tworzy konto partii zadań Azure i przedstawia różne właściwości konta hello można zbadać i aktualizacji.

## <a name="prerequisites"></a>Wymagania wstępne

Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.

## <a name="batch-account-sample-script"></a>Skrypt przykładowy konta

Podczas tworzenia konta usługi partia zadań domyślnie jego węzły obliczeniowe są przypisywane wewnętrznie przez hello usługa partia zadań. Węzły obliczeniowe przydzielone będzie limit przydziału rdzeni oddzielnych tooa podmiotu i hello konta mogą być uwierzytelniane za pośrednictwem klucza wspólnego poświadczeń lub Azure Active Dirctory token.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Przy użyciu skryptu próbki subskrypcji użytkownika konta usługi partia zadań

Można również włączyć toohave partii utworzyć jego węzłów obliczeniowych w ramach własnej subskrypcji platformy Azure.
Konta, które przydzielić obliczeniowe węzłów w ramach subskrypcji, musi zostać uwierzytelniony za pośrednictwem tokenu programu Azure Active Directory i węzły obliczeniowe hello przydzielone są zliczane limitu przydziału subskrypcji. toocreate konto w tym trybie, co należy określić odwołanie Key Vault podczas tworzenia konta hello.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu albo hello powyżej przykładowe skrypty, uruchom następujące polecenie tooremove hello grupy zasobów i wszystkie powiązane zasoby (w tym konta wsadowego, konta usługi Azure Storage i Azure magazynów kluczy).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupy zasobów konta usługi partia zadań i wszystkie powiązane zasoby. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie konta usługi partia zadań az](https://docs.microsoft.com/cli/azure/batch/account#create) | Tworzy hello konta usługi partia zadań.  |
| [Ustaw konto wsadowe az](https://docs.microsoft.com/cli/azure/batch/account#set) | Aktualizuje właściwości hello konta usługi partia zadań.  |
| [Pokaż konto wsadowe az](https://docs.microsoft.com/cli/azure/batch/account#show) | Pobiera szczegóły hello określić konta usługi partia zadań.  |
| [Lista kluczy konta zadań wsadowych az](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Pobiera klucze dostępu hello hello określić konta usługi partia zadań.  |
| [AZ logowanie się na koncie usługi partia zadań](https://docs.microsoft.com/cli/azure/batch/account#login) | Uwierzytelnia określony hello partii konta dla dalszego interakcja interfejsu wiersza polecenia.  |
| [Tworzenie konta magazynu az](https://docs.microsoft.com/cli/azure/storage/account#create) | Tworzy konto magazynu. |
| [Utwórz az keyvault](https://docs.microsoft.com/cli/azure/keyvault#create) | Tworzy magazyn kluczy. |
| [keyvault az set-policy.](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Zaktualizuj zasady zabezpieczeń hello hello określonego klucza magazynu. |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/group#delete) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).
