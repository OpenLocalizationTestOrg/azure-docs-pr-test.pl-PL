---
title: "aaaContinuous wdrożenie z aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Jak toosetup ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Ciągłe wdrażanie z aplikacji sieci Web platformy Azure w systemie Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

W tym samouczku, skonfiguruj ciągłe wdrażanie dla kontenera niestandardowego obrazu z zarządzanego [rejestru kontenera Azure](https://azure.microsoft.com/en-us/services/container-registry/) repozytoria lub [Centrum Docker](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Krok 1 — Logowanie tooAzure

Zaloguj się toohello portalu Azure w http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Krok 2 — Włączanie kontenera ciągłe wdrażanie funkcji

Można włączyć za pomocą funkcji ciągłego wdrażania hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonywania hello następujące polecenie

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

W hello ** [portalu Azure](https://portal.azure.com/)**, kliknij przycisk hello **usługi aplikacji** opcję na powitania po lewej stronie hello.

Kliknij nazwę hello interesujące tooconfigure Centrum Docker ciągłe wdrażanie dla aplikacji.

W hello **ustawień aplikacji**, dodaj aplikację nosi nazwę `DOCKER_ENABLE_CI` z wartością hello `true`.

![Wstaw obraz ustawienia aplikacji](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Krok 3 — Przygotowanie adresu URL elementu Webhook

Można uzyskać przy użyciu adresu URL elementu Webhook hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonywania hello następujące polecenie

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Dla adresu URL elementu Webhook hello, potrzebujesz hello toohave następującego punktu końcowego: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Można uzyskać z `publishingusername` i `publishingpwd` pobierając hello aplikacji sieci web Publikowanie profilu przy użyciu hello portalu Azure.

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Krok 4 — Dodaj haku sieci web

### <a name="azure-container-registry"></a>Azure Container Registry

W bloku portalu rejestru, kliknij **elementów Webhook**, Utwórz nowy element webhook, klikając **Dodaj**. W hello **tworzenia elementu webhook** bloku, nazwę użytkownika elementu webhook. Dla hello identyfikator URI elementu Webhook, potrzebujesz adresu URL hello tooprovide uzyskane z **krok 3**

Upewnij się, zdefiniuj zakres hello, jak hello repozytorium, który zawiera obraz kontenera.

![Wstaw obraz elementu webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Obraz powitania jest aktualizowana, hello aplikacji sieci web zostać zaktualizowane automatycznie z hello nowy obraz.

### <a name="docker-hub"></a>Centrum docker

Na stronie Centrum Docker kliknij **elementów Webhook**, następnie **tworzenia elementu WEBHOOK A**.

![Wstaw obraz dodawania elementu webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Dla hello adresu URL elementu Webhook, potrzebujesz adresu URL hello tooprovide uzyskane z **krok 3**

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Obraz powitania jest aktualizowana, hello aplikacji sieci web zostać zaktualizowane automatycznie z hello nowy obraz.

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](./app-service-linux-intro.md)
* [Rejestru kontenera platformy Azure](https://azure.microsoft.com/en-us/services/container-registry/)
* [Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-nodejs-pm2.md)
* [W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu platformy .NET Core](app-service-linux-using-dotnetcore.md)
* [W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu Ruby](app-service-linux-ruby-get-started.md)
* [Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-using-custom-docker-image.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](./app-service-linux-faq.md) 
* [Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu usługi Azure CLI 2.0](./app-service-linux-cli.md)



