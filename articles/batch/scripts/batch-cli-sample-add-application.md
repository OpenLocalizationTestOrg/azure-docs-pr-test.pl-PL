---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Dodawanie aplikacji w partii | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Dodawanie aplikacji w partii"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Dodawanie aplikacji tooAzure partii zadań z wiersza polecenia platformy Azure

Ten skrypt pokazuje, jak tooset aplikacji do użycia z puli partii zadań Azure lub zadania. tooset aplikacji, pakietu pliku wykonywalnego, oraz wszelkie zależności, do pliku zip. W zip pliku wykonywalnego hello przykład pliku o nazwie "Mój-aplikacji-exe.zip".

## <a name="prerequisites"></a>Wymagania wstępne

- Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.
- Tworzenie konta usługi partia zadań, jeśli nie został wcześniej. Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Oczyszczanie aplikacji

Po uruchomieniu hello powyżej przykładowy skrypt, uruchom następujące polecenia tooremove hello aplikacji i wszystkich jego pakietów przekazano aplikacji.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate polecenia aplikacji i przekazywanie pakietu aplikacji.
Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie aplikacji partii az](https://docs.microsoft.com/cli/azure/batch/application#create) | Tworzy aplikację.  |
| [zestaw aplikacji partii az](https://docs.microsoft.com/cli/azure/batch/application#set) | Aktualizuje właściwości aplikacji.  |
| [Utwórz pakiet aplikacji partii az](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Dodaje toohello pakietu aplikacji określonych aplikacji.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).
