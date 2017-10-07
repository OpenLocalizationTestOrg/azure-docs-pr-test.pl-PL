---
title: "aaaTroubleshoot Azure VPN lokacja-lokacja okresowo rozłącza | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot hello problem, w którego połączenia sieci VPN typu lokacja-lokacja hello regularnie odłączony."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Rozwiązywanie problemów: Azure VPN lokacja-lokacja rozłącza sporadycznie

Może wystąpić problem hello czy nowego lub istniejącego połączenia sieci VPN firmy Microsoft Azure punkt-lokacja nie jest stabilna lub odłącza regularnie. Ten artykuł zawiera Rozwiązywanie problemów z toohelp kroki identyfikowanie i rozwiązywanie hello przyczyną problemu hello. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów

### <a name="prerequisite-step"></a>Krok wymagań wstępnych

Sprawdź typ hello bramy sieci wirtualnej platformy Azure:

1. Przejdź za[portalu Azure](https://portal.azure.com).
2. Sprawdź hello **omówienie** strony bramy sieci wirtualnej hello hello typu informacji.
    
    ![Omówienie Hello hello bramy](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Krok 1 Sprawdź, czy hello lokalnie czy urządzenia sieci VPN został zweryfikowany.

1. Sprawdź, czy używasz [zweryfikowane urządzenia sieci VPN i wersję systemu operacyjnego](vpn-gateway-about-vpn-devices.md#devicetable). Witaj urządzenia sieci VPN nie jest weryfikowany, może zajść toosee producenta urządzenia hello toocontact istnieje jakikolwiek problem ze zgodnością.
2. Upewnij się, że urządzenia sieci VPN hello jest poprawnie skonfigurowana. Aby uzyskać więcej informacji, zobacz [przykłady konfiguracji urządzenia edytowania](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Krok 2 wyboru hello skojarzenia zabezpieczeń ustawienia (bramy oparte na zasadach sieci wirtualnej platformy Azure)

1. Upewnij się, że hello sieci wirtualnej, podsieci i zakresy w hello **bramy sieci lokalnej** definicji na platformie Microsoft Azure są takie same jak konfiguracja hello na powitania lokalnego urządzenia sieci VPN.
2. Sprawdź zgodnych ustawień hello skojarzenia zabezpieczeń.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Krok 3 wyboru dla tras zdefiniowanych przez użytkownika lub grupy zabezpieczeń sieci w podsieci bramy

Trasy zdefiniowane przez użytkownika na powitania podsieć bramy może ograniczanie część ruchu i stosowanie pozostałego ruchu. Dzięki temu są wyświetlane, czy połączenie sieci VPN hello jest zawodne dla niektórych ruchu i dobrej dla innych użytkowników. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Krok 4 wyboru Witaj "jeden tunel VPN na parę podsieć" (dla bram sieci wirtualnej na podstawie zasad)

Upewnij się, że hello lokalnego urządzenia sieci VPN jest ustawiona toohave **jeden tunel VPN na pary podsieci** dla bram sieci wirtualnej na podstawie zasad.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Sprawdź, czy krok 5 ograniczenia skojarzenia zabezpieczeń (dla bram sieci wirtualnej na podstawie zasad)

Brama sieci wirtualnej na podstawie zasad Hello ma limit 200 pary skojarzenia zabezpieczeń podsieci. Jeśli hello liczba podsieci sieci wirtualnej platformy Azure mnożona razy liczba podsieci lokalne powitania jest większe niż 200, zobacz sporadyczne podsieci rozłączeniem.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Krok 6 Sprawdź lokalne adres interfejsu zewnętrznego urządzenia sieci VPN

- Jeśli hello internetowy adres IP urządzenia sieci VPN hello jest uwzględniona w hello **bramy sieci lokalnej** definicji na platformie Azure, mogą występować sporadycznie rozłączeń.
- Witaj interfejsu zewnętrznego urządzenia musi być bezpośrednio na powitania Internet. Powinien istnieć nie translatora adresów sieciowych (NAT) lub zapora między hello Internet i urządzenia hello.
-  Jeśli skonfigurujesz klaster zapory toohave wirtualnego adresu IP, musi przerwać hello klastra i ujawnia hello urządzenia sieci VPN bezpośrednio tooa interfejs publiczny hello bramy mogą łączyć się z.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Krok 7 sprawdzanie, czy hello lokalnego urządzenia sieci VPN, ma doskonałego utajnienia włączone

Witaj **doskonałego utajnienia** funkcji może spowodować problemy rozłączenia hello. Jeśli urządzenie sieci VPN hello ma **doskonała utajnienie** włączyć, wyłączyć funkcję hello. Następnie [aktualizacji zasad protokołu IPsec bramy sieci wirtualnej hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Następne kroki

- [Konfigurowanie sieci wirtualnej tooa połączenia lokacja-lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Skonfiguruj zasady IPsec i IKE dla połączenia sieci VPN typu lokacja-lokacja](vpn-gateway-ipsecikepolicy-rm-powershell.md)

