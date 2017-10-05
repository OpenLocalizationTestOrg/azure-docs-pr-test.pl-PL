---
title: "Rozwiązywanie problemów z Azure sporadycznie zakończy połączenie sieci VPN typu lokacja-lokacja | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązać problem, w którym połączenie sieci VPN typu lokacja-lokacja rozłączone regularnie."
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="09297-103">Rozwiązywanie problemów: Azure VPN lokacja-lokacja rozłącza sporadycznie</span><span class="sxs-lookup"><span data-stu-id="09297-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="09297-104">Może wystąpić problem, że nowe lub istniejące połączenie sieci VPN firmy Microsoft Azure punkt-lokacja nie jest stabilna lub odłącza regularnie.</span><span class="sxs-lookup"><span data-stu-id="09297-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="09297-105">Ten artykuł zawiera Rozwiązywanie problemów z czynności, aby zidentyfikować i rozpoznać przyczynę problemu.</span><span class="sxs-lookup"><span data-stu-id="09297-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="09297-106">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="09297-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="09297-107">Krok wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="09297-107">Prerequisite step</span></span>

<span data-ttu-id="09297-108">Sprawdź typ bramy sieci wirtualnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="09297-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="09297-109">Przejdź do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09297-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="09297-110">Sprawdź **omówienie** strony bramy sieci wirtualnej, aby uzyskać informacje o typie.</span><span class="sxs-lookup"><span data-stu-id="09297-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![Omówienie bramy](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="09297-112">Krok 1 Sprawdź, czy lokalnego urządzenia sieci VPN zostanie zweryfikowany.</span><span class="sxs-lookup"><span data-stu-id="09297-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="09297-113">Sprawdź, czy używasz [zweryfikowane urządzenia sieci VPN i wersję systemu operacyjnego](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="09297-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="09297-114">Urządzenia sieci VPN nie jest weryfikowany, należy skontaktować się z producentem urządzenia, aby sprawdzić, czy jakikolwiek problem ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="09297-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="09297-115">Upewnij się, że urządzenia sieci VPN został poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="09297-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="09297-116">Aby uzyskać więcej informacji, zobacz [przykłady konfiguracji urządzenia edytowania](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="09297-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="09297-117">Krok 2 Sprawdź ustawienia skojarzenia zabezpieczeń (dla bramy oparte na zasadach sieci wirtualnej platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="09297-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="09297-118">Upewnij się, że sieci wirtualnej, podsieci i zakresy w **bramy sieci lokalnej** definicji na platformie Microsoft Azure są takie same jak konfiguracji lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="09297-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="09297-119">Upewnij się, że ustawienia skojarzenia zabezpieczeń są zgodne.</span><span class="sxs-lookup"><span data-stu-id="09297-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="09297-120">Krok 3 wyboru dla tras zdefiniowanych przez użytkownika lub grupy zabezpieczeń sieci w podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="09297-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="09297-121">Trasy zdefiniowane przez użytkownika w podsieci bramy może ograniczanie część ruchu i stosowanie pozostałego ruchu.</span><span class="sxs-lookup"><span data-stu-id="09297-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="09297-122">Dzięki temu są wyświetlane, czy połączenie sieci VPN jest zawodne dla niektórych ruchu i dobrej dla innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="09297-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="09297-123">Krok 4 sprawdzenie "Jeden tunel VPN na parę podsieć" (dla bram sieci wirtualnej na podstawie zasad)</span><span class="sxs-lookup"><span data-stu-id="09297-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="09297-124">Upewnij się, że ustawiono lokalnego urządzenia sieci VPN mają **jeden tunel VPN na pary podsieci** dla bram sieci wirtualnej na podstawie zasad.</span><span class="sxs-lookup"><span data-stu-id="09297-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="09297-125">Sprawdź, czy krok 5 ograniczenia skojarzenia zabezpieczeń (dla bram sieci wirtualnej na podstawie zasad)</span><span class="sxs-lookup"><span data-stu-id="09297-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="09297-126">Brama sieci wirtualnej na podstawie zasad ma limit 200 pary skojarzenia zabezpieczeń podsieci.</span><span class="sxs-lookup"><span data-stu-id="09297-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="09297-127">Jeśli mnożona liczba podsieci sieci wirtualnej platformy Azure czas liczbą podsieci lokalne jest większe niż 200, zobacz sporadyczne podsieci odłączania.</span><span class="sxs-lookup"><span data-stu-id="09297-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="09297-128">Krok 6 Sprawdź lokalne adres interfejsu zewnętrznego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="09297-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="09297-129">Jeśli internetowy adres IP urządzenia sieci VPN wchodzi w **bramy sieci lokalnej** definicji na platformie Azure, mogą występować sporadycznie rozłączeń.</span><span class="sxs-lookup"><span data-stu-id="09297-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="09297-130">Interfejs zewnętrzne urządzenie musi być bezpośrednio połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="09297-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="09297-131">Powinien istnieć nie translatora adresów sieciowych (NAT) lub urządzenia od Internetu zaporą.</span><span class="sxs-lookup"><span data-stu-id="09297-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="09297-132">Jeśli konfigurujesz zapory klaster ma wirtualnego adresu IP, musi przerwać klastra i ujawnia urządzenia sieci VPN bezpośrednio na interfejs publiczny, który bramy mogą łączyć się z.</span><span class="sxs-lookup"><span data-stu-id="09297-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="09297-133">Krok 7 sprawdzanie, czy doskonałego utajnienia włączone ma lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="09297-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="09297-134">**Doskonałego utajnienia** funkcji może spowodować problemy rozłączenia.</span><span class="sxs-lookup"><span data-stu-id="09297-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="09297-135">Jeśli urządzenie sieci VPN ma **doskonała utajnienie** włączyć, wyłączyć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="09297-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="09297-136">Następnie [aktualizacji zasad protokołu IPsec bramy sieci wirtualnej](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="09297-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09297-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09297-137">Next steps</span></span>

- [<span data-ttu-id="09297-138">Skonfiguruj połączenie lokacja-lokacja sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09297-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="09297-139">Skonfiguruj zasady IPsec i IKE dla połączenia sieci VPN typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="09297-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

