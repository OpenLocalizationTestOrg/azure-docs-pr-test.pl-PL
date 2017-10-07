---
title: "Konfiguracja aaaSample — urządzenia Cisco ASA połączenie bramy sieci VPN tooAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera Przykładowa konfiguracja urządzenia Cisco ASA łączącego tooAzure bramy sieci VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Przykładowa konfiguracja: Cisco ASA urządzenia (BGP IKEv2/nie)
W tym artykule przedstawiono przykładowe konfiguracje dla urządzenia Cisco ASA łączenie tooAzure bramy sieci VPN.

## <a name="device-at-a-glance"></a>Urządzenia, w skrócie

|                        |                                   |
| ---                    | ---                               |
| Dostawca urządzenia          | Cisco                             |
| Model urządzenia           | ASA (adaptacyjnej zabezpieczeń urządzenia) |
| Wersja docelowa         | 8.4+                              |
| Przetestowany modelu           | 5505 ASA                          |
| Wersja przetestowany         | 9.2                               |
| Wersja IKE            | **Protokół IKEv2**                         |
| BGP                    | **Nie**                            |
| Typ bramy sieci VPN platformy Azure | **Oparte na trasach** bramy sieci VPN       |
|                        |                                   |

> [!NOTE]
> 1. Konfiguracja Hello poniżej łączy tooan urządzenia Cisco ASA Azure **opartej na trasach** bramy sieci VPN za pomocą niestandardowych zasad IPsec i IKE z opcją "UserPolicyBasedTrafficSelectors", zgodnie z opisem w [w tym artykule](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. Wymaga ASA urządzeń toouse **IKEv2** z konfiguracjami oparte na liście dostępu, nie VTI na podstawie.
> 3. Skontaktuj się z tooensure zasad hello jest obsługiwana na urządzeniach sieci VPN między lokalnymi specyfikację dostawcy urządzenia sieci VPN.

## <a name="vpn-device-requirements"></a>Wymagania dotyczące urządzeń sieci VPN
Bramy sieci VPN platformy Azure, użyj standardowe tunel S2S VPN tooestablish pakietów protokołu IPsec/IKE protokołu. Odwołuje się zbyt[urządzenia sieci VPN o](vpn-gateway-about-vpn-devices.md) dla hello szczegółowe parametry protokołu IPsec i IKE i domyślne algorytmów kryptograficznych dla bram sieci VPN platformy Azure. Opcjonalnie można określić kombinację dokładne hello algorytmów kryptograficznych i kluczy sile dla określonego połączenia, zgodnie z opisem w [o wymaganiach dotyczących kryptograficznych](vpn-gateway-about-compliance-crypto.md). W przypadku wybrania określona kombinacja algorytmów kryptograficznych i kluczy sile, upewnij się, używać hello specyfikacje odpowiedniego dla urządzenia sieci VPN.

## <a name="single-vpn-tunnel"></a>Jeden tunel VPN
Ta topologia składa się z jednego tunelu S2S VPN między bramą sieci VPN platformy Azure i lokalnego urządzenia sieci VPN. Opcjonalnie można skonfigurować protokołu BGP przez tunel VPN hello.

![jednego tunelu](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Odwołuje się zbyt[Instalatora jednego tunelu](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) szczegółowe instrukcje krok po kroku toobuild hello konfiguracji platformy Azure.

### <a name="network-and-vpn-gateway-information"></a>Informacji bramy sieci VPN i sieci
W tej sekcji znajduje się lista hello parametrów dla hello w tym przykładzie.

| **Parametr**                | **Wartość**                    |
| ---                          | ---                          |
| Prefiksy adresów sieci wirtualnej        | 10.11.0.0/16<br>10.12.0.0/16 |
| Adres IP bramy sieci VPN platformy Azure         | Azure_Gateway_Public_IP      |
| Prefiksy adresów lokalnych | 10.51.0.0/16<br>10.52.0.0/16 |
| Lokalny adres IP urządzenia sieci VPN    | OnPrem_Device_Public_IP     |
| * Numer ASN BGP sieci wirtualnej                | 65010                        |
| * Azure IP elementu równorzędnego protokołu BGP           | 10.12.255.30                 |
| * Lokalnymi BGP ASN         | 65050                        |
| * IP elementu równorzędnego BGP lokalnej     | 10.52.255.254                |
|                              |                              |

* (*) Parametry opcjonalne dla protokołu BGP tylko.

### <a name="ipsecike-policy--parameters"></a>Zasady protokołu IPsec/IKE & parametrów

Witaj w poniższej tabeli wymieniono hello Algorytmy IPsec/IKE i parametry używane w przykładowym hello. Zapoznaj się z toomake specyfikacje urządzenia sieci VPN się, że wszystkie algorytmy wymienione powyżej są obsługiwane przez modeli urządzenia sieci VPN i wersji oprogramowania układowego.

| **IPsec/IKEv2**  | **Wartość**                            |
| ---              | ---                                  |
| Szyfrowanie IKEv2 | AES256                               |
| Integralność IKEv2  | SHA384                               |
| Grupa DH         | DHGroup24                            |
| Szyfrowanie IPsec | AES256                               |
| Integralność IPsec  | SHA1                                 |
| Grupa PFS        | PFS24                                |
| Okres istnienia skojarzeń zabezpieczeń QM   | 7200 sekund                         |
| Selektor ruchu | UsePolicyBasedTrafficSelectors $True |
| Klucz wstępny   | PreSharedKey                         |
|                  |                                      |

- (*) Na niektórych urządzeniach integralności IPsec musi być "null", jeśli usługi GCM AES jest używany jako algorytmu szyfrowania IPsec.

### <a name="device-notes"></a>Informacje o urządzeniu

>[!NOTE]
>
> 1. Obsługa protokołu IKEv2 wymaga ASA wersji 8.4 i powyżej.
> 2. Obsługa grupa DH wyższej i PFS (poza grupy 5) wymaga wersji ASA 9.x.
> 3. Szyfrowanie protokołu IPsec z integralnością AES-GCM i IPsec z algorytmu SHA-256, SHA-384, obsługi algorytmu SHA-512 wymaga wersji ASA 9.x na sprzęcie ASA nowszej; 5505 ASA, 5510, 5520, 5540, 5550, są 5580 **nie** obsługiwane. (Sprawdź, czy hello dostawcy specyfikacje tooconfirm.)
>


### <a name="sample-device-configurations"></a>Przykład konfiguracji urządzeń
Poniższy skrypt Hello zapewnia Przykładowa konfiguracja na podstawie topologii hello i parametry wymienione powyżej. konfiguracja tunelu S2S VPN Hello składa się z hello następujące elementy:

1. Interfejsy & tras
2. Dostęp do listy
3. Parametry (fazy 1 lub trybu głównego) i zasad IKE
4. Parametry (faza 2 lub trybu szybkiego) i zasad protokołu IPsec
5. Inne parametry (TCP MSS ładunku itp.)

>[!IMPORTANT] 
>Upewnij się ukończyć hello dodatkowej konfiguracji wymienione poniżej i zastąp symbole zastępcze hello hello rzeczywiste wartości:
> 
> - Konfiguracja zarówno wewnątrz lub na zewnątrz interfejsów dla interfejsu
> - Trasy do sieci wewnętrznej i prywatnego oraz publicznego i na zewnątrz
> - Upewnij się, wszystkie nazwy i numery zasad są unikatowe w urządzeniu hello
> - Upewnij się, że algorytmy kryptograficzne hello są obsługiwane na urządzeniu
> - Zastąp powitania po symbole zastępcze hello rzeczywiste wartości.
>   - Poza Nazwa interfejsu: "poza"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - Sieć wirtualną i nazwy bramy sieci lokalnej (VNetName, LNGName)
>   - Prefiksy adresów sieci sieci wirtualnej i lokalnej
>   - Odpowiednie maski sieci

#### <a name="sample-configuration"></a>Przykładowa konfiguracja

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Prostych poleceń debugowania

Poniżej przedstawiono niektóre polecenia ASA na potrzeby debugowania:

1. Pokaż hello IPsec i IKE SA
    - "Pokaż szyfrowania ipsec sa"
    - "Pokaż kryptograficznego ikev2 sa"
2. Wprowadzanie tryb debugowania — to można uzyskać bardzo dużo na powitania konsoli
    - "debugowania ikev2 kryptograficznych platformy <level>"
    - "debug protokołu ikev2 kryptograficzny <level>"
3. Bieżące konfiguracje listy
    - "show uruchamiania" - pokazuje hello bieżące konfiguracje w urządzeniu hello; można użyć hello różnych określonych części toolist polecenia podrzędne hello konfiguracji. Np. "Pokaż Uruchom kryptograficznego", "Pokaż Uruchom listy dostępu", "Pokaż Uruchom tunelu group",... itd.


## <a name="next-steps"></a>Następne kroki
Zobacz [konfigurowania bramy sieci VPN aktywny-aktywny między lokalizacjami i połączeń między wirtualnymi do](vpn-gateway-activeactive-rm-powershell.md) procedury tooconfigure aktywny aktywny między lokalizacjami i połączeń do wirtualnymi.

