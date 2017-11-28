---
title: "Tryb urządzenia StorSimple hello aaaChange | Dokumentacja firmy Microsoft"
description: "Zawiera opis tryby urządzenia StorSimple hello i jak toouse środowiska Windows PowerShell dla StorSimple toochange hello tryb urządzenia."
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
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="58c46-103">Zmień tryb urządzenia hello na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="58c46-103">Change hello device mode on your StorSimple device</span></span>
<span data-ttu-id="58c46-104">Ten artykuł zawiera krótki opis hello różnych trybach, w których może działać urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="58c46-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="58c46-105">Urządzenia StorSimple może działać w trzech trybów: Normalny, obsługi i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="58c46-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="58c46-106">Po przeczytaniu tego artykułu, oznacza to:</span><span class="sxs-lookup"><span data-stu-id="58c46-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="58c46-107">Jakie są tryby urządzenia StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="58c46-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="58c46-108">Jak toofigure limit trybu hello urządzenia StorSimple znajduje się w</span><span class="sxs-lookup"><span data-stu-id="58c46-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="58c46-109">Jak toochange w trybie normalnym toomaintenance i *na odwrót*</span><span class="sxs-lookup"><span data-stu-id="58c46-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="58c46-110">Witaj powyżej zadania związane z zarządzaniem można wykonać tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="58c46-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="58c46-111">Temat trybów urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="58c46-111">About StorSimple device modes</span></span>
<span data-ttu-id="58c46-112">Urządzenia StorSimple może działać w trybie normalnym, konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="58c46-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="58c46-113">Każdy z tych trybów krótko opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="58c46-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="58c46-114">Tryb normalny</span><span class="sxs-lookup"><span data-stu-id="58c46-114">Normal mode</span></span>
<span data-ttu-id="58c46-115">To jest zdefiniowany jako hello normalnym trybem operacyjnych urządzenie StorSimple w pełni skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="58c46-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="58c46-116">Domyślnie urządzenia powinny być w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="58c46-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="58c46-117">Tryb konserwacji</span><span class="sxs-lookup"><span data-stu-id="58c46-117">Maintenance mode</span></span>
<span data-ttu-id="58c46-118">Czasami hello urządzenia StorSimple może być konieczne toobe przełączony w tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="58c46-119">Ten tryb umożliwia tooperform konserwacji na urządzeniu hello i zainstaluj destrukcyjne aktualizacje, takie jak te dotyczące toodisk oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="58c46-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="58c46-120">Hello system można umieścić w tryb konserwacji tylko przy użyciu hello środowiska Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="58c46-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="58c46-121">Wszystkie żądania We/Wy są wstrzymane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="58c46-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="58c46-122">Usług takich jak trwałej pamięci (NVRAM) lub usługa klastrowania hello również zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="58c46-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="58c46-123">Zarówno kontrolery hello są ponownie uruchamiane po wprowadzeniu lub opuścić ten tryb.</span><span class="sxs-lookup"><span data-stu-id="58c46-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="58c46-124">Po wyjściu z trybu konserwacji hello, wszystkie usługi hello wznowi i powinna być w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="58c46-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="58c46-125">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="58c46-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="58c46-126">**Tryb konserwacji jest obsługiwana tylko na urządzeniu działa prawidłowo. Nie jest obsługiwane na urządzeniu, w którym jednego lub obu kontrolerów hello nie działają.**
> </span><span class="sxs-lookup"><span data-stu-id="58c46-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="58c46-127">Tryb odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="58c46-127">Recovery mode</span></span>
<span data-ttu-id="58c46-128">Tryb odzyskiwania można określić jako "Tryb awaryjny dla systemu Windows z obsługą sieci".</span><span class="sxs-lookup"><span data-stu-id="58c46-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="58c46-129">Tryb odzyskiwania angażujący zespołu Microsoft Support hello oraz pozwala tooperform diagnostyki w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="58c46-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="58c46-130">podstawowym celem Hello trybu odzyskiwania jest dzienniki systemu hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="58c46-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="58c46-131">System przechodzi do trybu odzyskiwania, należy skontaktować się Microsoft Support dalsze czynności.</span><span class="sxs-lookup"><span data-stu-id="58c46-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="58c46-132">Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="58c46-132">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58c46-133">**Nie można umieścić hello urządzenia w trybie odzyskiwania. Jeśli urządzenie hello jest w złym stanie, tryb odzyskiwania próbuje tooget hello urządzenia do stanu, w której personel firmy Microsoft Support można sprawdzić jego.**</span><span class="sxs-lookup"><span data-stu-id="58c46-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="58c46-134">Określić tryb urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="58c46-134">Determine StorSimple device mode</span></span>
#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="58c46-135">bieżący tryb urządzenia toodetermine hello</span><span class="sxs-lookup"><span data-stu-id="58c46-135">toodetermine hello current device mode</span></span>
1. <span data-ttu-id="58c46-136">Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="58c46-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="58c46-137">Sprawdź komunikat transparentu hello w menu konsoli szeregowej hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="58c46-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="58c46-138">Ten komunikat oznacza jawnie, czy urządzenie hello jest w trybie konserwacji lub odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="58c46-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="58c46-139">Jeśli wiadomość hello nie zawiera żadnych określonych informacji dotyczących trybu systemu toohello, urządzenie hello jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="58c46-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="58c46-140">Zmień tryb urządzenia StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="58c46-140">Change hello StorSimple device mode</span></span>
<span data-ttu-id="58c46-141">Możesz umieścić hello urządzenia StorSimple do obsługi trybu (w trybie normalnym) tooperform konserwacji lub aktualizacji trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="58c46-142">Wykonaj następujące procedury tooenter lub zakończenia trybu konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="58c46-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58c46-143">Przed wprowadzeniem tryb konserwacji, sprawdź, czy zarówno kontrolery urządzeń są dobrej kondycji, uzyskując dostęp do hello **stan sprzętu** na powitania **konserwacji** strony w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58c46-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="58c46-144">Jeśli jeden lub oba kontrolerów hello nie jest dobra, skontaktuj się z Microsoft Support hello następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="58c46-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="58c46-145">Aby uzyskać więcej informacji, przejdź zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="58c46-145">For more information, go too[Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="58c46-146">Tryb konserwacji tooenter</span><span class="sxs-lookup"><span data-stu-id="58c46-146">tooenter maintenance mode</span></span>
1. <span data-ttu-id="58c46-147">Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="58c46-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="58c46-148">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="58c46-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="58c46-149">Po wyświetleniu monitu podaj hello **hasło administratora urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="58c46-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="58c46-150">jest Hello domyślne hasło: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="58c46-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="58c46-151">Wpisz w wierszu polecenia hello</span><span class="sxs-lookup"><span data-stu-id="58c46-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="58c46-152">Pojawi się komunikat ostrzegawczy informujący, że tryb konserwacji będzie zakłócać wszystkich żądań We/Wy i sever hello połączenia toohello klasycznego portalu Azure i zostanie wyświetlony monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="58c46-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="58c46-153">Typ **Y** tooenter tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="58c46-154">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="58c46-154">Both controllers will restart.</span></span> <span data-ttu-id="58c46-155">Po zakończeniu ponownego uruchomienia hello innego pojawi się komunikat wskazujący, że urządzenie hello jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-155">When hello restart is complete, another message will appear indicating that hello device is in maintenance mode.</span></span>

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="58c46-156">Tryb konserwacji tooexit</span><span class="sxs-lookup"><span data-stu-id="58c46-156">tooexit maintenance mode</span></span>
1. <span data-ttu-id="58c46-157">Zaloguj się na konsoli szeregowej urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="58c46-157">Log on toohello device serial console.</span></span> <span data-ttu-id="58c46-158">Sprawdź z hello komunikat transparentu, że urządzenie jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-158">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="58c46-159">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="58c46-159">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="58c46-160">Zostanie wyświetlony komunikat ostrzegawczy i komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="58c46-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="58c46-161">Typ **Y** tooexit tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="58c46-161">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="58c46-162">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="58c46-162">Both controllers will restart.</span></span> <span data-ttu-id="58c46-163">Po zakończeniu ponownego uruchomienia hello innego pojawi się komunikat wskazujący, że urządzenie tym hello jest w trybie normalnym.</span><span class="sxs-lookup"><span data-stu-id="58c46-163">When hello restart is complete, another message will appear indicating that hello device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58c46-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58c46-164">Next steps</span></span>
<span data-ttu-id="58c46-165">Dowiedz się, jak za[stosowania aktualizacji tryb normalny i konserwacja](storsimple-update-device.md) na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="58c46-165">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

