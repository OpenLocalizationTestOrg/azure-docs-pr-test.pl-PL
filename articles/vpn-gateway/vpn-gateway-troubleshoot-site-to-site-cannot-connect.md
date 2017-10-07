---
title: "aaaTroubleshoot Azure połączenia sieci VPN lokacja lokacja nie może połączyć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot połączenia sieci VPN typu lokacja lokacja czy nagle przestanie działać i nie można ponownie."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Rozwiązywanie problemów: Nie można połączyć z połączenia sieci VPN typu lokacja lokacja Azure oraz przestaje działać

Po skonfigurowaniu połączenia VPN lokacja lokacja między siecią lokalną i sieci wirtualnej platformy Azure hello połączenia sieci VPN nagle przestanie działać i nie można ponownie. Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów

tooresolve hello problem, spróbuj najpierw zbyt[bramy sieci VPN platformy Azure hello resetowania](vpn-gateway-resetgw-classic.md) i zresetuj tunelu hello z hello lokalnego urządzenia sieci VPN. Jeśli hello problem będzie nadal występował, wykonaj te kroki tooidentify hello przyczyna problemu hello.

### <a name="prerequisite-step"></a>Krok wymagań wstępnych

Sprawdź typ hello hello bramy sieci VPN platformy Azure.

1. Przejdź toohello [portalu Azure](https://portal.azure.com).

2. Sprawdź hello **omówienie** strony bramy sieci VPN hello hello typu informacji.
    
    ![Omówienie hello bramy](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Krok 1. Sprawdź, czy jest zweryfikowany hello lokalnego urządzenia sieci VPN

1. Sprawdź, czy używasz [zweryfikowane urządzenia sieci VPN i wersję systemu operacyjnego](vpn-gateway-about-vpn-devices.md#devicetable). Witaj urządzenie nie jest zweryfikowany urządzenia sieci VPN, może zajść toosee producenta urządzenia hello toocontact występuje problem ze zgodnością.

2. Upewnij się, że urządzenia sieci VPN hello jest poprawnie skonfigurowana. Aby uzyskać więcej informacji, zobacz [Edytuj przykłady konfiguracji urządzenia](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Krok 2. Sprawdź hello klucza wspólnego

Porównaj hello klucza wspólnego dla hello lokalnej sieci VPN urządzenia toohello Azure wirtualnej sieci VPN toomake się, że klucze hello zgodne. 

tooview hello klucza wspólnego dla hello połączenia sieci VPN platformy Azure, użyj jednej z hello następujące metody:

**Witryna Azure Portal**

1. Przejdź połączenia lokacja lokacja bramy sieci VPN toohello, który został utworzony.

2. W hello **ustawienia** kliknij **klucz udostępniony**.
    
    ![Klucz współużytkowany](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Dla modelu wdrażania usługi Azure Resource Manager hello:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Dla hello klasycznego modelu wdrażania:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Krok 3. Sprawdź elementu równorzędnego sieci VPN hello adresów IP

-   Witaj, IP definicji w hello **bramy sieci lokalnej** obiektu w usłudze Azure powinna być zgodna IP urządzenia lokalne powitania.
-   Hello definicji IP bramy Azure, która jest ustawiona na powitania lokalnego urządzenia powinna być taka sama hello Azure brama IP.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Krok 4. Sprawdź przez i grupy NSG na powitania podsieci bramy

Sprawdź, czy i Usuń tras zdefiniowanych przez użytkownika (przez) lub grupy zabezpieczeń sieci (NSG) na powitania podsieć bramy, a następnie hello wyniku testu. Jeśli hello problem zostanie rozwiązany, sprawdź poprawność ustawień hello, które stosowane przez lub NSG.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Krok 5. Witaj wyboru lokalny adres interfejsu zewnętrznego urządzenia sieci VPN

- Jeśli hello adres internetowy IP urządzenia sieci VPN hello jest uwzględniona w hello **sieci lokalnej** definicji na platformie Azure, mogą występować sporadycznie rozłączeń.
- Witaj interfejsu zewnętrznego urządzenia musi być bezpośrednio na powitania Internet. Powinien to być nie translatora adresów sieciowych lub zapora między hello Internet i urządzenia hello.
- tooconfigure zapory klastrowania toohave wirtualnego adresu IP, należy przerwać hello klastra i ujawnia hello urządzenia sieci VPN bezpośrednio interfejs publiczny tooa tej bramy hello mogą łączyć się z.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Krok 6. Sprawdź, czy podsieci hello są takie same (Azure bramy oparte na zasadach)

-   Sprawdź, czy podsieci hello pasują dokładnie między hello sieci wirtualnej platformy Azure i definicje lokalne powitania sieci wirtualnej platformy Azure.
-   Sprawdź, czy podsieci hello pasują dokładnie między hello **bramy sieci lokalnej** i definicje sieci lokalne powitania lokalnymi.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Krok 7. Sprawdź sondy kondycji Azure bramy hello

1. Przejdź toohello [sondy kondycji](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Kliknij hello ostrzeżenia dotyczące certyfikatu.
3. Jeśli otrzymasz odpowiedź hello bramy sieci VPN jest uznawany za dobrej kondycji. Jeśli nie otrzymasz odpowiedź hello bramy może nie być w dobrej kondycji lub grupy NSG podsieci bramy hello jest przyczyną problemu hello. powitania po tekst jest przykładowa odpowiedź:

    &lt;? wersji xml = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">podstawowego: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / ciąg&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Krok 8. Sprawdź, czy hello lokalnego urządzenia sieci VPN ma włączoną funkcję doskonałego utajnienia hello

funkcja doskonałego utajnienia Hello może spowodować problemy rozłączenia. Jeśli urządzenia sieci VPN hello doskonałego utajnienia, należy wyłączyć funkcję hello. Następnie zaktualizuj zasady IPsec bramy sieci VPN hello.

## <a name="next-steps"></a>Następne kroki

-   [Skonfiguruj sieć wirtualną tooa połączenie lokacja lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Konfigurowanie zasad IPsec i IKE dla połączeń VPN lokacja lokacja](vpn-gateway-ipsecikepolicy-rm-powershell.md)
