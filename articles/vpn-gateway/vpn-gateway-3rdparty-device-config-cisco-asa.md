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
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="ddc80-103">Przykładowa konfiguracja: Cisco ASA urządzenia (BGP IKEv2/nie)</span><span class="sxs-lookup"><span data-stu-id="ddc80-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="ddc80-104">W tym artykule przedstawiono przykładowe konfiguracje dla urządzenia Cisco ASA łączenie tooAzure bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ddc80-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="ddc80-105">Urządzenia, w skrócie</span><span class="sxs-lookup"><span data-stu-id="ddc80-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="ddc80-106">Dostawca urządzenia</span><span class="sxs-lookup"><span data-stu-id="ddc80-106">Device vendor</span></span>          | <span data-ttu-id="ddc80-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="ddc80-107">Cisco</span></span>                             |
| <span data-ttu-id="ddc80-108">Model urządzenia</span><span class="sxs-lookup"><span data-stu-id="ddc80-108">Device model</span></span>           | <span data-ttu-id="ddc80-109">ASA (adaptacyjnej zabezpieczeń urządzenia)</span><span class="sxs-lookup"><span data-stu-id="ddc80-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="ddc80-110">Wersja docelowa</span><span class="sxs-lookup"><span data-stu-id="ddc80-110">Target version</span></span>         | <span data-ttu-id="ddc80-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="ddc80-111">8.4+</span></span>                              |
| <span data-ttu-id="ddc80-112">Przetestowany modelu</span><span class="sxs-lookup"><span data-stu-id="ddc80-112">Tested model</span></span>           | <span data-ttu-id="ddc80-113">5505 ASA</span><span class="sxs-lookup"><span data-stu-id="ddc80-113">ASA 5505</span></span>                          |
| <span data-ttu-id="ddc80-114">Wersja przetestowany</span><span class="sxs-lookup"><span data-stu-id="ddc80-114">Tested version</span></span>         | <span data-ttu-id="ddc80-115">9.2</span><span class="sxs-lookup"><span data-stu-id="ddc80-115">9.2</span></span>                               |
| <span data-ttu-id="ddc80-116">Wersja IKE</span><span class="sxs-lookup"><span data-stu-id="ddc80-116">IKE version</span></span>            | <span data-ttu-id="ddc80-117">**Protokół IKEv2**</span><span class="sxs-lookup"><span data-stu-id="ddc80-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="ddc80-118">BGP</span><span class="sxs-lookup"><span data-stu-id="ddc80-118">BGP</span></span>                    | <span data-ttu-id="ddc80-119">**Nie**</span><span class="sxs-lookup"><span data-stu-id="ddc80-119">**No**</span></span>                            |
| <span data-ttu-id="ddc80-120">Typ bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ddc80-120">Azure VPN gateway type</span></span> | <span data-ttu-id="ddc80-121">**Oparte na trasach** bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="ddc80-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="ddc80-122">Konfiguracja Hello poniżej łączy tooan urządzenia Cisco ASA Azure **opartej na trasach** bramy sieci VPN za pomocą niestandardowych zasad IPsec i IKE z opcją "UserPolicyBasedTrafficSelectors", zgodnie z opisem w [w tym artykule](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ddc80-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="ddc80-123">Wymaga ASA urządzeń toouse **IKEv2** z konfiguracjami oparte na liście dostępu, nie VTI na podstawie.</span><span class="sxs-lookup"><span data-stu-id="ddc80-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="ddc80-124">Skontaktuj się z tooensure zasad hello jest obsługiwana na urządzeniach sieci VPN między lokalnymi specyfikację dostawcy urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ddc80-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="ddc80-125">Wymagania dotyczące urządzeń sieci VPN</span><span class="sxs-lookup"><span data-stu-id="ddc80-125">VPN device requirements</span></span>
<span data-ttu-id="ddc80-126">Bramy sieci VPN platformy Azure, użyj standardowe tunel S2S VPN tooestablish pakietów protokołu IPsec/IKE protokołu.</span><span class="sxs-lookup"><span data-stu-id="ddc80-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="ddc80-127">Odwołuje się zbyt[urządzenia sieci VPN o](vpn-gateway-about-vpn-devices.md) dla hello szczegółowe parametry protokołu IPsec i IKE i domyślne algorytmów kryptograficznych dla bram sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc80-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="ddc80-128">Opcjonalnie można określić kombinację dokładne hello algorytmów kryptograficznych i kluczy sile dla określonego połączenia, zgodnie z opisem w [o wymaganiach dotyczących kryptograficznych](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="ddc80-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="ddc80-129">W przypadku wybrania określona kombinacja algorytmów kryptograficznych i kluczy sile, upewnij się, używać hello specyfikacje odpowiedniego dla urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ddc80-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="ddc80-130">Jeden tunel VPN</span><span class="sxs-lookup"><span data-stu-id="ddc80-130">Single VPN tunnel</span></span>
<span data-ttu-id="ddc80-131">Ta topologia składa się z jednego tunelu S2S VPN między bramą sieci VPN platformy Azure i lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ddc80-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="ddc80-132">Opcjonalnie można skonfigurować protokołu BGP przez tunel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="ddc80-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![jednego tunelu](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="ddc80-134">Odwołuje się zbyt[Instalatora jednego tunelu](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) szczegółowe instrukcje krok po kroku toobuild hello konfiguracji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc80-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="ddc80-135">Informacji bramy sieci VPN i sieci</span><span class="sxs-lookup"><span data-stu-id="ddc80-135">Network and VPN gateway information</span></span>
<span data-ttu-id="ddc80-136">W tej sekcji znajduje się lista hello parametrów dla hello w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ddc80-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="ddc80-137">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="ddc80-137">**Parameter**</span></span>                | <span data-ttu-id="ddc80-138">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="ddc80-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="ddc80-139">Prefiksy adresów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ddc80-139">VNet address prefixes</span></span>        | <span data-ttu-id="ddc80-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ddc80-140">10.11.0.0/16</span></span><br><span data-ttu-id="ddc80-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ddc80-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="ddc80-142">Adres IP bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ddc80-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="ddc80-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="ddc80-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="ddc80-144">Prefiksy adresów lokalnych</span><span class="sxs-lookup"><span data-stu-id="ddc80-144">On-premises address prefixes</span></span> | <span data-ttu-id="ddc80-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ddc80-145">10.51.0.0/16</span></span><br><span data-ttu-id="ddc80-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ddc80-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="ddc80-147">Lokalny adres IP urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="ddc80-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="ddc80-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="ddc80-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="ddc80-149">* Numer ASN BGP sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ddc80-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="ddc80-150">65010</span><span class="sxs-lookup"><span data-stu-id="ddc80-150">65010</span></span>                        |
| <span data-ttu-id="ddc80-151">* Azure IP elementu równorzędnego protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="ddc80-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="ddc80-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="ddc80-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="ddc80-153">* Lokalnymi BGP ASN</span><span class="sxs-lookup"><span data-stu-id="ddc80-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="ddc80-154">65050</span><span class="sxs-lookup"><span data-stu-id="ddc80-154">65050</span></span>                        |
| <span data-ttu-id="ddc80-155">* IP elementu równorzędnego BGP lokalnej</span><span class="sxs-lookup"><span data-stu-id="ddc80-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="ddc80-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="ddc80-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="ddc80-157">(*) Parametry opcjonalne dla protokołu BGP tylko.</span><span class="sxs-lookup"><span data-stu-id="ddc80-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="ddc80-158">Zasady protokołu IPsec/IKE & parametrów</span><span class="sxs-lookup"><span data-stu-id="ddc80-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="ddc80-159">Witaj w poniższej tabeli wymieniono hello Algorytmy IPsec/IKE i parametry używane w przykładowym hello.</span><span class="sxs-lookup"><span data-stu-id="ddc80-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="ddc80-160">Zapoznaj się z toomake specyfikacje urządzenia sieci VPN się, że wszystkie algorytmy wymienione powyżej są obsługiwane przez modeli urządzenia sieci VPN i wersji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="ddc80-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="ddc80-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="ddc80-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="ddc80-162">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="ddc80-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="ddc80-163">Szyfrowanie IKEv2</span><span class="sxs-lookup"><span data-stu-id="ddc80-163">IKEv2 Encryption</span></span> | <span data-ttu-id="ddc80-164">AES256</span><span class="sxs-lookup"><span data-stu-id="ddc80-164">AES256</span></span>                               |
| <span data-ttu-id="ddc80-165">Integralność IKEv2</span><span class="sxs-lookup"><span data-stu-id="ddc80-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="ddc80-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="ddc80-166">SHA384</span></span>                               |
| <span data-ttu-id="ddc80-167">Grupa DH</span><span class="sxs-lookup"><span data-stu-id="ddc80-167">DH Group</span></span>         | <span data-ttu-id="ddc80-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="ddc80-168">DHGroup24</span></span>                            |
| <span data-ttu-id="ddc80-169">Szyfrowanie IPsec</span><span class="sxs-lookup"><span data-stu-id="ddc80-169">IPsec Encryption</span></span> | <span data-ttu-id="ddc80-170">AES256</span><span class="sxs-lookup"><span data-stu-id="ddc80-170">AES256</span></span>                               |
| <span data-ttu-id="ddc80-171">Integralność IPsec</span><span class="sxs-lookup"><span data-stu-id="ddc80-171">IPsec Integrity</span></span>  | <span data-ttu-id="ddc80-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="ddc80-172">SHA1</span></span>                                 |
| <span data-ttu-id="ddc80-173">Grupa PFS</span><span class="sxs-lookup"><span data-stu-id="ddc80-173">PFS Group</span></span>        | <span data-ttu-id="ddc80-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="ddc80-174">PFS24</span></span>                                |
| <span data-ttu-id="ddc80-175">Okres istnienia skojarzeń zabezpieczeń QM</span><span class="sxs-lookup"><span data-stu-id="ddc80-175">QM SA Lifetime</span></span>   | <span data-ttu-id="ddc80-176">7200 sekund</span><span class="sxs-lookup"><span data-stu-id="ddc80-176">7200 seconds</span></span>                         |
| <span data-ttu-id="ddc80-177">Selektor ruchu</span><span class="sxs-lookup"><span data-stu-id="ddc80-177">Traffic Selector</span></span> | <span data-ttu-id="ddc80-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="ddc80-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="ddc80-179">Klucz wstępny</span><span class="sxs-lookup"><span data-stu-id="ddc80-179">Pre-Shared Key</span></span>   | <span data-ttu-id="ddc80-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="ddc80-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="ddc80-181">(*) Na niektórych urządzeniach integralności IPsec musi być "null", jeśli usługi GCM AES jest używany jako algorytmu szyfrowania IPsec.</span><span class="sxs-lookup"><span data-stu-id="ddc80-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="ddc80-182">Informacje o urządzeniu</span><span class="sxs-lookup"><span data-stu-id="ddc80-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="ddc80-183">Obsługa protokołu IKEv2 wymaga ASA wersji 8.4 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="ddc80-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="ddc80-184">Obsługa grupa DH wyższej i PFS (poza grupy 5) wymaga wersji ASA 9.x.</span><span class="sxs-lookup"><span data-stu-id="ddc80-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="ddc80-185">Szyfrowanie protokołu IPsec z integralnością AES-GCM i IPsec z algorytmu SHA-256, SHA-384, obsługi algorytmu SHA-512 wymaga wersji ASA 9.x na sprzęcie ASA nowszej; 5505 ASA, 5510, 5520, 5540, 5550, są 5580 **nie** obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ddc80-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="ddc80-186">(Sprawdź, czy hello dostawcy specyfikacje tooconfirm.)</span><span class="sxs-lookup"><span data-stu-id="ddc80-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="ddc80-187">Przykład konfiguracji urządzeń</span><span class="sxs-lookup"><span data-stu-id="ddc80-187">Sample device configurations</span></span>
<span data-ttu-id="ddc80-188">Poniższy skrypt Hello zapewnia Przykładowa konfiguracja na podstawie topologii hello i parametry wymienione powyżej.</span><span class="sxs-lookup"><span data-stu-id="ddc80-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="ddc80-189">konfiguracja tunelu S2S VPN Hello składa się z hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ddc80-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="ddc80-190">Interfejsy & tras</span><span class="sxs-lookup"><span data-stu-id="ddc80-190">Interfaces & routes</span></span>
2. <span data-ttu-id="ddc80-191">Dostęp do listy</span><span class="sxs-lookup"><span data-stu-id="ddc80-191">Access lists</span></span>
3. <span data-ttu-id="ddc80-192">Parametry (fazy 1 lub trybu głównego) i zasad IKE</span><span class="sxs-lookup"><span data-stu-id="ddc80-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="ddc80-193">Parametry (faza 2 lub trybu szybkiego) i zasad protokołu IPsec</span><span class="sxs-lookup"><span data-stu-id="ddc80-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="ddc80-194">Inne parametry (TCP MSS ładunku itp.)</span><span class="sxs-lookup"><span data-stu-id="ddc80-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="ddc80-195">Upewnij się ukończyć hello dodatkowej konfiguracji wymienione poniżej i zastąp symbole zastępcze hello hello rzeczywiste wartości:</span><span class="sxs-lookup"><span data-stu-id="ddc80-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="ddc80-196">Konfiguracja zarówno wewnątrz lub na zewnątrz interfejsów dla interfejsu</span><span class="sxs-lookup"><span data-stu-id="ddc80-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="ddc80-197">Trasy do sieci wewnętrznej i prywatnego oraz publicznego i na zewnątrz</span><span class="sxs-lookup"><span data-stu-id="ddc80-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="ddc80-198">Upewnij się, wszystkie nazwy i numery zasad są unikatowe w urządzeniu hello</span><span class="sxs-lookup"><span data-stu-id="ddc80-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="ddc80-199">Upewnij się, że algorytmy kryptograficzne hello są obsługiwane na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="ddc80-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="ddc80-200">Zastąp powitania po symbole zastępcze hello rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="ddc80-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="ddc80-201">Poza Nazwa interfejsu: "poza"</span><span class="sxs-lookup"><span data-stu-id="ddc80-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="ddc80-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="ddc80-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="ddc80-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="ddc80-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="ddc80-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="ddc80-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="ddc80-205">Sieć wirtualną i nazwy bramy sieci lokalnej (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="ddc80-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="ddc80-206">Prefiksy adresów sieci sieci wirtualnej i lokalnej</span><span class="sxs-lookup"><span data-stu-id="ddc80-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="ddc80-207">Odpowiednie maski sieci</span><span class="sxs-lookup"><span data-stu-id="ddc80-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="ddc80-208">Przykładowa konfiguracja</span><span class="sxs-lookup"><span data-stu-id="ddc80-208">Sample configuration</span></span>

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

## <a name="simple-debugging-commands"></a><span data-ttu-id="ddc80-209">Prostych poleceń debugowania</span><span class="sxs-lookup"><span data-stu-id="ddc80-209">Simple debugging commands</span></span>

<span data-ttu-id="ddc80-210">Poniżej przedstawiono niektóre polecenia ASA na potrzeby debugowania:</span><span class="sxs-lookup"><span data-stu-id="ddc80-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="ddc80-211">Pokaż hello IPsec i IKE SA</span><span class="sxs-lookup"><span data-stu-id="ddc80-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="ddc80-212">"Pokaż szyfrowania ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="ddc80-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="ddc80-213">"Pokaż kryptograficznego ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="ddc80-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="ddc80-214">Wprowadzanie tryb debugowania — to można uzyskać bardzo dużo na powitania konsoli</span><span class="sxs-lookup"><span data-stu-id="ddc80-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="ddc80-215">"debugowania ikev2 kryptograficznych platformy <level>"</span><span class="sxs-lookup"><span data-stu-id="ddc80-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="ddc80-216">"debug protokołu ikev2 kryptograficzny <level>"</span><span class="sxs-lookup"><span data-stu-id="ddc80-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="ddc80-217">Bieżące konfiguracje listy</span><span class="sxs-lookup"><span data-stu-id="ddc80-217">List current configurations</span></span>
    - <span data-ttu-id="ddc80-218">"show uruchamiania" - pokazuje hello bieżące konfiguracje w urządzeniu hello; można użyć hello różnych określonych części toolist polecenia podrzędne hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ddc80-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="ddc80-219">Np. "Pokaż Uruchom kryptograficznego", "Pokaż Uruchom listy dostępu", "Pokaż Uruchom tunelu group",... itd.</span><span class="sxs-lookup"><span data-stu-id="ddc80-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ddc80-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ddc80-220">Next steps</span></span>
<span data-ttu-id="ddc80-221">Zobacz [konfigurowania bramy sieci VPN aktywny-aktywny między lokalizacjami i połączeń między wirtualnymi do](vpn-gateway-activeactive-rm-powershell.md) procedury tooconfigure aktywny aktywny między lokalizacjami i połączeń do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="ddc80-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

