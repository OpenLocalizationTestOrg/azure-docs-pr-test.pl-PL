---
title: "Konfigurowanie zasad IPsec i IKE dla połączeń sieci VPN S2S lub do wirtualnymi: usługi Azure Resource Manager: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono konfigurowanie zasad IPsec i IKE dla połączeń S2S lub do wirtualnymi przy użyciu bramy sieci VPN platformy Azure przy użyciu usługi Azure Resource Manager i programu PowerShell."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="5362f-103">Konfigurowanie zasad IPsec i IKE dla połączeń S2S sieci VPN lub sieć wirtualną do sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5362f-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="5362f-104">W tym artykule przedstawiono hello kroki tooconfigure zasad IPsec i IKE dla połączeń VPN lokacja-lokacja lub do wirtualnymi przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5362f-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="5362f-105"><a name="about"></a>Parametry zasad IPsec i IKE dla bram sieci VPN platformy Azure — informacje</span><span class="sxs-lookup"><span data-stu-id="5362f-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="5362f-106">Standardowego protokołu IPsec i IKE obsługuje szeroką gamę algorytmów kryptograficznych w różnych kombinacjach.</span><span class="sxs-lookup"><span data-stu-id="5362f-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="5362f-107">Odwołuje się zbyt[temat wymagań usług kryptograficznych i bram sieci VPN platformy Azure](vpn-gateway-about-compliance-crypto.md) toosee jak może to pomóc w sprawdzeniu między lokalizacjami i łączności do wirtualnymi spełniają wymagania zgodności i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5362f-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="5362f-108">Ten artykuł zawiera instrukcje toocreate i skonfigurować zasady IPsec i IKE i Zastosuj tooa nowego lub istniejącego połączenia:</span><span class="sxs-lookup"><span data-stu-id="5362f-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="5362f-109">Część 1 - toocreate przepływu pracy i ustawić zasady IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="5362f-110">Część 2 - obsługiwanych algorytmów kryptograficznych i kluczy sile</span><span class="sxs-lookup"><span data-stu-id="5362f-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="5362f-111">Część 3 — Utwórz nowe połączenie sieci VPN S2S z zasadami IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="5362f-112">Część 4 — Utwórz nowe połączenie do wirtualnymi z zasadami IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="5362f-113">Część 5 - zarządzania (Tworzenie, Dodaj i Usuń) zasady IPsec i IKE połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="5362f-114">Należy pamiętać, że zasady IPsec/IKE działa tylko na powitania po jednostki SKU bramy:</span><span class="sxs-lookup"><span data-stu-id="5362f-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="5362f-115">***VpnGw3 VpnGw1, VpnGw2,*** (opartej na trasach)</span><span class="sxs-lookup"><span data-stu-id="5362f-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="5362f-116">***Standardowe*** i ***wysokowydajnej*** (opartej na trasach)</span><span class="sxs-lookup"><span data-stu-id="5362f-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="5362f-117">Można określić tylko ***jedną*** kombinację zasad dla danego połączenia.</span><span class="sxs-lookup"><span data-stu-id="5362f-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="5362f-118">Należy określić wszystkie algorytmy i parametry IKE (tryb główny) i IPsec (trybu szybkiego).</span><span class="sxs-lookup"><span data-stu-id="5362f-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="5362f-119">Określenie zasad częściowych nie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="5362f-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="5362f-120">Zapoznaj się z tooensure zasad hello jest obsługiwana na urządzeniach sieci VPN między lokalnymi specyfikację dostawcy urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="5362f-121">S2S lub połączeń do wirtualnymi nie można ustanowić, jeśli zasady hello są niezgodne.</span><span class="sxs-lookup"><span data-stu-id="5362f-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="5362f-122"><a name ="workflow"></a>Część 1 - toocreate przepływu pracy i ustawić zasady IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="5362f-123">W tej sekcji przedstawiono hello przepływu pracy toocreate i aktualizacji IPsec i IKE zasad dla połączenia sieci VPN S2S lub wirtualnymi do:</span><span class="sxs-lookup"><span data-stu-id="5362f-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="5362f-124">Tworzenie sieci wirtualnej i bramy VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5362f-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="5362f-125">Tworzenie bramy sieci lokalnej dla krzyżyk lokalne połączenie lub innej sieci wirtualnej i brama dla połączenia do wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="5362f-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="5362f-126">Utwórz zasady IPsec i IKE z wybranych algorytmów i parametry</span><span class="sxs-lookup"><span data-stu-id="5362f-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="5362f-127">Utworzyć połączenie (protokołu IPsec lub VNet2VNet) za pomocą zasad IPsec i IKE hello</span><span class="sxs-lookup"><span data-stu-id="5362f-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="5362f-128">Dodawania/aktualizacji/usuwania zasad IPsec i IKE dla istniejącego połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="5362f-129">Witaj instrukcje w tym artykule ułatwia instalowanie i konfigurowanie zasad IPsec i IKE, jak pokazano na diagramie hello:</span><span class="sxs-lookup"><span data-stu-id="5362f-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![zasady protokołu IPSec-ike](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="5362f-131"><a name ="params"></a>Część 2 - obsługiwane algorytmy kryptograficzne & sile klucza</span><span class="sxs-lookup"><span data-stu-id="5362f-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="5362f-132">Witaj poniższej tabeli wymieniono obsługiwane hello algorytmów kryptograficznych i kluczy sile można konfigurować i klientom Witaj:</span><span class="sxs-lookup"><span data-stu-id="5362f-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="5362f-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="5362f-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="5362f-134">**Opcje**</span><span class="sxs-lookup"><span data-stu-id="5362f-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="5362f-135">Szyfrowanie IKEv2</span><span class="sxs-lookup"><span data-stu-id="5362f-135">IKEv2 Encryption</span></span> | <span data-ttu-id="5362f-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="5362f-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="5362f-137">Integralność IKEv2</span><span class="sxs-lookup"><span data-stu-id="5362f-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="5362f-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="5362f-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="5362f-139">Grupa DH</span><span class="sxs-lookup"><span data-stu-id="5362f-139">DH Group</span></span>         | <span data-ttu-id="5362f-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, Brak</span><span class="sxs-lookup"><span data-stu-id="5362f-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="5362f-141">Szyfrowanie IPsec</span><span class="sxs-lookup"><span data-stu-id="5362f-141">IPsec Encryption</span></span> | <span data-ttu-id="5362f-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Brak</span><span class="sxs-lookup"><span data-stu-id="5362f-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="5362f-143">Integralność IPsec</span><span class="sxs-lookup"><span data-stu-id="5362f-143">IPsec Integrity</span></span>  | <span data-ttu-id="5362f-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="5362f-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="5362f-145">Grupa PFS</span><span class="sxs-lookup"><span data-stu-id="5362f-145">PFS Group</span></span>        | <span data-ttu-id="5362f-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Brak</span><span class="sxs-lookup"><span data-stu-id="5362f-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="5362f-147">Okres istnienia skojarzeń zabezpieczeń QM</span><span class="sxs-lookup"><span data-stu-id="5362f-147">QM SA Lifetime</span></span>   | <span data-ttu-id="5362f-148">(**Opcjonalnie**: wartości domyślne są używane jeśli nie została określona)</span><span class="sxs-lookup"><span data-stu-id="5362f-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="5362f-149">Sekundy (liczba całkowita; **min. 300**/wartość domyślna 27 000 sekund)</span><span class="sxs-lookup"><span data-stu-id="5362f-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="5362f-150">KB (liczba całkowita; **min. 1024**/wartość domyślna to 102 400 000 KB)</span><span class="sxs-lookup"><span data-stu-id="5362f-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="5362f-151">Selektor ruchu</span><span class="sxs-lookup"><span data-stu-id="5362f-151">Traffic Selector</span></span> | <span data-ttu-id="5362f-152">UsePolicyBasedTrafficSelectors ** ($True/$False; **Opcjonalnie**, domyślna $False Jeśli nie została określona)</span><span class="sxs-lookup"><span data-stu-id="5362f-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="5362f-153">**Jeśli GCMAES jest używany jak w przypadku algorytmu szyfrowania IPsec, należy wybrać hello samego algorytmu GCMAES i długości kluczy dla protokołu IPsec integralności; na przykład za pomocą GCMAES128 zarówno dla**</span><span class="sxs-lookup"><span data-stu-id="5362f-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="5362f-154">Okres istnienia skojarzenia zabezpieczeń trybu głównego protokół IKEv2 jest ustalony na 28 800 sekund na powitania bram sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5362f-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="5362f-155">Ustawienie "UsePolicyBasedTrafficSelectors" zbyt$ True połączenia służy do konfigurowania hello sieci VPN platformy Azure bramy tooconnect toopolicy zapora oparta na sieci VPN lokalnie.</span><span class="sxs-lookup"><span data-stu-id="5362f-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="5362f-156">Po włączeniu PolicyBasedTrafficSelectors należy tooensure hello pasującego selektorów ruchu zdefiniowane z wszystkich kombinacji prefiksów (bramy sieci lokalnej) sieci lokalnej, tak z hello prefiksy sieci wirtualnej platformy Azure, ma urządzenie sieci VPN zamiast dowolny z każdym.</span><span class="sxs-lookup"><span data-stu-id="5362f-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="5362f-157">Na przykład jeśli są Twoje prefiksy sieci lokalnej, 10.1.0.0/16 i 10.2.0.0/16, a prefiksy Twojej sieci wirtualnej są 192.168.0.0/16 i 172.16.0.0/16, należy hello toospecify po selektorów ruchu:</span><span class="sxs-lookup"><span data-stu-id="5362f-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="5362f-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5362f-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5362f-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5362f-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="5362f-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5362f-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5362f-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5362f-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="5362f-162">Aby uzyskać więcej informacji dotyczących selektorów ruchu na podstawie zasad, zobacz [połączyć wiele urządzeń lokalnych, na podstawie zasad sieci VPN](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5362f-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="5362f-163">Witaj w następującej tabeli przedstawiono hello odpowiednich grup Diffie-Hellman obsługiwanych przez zasady niestandardowe hello:</span><span class="sxs-lookup"><span data-stu-id="5362f-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="5362f-164">**Grupa Diffie’ego-Hellmana**</span><span class="sxs-lookup"><span data-stu-id="5362f-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="5362f-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="5362f-165">**DHGroup**</span></span>              | <span data-ttu-id="5362f-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="5362f-166">**PFSGroup**</span></span> | <span data-ttu-id="5362f-167">**Długość klucza**</span><span class="sxs-lookup"><span data-stu-id="5362f-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5362f-168">1</span><span class="sxs-lookup"><span data-stu-id="5362f-168">1</span></span>                         | <span data-ttu-id="5362f-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="5362f-169">DHGroup1</span></span>                 | <span data-ttu-id="5362f-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="5362f-170">PFS1</span></span>         | <span data-ttu-id="5362f-171">MODP, 768-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-171">768-bit MODP</span></span>   |
| <span data-ttu-id="5362f-172">2</span><span class="sxs-lookup"><span data-stu-id="5362f-172">2</span></span>                         | <span data-ttu-id="5362f-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="5362f-173">DHGroup2</span></span>                 | <span data-ttu-id="5362f-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="5362f-174">PFS2</span></span>         | <span data-ttu-id="5362f-175">MODP, 1024-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="5362f-176">14</span><span class="sxs-lookup"><span data-stu-id="5362f-176">14</span></span>                        | <span data-ttu-id="5362f-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="5362f-177">DHGroup14</span></span><br><span data-ttu-id="5362f-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="5362f-178">DHGroup2048</span></span> | <span data-ttu-id="5362f-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="5362f-179">PFS2048</span></span>      | <span data-ttu-id="5362f-180">MODP, 2048-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="5362f-181">19</span><span class="sxs-lookup"><span data-stu-id="5362f-181">19</span></span>                        | <span data-ttu-id="5362f-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="5362f-182">ECP256</span></span>                   | <span data-ttu-id="5362f-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="5362f-183">ECP256</span></span>       | <span data-ttu-id="5362f-184">ECP, 256-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-184">256-bit ECP</span></span>    |
| <span data-ttu-id="5362f-185">20</span><span class="sxs-lookup"><span data-stu-id="5362f-185">20</span></span>                        | <span data-ttu-id="5362f-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="5362f-186">ECP384</span></span>                   | <span data-ttu-id="5362f-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="5362f-187">ECP284</span></span>       | <span data-ttu-id="5362f-188">ECP, 384-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-188">384-bit ECP</span></span>    |
| <span data-ttu-id="5362f-189">24</span><span class="sxs-lookup"><span data-stu-id="5362f-189">24</span></span>                        | <span data-ttu-id="5362f-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5362f-190">DHGroup24</span></span>                | <span data-ttu-id="5362f-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="5362f-191">PFS24</span></span>        | <span data-ttu-id="5362f-192">MODP, 2048-bitowy</span><span class="sxs-lookup"><span data-stu-id="5362f-192">2048-bit MODP</span></span>  |

<span data-ttu-id="5362f-193">Odwołuje się zbyt[RFC3526](https://tools.ietf.org/html/rfc3526) i [RFC5114](https://tools.ietf.org/html/rfc5114) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="5362f-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="5362f-194"><a name ="crossprem"></a>Część 3 — Utwórz nowe połączenie sieci VPN S2S z zasadami IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-195">Ta sekcja przeprowadzi Cię przez kroki hello tworzenia połączenia sieci VPN S2S przy użyciu zasad IPsec i IKE.</span><span class="sxs-lookup"><span data-stu-id="5362f-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="5362f-196">Hello następujące kroki tworzenia połączenia hello jak pokazano na diagramie hello:</span><span class="sxs-lookup"><span data-stu-id="5362f-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![zasady s2s](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="5362f-198">Zobacz [Tworzenie połączenia sieci VPN S2S](vpn-gateway-create-site-to-site-rm-powershell.md) Aby uzyskać szczegółowe instrukcje krok po kroku dotyczące tworzenia połączenia sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="5362f-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="5362f-199"><a name="before"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5362f-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="5362f-200">Sprawdź, czy masz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5362f-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5362f-201">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5362f-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5362f-202">Zainstaluj polecenia cmdlet programu PowerShell usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5362f-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5362f-203">Zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5362f-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="5362f-204"><a name="createvnet1"></a>Krok 1 — Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5362f-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5362f-205">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="5362f-205">1. Declare your variables</span></span>

<span data-ttu-id="5362f-206">W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5362f-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="5362f-207">Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="5362f-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="5362f-208">2. Połączyć subskrypcję tooyour i utworzyć nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="5362f-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="5362f-209">Upewnij się, że przełącznik tooPowerShell tryb toouse hello poleceń cmdlet Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="5362f-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="5362f-210">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5362f-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="5362f-211">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="5362f-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="5362f-212">Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="5362f-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="5362f-213">3. Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5362f-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="5362f-214">Hello następujące przykładowe tworzy hello sieci wirtualnej, TestVNet1, z trzech podsieci i hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="5362f-215">Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="5362f-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="5362f-216">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5362f-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="5362f-217"><a name="s2sconnection"></a>Krok 2 — Tworzenie połączenia sieci VPN S2S przy użyciu zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5362f-218">1. Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-219">Witaj następującego przykładowego skryptu tworzy zasady IPsec i IKE z hello algorytmów i parametry:</span><span class="sxs-lookup"><span data-stu-id="5362f-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="5362f-220">IKEv2: DHGroup24 AES256, SHA384</span><span class="sxs-lookup"><span data-stu-id="5362f-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5362f-221">Protokół IPsec: AES256, SHA256, PFS24, skojarzenia zabezpieczeń okres istnienia 7200 sekund & 2048KB</span><span class="sxs-lookup"><span data-stu-id="5362f-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="5362f-222">Jeśli używasz GCMAES dla protokołu IPsec, należy użyć hello samego algorytmu GCMAES i długość klucza szyfrowania IPsec i integralności, na przykład:</span><span class="sxs-lookup"><span data-stu-id="5362f-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="5362f-223">IKEv2: DHGroup24 AES256, SHA384</span><span class="sxs-lookup"><span data-stu-id="5362f-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5362f-224">Protokół IPsec: **GCMAES256, GCMAES256**, PFS24, skojarzenia zabezpieczeń okres istnienia 7200 sekund & 2048 KB</span><span class="sxs-lookup"><span data-stu-id="5362f-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5362f-225">2. Tworzenie połączenia sieci VPN S2S hello z hello zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-226">Tworzenie połączenia sieci VPN S2S i stosowanie zasad IPsec i IKE hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5362f-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="5362f-227">Opcjonalnie można dodać "-UsePolicyBasedTrafficSelectors $True" toohello utworzyć połączenie polecenia cmdlet tooenable sieci VPN platformy Azure bramy tooconnect toopolicy urządzeń opartych na sieci VPN lokalnie, jak opisano powyżej.</span><span class="sxs-lookup"><span data-stu-id="5362f-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5362f-228">Po zasad IPsec i IKE jest określony dla połączenia, bramy sieci VPN platformy Azure hello tylko wysłać lub Zaakceptuj propozycję IPsec i IKE hello z określonym algorytmów kryptograficznych i kluczy sile dla tego konkretnego połączenia.</span><span class="sxs-lookup"><span data-stu-id="5362f-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5362f-229">Upewnij się, urządzenie sieci VPN lokalne powitania połączenia używa lub akceptuje hello kombinacji dokładne zasady, w przeciwnym razie tunel S2S VPN hello nie zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="5362f-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="5362f-230"><a name ="vnet2vnet"></a>Część 4 — Utwórz nowe połączenie do wirtualnymi z zasadami IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-231">Witaj kroki tworzenia połączenia do wirtualnymi przy użyciu zasad IPsec i IKE są podobne toothat połączenia sieci S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="5362f-232">Witaj następujące przykładowe skrypty Utwórz hello połączenie jak pokazano na diagramie hello:</span><span class="sxs-lookup"><span data-stu-id="5362f-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v zasad](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="5362f-234">Zobacz [utworzyć połączenie do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md) bardziej szczegółowe kroki tworzenia połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="5362f-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="5362f-235">Należy wykonać [część 3](#crossprem) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="5362f-236"><a name="createvnet2"></a>Krok 1 — Tworzenie hello drugiej sieci wirtualnej i Brama sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5362f-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5362f-237">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="5362f-237">1. Declare your variables</span></span>

<span data-ttu-id="5362f-238">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5362f-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="5362f-239">2. Tworzenie hello drugiej sieci wirtualnej i Brama sieci VPN w hello nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="5362f-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5362f-240">Krok 2 — Tworzenie połączenia sieci wirtualnej toVNet z hello zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-241">Podobne toohello połączenia sieci VPN S2S, tworzenie zasad IPsec i IKE, zastosuj toopolicy toohello nowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="5362f-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5362f-242">1. Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-243">Hello następującego przykładowego skryptu tworzy różne zasady IPsec i IKE z hello algorytmów i parametry:</span><span class="sxs-lookup"><span data-stu-id="5362f-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="5362f-244">IKEv2: DHGroup14 AES128, SHA1,</span><span class="sxs-lookup"><span data-stu-id="5362f-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="5362f-245">Protokół IPsec: GCMAES128, GCMAES128, PFS14, okres istnienia SA 7200 sekund i 4096KB</span><span class="sxs-lookup"><span data-stu-id="5362f-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="5362f-246">2. Utwórz wirtualnymi do połączeń z hello zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="5362f-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5362f-247">Utwórz połączenia do wirtualnymi i Zastosuj zasady IPsec i IKE hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="5362f-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="5362f-248">W tym przykładzie zarówno bramy znajdują się w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5362f-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="5362f-249">Jest to możliwe toocreate i skonfigurować zarówno połączenia z hello jednych zasad IPsec i IKE w hello tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5362f-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="5362f-250">Po zasad IPsec i IKE jest określony dla połączenia, bramy sieci VPN platformy Azure hello tylko wysłać lub Zaakceptuj propozycję IPsec i IKE hello z określonym algorytmów kryptograficznych i kluczy sile dla tego konkretnego połączenia.</span><span class="sxs-lookup"><span data-stu-id="5362f-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5362f-251">Upewnij się, że hello zasad protokołu IPsec dla obu połączeń są hello takie same, w przeciwnym razie nie zostanie nawiązane połączenie do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="5362f-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="5362f-252">Po wykonaniu tych czynności hello połączenie zostanie nawiązane za kilka minut i będzie miał powitania od topologii sieci, pokazane na początku hello:</span><span class="sxs-lookup"><span data-stu-id="5362f-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![zasady protokołu IPSec-ike](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="5362f-254"><a name ="managepolicy"></a>Część 5 - zasad IPsec/IKE aktualizacji dla połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5362f-255">Witaj ostatniej sekcji przedstawiono toomanage zasady IPsec i IKE dla istniejącego połączenia S2S lub do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="5362f-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="5362f-256">Ćwiczenie Hello poniżej przeprowadzi Cię przez kolejne hello następujące operacje połączenia:</span><span class="sxs-lookup"><span data-stu-id="5362f-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="5362f-257">Pokaż hello zasad IPsec i IKE połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="5362f-258">Dodaj lub zaktualizuj połączenie tooa zasad IPsec i IKE hello</span><span class="sxs-lookup"><span data-stu-id="5362f-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="5362f-259">Usuń zasady IPsec/IKE hello z połączeniem</span><span class="sxs-lookup"><span data-stu-id="5362f-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5362f-260">Witaj te same czynności Zastosuj tooboth S2S i połączeń do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="5362f-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5362f-261">Zasady protokołu IPsec/IKE jest obsługiwana w *standardowe* i *wysokowydajnej* opartej na trasach bramy sieci VPN tylko.</span><span class="sxs-lookup"><span data-stu-id="5362f-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="5362f-262">Nie działa na powitania jednostka SKU bramy podstawowe lub brama sieci VPN opartych na zasadach hello.</span><span class="sxs-lookup"><span data-stu-id="5362f-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="5362f-263">1. Pokaż hello zasad IPsec i IKE połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="5362f-264">Witaj poniższy przykład pokazuje, jak tooget hello zasady IPsec i IKE skonfigurowane dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="5362f-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="5362f-265">skrypty Hello również kontynuować pracę z powyższego ćwiczenia hello.</span><span class="sxs-lookup"><span data-stu-id="5362f-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5362f-266">ostatnie polecenie Hello wymieniono hello bieżące zasady IPsec i IKE skonfigurowana w połączeniu hello, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="5362f-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="5362f-267">następujące przykładowe dane wyjściowe Hello jest hello połączenia:</span><span class="sxs-lookup"><span data-stu-id="5362f-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="5362f-268">Jeśli nie ma żadnych skonfigurowanych zasad IPsec i IKE, hello polecenia (PS > $connection6.policy) pobiera zwracany pusta.</span><span class="sxs-lookup"><span data-stu-id="5362f-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="5362f-269">Nie oznacza IPsec i IKE nie jest skonfigurowana w połączeniu hello, ale czy nie ma niestandardowych zasad IPsec i IKE.</span><span class="sxs-lookup"><span data-stu-id="5362f-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="5362f-270">połączenie rzeczywiste hello używa hello domyślne zasady negocjowane między hello bramy sieci VPN platformy Azure i lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="5362f-271">2. Dodania lub zaktualizowania zasad IPsec i IKE połączenia</span><span class="sxs-lookup"><span data-stu-id="5362f-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5362f-272">Hello kroki tooadd nowych zasad lub aktualizacji są istniejące zasady połączenia hello same: Utwórz nowe zasady, a następnie zastosować hello nowe zasady toohello połączenie.</span><span class="sxs-lookup"><span data-stu-id="5362f-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="5362f-273">tooenable "UsePolicyBasedTrafficSelectors", gdy połączenie tooan lokalnego urządzenia sieci VPN opartych na zasadach dodać hello "-UsePolicyBaseTrafficSelectors" parametru polecenia cmdlet toohello, lub ustaw ją za$ False toodisable hello opcji:</span><span class="sxs-lookup"><span data-stu-id="5362f-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="5362f-274">Można uzyskać połączenia hello ponownie toocheck Jeśli hello zasady są aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5362f-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5362f-275">Dane wyjściowe hello hello ostatni wiersz, powinny być widoczne, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5362f-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="5362f-276">3. Usuń zasady IPsec i IKE z połączeniem</span><span class="sxs-lookup"><span data-stu-id="5362f-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5362f-277">Po usunięciu zasad niestandardowych hello połączenie bramy sieci VPN platformy Azure hello przekształcenia wstecz toohello [domyślnej listy propozycje IPsec i IKE](vpn-gateway-about-vpn-devices.md) i podejmuje próbę negocjacje do lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="5362f-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="5362f-278">Można użyć tego samego skryptu toocheck hello, jeśli zasady hello zostały usunięte z połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="5362f-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5362f-279">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5362f-279">Next steps</span></span>

<span data-ttu-id="5362f-280">Zobacz [połączyć wiele urządzeń lokalnych, na podstawie zasad sieci VPN](vpn-gateway-connect-multiple-policybased-rm-ps.md) więcej szczegółów dotyczących ruchu na podstawie zasad selektorów.</span><span class="sxs-lookup"><span data-stu-id="5362f-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="5362f-281">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5362f-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5362f-282">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5362f-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
