---
title: "aaaChange haseł StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello toochange usługi Menedżer StorSimple urządzenia StorSimple Snapshot Manager i urządzeń hasła administratora."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="b1a6e-103">Użyj toochange usługi Menedżer StorSimple urządzenia hello hasła StorSimple</span><span class="sxs-lookup"><span data-stu-id="b1a6e-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="b1a6e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b1a6e-104">Overview</span></span>
<span data-ttu-id="b1a6e-105">Witaj w portalu Azure **ustawienia urządzenia** opcja zawiera wszystkie parametry hello urządzenia, które można skonfigurować na urządzeniu StorSimple, które jest zarządzane przez usługę Menedżera urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="b1a6e-106">W tym samouczku opisano, jak używasz hello **zabezpieczeń** opcję w obszarze **ustawienia urządzenia** toochange administratora urządzenia lub hasło programu StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="b1a6e-107">Hasło administratora urządzenia hello zmiany</span><span class="sxs-lookup"><span data-stu-id="b1a6e-107">Change hello device administrator password</span></span>
<span data-ttu-id="b1a6e-108">Gdy używasz urządzenia StorSimple hello tooaccess interfejsu programu Windows PowerShell jest wymagane tooenter hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="b1a6e-109">Po zarejestrowaniu hello pierwszego urządzenia StorSimple z usługą hello domyślne hasło dla tego interfejsu jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="b1a6e-110">Dla bezpieczeństwa hello danych, są wymagane toochange hasła przy hello koniec hello procesu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="b1a6e-111">Nie można zamknąć z hello procesu rejestracji, bez zmiany hasła.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="b1a6e-112">Aby uzyskać więcej informacji, zobacz [krok 3: Konfigurowanie i rejestrowanie urządzenia hello przy użyciu programu Windows PowerShell dla StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b1a6e-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="b1a6e-113">hasło Hello najpierw ustawione za pośrednictwem interfejsu programu Windows PowerShell hello podczas rejestracji można później zmienić za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="b1a6e-114">Wykonaj powitania po hasło administratora urządzenia hello toochange czynności.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="b1a6e-115">hasło administratora urządzenia hello toochange</span><span class="sxs-lookup"><span data-stu-id="b1a6e-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="b1a6e-116">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="b1a6e-117">Z hello tabelarycznej listę urządzeń, wybierz i kliknij hello urządzenie, którego hasło ma toochange.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="b1a6e-118">W hello **ustawienia** bloku Przejdź zbyt**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="b1a6e-119">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **hasło** hasło administratora urządzenia hello toochange.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="b1a6e-120">W hello **hasło** bloku, który zawiera z 8 znaków too15 hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="b1a6e-121">Hello hasło musi zawierać kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="b1a6e-122">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="b1a6e-123">Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="b1a6e-124">należy teraz zaktualizować hasło administratora urządzenia Hello.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="b1a6e-125">Można użyć tego interfejsu programu Windows PowerShell hello tooaccess zmodyfikowane hasło.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="b1a6e-126">Ustaw hasło programu StorSimple Snapshot Manager hello</span><span class="sxs-lookup"><span data-stu-id="b1a6e-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="b1a6e-127">Oprogramowanie StorSimple Snapshot Manager znajduje się na hoście z systemem Windows i pozwala administratorom tworzenie kopii zapasowych toomanage urządzenia StorSimple w formie hello lokalne i migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="b1a6e-128">Podczas konfigurowania urządzenia StorSimple Snapshot Manager, zostanie wyświetlony monit tooprovide hello IP urządzenia tooauthenticate adres i hasło urządzenia magazynującego.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="b1a6e-129">Możesz ustawić lub zmienić hasło hello StorSimple Snapshot Manager za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="b1a6e-130">Wykonaj następujące kroki tooset hello, lub zmień hasło programu StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="b1a6e-131">hasło programu StorSimple Snapshot Manager hello tooset</span><span class="sxs-lookup"><span data-stu-id="b1a6e-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="b1a6e-132">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="b1a6e-133">Z hello tabelarycznej listę urządzeń, wybierz i kliknij urządzenie hello którego hasło programu StorSimple Snapshot Manager mają tooset lub zmienić.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="b1a6e-134">W hello **ustawienia** bloku Przejdź zbyt**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="b1a6e-135">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **hasło** tooset lub zmień hasło programu StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="b1a6e-136">W hello **hasło** bloku, wprowadź hasło składające się z 14 do 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="b1a6e-137">Upewnij się, że to hasło hello zawiera kombinację 3 lub więcej znaków wielkie litery, małe litery, liczbowych i specjalnych.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="b1a6e-138">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="b1a6e-139">Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="b1a6e-140">hasło programu StorSimple Snapshot Manager Hello teraz powinny zostać uaktualnione.</span><span class="sxs-lookup"><span data-stu-id="b1a6e-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a6e-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1a6e-141">Next steps</span></span>
* <span data-ttu-id="b1a6e-142">Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="b1a6e-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="b1a6e-143">Dowiedz się więcej o [modyfikowanie konfiguracji urządzenia](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="b1a6e-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="b1a6e-144">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b1a6e-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

