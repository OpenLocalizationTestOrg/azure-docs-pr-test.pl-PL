---
title: "aaaApplication lub usługi Marathon specyficzne dla użytkownika | Dokumentacja firmy Microsoft"
description: "Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, Marathon, mikrousługi, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika
Usługa kontenera platformy Azure oferuje zestaw serwerów głównych, na których wstępnie konfigurujemy usługi Apache Mesos i Marathon. Mogą to być tooorchestrate używanych aplikacji na powitania klastra, ale najlepiej nie toouse hello serwerów głównych, w tym celu. Na przykład Dostosowywanie konfiguracji hello usługi Marathon wymaga logowania do serwerów głównych hello się i wprowadzania zmian — to unikatowych serwerów głównych, które są nieco inne niż standardowe hello i toobe należy zapewnić opiekę i zarządzanie nimi niezależnie od siebie. Ponadto Konfiguracja hello wymagana przez jeden zespół może nie być hello konfiguracją optymalną dla innego zespołu.

W tym artykule wyjaśniamy sposób tooadd usługi Marathon dla aplikacji lub specyficzne dla użytkownika.

Ponieważ usługa ta będzie należeć tooa jednego użytkownika lub zespołu, są one wolnego tooconfigure w dowolny sposób, że chcą mieć. Usługi kontenera platformy Azure będzie upewnij się również, że usługa hello nadal toorun. W przypadku niepowodzenia usługi hello będzie Uruchom usługi kontenera platformy Azure. W większości przypadków hello nie nawet widać, że miała przestoju.

## <a name="prerequisites"></a>Wymagania wstępne
[Wdróż wystąpienie usługi kontenera platformy Azure](container-service-deployment.md) z programem orchestrator wpisz DC/OS i [upewnij się, że klient połączenie klastra tooyour](../container-service-connect.md). Ponadto hello następujące kroki.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika
Rozpocznij od utworzenia pliku konfiguracji JSON, który definiuje nazwę hello hello usługi aplikacji, które mają toocreate. W tym miejscu użyjemy `marathon-alice` jako nazwa struktury hello. Zapisz plik hello jako przypominać `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Następnie użyj wystąpienie hello tooinstall hello interfejsu wiersza polecenia DC/OS usługi Marathon z opcjami hello, które są ustawione w pliku konfiguracji:

```bash
dcos package install --options=marathon-alice.json marathon
```

Powinien zostać wyświetlony z `marathon-alice` usługa jest uruchomiona hello karcie usług interfejsu użytkownika DC/OS. Witaj interfejs użytkownika zostanie `http://<hostname>/service/marathon-alice/` Jeśli chcesz tooaccess go bezpośrednio.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Ustaw tooaccess interfejsu wiersza polecenia DC/OS hello hello usługę
Opcjonalnie można skonfigurować sieci tooaccess interfejsu wiersza polecenia DC/OS nowej usługi przez ustawienie hello `marathon.url` toohello toopoint właściwości `marathon-alice` wystąpienia w następujący sposób:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Możesz sprawdzić, którego wystąpienia usługi Marathon, czy interfejs wiersza polecenia działa z hello przed `dcos config show` polecenia. Możesz przywrócić toousing głównej usługi Marathon przy użyciu polecenia hello `dcos config unset marathon.url`.

