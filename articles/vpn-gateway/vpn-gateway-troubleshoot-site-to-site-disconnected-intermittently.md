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
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="abedc-103">Rozwiązywanie problemów: Azure VPN lokacja-lokacja rozłącza sporadycznie</span><span class="sxs-lookup"><span data-stu-id="abedc-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="abedc-104">Może wystąpić problem hello czy nowego lub istniejącego połączenia sieci VPN firmy Microsoft Azure punkt-lokacja nie jest stabilna lub odłącza regularnie.</span><span class="sxs-lookup"><span data-stu-id="abedc-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="abedc-105">Ten artykuł zawiera Rozwiązywanie problemów z toohelp kroki identyfikowanie i rozwiązywanie hello przyczyną problemu hello.</span><span class="sxs-lookup"><span data-stu-id="abedc-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="abedc-106">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="abedc-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="abedc-107">Krok wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="abedc-107">Prerequisite step</span></span>

<span data-ttu-id="abedc-108">Sprawdź typ hello bramy sieci wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="abedc-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="abedc-109">Przejdź za[portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abedc-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abedc-110">Sprawdź hello **omówienie** strony bramy sieci wirtualnej hello hello typu informacji.</span><span class="sxs-lookup"><span data-stu-id="abedc-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Omówienie Hello hello bramy](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="abedc-112">Krok 1 Sprawdź, czy hello lokalnie czy urządzenia sieci VPN został zweryfikowany.</span><span class="sxs-lookup"><span data-stu-id="abedc-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="abedc-113">Sprawdź, czy używasz [zweryfikowane urządzenia sieci VPN i wersję systemu operacyjnego](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="abedc-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="abedc-114">Witaj urządzenia sieci VPN nie jest weryfikowany, może zajść toosee producenta urządzenia hello toocontact istnieje jakikolwiek problem ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="abedc-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="abedc-115">Upewnij się, że urządzenia sieci VPN hello jest poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="abedc-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="abedc-116">Aby uzyskać więcej informacji, zobacz [przykłady konfiguracji urządzenia edytowania](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="abedc-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="abedc-117">Krok 2 wyboru hello skojarzenia zabezpieczeń ustawienia (bramy oparte na zasadach sieci wirtualnej platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="abedc-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="abedc-118">Upewnij się, że hello sieci wirtualnej, podsieci i zakresy w hello **bramy sieci lokalnej** definicji na platformie Microsoft Azure są takie same jak konfiguracja hello na powitania lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="abedc-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="abedc-119">Sprawdź zgodnych ustawień hello skojarzenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="abedc-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="abedc-120">Krok 3 wyboru dla tras zdefiniowanych przez użytkownika lub grupy zabezpieczeń sieci w podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="abedc-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="abedc-121">Trasy zdefiniowane przez użytkownika na powitania podsieć bramy może ograniczanie część ruchu i stosowanie pozostałego ruchu.</span><span class="sxs-lookup"><span data-stu-id="abedc-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="abedc-122">Dzięki temu są wyświetlane, czy połączenie sieci VPN hello jest zawodne dla niektórych ruchu i dobrej dla innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="abedc-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="abedc-123">Krok 4 wyboru Witaj "jeden tunel VPN na parę podsieć" (dla bram sieci wirtualnej na podstawie zasad)</span><span class="sxs-lookup"><span data-stu-id="abedc-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="abedc-124">Upewnij się, że hello lokalnego urządzenia sieci VPN jest ustawiona toohave **jeden tunel VPN na pary podsieci** dla bram sieci wirtualnej na podstawie zasad.</span><span class="sxs-lookup"><span data-stu-id="abedc-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="abedc-125">Sprawdź, czy krok 5 ograniczenia skojarzenia zabezpieczeń (dla bram sieci wirtualnej na podstawie zasad)</span><span class="sxs-lookup"><span data-stu-id="abedc-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="abedc-126">Brama sieci wirtualnej na podstawie zasad Hello ma limit 200 pary skojarzenia zabezpieczeń podsieci.</span><span class="sxs-lookup"><span data-stu-id="abedc-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="abedc-127">Jeśli hello liczba podsieci sieci wirtualnej platformy Azure mnożona razy liczba podsieci lokalne powitania jest większe niż 200, zobacz sporadyczne podsieci rozłączeniem.</span><span class="sxs-lookup"><span data-stu-id="abedc-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="abedc-128">Krok 6 Sprawdź lokalne adres interfejsu zewnętrznego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="abedc-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="abedc-129">Jeśli hello internetowy adres IP urządzenia sieci VPN hello jest uwzględniona w hello **bramy sieci lokalnej** definicji na platformie Azure, mogą występować sporadycznie rozłączeń.</span><span class="sxs-lookup"><span data-stu-id="abedc-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="abedc-130">Witaj interfejsu zewnętrznego urządzenia musi być bezpośrednio na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="abedc-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="abedc-131">Powinien istnieć nie translatora adresów sieciowych (NAT) lub zapora między hello Internet i urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="abedc-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="abedc-132">Jeśli skonfigurujesz klaster zapory toohave wirtualnego adresu IP, musi przerwać hello klastra i ujawnia hello urządzenia sieci VPN bezpośrednio tooa interfejs publiczny hello bramy mogą łączyć się z.</span><span class="sxs-lookup"><span data-stu-id="abedc-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="abedc-133">Krok 7 sprawdzanie, czy hello lokalnego urządzenia sieci VPN, ma doskonałego utajnienia włączone</span><span class="sxs-lookup"><span data-stu-id="abedc-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="abedc-134">Witaj **doskonałego utajnienia** funkcji może spowodować problemy rozłączenia hello.</span><span class="sxs-lookup"><span data-stu-id="abedc-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="abedc-135">Jeśli urządzenie sieci VPN hello ma **doskonała utajnienie** włączyć, wyłączyć funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="abedc-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="abedc-136">Następnie [aktualizacji zasad protokołu IPsec bramy sieci wirtualnej hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="abedc-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="abedc-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abedc-137">Next steps</span></span>

- [<span data-ttu-id="abedc-138">Konfigurowanie sieci wirtualnej tooa połączenia lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="abedc-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="abedc-139">Skonfiguruj zasady IPsec i IKE dla połączenia sieci VPN typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="abedc-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

