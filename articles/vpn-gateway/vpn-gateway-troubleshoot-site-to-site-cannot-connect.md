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
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="fe5f4-103">Rozwiązywanie problemów: Nie można połączyć z połączenia sieci VPN typu lokacja lokacja Azure oraz przestaje działać</span><span class="sxs-lookup"><span data-stu-id="fe5f4-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="fe5f4-104">Po skonfigurowaniu połączenia VPN lokacja lokacja między siecią lokalną i sieci wirtualnej platformy Azure hello połączenia sieci VPN nagle przestanie działać i nie można ponownie.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="fe5f4-105">Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="fe5f4-106">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="fe5f4-106">Troubleshooting steps</span></span>

<span data-ttu-id="fe5f4-107">tooresolve hello problem, spróbuj najpierw zbyt[bramy sieci VPN platformy Azure hello resetowania](vpn-gateway-resetgw-classic.md) i zresetuj tunelu hello z hello lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="fe5f4-108">Jeśli hello problem będzie nadal występował, wykonaj te kroki tooidentify hello przyczyna problemu hello.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="fe5f4-109">Krok wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="fe5f4-109">Prerequisite step</span></span>

<span data-ttu-id="fe5f4-110">Sprawdź typ hello hello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="fe5f4-111">Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe5f4-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="fe5f4-112">Sprawdź hello **omówienie** strony bramy sieci VPN hello hello typu informacji.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Omówienie hello bramy](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="fe5f4-114">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-114">Step 1.</span></span> <span data-ttu-id="fe5f4-115">Sprawdź, czy jest zweryfikowany hello lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="fe5f4-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="fe5f4-116">Sprawdź, czy używasz [zweryfikowane urządzenia sieci VPN i wersję systemu operacyjnego](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="fe5f4-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="fe5f4-117">Witaj urządzenie nie jest zweryfikowany urządzenia sieci VPN, może zajść toosee producenta urządzenia hello toocontact występuje problem ze zgodnością.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="fe5f4-118">Upewnij się, że urządzenia sieci VPN hello jest poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="fe5f4-119">Aby uzyskać więcej informacji, zobacz [Edytuj przykłady konfiguracji urządzenia](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="fe5f4-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="fe5f4-120">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-120">Step 2.</span></span> <span data-ttu-id="fe5f4-121">Sprawdź hello klucza wspólnego</span><span class="sxs-lookup"><span data-stu-id="fe5f4-121">Verify hello shared key</span></span>

<span data-ttu-id="fe5f4-122">Porównaj hello klucza wspólnego dla hello lokalnej sieci VPN urządzenia toohello Azure wirtualnej sieci VPN toomake się, że klucze hello zgodne.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="fe5f4-123">tooview hello klucza wspólnego dla hello połączenia sieci VPN platformy Azure, użyj jednej z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="fe5f4-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="fe5f4-124">**Witryna Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="fe5f4-124">**Azure portal**</span></span>

1. <span data-ttu-id="fe5f4-125">Przejdź połączenia lokacja lokacja bramy sieci VPN toohello, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="fe5f4-126">W hello **ustawienia** kliknij **klucz udostępniony**.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Klucz współużytkowany](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="fe5f4-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fe5f4-128">**Azure PowerShell**</span></span>

<span data-ttu-id="fe5f4-129">Dla modelu wdrażania usługi Azure Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="fe5f4-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="fe5f4-130">Dla hello klasycznego modelu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="fe5f4-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="fe5f4-131">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-131">Step 3.</span></span> <span data-ttu-id="fe5f4-132">Sprawdź elementu równorzędnego sieci VPN hello adresów IP</span><span class="sxs-lookup"><span data-stu-id="fe5f4-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="fe5f4-133">Witaj, IP definicji w hello **bramy sieci lokalnej** obiektu w usłudze Azure powinna być zgodna IP urządzenia lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="fe5f4-134">Hello definicji IP bramy Azure, która jest ustawiona na powitania lokalnego urządzenia powinna być taka sama hello Azure brama IP.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="fe5f4-135">Krok 4.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-135">Step 4.</span></span> <span data-ttu-id="fe5f4-136">Sprawdź przez i grupy NSG na powitania podsieci bramy</span><span class="sxs-lookup"><span data-stu-id="fe5f4-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="fe5f4-137">Sprawdź, czy i Usuń tras zdefiniowanych przez użytkownika (przez) lub grupy zabezpieczeń sieci (NSG) na powitania podsieć bramy, a następnie hello wyniku testu.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="fe5f4-138">Jeśli hello problem zostanie rozwiązany, sprawdź poprawność ustawień hello, które stosowane przez lub NSG.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="fe5f4-139">Krok 5.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-139">Step 5.</span></span> <span data-ttu-id="fe5f4-140">Witaj wyboru lokalny adres interfejsu zewnętrznego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="fe5f4-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="fe5f4-141">Jeśli hello adres internetowy IP urządzenia sieci VPN hello jest uwzględniona w hello **sieci lokalnej** definicji na platformie Azure, mogą występować sporadycznie rozłączeń.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="fe5f4-142">Witaj interfejsu zewnętrznego urządzenia musi być bezpośrednio na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="fe5f4-143">Powinien to być nie translatora adresów sieciowych lub zapora między hello Internet i urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="fe5f4-144">tooconfigure zapory klastrowania toohave wirtualnego adresu IP, należy przerwać hello klastra i ujawnia hello urządzenia sieci VPN bezpośrednio interfejs publiczny tooa tej bramy hello mogą łączyć się z.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="fe5f4-145">Krok 6.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-145">Step 6.</span></span> <span data-ttu-id="fe5f4-146">Sprawdź, czy podsieci hello są takie same (Azure bramy oparte na zasadach)</span><span class="sxs-lookup"><span data-stu-id="fe5f4-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="fe5f4-147">Sprawdź, czy podsieci hello pasują dokładnie między hello sieci wirtualnej platformy Azure i definicje lokalne powitania sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="fe5f4-148">Sprawdź, czy podsieci hello pasują dokładnie między hello **bramy sieci lokalnej** i definicje sieci lokalne powitania lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="fe5f4-149">Krok 7.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-149">Step 7.</span></span> <span data-ttu-id="fe5f4-150">Sprawdź sondy kondycji Azure bramy hello</span><span class="sxs-lookup"><span data-stu-id="fe5f4-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="fe5f4-151">Przejdź toohello [sondy kondycji](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="fe5f4-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="fe5f4-152">Kliknij hello ostrzeżenia dotyczące certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="fe5f4-153">Jeśli otrzymasz odpowiedź hello bramy sieci VPN jest uznawany za dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="fe5f4-154">Jeśli nie otrzymasz odpowiedź hello bramy może nie być w dobrej kondycji lub grupy NSG podsieci bramy hello jest przyczyną problemu hello.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="fe5f4-155">powitania po tekst jest przykładowa odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="fe5f4-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="fe5f4-156">&lt;? wersji xml = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">podstawowego: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / ciąg&gt;</span><span class="sxs-lookup"><span data-stu-id="fe5f4-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="fe5f4-157">Krok 8.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-157">Step 8.</span></span> <span data-ttu-id="fe5f4-158">Sprawdź, czy hello lokalnego urządzenia sieci VPN ma włączoną funkcję doskonałego utajnienia hello</span><span class="sxs-lookup"><span data-stu-id="fe5f4-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="fe5f4-159">funkcja doskonałego utajnienia Hello może spowodować problemy rozłączenia.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="fe5f4-160">Jeśli urządzenia sieci VPN hello doskonałego utajnienia, należy wyłączyć funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="fe5f4-161">Następnie zaktualizuj zasady IPsec bramy sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="fe5f4-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe5f4-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe5f4-162">Next steps</span></span>

-   [<span data-ttu-id="fe5f4-163">Skonfiguruj sieć wirtualną tooa połączenie lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="fe5f4-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="fe5f4-164">Konfigurowanie zasad IPsec i IKE dla połączeń VPN lokacja lokacja</span><span class="sxs-lookup"><span data-stu-id="fe5f4-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
