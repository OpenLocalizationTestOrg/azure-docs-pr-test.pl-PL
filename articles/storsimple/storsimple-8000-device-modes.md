---
title: "Tryb urządzenia StorSimple aaaChange | Dokumentacja firmy Microsoft"
description: "Zawiera opis tryby urządzenia StorSimple hello i jak toouse środowiska Windows PowerShell dla StorSimple toochange hello tryb urządzenia."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="73d84-103">Zmień tryb urządzenia hello na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="73d84-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="73d84-104">Ten artykuł zawiera krótki opis hello różnych trybach, w których może działać urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73d84-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="73d84-105">Urządzenia StorSimple może działać w trzech trybów: Normalny, obsługi i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="73d84-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="73d84-106">Po przeczytaniu tego artykułu, oznacza to:</span><span class="sxs-lookup"><span data-stu-id="73d84-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="73d84-107">Jakie są tryby urządzenia StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="73d84-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="73d84-108">Jak toofigure limit trybu hello urządzenia StorSimple znajduje się w</span><span class="sxs-lookup"><span data-stu-id="73d84-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="73d84-109">Jak toochange w trybie normalnym toomaintenance i *na odwrót*</span><span class="sxs-lookup"><span data-stu-id="73d84-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="73d84-110">Witaj powyżej zadania związane z zarządzaniem można wykonać tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73d84-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="73d84-111">Temat trybów urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="73d84-111">About StorSimple device modes</span></span>

<span data-ttu-id="73d84-112">Urządzenia StorSimple może działać w trybie normalnym, konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="73d84-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="73d84-113">Każdy z tych trybów krótko opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="73d84-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="73d84-114">Tryb normalny</span><span class="sxs-lookup"><span data-stu-id="73d84-114">Normal mode</span></span>

<span data-ttu-id="73d84-115">To jest zdefiniowany jako hello normalnym trybem operacyjnych urządzenie StorSimple w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="73d84-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="73d84-116">Domyślnie urządzenia powinny być w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="73d84-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="73d84-117">Tryb konserwacji</span><span class="sxs-lookup"><span data-stu-id="73d84-117">Maintenance mode</span></span>

<span data-ttu-id="73d84-118">Czasami hello urządzenia StorSimple może być konieczne toobe przełączony w tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="73d84-119">Ten tryb umożliwia tooperform konserwacji na urządzeniu hello i zainstaluj destrukcyjne aktualizacje, takie jak te dotyczące toodisk oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="73d84-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="73d84-120">Hello system można umieścić w tryb konserwacji tylko przy użyciu hello środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73d84-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="73d84-121">Wszystkie żądania We/Wy są wstrzymane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="73d84-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="73d84-122">Usług takich jak trwałej pamięci (NVRAM) lub usługa klastrowania hello również zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="73d84-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="73d84-123">Zarówno kontrolery hello są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb.</span><span class="sxs-lookup"><span data-stu-id="73d84-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="73d84-124">Po wyjściu z trybu konserwacji hello, wszystkie usługi hello wznowi i powinna być w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="73d84-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="73d84-125">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="73d84-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="73d84-126">**Tryb konserwacji jest obsługiwana tylko na urządzeniu działa prawidłowo. Nie jest obsługiwane na urządzeniu, w którym jednego lub obu kontrolerów hello nie działają.**</span><span class="sxs-lookup"><span data-stu-id="73d84-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="73d84-127">Tryb odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="73d84-127">Recovery mode</span></span>

