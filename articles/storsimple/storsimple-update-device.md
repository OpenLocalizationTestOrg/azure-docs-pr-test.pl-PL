---
title: "Aktualizowanie urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak korzystać z funkcji aktualizacji StorSimple do zainstalowania zwykłych oraz obsługi trybu aktualizacje i poprawki."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="52586-103">Zaktualizuj urządzenia z serii StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="52586-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="52586-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="52586-104">Overview</span></span>
<span data-ttu-id="52586-105">Funkcje aktualizacji StorSimple umożliwiają łatwe aktualizowanie urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="52586-106">W zależności od typu aktualizacji należy zastosować aktualizacje na urządzeniu za pośrednictwem klasycznego portalu Azure lub za pośrednictwem interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52586-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="52586-107">W tym samouczku opisano typy aktualizacji i sposobu instalacji każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="52586-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="52586-108">Można zastosować dwa typy aktualizacji urządzenia:</span><span class="sxs-lookup"><span data-stu-id="52586-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="52586-109">Regularne (lub tryb normalny) aktualizacji</span><span class="sxs-lookup"><span data-stu-id="52586-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="52586-110">Aktualizacje trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="52586-110">Maintenance mode updates</span></span>

<span data-ttu-id="52586-111">Możesz zainstalować regularne aktualizacje za pośrednictwem klasycznego portalu Azure lub programu Windows PowerShell; jednak należy użyć środowiska Windows PowerShell do instalowania aktualizacji trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="52586-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="52586-112">Każdy typ aktualizacji jest opisane oddzielnie, poniżej.</span><span class="sxs-lookup"><span data-stu-id="52586-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="52586-113">Regularne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="52586-113">Regular updates</span></span>
<span data-ttu-id="52586-114">Regularne aktualizacje są Brak aktualizacji, które mogą być instalowane, gdy urządzenie jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="52586-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="52586-115">Te aktualizacje są stosowane za pośrednictwem witryny Microsoft Update w każdym kontrolerze urządzenia.</span><span class="sxs-lookup"><span data-stu-id="52586-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="52586-116">Tryb failover kontroler może wystąpić podczas procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="52586-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="52586-117">Jednak nie wpłynie to dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="52586-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="52586-118">Aby uzyskać więcej informacji na temat instalowania regularne aktualizacje za pośrednictwem klasycznego portalu Azure, zobacz [zainstalować regularne aktualizacje za pośrednictwem klasycznego portalu Azure](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="52586-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="52586-119">Można także zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="52586-120">Aby uzyskać więcej informacji, zobacz [zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="52586-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="52586-121">Aktualizacje trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="52586-121">Maintenance mode updates</span></span>
<span data-ttu-id="52586-122">Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, takie jak aktualizacje oprogramowania dysku.</span><span class="sxs-lookup"><span data-stu-id="52586-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="52586-123">Te aktualizacje urządzenie musi znajdować się w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="52586-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="52586-124">Aby uzyskać więcej informacji, zobacz [krok 2: tryb konserwacji wprowadź](#step2).</span><span class="sxs-lookup"><span data-stu-id="52586-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="52586-125">Klasyczny portal Azure nie można używać do instalowania aktualizacji tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="52586-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="52586-126">Zamiast tego należy użyć programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="52586-127">Aby uzyskać więcej informacji na temat sposobu instalowania aktualizacji tryb konserwacji, zobacz [zainstalować obsługi trybu aktualizacje za pomocą programu Windows PowerShell dla StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="52586-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52586-128">Aktualizacje trybu konserwacji musi zostać zastosowana osobno na każdym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="52586-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="52586-129">Zainstaluj regularne aktualizacje za pośrednictwem klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52586-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="52586-130">Klasyczny portal Azure służy do stosowania aktualizacji na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="52586-131">Zainstaluj regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="52586-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="52586-132">Alternatywnie można użyć programu Windows PowerShell dla StorSimple do stosowania aktualizacji regularne (tryb normalny).</span><span class="sxs-lookup"><span data-stu-id="52586-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52586-133">Mimo że można zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple, zdecydowanie zaleca się zainstalowanie regularne aktualizacje za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="52586-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="52586-134">Począwszy od aktualizacji 1, wstępne sprawdzanie będzie przeprowadzane przed zainstalowaniem aktualizacji z portalu.</span><span class="sxs-lookup"><span data-stu-id="52586-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="52586-135">Kontrole wstępne będzie zastępują błędy i upewnij się, płynniejszy efekt.</span><span class="sxs-lookup"><span data-stu-id="52586-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="52586-136">Zainstaluj aktualizacje tryb konserwacji za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="52586-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="52586-137">Program Windows PowerShell dla StorSimple umożliwia stosowanie aktualizacji trybu konserwacji do urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="52586-138">Wszystkie żądania We/Wy są wstrzymane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="52586-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="52586-139">Usługi, takie jak trwałej pamięci (NVRAM) lub usługę klastrowania również zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="52586-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="52586-140">Zarówno kontrolery są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb.</span><span class="sxs-lookup"><span data-stu-id="52586-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="52586-141">Po zakończeniu pracy w tym trybie, wszystkie usługi zostanie wznowiona i powinna być w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="52586-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="52586-142">(Może to potrwać kilka minut).</span><span class="sxs-lookup"><span data-stu-id="52586-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="52586-143">Jeśli trzeba zastosować aktualizacje tryb konserwacji, otrzymasz alert przy użyciu klasycznego portalu Azure, czy są aktualizacje, które muszą zostać zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52586-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="52586-144">Ten alert zawiera instrukcje dotyczące instalowanie aktualizacji za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="52586-145">Po zaktualizowaniu urządzenia należy użyć tej samej procedury, aby zmienić urządzenia do trybu regularne.</span><span class="sxs-lookup"><span data-stu-id="52586-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="52586-146">Aby uzyskać instrukcje, zobacz [krok 4: tryb konserwacji zakończenia](#step4).</span><span class="sxs-lookup"><span data-stu-id="52586-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="52586-147">Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, sprawdzając **stan sprzętu** na **konserwacji** strony w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="52586-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="52586-148">Jeśli kontroler nie jest w dobrej kondycji, skontaktuj się z Microsoft Support następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="52586-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="52586-149">Aby uzyskać więcej informacji przejdź do skontaktuj się z pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52586-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="52586-150">Podczas pracy w trybie konserwacji, należy najpierw zastosować aktualizację na jeden kontroler, a następnie na innym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="52586-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="52586-151">Krok 1: Łączenie z konsolą szeregową<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="52586-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="52586-152">Po pierwsze korzystanie z aplikacji, takiego jak PuTTY dostęp do konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="52586-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="52586-153">W poniższej procedurze wyjaśniono sposób nawiązywania połączenia z konsolą szeregową przy użyciu programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="52586-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="52586-154">Krok 2: Wprowadź trybu konserwacji<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="52586-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="52586-155">Po połączeniu konsoli, należy ustalić, czy są aktualizacje do zainstalowania, a następnie przejść do trybu konserwacji na ich instalację.</span><span class="sxs-lookup"><span data-stu-id="52586-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="52586-156">Krok 3: Instalowanie aktualizacji<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="52586-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="52586-157">Następnie zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="52586-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="52586-158">Krok 4: Tryb obsługi zakończenia<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="52586-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="52586-159">Na koniec wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="52586-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="52586-160">Instalowanie poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="52586-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="52586-161">W przeciwieństwie do aktualizacji dla programu Microsoft Azure StorSimple są zainstalowane poprawki z folderu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="52586-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="52586-162">Podobnie jak w przypadku aktualizacji, istnieją dwa typy poprawki:</span><span class="sxs-lookup"><span data-stu-id="52586-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="52586-163">Regularne poprawki</span><span class="sxs-lookup"><span data-stu-id="52586-163">Regular hotfixes</span></span> 
* <span data-ttu-id="52586-164">Poprawki trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="52586-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="52586-165">Poniższe procedury dotyczą sposobu używania programu Windows PowerShell dla StorSimple zainstalować regularne i poprawki dla trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="52586-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="52586-166">Co się dzieje z aktualizacji w przypadku resetowania urządzenia do ustawień fabrycznych?</span><span class="sxs-lookup"><span data-stu-id="52586-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="52586-167">Jeśli urządzenie jest zresetowane do ustawień fabrycznych, wszystkie aktualizacje zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="52586-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="52586-168">Po rejestracji i konfiguracji Resetowanie do ustawień fabrycznych urządzenia, należy ręcznie zainstalować aktualizacje za pośrednictwem klasycznego portalu Azure i/lub środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="52586-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="52586-169">Aby uzyskać więcej informacji na temat resetowania do ustawień fabrycznych, zobacz [zresetowania urządzenia do domyślnych ustawień fabrycznych](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="52586-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52586-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52586-170">Next steps</span></span>
* <span data-ttu-id="52586-171">Dowiedz się więcej o [przy użyciu programu Windows PowerShell dla StorSimple do administrowania urządzeniem StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="52586-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="52586-172">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple do administrowania urządzeniem StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="52586-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

