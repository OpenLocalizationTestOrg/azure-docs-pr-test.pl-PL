---
title: "aaaUpdate urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak toouse hello StorSimple aktualizacji funkcji tooinstall regularnych i obsługi trybu aktualizacje i poprawki."
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
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="7464b-103">Zaktualizuj urządzenia z serii StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="7464b-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="7464b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7464b-104">Overview</span></span>
<span data-ttu-id="7464b-105">Hello StorSimple aktualizacje funkcji pozwalają tooeasily aktualizowanie urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7464b-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="7464b-106">W zależności od typu aktualizacji hello należy zastosować aktualizacje toohello urządzenia za pośrednictwem hello klasycznego portalu Azure lub za pośrednictwem interfejsu programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7464b-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="7464b-107">W tym samouczku opisano typy aktualizacji hello i w jaki sposób tooinstall każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="7464b-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="7464b-108">Można zastosować dwa typy aktualizacji urządzenia:</span><span class="sxs-lookup"><span data-stu-id="7464b-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="7464b-109">Regularne (lub tryb normalny) aktualizacji</span><span class="sxs-lookup"><span data-stu-id="7464b-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="7464b-110">Aktualizacje trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="7464b-110">Maintenance mode updates</span></span>

<span data-ttu-id="7464b-111">Możesz zainstalować regularne aktualizacje za pośrednictwem hello klasycznego portalu Azure lub programu Windows PowerShell; należy jednak używać aktualizacji trybu konserwacji tooinstall środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7464b-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="7464b-112">Każdy typ aktualizacji jest opisane oddzielnie, poniżej.</span><span class="sxs-lookup"><span data-stu-id="7464b-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="7464b-113">Regularne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="7464b-113">Regular updates</span></span>
<span data-ttu-id="7464b-114">Regularne aktualizacje są Brak aktualizacji, które mogą być instalowane, gdy urządzenie hello jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="7464b-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="7464b-115">Aktualizacje te są stosowane przy użyciu hello Microsoft Update witryny sieci Web tooeach urządzenia kontrolera.</span><span class="sxs-lookup"><span data-stu-id="7464b-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7464b-116">Tryb failover kontrolera mogą wystąpić podczas procesu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="7464b-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="7464b-117">Jednak nie wpłynie to dostępność systemu lub operacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="7464b-118">Szczegółowe informacje dotyczące sposobu tooinstall regular aktualizacje za pośrednictwem hello klasycznego portalu Azure, zobacz [zainstalować regularne aktualizacje za pośrednictwem klasycznego portalu Azure hello](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="7464b-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="7464b-119">Można także zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7464b-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7464b-120">Aby uzyskać więcej informacji, zobacz [zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="7464b-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="7464b-121">Aktualizacje trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="7464b-121">Maintenance mode updates</span></span>
<span data-ttu-id="7464b-122">Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, takie jak aktualizacje oprogramowania dysku.</span><span class="sxs-lookup"><span data-stu-id="7464b-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="7464b-123">Te aktualizacje wymagają toobe urządzenia hello przełączyć w tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="7464b-124">Aby uzyskać więcej informacji, zobacz [krok 2: tryb konserwacji wprowadź](#step2).</span><span class="sxs-lookup"><span data-stu-id="7464b-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="7464b-125">Nie można użyć hello Azure classic portal tooinstall obsługi trybu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="7464b-126">Zamiast tego należy użyć programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7464b-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="7464b-127">Aby uzyskać szczegółowe informacje na sposób aktualizowania tooinstall tryb konserwacji, zobacz [zainstalować obsługi trybu aktualizacje za pomocą programu Windows PowerShell dla StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="7464b-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7464b-128">Tryb konserwacji, aktualizacje należy zastosować oddzielnie tooeach kontrolera.</span><span class="sxs-lookup"><span data-stu-id="7464b-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="7464b-129">Zainstaluj regularne aktualizacje za pomocą hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7464b-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="7464b-130">Można użyć urządzenia StorSimple tooyour hello Azure classic portal tooapply aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7464b-131">Zainstaluj regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="7464b-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7464b-132">Alternatywnie można użyć programu Windows PowerShell aktualizacji regularne (tryb normalny) tooapply StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7464b-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7464b-133">Mimo że można zainstalować regularne aktualizacje za pomocą środowiska Windows PowerShell dla urządzenia StorSimple, zdecydowanie zaleca się zainstalowanie regularne aktualizacje za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7464b-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="7464b-134">Począwszy od aktualizacji 1, wstępne sprawdzanie jest wykonywane wcześniejsze tooinstalling aktualizacje z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7464b-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="7464b-135">Kontrole wstępne będzie zastępują błędy i upewnij się, płynniejszy efekt.</span><span class="sxs-lookup"><span data-stu-id="7464b-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7464b-136">Zainstaluj aktualizacje tryb konserwacji za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="7464b-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7464b-137">Korzystając z programu Windows PowerShell dla urządzenia StorSimple tooyour StorSimple tooapply obsługi trybu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="7464b-138">Wszystkie żądania We/Wy są wstrzymane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="7464b-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="7464b-139">Usług takich jak trwałej pamięci (NVRAM) lub usługa klastrowania hello również zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="7464b-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="7464b-140">Zarówno kontrolery są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb.</span><span class="sxs-lookup"><span data-stu-id="7464b-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="7464b-141">Po zakończeniu pracy w tym trybie, wszystkie usługi hello wznowi i powinna być w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="7464b-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="7464b-142">(Może to potrwać kilka minut).</span><span class="sxs-lookup"><span data-stu-id="7464b-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="7464b-143">Aktualizacje trybu konserwacji tooapply należy otrzymasz alert za pośrednictwem hello klasycznego portalu Azure, czy są aktualizacje, które muszą zostać zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="7464b-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="7464b-144">Ten alert zawiera instrukcje dotyczące używania środowiska Windows PowerShell dla StorSimple tooinstall hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="7464b-145">Po zaktualizowaniu urządzenia, użyj hello sam tryb tooRegular procedury toochange hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7464b-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="7464b-146">Aby uzyskać instrukcje, zobacz [krok 4: tryb konserwacji zakończenia](#step4).</span><span class="sxs-lookup"><span data-stu-id="7464b-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7464b-147">Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, sprawdzając hello **stan sprzętu** na powitania **konserwacji** strony w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7464b-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="7464b-148">Jeśli kontroler hello nie działa prawidłowo, skontaktuj się z Microsoft Support hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="7464b-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="7464b-149">Aby uzyskać więcej informacji Przejdź tooContact Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7464b-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="7464b-150">Podczas pracy w trybie konserwacji, należy tooapply hello aktualizacji najpierw na jeden kontroler, a następnie na hello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="7464b-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="7464b-151">Krok 1: Łączenie toohello konsoli szeregowej<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="7464b-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="7464b-152">Po pierwsze korzystanie z aplikacji, takich jak PuTTY tooaccess hello konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="7464b-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="7464b-153">Witaj poniższej procedurze wyjaśniono, jak konsoli szeregowej toohello toouse PuTTY tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7464b-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="7464b-154">Krok 2: Wprowadź trybu konserwacji<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="7464b-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="7464b-155">Po podłączeniu konsoli toohello ustalić, czy są aktualizacje tooinstall, a następnie wprowadź tooinstall trybu konserwacji je.</span><span class="sxs-lookup"><span data-stu-id="7464b-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="7464b-156">Krok 3: Instalowanie aktualizacji<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="7464b-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="7464b-157">Następnie zainstaluj aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="7464b-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="7464b-158">Krok 4: Tryb obsługi zakończenia<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="7464b-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="7464b-159">Na koniec wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="7464b-160">Instalowanie poprawek za pomocą środowiska Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="7464b-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7464b-161">W przeciwieństwie do aktualizacji dla programu Microsoft Azure StorSimple są zainstalowane poprawki z folderu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="7464b-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="7464b-162">Podobnie jak w przypadku aktualizacji, istnieją dwa typy poprawki:</span><span class="sxs-lookup"><span data-stu-id="7464b-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="7464b-163">Regularne poprawki</span><span class="sxs-lookup"><span data-stu-id="7464b-163">Regular hotfixes</span></span> 
* <span data-ttu-id="7464b-164">Poprawki trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="7464b-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="7464b-165">Witaj poniższe procedury wyjaśniają, jak toouse środowiska Windows PowerShell dla regularne tooinstall StorSimple i poprawki dla trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="7464b-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="7464b-166">Co się stanie, resetowania urządzenia hello tooupdates Jeśli przeprowadzenie do ustawień fabrycznych?</span><span class="sxs-lookup"><span data-stu-id="7464b-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="7464b-167">Jeśli urządzenie jest ustawienia toofactory resetowania, wszystkie aktualizacje hello zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="7464b-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="7464b-168">Po rejestracji i konfiguracji hello Resetowanie do ustawień fabrycznych urządzenia należy toomanually Zainstaluj aktualizacje za pośrednictwem hello klasycznego portalu Azure i/lub środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7464b-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7464b-169">Aby uzyskać więcej informacji na temat resetowania do ustawień fabrycznych, zobacz [przywrócić ustawienia domyślne toofactory urządzenia hello](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="7464b-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7464b-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7464b-170">Next steps</span></span>
* <span data-ttu-id="7464b-171">Dowiedz się więcej o [środowiska Windows PowerShell dla StorSimple tooadminister urządzenia StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7464b-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="7464b-172">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7464b-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

