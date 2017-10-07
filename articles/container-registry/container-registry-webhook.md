---
title: "elementów webhook rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft"
description: "Elementów webhook rejestru kontenera platformy Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker kontenerów, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Za pomocą elementów webhook rejestru kontenera Azure - Azure portal

Rejestru kontenera platformy Azure przechowywanych i zarządzanych obrazów prywatnej kontenera Docker, podobnie toohello Centrum Docker przechowuje publiczny obrazy usługi Docker. Możesz użyć zdarzenia tootrigger elementów webhook, gdy pewne akcje została wykonana w jednym z repozytoriami rejestru. Elementów Webhook mogą odpowiadać tooevents na poziomie rejestru hello lub może być zakres dół tooa repozytorium określonego tagu. 

Więcej tła i pojęć, zobacz hello [omówienie](./container-registry-intro.md).

## <a name="prerequisites"></a>Wymagania wstępne 

- Kontenera platformy Azure zarządzanych rejestru — Tworzenie rejestru kontenera zarządzanych w Twojej subskrypcji platformy Azure. Na przykład użyć hello portalu Azure lub hello Azure CLI 2.0. 
- Docker CLI - tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, należy zainstalować aparatem platformy Docker. 

## <a name="create-webhook-azure-portal"></a>Tworzenie elementu webhook w portalu Azure

1. Zaloguj się za toohello portalu Azure i przejdź toohello rejestru, w której ma zostać toocreate elementów webhook. 

2. W bloku kontenera hello wybierz kartę "Elementów Webhook" hello. 

3. Wybierz "Dodaj" hello elementu webhook bloku narzędzi. 

4. Zakończenie hello *tworzenia elementu Webhook* formularza z hello następujących informacji:

| Wartość | Opis |
|---|---|
| Nazwa | Nazwa Hello ma toogive toohello webhook. Może zawierać tylko małe litery i cyfry oraz od 5 do 50 znaków. |
| Identyfikator URI usługi | Witaj gdzie hello webhook wysłać powiadomienia POST identyfikator URI. |
| Niestandardowe nagłówki | Nagłówki ma toopass wraz z hello wysłanie żądania POST. Należy je w "klucz: wartość" format. |
| Akcje wyzwalacza | Akcje wyzwalających hello elementu webhook. Obecnie elementów webhook może zostać wyzwolone przez wypychania i/lub Usuń obraz tooan akcje. |
| Stan | Stan Hello hello webhook po jego utworzeniu. Jest ona włączona domyślnie. |
| Zakres | Hello zakresu, na który hello działa elementu webhook. Zakres hello jest domyślnie dla wszystkich zdarzeń w rejestrze hello. Można ją określić repozytorium lub tag przy użyciu formatu hello "repozytorium: tag". |

Przykład elementu webhook formularza:

![DCOS INTERFEJSU UŻYTKOWNIKA](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Tworzenie elementu webhook wiersza polecenia platformy Azure

toocreate przy użyciu elementu webhook hello interfejsu wiersza polecenia Azure, użyj hello [tworzenia elementu webhook acr az](/cli/azure/acr/webhook#create) polecenia.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Element webhook testu

### <a name="azure-portal"></a>Azure Portal

Wcześniejsze toousing webhook hello w kontenerze obrazu wypychania i akcje usuwania, można zbadać, przy użyciu hello **Ping** przycisku. W przypadku hello Ping wysyła toohello żądania post ogólnego określony punkt końcowy i dzienniki hello odpowiedzi. Jest to przydatne tooverify, który hello elementu webhook nie został skonfigurowany poprawnie.

1. Wybierz hello elementu webhook ma tootest. 
2. W górnym pasku narzędzi hello wybierz akcję "Wyślij polecenie Ping" hello. 
3. Sprawdź hello żądań i odpowiedzi.

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

tootest element webhook ACR z hello Azure CLI Użyj hello [az acr elementu webhook ping](/cli/azure/acr/webhook#ping) polecenia.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

wyniki hello toosee, użyj hello [webhook acr az listy zdarzenia](/cli/azure/acr/webhook#list-events) polecenia. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Usuń element webhook

### <a name="azure-portal"></a>Azure Portal

Każdy element webhook może zostać usunięta przez wybranie elementu webhook hello, a następnie przycisk Usuń hello na powitania portalu Azure.

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```