---
title: "Zmień tryb urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano tryby urządzenia StorSimple i wyjaśniono, jak zmienić tryb urządzenia za pomocą programu Windows PowerShell dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="d9d4f-103">Zmień tryb urządzenia na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9d4f-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="d9d4f-104">Ten artykuł zawiera krótki opis różnych trybach, w których może działać urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="d9d4f-105">Urządzenia StorSimple może działać w trzech trybów: Normalny, obsługi i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="d9d4f-106">Po przeczytaniu tego artykułu, oznacza to:</span><span class="sxs-lookup"><span data-stu-id="d9d4f-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="d9d4f-107">Jakie tryby urządzenia StorSimple są</span><span class="sxs-lookup"><span data-stu-id="d9d4f-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="d9d4f-108">Znajduje się w sposób dowiedzieć się, który tryb urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9d4f-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="d9d4f-109">Jak zmienić z normalnym i tryb konserwacji i *na odwrót*</span><span class="sxs-lookup"><span data-stu-id="d9d4f-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="d9d4f-110">Powyżej zadań zarządzania można wykonać tylko za pośrednictwem interfejsu programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="d9d4f-111">Temat trybów urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9d4f-111">About StorSimple device modes</span></span>
<span data-ttu-id="d9d4f-112">Urządzenia StorSimple może działać w trybie normalnym, konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="d9d4f-113">Każdy z tych trybów krótko opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="d9d4f-114">Tryb normalny</span><span class="sxs-lookup"><span data-stu-id="d9d4f-114">Normal mode</span></span>
<span data-ttu-id="d9d4f-115">To jest zdefiniowana jako normalne tryb operacyjnych urządzenie StorSimple w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="d9d4f-116">Domyślnie urządzenia powinny być w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="d9d4f-117">Tryb konserwacji</span><span class="sxs-lookup"><span data-stu-id="d9d4f-117">Maintenance mode</span></span>
<span data-ttu-id="d9d4f-118">Czasami urządzenia StorSimple może być konieczne umieszczenie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="d9d4f-119">Ten tryb służy do przeprowadzania konserwacji na urządzeniu i zainstaluj aktualizacje destrukcyjne, takich jak powiązane z oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="d9d4f-120">System można umieścić w trybie konserwacji tylko przy użyciu programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d9d4f-121">Wszystkie żądania We/Wy są wstrzymane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="d9d4f-122">Usługi, takie jak trwałej pamięci (NVRAM) lub usługę klastrowania również zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="d9d4f-123">Zarówno kontrolery są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="d9d4f-124">Po wyjściu z trybu konserwacji, wszystkie usługi zostanie wznowiona i powinna być w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="d9d4f-125">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="d9d4f-126">**Tryb konserwacji jest obsługiwana tylko na urządzeniu działa prawidłowo. Nie jest obsługiwane na urządzeniu, w którym jednego lub obu kontrolerów nie działają.**
> </span><span class="sxs-lookup"><span data-stu-id="d9d4f-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="d9d4f-127">Tryb odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="d9d4f-127">Recovery mode</span></span>
<span data-ttu-id="d9d4f-128">Tryb odzyskiwania można określić jako "Tryb awaryjny dla systemu Windows z obsługą sieci".</span><span class="sxs-lookup"><span data-stu-id="d9d4f-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="d9d4f-129">Tryb odzyskiwania angażujący zespołu Support firmy Microsoft i umożliwia im wykonywanie diagnostyki w systemie.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="d9d4f-130">Podstawowym celem trybu odzyskiwania jest pobrać dzienniki systemu.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="d9d4f-131">System przechodzi do trybu odzyskiwania, należy skontaktować się Microsoft Support dalsze czynności.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="d9d4f-132">Aby uzyskać więcej informacji, przejdź do [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d9d4f-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9d4f-133">**Nie można umieścić urządzenia w trybie odzyskiwania. Jeśli urządzenie jest w złym stanie, tryb odzyskiwania próbuje pobrać urządzenia do stanu, w której personel firmy Microsoft Support można ją zbadać.**</span><span class="sxs-lookup"><span data-stu-id="d9d4f-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="d9d4f-134">Określić tryb urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9d4f-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="d9d4f-135">Aby określić bieżący tryb urządzenia</span><span class="sxs-lookup"><span data-stu-id="d9d4f-135">To determine the current device mode</span></span>
1. <span data-ttu-id="d9d4f-136">Zaloguj się do konsoli szeregowej urządzenia, wykonując kroki opisane w [przy użyciu programu PuTTY można nawiązać połączenia z konsolą szeregową urządzenia](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d9d4f-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d9d4f-137">Sprawdź komunikat transparentu, w menu konsoli szeregowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="d9d4f-138">Ten komunikat oznacza jawnie, czy urządzenie jest w trybie konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="d9d4f-139">Jeśli komunikat nie zawiera żadnych określonych informacji dotyczących trybu systemu, urządzenie jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="d9d4f-140">Zmień tryb urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="d9d4f-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="d9d4f-141">Urządzenia StorSimple można umieścić w tryb konserwacji (w trybie normalnym) do wykonania konserwacji lub instalowania aktualizacji tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="d9d4f-142">Wykonaj poniższe procedury, aby wprowadzić lub wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9d4f-143">Przed trybu konserwacji, sprawdź, czy zarówno kontrolery urządzeń są w dobrej kondycji po zalogowaniu się do **stan sprzętu** na **konserwacji** strony w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="d9d4f-144">Jeśli jeden lub oba kontrolery nie są w dobrej kondycji, skontaktuj się z Microsoft Support następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="d9d4f-145">Aby uzyskać więcej informacji, przejdź do [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d9d4f-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="d9d4f-146">Aby przejść do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="d9d4f-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="d9d4f-147">Zaloguj się do konsoli szeregowej urządzenia, wykonując kroki opisane w [przy użyciu programu PuTTY można nawiązać połączenia z konsolą szeregową urządzenia](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d9d4f-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d9d4f-148">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="d9d4f-149">Po wyświetleniu monitu podaj **hasło administratora urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="d9d4f-150">Domyślne hasło jest: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="d9d4f-151">W wierszu polecenia wpisz</span><span class="sxs-lookup"><span data-stu-id="d9d4f-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="d9d4f-152">Zobaczysz komunikat ostrzegawczy informujący o trybu konserwacji będzie zakłócać wszystkich żądań We/Wy i sever połączenia do klasycznego portalu Azure i zostanie wyświetlony monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="d9d4f-153">Typ **Y** do trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="d9d4f-154">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-154">Both controllers will restart.</span></span> <span data-ttu-id="d9d4f-155">Po zakończeniu ponownego uruchomienia innego pojawi się komunikat wskazujący, że urządzenie jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="d9d4f-156">Aby wyjść z trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="d9d4f-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="d9d4f-157">Zaloguj się do konsoli szeregowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-157">Log on to the device serial console.</span></span> <span data-ttu-id="d9d4f-158">Sprawdź z komunikat transparentu, że urządzenie jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="d9d4f-159">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="d9d4f-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="d9d4f-160">Zostanie wyświetlony komunikat ostrzegawczy i komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="d9d4f-161">Typ **Y** aby wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="d9d4f-162">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-162">Both controllers will restart.</span></span> <span data-ttu-id="d9d4f-163">Po zakończeniu ponownego uruchomienia innego pojawi się komunikat wskazujący, że urządzenie jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d4f-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9d4f-164">Next steps</span></span>
<span data-ttu-id="d9d4f-165">Dowiedz się, jak [stosowania aktualizacji tryb normalny i konserwacja](storsimple-update-device.md) na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d9d4f-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

