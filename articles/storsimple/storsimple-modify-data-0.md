---
title: "Modyfikowanie danych 0 ustawienia na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować interfejs sieciowy 0 danych na urządzeniu StorSimple za pomocą programu Windows PowerShell dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 3a47ff1eed220cede820e8698c3384300e94688d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="e97d9-103">Zmodyfikuj ustawienia interfejsu sieciowego 0 danych na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="e97d9-103">Modify the DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="e97d9-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e97d9-104">Overview</span></span>
<span data-ttu-id="e97d9-105">Microsoft Azure StorSimple urządzenie ma sześć interfejsów sieciowych z dane 0 do dane 5.</span><span class="sxs-lookup"><span data-stu-id="e97d9-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="e97d9-106">DANE 0 interfejsu zawsze jest skonfigurowana za pośrednictwem interfejsu programu Windows PowerShell lub konsoli szeregowej i jest automatycznie włączoną obsługę chmury.</span><span class="sxs-lookup"><span data-stu-id="e97d9-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="e97d9-107">Należy pamiętać, że nie można skonfigurować interfejs sieciowy 0 danych za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e97d9-107">Note that you cannot configure DATA 0 network interface through the Azure classic portal.</span></span> 

<span data-ttu-id="e97d9-108">DANE 0 interfejs został skonfigurowany za pomocą Kreatora instalacji podczas początkowej wdrażania urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e97d9-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="e97d9-109">Gdy urządzenie jest w trybie operacyjne, konieczne może być ponownie skonfigurować dane 0 ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e97d9-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="e97d9-110">Ten samouczek zawiera dwie metody, aby zmodyfikować dane 0 sieci ustawienia, zarówno za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e97d9-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="e97d9-111">Po przeczytaniu tego samouczka, będą mieć możliwość:</span><span class="sxs-lookup"><span data-stu-id="e97d9-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="e97d9-112">Modyfikowanie danych 0 ustawienie za pomocą Kreatora konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="e97d9-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="e97d9-113">Modyfikowanie ustawień sieciowych 0 danych za pośrednictwem `Set-HcsNetInterface` polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="e97d9-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="e97d9-114">Modyfikowanie ustawień sieciowych 0 danych za pomocą Kreatora konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e97d9-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="e97d9-115">Można ponownie skonfigurować ustawienia sieciowe 0 danych, łącząc się interfejsu programu Windows PowerShell urządzenia StorSimple i uruchomić sesję kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="e97d9-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="e97d9-116">Wykonaj poniższe kroki, aby zmodyfikować dane 0 ustawienia:</span><span class="sxs-lookup"><span data-stu-id="e97d9-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="e97d9-117">Aby zmodyfikować ustawienia sieciowe 0 danych za pomocą Kreatora konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e97d9-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="e97d9-118">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="e97d9-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="e97d9-119">Po wyświetleniu monitu podaj **hasło administratora urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="e97d9-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="e97d9-120">Domyślne hasło jest `Password1`.</span><span class="sxs-lookup"><span data-stu-id="e97d9-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="e97d9-121">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="e97d9-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="e97d9-122">Aby skonfigurować dane 0 pojawi się Kreator instalacji interfejsu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e97d9-122">A setup wizard will appear to help you configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="e97d9-123">Podaj wartości nowy adres IP, bramę i maski podsieci.</span><span class="sxs-lookup"><span data-stu-id="e97d9-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="e97d9-124">Kontrolery stałe adresy IP należy tak skonfigurować za pomocą **Konfiguruj** strona urządzenia StorSimple w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e97d9-124">The fixed controllers IPs will need to be reconfigured through the **Configure** page of the StorSimple device in the Azure classic portal.</span></span> <span data-ttu-id="e97d9-125">Aby uzyskać więcej informacji, przejdź do [zmodyfikować interfejsów sieciowych](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="e97d9-125">For more information, go to [Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="e97d9-126">Modyfikowanie ustawień sieciowych 0 danych za pomocą polecenia cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="e97d9-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="e97d9-127">Innym sposobem ponownie skonfigurować dane 0 interfejs sieciowy jest za pośrednictwem `Set-HcsNetInterface` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e97d9-127">An alternate way to reconfigure DATA 0 network interface is through the use of  the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="e97d9-128">Polecenia cmdlet jest uruchamiane z interfejsu programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e97d9-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="e97d9-129">Korzystając z tej procedury, kontroler, stałe adresy IP można również skonfigurować w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e97d9-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="e97d9-130">Wykonaj poniższe kroki, aby zmodyfikować dane 0 ustawienia:</span><span class="sxs-lookup"><span data-stu-id="e97d9-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="e97d9-131">Aby zmodyfikować ustawienia sieciowe 0 danych za pomocą polecenia cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="e97d9-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="e97d9-132">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="e97d9-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="e97d9-133">Po wyświetleniu monitu podaj hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e97d9-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="e97d9-134">Domyślne hasło jest `Password1`.</span><span class="sxs-lookup"><span data-stu-id="e97d9-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="e97d9-135">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="e97d9-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="e97d9-136">W nawiasach wpisz następujące wartości dla danych 0:</span><span class="sxs-lookup"><span data-stu-id="e97d9-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="e97d9-137">Adres IPv4</span><span class="sxs-lookup"><span data-stu-id="e97d9-137">IPv4 address</span></span>
   * <span data-ttu-id="e97d9-138">Brama IPv4</span><span class="sxs-lookup"><span data-stu-id="e97d9-138">IPv4 gateway</span></span>
   * <span data-ttu-id="e97d9-139">Maska podsieci IPv4</span><span class="sxs-lookup"><span data-stu-id="e97d9-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="e97d9-140">Stały adres IPv4 dla kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="e97d9-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="e97d9-141">Stały adres IPv4 dla kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="e97d9-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="e97d9-142">Aby uzyskać więcej informacji dotyczących użycia tego polecenia cmdlet, przejdź do [programu Windows PowerShell dla StorSimple dokumentacji poleceń cmdlet](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="e97d9-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e97d9-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e97d9-143">Next steps</span></span>
* <span data-ttu-id="e97d9-144">Aby skonfigurować interfejsy sieciowe inne niż dane 0, można użyć [strony konfiguracji w klasycznym portalu Azure](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="e97d9-144">To configure network interfaces other than DATA 0, you can use the [Configure page in the Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="e97d9-145">Jeśli wystąpią problemy podczas konfigurowania interfejsów sieciowych, zapoznaj się [Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e97d9-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

