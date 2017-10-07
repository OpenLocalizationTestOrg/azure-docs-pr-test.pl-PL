---
title: "aaaStage wdrożenie usługi chmury (Node.js) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Twojego tooa aplikacji Azure przemieszczania środowiska, następnie wdrożyć środowiska produkcyjnego tooa przy użyciu wirtualnego adresu IP (VIP) wymiany."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Przemieszczania aplikacji na platformie Azure
Opakowanej aplikacji mogą być wdrożone toohello przemieszczania środowiska Azure toobe przetestowane przed przeniesieniem produkcji toohello środowisko, w którym hello aplikacji jest dostępny na powitania Internet. Środowisko przejściowe jest dokładnie takie same jak hello środowiska produkcyjnego, ale można tylko hello dostępu przygotowanych aplikacji zaciemnionego adresu URL, który jest generowany przez usługę Azure. Po upewnieniu się, że aplikacja działa prawidłowo, może być wdrożony toohello środowiska produkcyjnego, wykonując wymiany wirtualnego adresu IP (VIP).

> [!NOTE]
> Witaj kroki opisane w tym artykule są stosowane tylko wtedy toonode hostowanych jako usługi w chmurze platformy Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Krok 1: Przemieszczanie aplikacji
To zadanie obejmuje jak hello toostage aplikacji przy użyciu **Microsoft Azure PowerShell**.

1. Podczas publikowania usługi, po prostu Przekaż hello **-gniazdo** parametru na powitania **Publish-AzureServiceProject** polecenia cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Zaloguj się na toohello [klasycznego portalu Azure] i wybierz **usługi w chmurze**. Po hello usługi w chmurze jest tworzona i hello **przemieszczania** kolumny Stan został zaktualizowany za**systemem**, kliknij nazwę usługi hello.
   
   ![Wyświetlanie działającej usłudze portalu][cloud-service]
3. Wybierz hello **pulpitu nawigacyjnego**, a następnie wybierz **przemieszczania**.
   
   ![pulpit nawigacyjny usługi w chmurze][cloud-service-dashboard]
4. Zanotuj wartość hello w hello **adres URL witryny** prawo toohello wpisu. Nazwa DNS Hello jest zaciemnionego wewnętrzny identyfikator, który wygenerował Azure.
   
    ![adres url witryny][cloud-service-staging-url]

Teraz można sprawdzić, czy aplikacja hello działa prawidłowo w hello przemieszczania środowiska przy użyciu hello przemieszczania adres URL witryny.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Krok 2: Uaktualnianie aplikacji w środowisku produkcyjnym przez Trwa zamienianie adresów VIP
Po zweryfikowaniu hello uaktualnionej wersji aplikacji w środowisku przemieszczania, można szybko udostępnić go w środowisku produkcyjnym przez zamianę hello wirtualnych adresów IP (VIP) hello środowisk przemieszczania i produkcji.

> [!NOTE]
> Tego kroku przyjęto założenie, że już wdrożone tooproduction aplikacji i przemieszczane hello uaktualnionej wersji aplikacji.
> 
> 

1. Zaloguj się do hello [klasycznego portalu Azure], kliknij przycisk **usługi w chmurze** , a następnie wybierz nazwę usługi hello.
2. Z hello **pulpitu nawigacyjnego**, wybierz pozycję **przemieszczania**, a następnie kliknij przycisk **wymiany** u dołu hello hello strony. Spowoduje to otwarcie hello okna dialogowego wymiany wirtualnych adresów IP.
   
   ![okno dialogowe wymiany adresów VIP][vip-swap-dialog]
3. Przejrzyj informacje hello, a następnie kliknij przycisk **OK**. Hello dwa wdrożenia Rozpocznij aktualizowanie jako hello przemieszczania wdrożenia przełączników tooproduction i hello produkcji wdrożenia przełączników toostaging.

Pomyślnie przemieszczane wdrożenia i uaktualnienia wdrożenia produkcyjnego przez zamianę wirtualne adresy IP z wdrożeniem hello tymczasowych.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Jak tooDeploy tooProduction uaktualnienia usługi przez zamianę wirtualne adresy IP na platformie Azure]

[klasycznego portalu Azure]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Jak tooDeploy tooProduction uaktualnienia usługi przez zamianę wirtualne adresy IP na platformie Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
