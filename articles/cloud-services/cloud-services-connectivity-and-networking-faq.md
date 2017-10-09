---
title: "sieć i aaaConnectivity problemy dotyczące Microsoft Azure Cloud Services często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono hello często zadawane pytania dotyczące łączności i sieci dla usługi w chmurze Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemów dotyczących łączności i sieci dla usług Azure Cloud Services: często zadawane pytania (FAQ)

Ten artykuł zawiera często zadawane pytania dotyczące problemów dotyczących łączności i sieci dla [usługi w chmurze Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>I nie można zastrzec adresu IP w usłudze chmury wielu wirtualnych adresów IP
Najpierw upewnij się, że to wystąpienie maszyny wirtualnej hello, który próbujesz tooreserve hello IP dla jest włączony. Po drugie upewnij się, że używasz zastrzeżonych adresów IP dla obu hello wdrożeń tymczasowych i produkcyjnych. **Nie** ustawień hello podczas uaktualniania jest hello wdrożenia.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Jak Pulpit zdalny gdy grupa NSG?
Dodaj toohello reguły NSG, które zezwalają na ruch na portach **3389** i **20000**.  Pulpit zdalny używa portu **3389**.  Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować tooconnect wystąpienia, które do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i Zezwalaj na powitania klienta toosend pliku cookie protokołu RDP i określ tooconnect poszczególnych wystąpień do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.

## <a name="can-i-ping-a-cloud-service"></a>Czy można wywołać usługi w chmurze?

Nie, nie za pomocą hello Normalny "ping" / protokołu ICMP. Hello protokołu ICMP jest niedozwolone przez moduł równoważenia obciążenia Azure hello.

połączenie tootest, zaleca się wykonanie polecenia ping portu. Gdy Ping.exe korzysta z protokołu ICMP, innych narzędzi, takich jak narzędzia PSPing, Nmap i telnet Zezwalaj tootest łączności tooa określonym porcie TCP.

Aby uzyskać więcej informacji, zobacz [użyj polecenia ping portu zamiast tootest ICMP łączności maszyny Wirtualnej Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Jak zapobiec odbieranie tysięcy trafień z nieznanych adresów IP, które wskazują jakiegoś toohello ataku usługi w chmurze?
Azure implementuje tooprotect zabezpieczeń sieci wielowarstwowych jego usług platformy atakami rozproszone (DDoS) typu "odmowa usługi". Hello systemu obrony przed atakami DDoS Azure jest częścią systemu Azure ciągłego monitorowania procesu, który stale zwiększona testy penetracji. Ten system obrony przed atakami DDoS został zaprojektowany toowithstand ataków nie tylko z hello poza, ale także od innych dzierżawców Azure. Aby uzyskać więcej szczegółów, zobacz [zabezpieczenia sieci Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Można również utworzyć bloku tooselectively zadania uruchamiania niektórych z określonych adresów IP. Aby uzyskać więcej informacji, zobacz [zablokować określonego adresu IP](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Przy próbie wystąpienie usługi w chmurze toomy tooRDP komunikat Witaj, "upłynął konta użytkownika hello".
Po obejściu hello datę wygaśnięcia, który jest skonfigurowany w ustawieniach protokołu RDP, może otrzymywać hello komunikat o błędzie "upłynął to konto użytkownika". Data wygaśnięcia hello można zmienić z portalu hello, wykonaj następujące czynności:
1. Zaloguj się za toohello konsolą zarządzania platformy Azure (https://manage.windowsazure.com), przejdź tooyour usługi w chmurze i wybierz hello **Konfiguruj** kartę.
2. Wybierz **zdalnego**.
3. Zmień datę "Wygasa na" hello, a następnie zapisz hello konfiguracji.

Teraz powinno być możliwe tooRDP tooyour maszyny.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Dlaczego jest modułu równoważenia obciążenia nie równoważenia ruch równomiernie?
Aby uzyskać informacje o jak wewnętrzne działania usługi równoważenia obciążenia, zobacz [nowy tryb dystrybucji modułu równoważenia obciążenia w Azure](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

Hello dystrybucji algorytm używany jest krotka 5 (źródłowy adres IP, port źródłowy typ protokołu docelowy adres IP, port docelowy) skrótów toomap ruchu tooavailable serwerów. Zapewnia on lepkości tylko w ramach sesji transportu. Pakietów hello tej samej sesji TCP lub UDP zostanie przekierowany toohello wystąpienie tego samego centrum danych adresu IP (DIP) za punkt końcowy ze zrównoważonym obciążeniem hello. Powitania klienta zostanie zamknięte i ponownie otwiera hello połączenia lub uruchamia nową sesję hello sam źródłowy adres IP, port źródłowy hello zmiany i powoduje, że hello ruchu toogo tooa różnych DIP punktu końcowego.