<span data-ttu-id="73d84-128">Tryb odzyskiwania można określić jako "Tryb awaryjny dla systemu Windows z obsługą sieci".</span><span class="sxs-lookup"><span data-stu-id="73d84-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="73d84-129">Tryb odzyskiwania angażujący zespołu Microsoft Support hello oraz pozwala tooperform diagnostyki w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="73d84-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="73d84-130">podstawowym celem Hello trybu odzyskiwania jest dzienniki systemu hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="73d84-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="73d84-131">System przechodzi do trybu odzyskiwania, należy skontaktować się Microsoft Support dalsze czynności.</span><span class="sxs-lookup"><span data-stu-id="73d84-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="73d84-132">Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="73d84-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="73d84-133">**Nie można umieścić hello urządzenia w trybie odzyskiwania. Jeśli urządzenie hello jest w złym stanie, tryb odzyskiwania próbuje tooget hello urządzenia do stanu, w której personel firmy Microsoft Support można sprawdzić jego.**</span><span class="sxs-lookup"><span data-stu-id="73d84-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="73d84-134">Określić tryb urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="73d84-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="73d84-135">bieżący tryb urządzenia toodetermine hello</span><span class="sxs-lookup"><span data-stu-id="73d84-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="73d84-136">Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="73d84-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="73d84-137">Sprawdź komunikat transparentu hello w menu konsoli szeregowej hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="73d84-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="73d84-138">Ten komunikat oznacza jawnie, czy urządzenie hello jest w trybie konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="73d84-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="73d84-139">Jeśli wiadomość hello nie zawiera żadnych określonych informacji dotyczących trybu systemu toohello, urządzenie hello jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="73d84-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="73d84-140">Zmień tryb urządzenia StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="73d84-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="73d84-141">Możesz umieścić hello urządzenia StorSimple do obsługi trybu (w trybie normalnym) tooperform konserwacji lub aktualizacji trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="73d84-142">Wykonaj następujące procedury tooenter lub zakończenia trybu konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="73d84-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73d84-143">Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, uzyskując dostęp do hello **ustawienia urządzenia > kondycji sprzętu** dla urządzenia w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="73d84-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="73d84-144">Jeśli jeden lub oba kontrolerów hello nie jest dobra, skontaktuj się z Microsoft Support hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="73d84-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="73d84-145">Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="73d84-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="73d84-146">Tryb konserwacji tooenter</span><span class="sxs-lookup"><span data-stu-id="73d84-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="73d84-147">Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="73d84-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="73d84-148">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="73d84-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="73d84-149">Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="73d84-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="73d84-150">jest Hello domyślne hasło: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="73d84-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="73d84-151">Wpisz w wierszu polecenia hello</span><span class="sxs-lookup"><span data-stu-id="73d84-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="73d84-152">Pojawi się komunikat ostrzegawczy informujący, że tryb konserwacji będzie zakłócać wszystkich żądań We/Wy i sever hello połączenia toohello portalu Azure i zostanie wyświetlony monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="73d84-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="73d84-153">Typ **Y** tooenter tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="73d84-154">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="73d84-154">Both controllers will restart.</span></span> <span data-ttu-id="73d84-155">Po zakończeniu ponownego uruchomienia hello transparent konsoli szeregowej hello będzie wskazująca, że urządzenie hello jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="73d84-156">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="73d84-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="73d84-157">Tryb konserwacji tooexit</span><span class="sxs-lookup"><span data-stu-id="73d84-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="73d84-158">Zaloguj się na konsoli szeregowej urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="73d84-158">Log on toohello device serial console.</span></span> <span data-ttu-id="73d84-159">Sprawdź z hello komunikat transparentu, że urządzenie jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="73d84-160">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="73d84-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="73d84-161">Zostanie wyświetlony komunikat ostrzegawczy i komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="73d84-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="73d84-162">Typ **Y** tooexit tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="73d84-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="73d84-163">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="73d84-163">Both controllers will restart.</span></span> <span data-ttu-id="73d84-164">Po zakończeniu ponownego uruchomienia hello hello transparent konsoli szeregowej wskazuje, że urządzenie tym hello jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="73d84-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="73d84-165">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="73d84-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="73d84-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73d84-166">Next steps</span></span>

<span data-ttu-id="73d84-167">Dowiedz się, jak za[stosowania aktualizacji tryb normalny i konserwacja](storsimple-update-device.md) na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73d84-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

