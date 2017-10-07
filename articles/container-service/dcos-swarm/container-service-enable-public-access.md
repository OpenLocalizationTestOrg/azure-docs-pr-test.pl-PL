---
title: "aaaEnable dostępu tooAzure DC/OS kontenera aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tooenable publiczny dostęp do kontenerów tooDC/OS usługi kontenera platformy Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Włączenie aplikacji usługi kontenera platformy Azure tooan dostępu publicznego
Każdy kontener DC/OS w hello ACS [puli agenta publicznego](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) jest automatycznie narażonych toohello internet. Domyślnie porty **80**, **443**, **8080** są otwarte i każdy kontener (publicznych) nasłuchuje na te porty są dostępne. W tym artykule opisano, jak tooopen więcej portów dla aplikacji w usłudze kontenera platformy Azure.

## <a name="open-a-port-portal"></a>Otwórz port (portal)
Najpierw należy tooopen hello portu, którą chcemy udostępnić.

1. Zaloguj się w portalu toohello.
2. Znajdź grupę zasobów hello, która została wdrożona hello usługi kontenera platformy Azure.
3. Wybierz moduł równoważenia obciążenia agenta hello (który nosi nazwę podobne zbyt**XXXX-agent-lb-XXXX**).
   
    ![Moduł równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Kliknij przycisk **sondy** , a następnie **dodać**.
   
    ![Sondy modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-probe.png)
5. Wypełnij formularz sondowania hello, a następnie kliknij przycisk **OK**.
   
   | Pole | Opis |
   | --- | --- |
   | Nazwa |Nazwa opisowa hello sondowania. |
   | Port |port Hello hello tootest kontenera. |
   | Ścieżka |(Podczas w trybie HTTP) hello tooprobe ścieżki względnej witryny sieci Web. Protokół HTTPS nie jest obsługiwane. |
   | Interwał |próbuje Hello ilość czasu między sondowania, w sekundach. |
   | Próg złej kondycji |Liczba kolejnych sondowania prób przed uwzględnieniu kontenera hello złej kondycji. |
6. W hello właściwości usługi równoważenia obciążenia agenta hello, kliknij przycisk **reguły równoważenia obciążenia** , a następnie **Dodaj**.
   
    ![Reguły modułu równoważenia obciążenia usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Wypełnij formularz usługi równoważenia obciążenia hello, a następnie kliknij przycisk **OK**.
   
   | Pole | Opis |
   | --- | --- |
   | Nazwa |Nazwa opisowa hello modułu równoważenia obciążenia. |
   | Port |port publiczny przychodzące Hello. |
   | Port zaplecza |port wewnętrzny publicznego Hello hello kontenera tooroute ruchu do. |
   | Puli wewnętrznej bazy danych |kontenery Hello w tej puli będzie hello docelowej dla tej usługi równoważenia obciążenia. |
   | Sondy |Witaj toodetermine sondowania używany, jeśli obiektem docelowym hello **puli zaplecza** jest w dobrej kondycji. |
   | Trwałość sesji |Określa sposób obsługi ruchu w kliencie na czas trwania hello hello sesji.<br><br>**Brak**: kolejne żądania z tego samego klienta mogą być obsługiwane przez każdy kontener hello.<br>**Klient IP**: kolejne żądania z tego samego adresu IP klienta są obsługiwane przez hello hello tego samego kontenera.<br>**Klient IP i protokół**: kolejne żądania z samej kombinacji adresu IP i Protokół klienta są obsługiwane przez hello hello tego samego kontenera. |
   | Limit czasu bezczynności |(Tylko TCP) (W minutach) hello tookeep czasu klienta TCP/HTTP otwarty bez polegania na *keep-alive* wiadomości. |

## <a name="add-a-security-rule-portal"></a>Dodawanie reguły zabezpieczeń (portal)
Następnie muszą tooadd regułę zabezpieczeń, który przekierowuje ruch z naszych otwarty port przez zaporę Windows hello.

1. Zaloguj się w portalu toohello.
2. Znajdź grupę zasobów hello, która została wdrożona hello usługi kontenera platformy Azure.
3. Wybierz hello **publicznego** agenta sieciowej grupy zabezpieczeń (który nosi nazwę podobne zbyt**XXXX-agent publicznego nsg-XXXX**).
   
    ![Grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. Wybierz **reguły zabezpieczeń dla ruchu przychodzącego** , a następnie **Dodaj**.
   
    ![Reguły grupy zabezpieczeń sieci usługi kontenera platformy Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Wypełnianie tooallow reguły zapory hello port publiczny i kliknij przycisk **OK**.
   
   | Pole | Opis |
   | --- | --- |
   | Nazwa |Nazwę opisową hello reguły zapory. |
   | Priorytet |Priorytet rangę hello reguły. Witaj niższe hello numer hello wyższy hello priorytet. |
   | Element źródłowy |Ogranicz hello przychodzące IP adres zakresu toobe dozwolony lub odrzucany przez tę regułę. Użyj **żadnych** toonot określ ograniczenie. |
   | Usługa |Wybierz zestaw wstępnie zdefiniowanych usług, których dotyczy ta zasada zabezpieczeń. W przeciwnym razie użyj **niestandardowy** toocreate własne. |
   | Protokół |Ograniczanie ruchu na podstawie **TCP** lub **UDP**. Użyj **żadnych** toonot określ ograniczenie. |
   | Zakres portów |Gdy **usługi** jest **niestandardowe**, określa hello zakres portów, które ma wpływ ta reguła. Można użyć jednego portu, takich jak **80**, lub zakres, takich jak **1024 1500**. |
   | Akcja |Zezwalaj lub Odmów ruchu, który spełnia kryteria hello. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello różnica między [publiczne i prywatne agentów DC/OS](container-service-dcos-agents.md).

Przeczytaj więcej informacji na temat [Zarządzanie kontenerów DC/OS](container-service-mesos-marathon-ui.md).

