---
title: "hasło administratora urządzenia StorSimple wirtualnego tablicy aaaChange | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse albo hello portalu Azure lub interfejsu użytkownika sieci web tablicy wirtualnego StorSimple toochange hasło administratora urządzenia hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="ef741-103">Zmień hasło administratora urządzenia StorSimple wirtualnego tablicy hello za pomocą Menedżera urządzeń StorSimple</span><span class="sxs-lookup"><span data-stu-id="ef741-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="ef741-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ef741-104">Overview</span></span>

<span data-ttu-id="ef741-105">Gdy używasz tooaccess interfejsu programu Windows PowerShell hello hello tablicy wirtualnego StorSimple, są wymagane tooenter hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ef741-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="ef741-106">Gdy urządzenie StorSimple hello jest najpierw udostępnione i uruchomiony, jest hello domyślne hasło *Password1*.</span><span class="sxs-lookup"><span data-stu-id="ef741-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="ef741-107">Dla bezpieczeństwa hello danych, hello domyślne hasło wygaśnie hello zalogowaniu się po raz pierwszy, a są toochange wymagane hasło.</span><span class="sxs-lookup"><span data-stu-id="ef741-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="ef741-108">Umożliwia także albo hello lokalnej sieci web interfejsu użytkownika lub hello Azure toochange portalu hello hasło administratora urządzenia w dowolnej chwili po wdrożeniu urządzenia hello w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="ef741-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="ef741-109">W tym artykule opisano każdy z tych procedur.</span><span class="sxs-lookup"><span data-stu-id="ef741-109">Each of these procedures is described in this article.</span></span>

 ![Blok urządzeń](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="ef741-111">Użyj hello Azure toochange portalu hello hasła</span><span class="sxs-lookup"><span data-stu-id="ef741-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="ef741-112">Wykonaj następujące kroki toochange hello hasło administratora urządzenia za pośrednictwem portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="ef741-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="ef741-113">hasło administratora urządzenia hello toochange za pośrednictwem hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ef741-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="ef741-114">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **zarządzania** kliknij **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="ef741-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="ef741-115">Spowoduje to otwarcie hello **urządzeń** bloku, który zawiera listę wszystkich urządzeń wirtualnych tablicy StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ef741-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="ef741-116">W hello **urządzeń** bloku, kliknij dwukrotnie urządzenie hello, który wymaga zmiany hasła.</span><span class="sxs-lookup"><span data-stu-id="ef741-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="ef741-117">W hello **ustawienia** bloku dla danego urządzenia, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="ef741-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="ef741-118">W hello **ustawienia zabezpieczeń** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ef741-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="ef741-119">Przewiń w dół toohello **hasło administratora urządzenia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef741-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="ef741-120">Podaj hasło administratora, który zawiera z 8 znaków too15.</span><span class="sxs-lookup"><span data-stu-id="ef741-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="ef741-121">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="ef741-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="ef741-122">Kliknij przycisk **zapisać** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="ef741-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="ef741-123">hasło administratora urządzenia Hello jest już uaktualniona.</span><span class="sxs-lookup"><span data-stu-id="ef741-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="ef741-124">Można użyć tego hasła zmodyfikowanych tooaccess hello urządzenia lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ef741-124">You can use this modified password tooaccess hello device locally.</span></span>

![Blok ustawień zabezpieczeń](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="ef741-126">Użyj hello lokalnej sieci web UI toochange hello hasła</span><span class="sxs-lookup"><span data-stu-id="ef741-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="ef741-127">Wykonaj następujące kroki toochange hello hasło administratora urządzenia za pośrednictwem lokalne powitania interfejsu użytkownika sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="ef741-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="ef741-128">hasło administratora urządzenia hello toochange za pośrednictwem lokalne powitania interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="ef741-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="ef741-129">W hello lokalnego interfejsu użytkownika sieci web, kliknij przycisk **konserwacji** > **zmiany hasła** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ef741-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![Zmień password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="ef741-131">Wprowadź hello **bieżące hasło**.</span><span class="sxs-lookup"><span data-stu-id="ef741-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="ef741-132">Podaj **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="ef741-132">Provide a **New Password**.</span></span> <span data-ttu-id="ef741-133">Witaj hasło musi być co najmniej 8 znaków.</span><span class="sxs-lookup"><span data-stu-id="ef741-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="ef741-134">Musi zawierać 3 z 4 poniżej hello: wielkie litery, małe litery, liczbowego i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="ef741-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="ef741-135">Należy pamiętać, że hasło nie może być hello tak samo jak hello ostatnie 24 haseł.</span><span class="sxs-lookup"><span data-stu-id="ef741-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="ef741-136">Wprowadź ponownie tooconfirm hasło hello go.</span><span class="sxs-lookup"><span data-stu-id="ef741-136">Reenter hello password tooconfirm it.</span></span>
   
    ![Zmień Hasło2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="ef741-138">U dołu hello hello strony, kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="ef741-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="ef741-139">teraz zastosowano Hello nowe hasło.</span><span class="sxs-lookup"><span data-stu-id="ef741-139">hello new password is now applied.</span></span> <span data-ttu-id="ef741-140">Jeśli zmiana hasła hello zakończy się niepowodzeniem, zostanie wyświetlony hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="ef741-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![Błąd hasła](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="ef741-142">Po pomyślnej aktualizacji hasła hello, użytkownik jest powiadamiany.</span><span class="sxs-lookup"><span data-stu-id="ef741-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="ef741-143">To hasło modyfikacji tooaccess hello urządzenia można następnie użyć lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ef741-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ef741-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef741-144">Next steps</span></span>
<span data-ttu-id="ef741-145">Dowiedz się, jak za[administrowania tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="ef741-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

