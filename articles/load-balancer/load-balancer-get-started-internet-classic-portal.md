---
title: "równoważenia obciążenia aaaCreate internetowy - klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia przy użyciu modelu wdrażania klasycznego hello klasycznego portalu Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Rozpocząć tworzenie internetowy modułu równoważenia obciążenia (klasyczne) w hello klasycznego portalu Azure

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny. Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md). Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu. W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Konfigurowanie dostępnego z Internetu modułu równoważenia obciążenia do maszyn wirtualnych

Kolejność tooload równowagi ruchu w sieci z hello Internet między maszynami wirtualnymi hello usługi w chmurze należy utworzyć zestawu z równoważeniem obciążenia. W tej procedurze założono, że utworzono już hello maszyn wirtualnych oraz czy są one wszystkich w hello sama usługa w chmurze.

**tooconfigure zestaw z równoważeniem obciążenia dla maszyn wirtualnych**

1. W hello klasycznego portalu Azure, kliknij przycisk **maszyn wirtualnych**, a następnie kliknij nazwę hello maszyny wirtualnej w zestawie o zrównoważonym obciążeniu hello.
2. Kliknij kolejno opcje **Punkty końcowe** i **Dodaj**.
3. Na powitania **Dodaj maszynę wirtualną punktu końcowego tooa** kliknij strzałkę w prawo hello.
4. Na powitania **Określ szczegóły hello punktu końcowego hello** strony:

   * W **nazwa**, wpisz nazwę dla punktu końcowego hello, lub wybierz nazwę hello z hello listy wstępnie zdefiniowanych punktów końcowych dla wspólnych protokołów.
   * W **protokołu**, wybierz protokół hello wymagany przez typ hello punktu końcowego TCP lub UDP, zgodnie z potrzebami.
   * W **portu publicznego i prywatnego**, wpisz numery portów hello, który ma hello toouse maszyny wirtualnej, zgodnie z potrzebami. Można użyć hello port prywatny i reguły zapory na powitania ruchu tooredirect maszyny wirtualnej w taki sposób, który jest odpowiedni dla twojej aplikacji. port prywatny Hello można hello w taki sam jak port publiczny hello. Na przykład dla punktu końcowego dla ruchu w sieci web (HTTP), można przypisać portu 80 tooboth hello publicznych i prywatnych portów.

5. Wybierz **Utwórz zestaw o zrównoważonym obciążeniu**, a następnie kliknij przycisk strzałki w prawo hello.
6. Na powitania **skonfigurować zestaw z równoważeniem obciążenia hello** strony, wpisz nazwę zestawu o zrównoważonym obciążeniu hello, a następnie przypisz wartości hello sondowania zachowanie hello moduł równoważenia obciążenia Azure. Witaj moduł równoważenia obciążenia używa toodetermine sond hello maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello są dostępne tooreceive ruchu przychodzącego.
7. Kliknij przycisk endpoint hello znacznik wyboru toocreate hello równoważeniem obciążenia. Zobaczysz **tak** w hello **Nazwa zestawu o zrównoważonym obciążeniu** kolumny hello **punkty końcowe** strony hello maszyny wirtualnej.
8. W portalu powitania kliknij **maszyn wirtualnych**, kliknij nazwę hello dodatkowe maszyny wirtualnej w zestawie o zrównoważonym obciążeniu hello, kliknij przycisk **punkty końcowe**, a następnie kliknij przycisk **Dodaj**.
9. Na powitania **Dodaj maszynę wirtualną punktu końcowego tooa** kliknij przycisk **Dodawanie punktu końcowego tooan równoważeniem obciążenia zestawu**, wybierz nazwę hello hello zestawu z równoważeniem obciążenia, a następnie kliknij strzałkę w prawo hello.
10. Na powitania **Określ szczegóły hello punktu końcowego hello** , wpisz nazwę dla punktu końcowego hello, a następnie kliknij przycisk znacznika wyboru hello.

Witaj dodatkowych maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello Powtórz kroki od 8-10.

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
