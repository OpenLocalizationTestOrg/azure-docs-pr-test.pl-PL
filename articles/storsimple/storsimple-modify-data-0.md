---
title: "Witaj aaaModify dane 0 ustawienia na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse środowiska Windows PowerShell dla StorSimple tooreconfigure hello interfejs sieciowy 0 danych na urządzeniu StorSimple."
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
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="07dd1-103">Zmodyfikuj ustawienia interfejsu sieciowego 0 danych hello na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="07dd1-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="07dd1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="07dd1-104">Overview</span></span>
<span data-ttu-id="07dd1-105">Microsoft Azure StorSimple urządzenie ma sześć interfejsów sieciowych, dane 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="07dd1-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="07dd1-106">Witaj dane 0 interfejsu zawsze jest skonfigurowana za pośrednictwem interfejsu programu Windows PowerShell hello lub konsoli szeregowej hello i jest automatycznie włączoną obsługę chmury.</span><span class="sxs-lookup"><span data-stu-id="07dd1-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="07dd1-107">Należy pamiętać, że nie można skonfigurować interfejs sieciowy 0 danych za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="07dd1-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="07dd1-108">Witaj interfejs został skonfigurowany za pomocą Kreatora instalacji hello podczas pierwszego wdrożenia urządzenia StorSimple hello dane 0.</span><span class="sxs-lookup"><span data-stu-id="07dd1-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="07dd1-109">Jeśli urządzenie hello jest w trybie operacyjnych, może być konieczne tooreconfigure dane 0 ustawienia.</span><span class="sxs-lookup"><span data-stu-id="07dd1-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="07dd1-110">W tym samouczku udostępnia dwie metody ustawienia sieci 0 danych toomodify, zarówno za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="07dd1-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="07dd1-111">Po przeczytaniu tego samouczka, będą mieć możliwość:</span><span class="sxs-lookup"><span data-stu-id="07dd1-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="07dd1-112">Modyfikowanie danych 0 ustawienie za pomocą Kreatora instalacji hello sieci</span><span class="sxs-lookup"><span data-stu-id="07dd1-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="07dd1-113">Modyfikowanie ustawień sieciowych 0 danych za pośrednictwem hello `Set-HcsNetInterface` polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="07dd1-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="07dd1-114">Modyfikowanie ustawień sieciowych 0 danych za pomocą Kreatora konfiguracji</span><span class="sxs-lookup"><span data-stu-id="07dd1-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="07dd1-115">Można ponownie skonfigurować ustawienia sieciowe 0 danych, łącząc interfejsu programu Windows PowerShell toohello urządzenia StorSimple i uruchomić sesję kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="07dd1-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="07dd1-116">Wykonaj hello następujące kroki toomodify dane 0 ustawienia:</span><span class="sxs-lookup"><span data-stu-id="07dd1-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="07dd1-117">Ustawienia sieciowe 0 danych toomodify za pośrednictwem Kreatora instalacji</span><span class="sxs-lookup"><span data-stu-id="07dd1-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="07dd1-118">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="07dd1-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="07dd1-119">Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="07dd1-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="07dd1-120">Witaj domyślne hasło jest `Password1`.</span><span class="sxs-lookup"><span data-stu-id="07dd1-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="07dd1-121">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="07dd1-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="07dd1-122">Kreator instalacji pojawi się toohelp skonfigurować hello dane 0 interfejsu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="07dd1-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="07dd1-123">Podanie nowej wartości hello adres IP, bramy i maski podsieci.</span><span class="sxs-lookup"><span data-stu-id="07dd1-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="07dd1-124">Witaj, stałe adresy IP, należy ponownie skonfigurować za pomocą hello toobe kontrolerów **Konfiguruj** strony hello urządzenia StorSimple w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="07dd1-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="07dd1-125">Aby uzyskać więcej informacji, przejdź zbyt[zmodyfikować interfejsów sieciowych](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="07dd1-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="07dd1-126">Modyfikowanie ustawień sieciowych 0 danych za pomocą polecenia cmdlet Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="07dd1-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="07dd1-127">Alternatywną metodą tooreconfigure dane 0 interfejs sieciowy jest przy użyciu hello hello `Set-HcsNetInterface` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="07dd1-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="07dd1-128">polecenia cmdlet Hello jest wykonywany z interfejsu programu Windows PowerShell hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="07dd1-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="07dd1-129">Korzystając z tej procedury, stałe adresy IP kontrolera hello można również skonfigurować w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="07dd1-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="07dd1-130">Wykonaj hello następujące kroki toomodify hello dane 0 ustawienia:</span><span class="sxs-lookup"><span data-stu-id="07dd1-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="07dd1-131">Ustawienia sieci 0 danych toomodify za pomocą polecenia cmdlet hello HcsNetInterface zestawu</span><span class="sxs-lookup"><span data-stu-id="07dd1-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="07dd1-132">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="07dd1-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="07dd1-133">Po wyświetleniu monitu podaj hasło administratora urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="07dd1-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="07dd1-134">Witaj domyślne hasło jest `Password1`.</span><span class="sxs-lookup"><span data-stu-id="07dd1-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="07dd1-135">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="07dd1-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="07dd1-136">W nawiasach hello pod kątem wpisz hello następujące wartości dla danych 0:</span><span class="sxs-lookup"><span data-stu-id="07dd1-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="07dd1-137">Adres IPv4</span><span class="sxs-lookup"><span data-stu-id="07dd1-137">IPv4 address</span></span>
   * <span data-ttu-id="07dd1-138">Brama IPv4</span><span class="sxs-lookup"><span data-stu-id="07dd1-138">IPv4 gateway</span></span>
   * <span data-ttu-id="07dd1-139">Maska podsieci IPv4</span><span class="sxs-lookup"><span data-stu-id="07dd1-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="07dd1-140">Stały adres IPv4 dla kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="07dd1-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="07dd1-141">Stały adres IPv4 dla kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="07dd1-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="07dd1-142">Aby uzyskać więcej informacji na powitania Użyj tego polecenia cmdlet, przejdź zbyt[programu Windows PowerShell dla StorSimple dokumentacji poleceń cmdlet](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="07dd1-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07dd1-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07dd1-143">Next steps</span></span>
* <span data-ttu-id="07dd1-144">Interfejsy sieciowe tooconfigure inne niż dane 0, można użyć hello [strony konfiguracji w hello klasycznego portalu Azure](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="07dd1-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="07dd1-145">Jeśli wystąpią problemy podczas konfigurowania interfejsów sieciowych, zapoznaj się zbyt[Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="07dd1-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

