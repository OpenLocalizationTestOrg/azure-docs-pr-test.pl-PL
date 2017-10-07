---
title: "aaaAbout wymagania dotyczące szyfrowania i bram sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono wymagania dotyczące szyfrowania i bram sieci VPN platformy Azure"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Informacje dotyczące wymagań kryptograficznych i bram sieci VPN platformy Azure

W tym artykule opisano, jak konfigurować toosatisfy bram sieci VPN platformy Azure wymagań kryptograficznych dla tuneli S2S VPN między lokalizacjami i połączeń między wirtualnymi na platformie Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Parametry zasad IPsec i IKE dla bram sieci VPN platformy Azure — informacje
Standardowego protokołu IPsec i IKE obsługuje szeroką gamę algorytmów kryptograficznych w różnych kombinacjach. Jeśli klienci nie Żądaj określona kombinacja algorytmów kryptograficznych i parametrów, bram sieci VPN platformy Azure, użyj zestaw propozycji domyślne. Ustawia zasady domyślne Hello wybrano toomaximize współdziałanie z szeroką gamę urządzenia sieci VPN innych firm w domyślnej konfiguracji. W związku z tym hello zasady i liczba hello propozycje nie obejmuje wszystkich możliwych kombinacji dostępnych algorytmów kryptograficznych i kluczy sile.

Witaj zasady domyślne ustawienie dla bramy sieci VPN platformy Azure znajduje się w dokumencie hello: [urządzenia sieci VPN o i IPsec i IKE parametry połączenia bramy sieci VPN typu lokacja-lokacja](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Wymagania dotyczące usług kryptograficznych
Komunikacji, który wymaga parametrów lub algorytmy kryptograficzne zwykle ze względu na wymagania toocompliance lub zabezpieczeń, klientów można teraz skonfigurować ich toouse bram sieci VPN platformy Azure niestandardowych zasad IPsec i IKE z określonymi kryptograficznych algorytmy i sile klucza, a nie hello Azure domyślne zasady zestawy.

Na przykład hello zasady trybu głównego protokołu IKEv2 dla bram sieci VPN platformy Azure korzystać tylko Diffie-Hellman grupa 2 (1024 bity), klienci mogą powinny toospecify silniejszych toobe grupy używane w IKE, takie jak grupy 14 (2048-bitowego), 24 grupy (grupa MODP 2048-bitowego) lub ECP (elliptic krzywą grup) bit 256 lub 384 (grupa 19 i 20 grupy odpowiednio). Podobne wymagania zastosować także zasady trybu szybkiego tooIPsec.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Niestandardowe zasady IPsec i IKE z bram sieci VPN platformy Azure
Bramy sieci VPN platformy Azure obsługuje teraz poszczególnych połączeń, zasad IPsec i IKE niestandardowych. Lokacja-lokacja lub połączenia do wirtualnymi można wybrać określona kombinacja algorytmów kryptograficznych dla protokołu IPsec i IKE hello potrzeby siły kluczy, jak pokazano w hello poniższy przykład:

![zasady protokołu IPSec-ike](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Możesz utworzyć zasady IPsec i IKE i zastosować tooa nowego lub istniejącego połączenia. 

### <a name="workflow"></a>Przepływ pracy

1. Tworzenie sieci wirtualnych hello, bram sieci VPN lub bramy sieci lokalnej dla topologii łączności zgodnie z opisem w innych toodocuments jak
2. Tworzenie zasad IPsec i IKE
3. Hello zasad można zastosować podczas tworzenia połączenia S2S lub do wirtualnymi
4. Jeśli połączenie hello jest już utworzony, można zastosować lub zaktualizować hello zasad tooan istniejącego połączenia


## <a name="ipsecike-policy-faq"></a>Zasady protokołu IPsec/IKE — często zadawane pytania

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Następne kroki
Zobacz [zasady IPsec/IKE skonfigurować](vpn-gateway-ipsecikepolicy-rm-powershell.md) instrukcje krok po kroku dotyczące konfigurowania niestandardowych zasad IPsec i IKE połączenia.

Zobacz też [podłączenie wielu urządzeń sieci VPN opartych na zasadach](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn więcej informacji na temat hello UsePolicyBasedTrafficSelectors opcji.
