---
title: "Informacje dotyczące wymagań kryptograficznych i bram sieci VPN platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="43ee7-103">Informacje dotyczące wymagań kryptograficznych i bram sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43ee7-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="43ee7-104">W tym artykule opisano, jak można skonfigurować bramy sieci VPN platformy Azure do zaspokojenia wymagań kryptograficznych dla tuneli S2S VPN między lokalizacjami i połączeń między wirtualnymi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="43ee7-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="43ee7-105">Parametry zasad IPsec i IKE dla bram sieci VPN platformy Azure — informacje</span><span class="sxs-lookup"><span data-stu-id="43ee7-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="43ee7-106">Standardowego protokołu IPsec i IKE obsługuje szeroką gamę algorytmów kryptograficznych w różnych kombinacjach.</span><span class="sxs-lookup"><span data-stu-id="43ee7-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="43ee7-107">Jeśli klienci nie Żądaj określona kombinacja algorytmów kryptograficznych i parametrów, bram sieci VPN platformy Azure, użyj zestaw propozycji domyślne.</span><span class="sxs-lookup"><span data-stu-id="43ee7-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="43ee7-108">Ustawia zasady domyślne zostały wybrane do zmaksymalizowania współdziałanie z szeroką gamę urządzenia sieci VPN innych firm w domyślnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43ee7-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="43ee7-109">W związku z tym zasady i liczba propozycje nie obejmować wszystkich możliwych kombinacji dostępnych algorytmów kryptograficznych i kluczy sile.</span><span class="sxs-lookup"><span data-stu-id="43ee7-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="43ee7-110">Domyślne zasady ustawione dla bramy sieci VPN platformy Azure znajduje się w dokumencie: [urządzenia sieci VPN o i IPsec i IKE parametry połączenia bramy sieci VPN typu lokacja-lokacja](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="43ee7-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="43ee7-111">Wymagania dotyczące usług kryptograficznych</span><span class="sxs-lookup"><span data-stu-id="43ee7-111">Cryptographic requirements</span></span>
<span data-ttu-id="43ee7-112">Komunikacji, który wymaga parametrów lub algorytmy kryptograficzne zazwyczaj z powodu zgodności lub wymagania dotyczące zabezpieczeń klientów można teraz skonfigurować ich bramy sieci VPN platformy Azure do niestandardowych zasad IPsec i IKE za pomocą określonych algorytmów kryptograficznych i kluczy sile, a nie ustawia Azure domyślne zasady.</span><span class="sxs-lookup"><span data-stu-id="43ee7-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="43ee7-113">Na przykład zasady trybu głównego protokołu IKEv2 dla bram sieci VPN platformy Azure korzystać tylko Diffie-Hellman grupa 2 (1024 bity), natomiast klientów może być konieczne podanie silniejsze grupy do użycia w IKE, takich jak grupy 14 (2048-bitowego), 24 grupy (grupa MODP 2048-bitowego) lub ECP (krzywej eliptycznej grupy) bit 256 lub 384 (grupa 19 i 20 grupy odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="43ee7-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="43ee7-114">Podobne wymagania dotyczą również zasady IPsec trybu szybkiego.</span><span class="sxs-lookup"><span data-stu-id="43ee7-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="43ee7-115">Niestandardowe zasady IPsec i IKE z bram sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43ee7-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="43ee7-116">Bramy sieci VPN platformy Azure obsługuje teraz poszczególnych połączeń, zasad IPsec i IKE niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="43ee7-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="43ee7-117">Lokacja-lokacja lub połączenia do wirtualnymi można wybrać określoną kombinację algorytmów kryptograficznych dla protokołu IPsec i IKE żądaną siły kluczy, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="43ee7-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![zasady protokołu IPSec-ike](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="43ee7-119">Możesz utworzyć zasady IPsec i IKE i zastosować do nowego lub istniejącego połączenia.</span><span class="sxs-lookup"><span data-stu-id="43ee7-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="43ee7-120">Przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="43ee7-120">Workflow</span></span>

1. <span data-ttu-id="43ee7-121">Tworzenie sieci wirtualnych, bram sieci VPN lub bramy sieci lokalnej dla topologii łączności zgodnie z opisem w innych dokumenty z poradami</span><span class="sxs-lookup"><span data-stu-id="43ee7-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="43ee7-122">Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="43ee7-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="43ee7-123">Zasady można zastosować podczas tworzenia połączenia S2S lub do wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="43ee7-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="43ee7-124">Jeśli połączenie jest już utworzony, można zastosować lub zaktualizuj zasady do istniejącego połączenia</span><span class="sxs-lookup"><span data-stu-id="43ee7-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="43ee7-125">Zasady protokołu IPsec/IKE — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="43ee7-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="43ee7-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43ee7-126">Next steps</span></span>
<span data-ttu-id="43ee7-127">Zobacz [zasady IPsec/IKE skonfigurować](vpn-gateway-ipsecikepolicy-rm-powershell.md) instrukcje krok po kroku dotyczące konfigurowania niestandardowych zasad IPsec i IKE połączenia.</span><span class="sxs-lookup"><span data-stu-id="43ee7-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="43ee7-128">Zobacz też [podłączenie wielu urządzeń sieci VPN opartych na zasadach](vpn-gateway-connect-multiple-policybased-rm-ps.md) Aby dowiedzieć się więcej na temat opcji UsePolicyBasedTrafficSelectors.</span><span class="sxs-lookup"><span data-stu-id="43ee7-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>