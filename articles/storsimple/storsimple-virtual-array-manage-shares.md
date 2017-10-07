---
title: "udostępnia tablicy wirtualnego StorSimple aaaManage | Dokumentacja firmy Microsoft"
description: "Zawiera opis hello Menedżera urządzeń StorSimple i jak toouse on toomanage udziałów na tablica wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="18ce4-103">Użyj udziałów toomanage usługi Menedżer StorSimple urządzenia hello na powitania tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="18ce4-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="18ce4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="18ce4-104">Overview</span></span>

<span data-ttu-id="18ce4-105">W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać udziałami w macierzy wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="18ce4-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="18ce4-106">Witaj usługi Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="18ce4-107">Dodanie toomanaging udziałów i woluminów można użyć tooview usługi Menedżer StorSimple urządzenia hello i zarządzanie urządzeniami, wyświetlanie alertów, zarządzania zasad tworzenia kopii zapasowych oraz zarządzania hello katalogu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="18ce4-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="18ce4-108">Typy udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-108">Share Types</span></span>

<span data-ttu-id="18ce4-109">Udziały StorSimple można:</span><span class="sxs-lookup"><span data-stu-id="18ce4-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="18ce4-110">**Przypięty lokalnie**: dane w tych udziałach pozostaje w macierzy hello przez cały czas i nie zostaną przeniesione toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="18ce4-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="18ce4-111">**Do warstwy**: dane w tych udziałach można zostaną przeniesione toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="18ce4-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="18ce4-112">Podczas tworzenia udziału warstwowych około 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="18ce4-113">Na przykład jeśli udostępniane udziału 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="18ce4-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="18ce4-114">Z kolei oznacza to, że jeśli zabraknie wszystkie lokalne powitania miejsce na urządzeniu hello nie można dostarczać warstwowych udziału (ponieważ hello 10% wymaganych na lokalne powitania warstwa nie będzie dostępna).</span><span class="sxs-lookup"><span data-stu-id="18ce4-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="18ce4-115">Udostępnione pojemności</span><span class="sxs-lookup"><span data-stu-id="18ce4-115">Provisioned capacity</span></span>

<span data-ttu-id="18ce4-116">Można znaleźć w poniższej tabeli dla maksymalnej pojemności udostępnione dla każdego typu udziału toohello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="18ce4-117">**Identyfikator limit**</span><span class="sxs-lookup"><span data-stu-id="18ce4-117">**Limit identifier**</span></span> | <span data-ttu-id="18ce4-118">**Limit**</span><span class="sxs-lookup"><span data-stu-id="18ce4-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="18ce4-119">Minimalny rozmiar udziału warstwowych</span><span class="sxs-lookup"><span data-stu-id="18ce4-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="18ce4-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="18ce4-120">500 GB</span></span> |
| <span data-ttu-id="18ce4-121">Maksymalny rozmiar udziału warstwowych</span><span class="sxs-lookup"><span data-stu-id="18ce4-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="18ce4-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="18ce4-122">20 TB</span></span> |
| <span data-ttu-id="18ce4-123">Minimalny rozmiar udziału przypiętych lokalnie</span><span class="sxs-lookup"><span data-stu-id="18ce4-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="18ce4-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="18ce4-124">50 GB</span></span> |
| <span data-ttu-id="18ce4-125">Maksymalny rozmiar udziału przypiętych lokalnie</span><span class="sxs-lookup"><span data-stu-id="18ce4-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="18ce4-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="18ce4-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="18ce4-127">Witaj udziałów bloku</span><span class="sxs-lookup"><span data-stu-id="18ce4-127">hello Shares blade</span></span>

<span data-ttu-id="18ce4-128">Witaj **udziałów** menu w bloku podsumowania usługi StorSimple Wyświetla listę hello udziałów magazynu w danej macierzy StorSimple i pozwala toomanage je.</span><span class="sxs-lookup"><span data-stu-id="18ce4-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Udziałów bloku](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="18ce4-130">Udział składa się z szeregu atrybuty:</span><span class="sxs-lookup"><span data-stu-id="18ce4-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="18ce4-131">**Nazwa udziału** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="18ce4-132">**Stan** — może być w trybie online lub offline.</span><span class="sxs-lookup"><span data-stu-id="18ce4-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="18ce4-133">Jeśli udział jest w trybie offline, użytkownicy udziału hello nie będą mogli tooaccess go.</span><span class="sxs-lookup"><span data-stu-id="18ce4-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="18ce4-134">**Typ** — wskazuje, czy udział hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="18ce4-135">**Pojemność** — określa ilość hello danych używana jako porównaniu toohello łączna ilość danych, które mogą być przechowywane w udziale hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="18ce4-136">**Opis elementu** — ustawienie opcjonalne pomaga opisano hello udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="18ce4-137">**Uprawnienia** -udziału toohello uprawnienia systemu plików NTFS hello, którymi można zarządzać za pomocą Eksploratora Windows.</span><span class="sxs-lookup"><span data-stu-id="18ce4-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="18ce4-138">**Kopia zapasowa** — w przypadku, gdy z hello tablicy wirtualnego StorSimple, wszystkie udziały są włączane automatycznie do kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="18ce4-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Udostępnia szczegóły](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="18ce4-140">Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="18ce4-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="18ce4-141">Dodawanie udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-141">Add a share</span></span>
* <span data-ttu-id="18ce4-142">Modyfikowanie udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-142">Modify a share</span></span>
* <span data-ttu-id="18ce4-143">Przełącz do trybu offline udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-143">Take a share offline</span></span>
* <span data-ttu-id="18ce4-144">Usuń udział</span><span class="sxs-lookup"><span data-stu-id="18ce4-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="18ce4-145">Dodawanie udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-145">Add a share</span></span>

1. <span data-ttu-id="18ce4-146">Witaj StorSimple podsumowania bloku usługi, kliknij **+ Dodaj udział** z hello paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="18ce4-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="18ce4-147">Spowoduje to otwarcie zapasowej hello **Dodaj udział** bloku.</span><span class="sxs-lookup"><span data-stu-id="18ce4-147">This opens up hello **Add share** blade.</span></span>

    ![Dodaj udział](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="18ce4-149">W hello **Dodaj udział** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="18ce4-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="18ce4-150">W hello **nazwa udziału** wprowadź unikatową nazwę udziału użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18ce4-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="18ce4-151">Nazwa Hello musi być ciągiem o długości 3 znaków too127.</span><span class="sxs-lookup"><span data-stu-id="18ce4-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="18ce4-152">Opcjonalny **opis** hello udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="18ce4-153">Opis Hello pomoże zidentyfikować hello właścicieli udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="18ce4-154">W hello **typu** listy rozwijanej listy, określ, czy toocreate **warstwowego** lub **przypięty lokalnie** udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="18ce4-155">W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **przypięty lokalnie udziału**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="18ce4-156">Dla wszystkich innych danych wybierz **warstwowego** udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="18ce4-157">W hello **pojemności** Określ rozmiar hello hello udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="18ce4-158">Udział warstwowych musi wynosić od 500 GB do 20 TB i przypiętych lokalnie udziału musi należeć do zakresu od 50 GB i 2 TB.</span><span class="sxs-lookup"><span data-stu-id="18ce4-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="18ce4-159">W hello **ustawioną domyślną pełne uprawnienia** pola, należy przypisać hello uprawnienia toohello użytkownika lub grupy hello, który uzyskuje dostęp do tego udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="18ce4-160">Określ nazwę hello hello użytkownika lub grupy użytkowników hello w  _john@contoso.com_  format.</span><span class="sxs-lookup"><span data-stu-id="18ce4-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="18ce4-161">Zalecane jest użycie tooaccess uprawnienia użytkownika grupy (zamiast jednego użytkownika) tooallow admin te udziały.</span><span class="sxs-lookup"><span data-stu-id="18ce4-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="18ce4-162">Po przypisaniu hello uprawnienia w tym miejscu, następnie można toomodify Eksploratora plików te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="18ce4-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="18ce4-163">Po zakończeniu konfigurowania udziału użytkownika, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="18ce4-164">Udział zostanie utworzony z hello określonych ustawień i otrzymają powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="18ce4-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="18ce4-165">Domyślnie kopia zapasowa będzie można włączyć hello udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="18ce4-166">tooconfirm, który hello udziału został został pomyślnie utworzony, przejdź do pozycji toohello **udziałów** bloku.</span><span class="sxs-lookup"><span data-stu-id="18ce4-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="18ce4-167">Udostępnianie wymienionych hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="18ce4-167">You should see hello share listed.</span></span>
   
    ![Sukces tworzenia udziału](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="18ce4-169">Modyfikowanie udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-169">Modify a share</span></span>

<span data-ttu-id="18ce4-170">Zmodyfikuj udział, gdy będziesz potrzebować toochange hello opis udziału hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="18ce4-171">Brak właściwości udziału można zmodyfikować po utworzeniu udziału hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="18ce4-172">toomodify udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-172">toomodify a share</span></span>

1. <span data-ttu-id="18ce4-173">Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się udział chcesz, możesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="18ce4-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="18ce4-174">**Wybierz** hello opis bieżącego hello tooview udziału, a następnie zmodyfikować go.</span><span class="sxs-lookup"><span data-stu-id="18ce4-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="18ce4-175">Zapisz zmiany, klikając hello **zapisać** paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="18ce4-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="18ce4-176">Określony ustawienia będą stosowane i zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="18ce4-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="18ce4-177">Edytuj udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="18ce4-178">Przełącz do trybu offline udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-178">Take a share offline</span></span>

<span data-ttu-id="18ce4-179">Może być konieczne tootake udział w trybie offline podczas planowania toomodify albo go usunąć go.</span><span class="sxs-lookup"><span data-stu-id="18ce4-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="18ce4-180">Jeśli udział jest w trybie offline, nie jest dostępny do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="18ce4-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="18ce4-181">Konieczne będzie tootake hello udziału w tryb offline na hoście hello, a także na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="18ce4-182">tootake udziału w trybie offline</span><span class="sxs-lookup"><span data-stu-id="18ce4-182">tootake a share offline</span></span>

1. <span data-ttu-id="18ce4-183">Upewnij się, że udział ten hello zagrożona nie jest używana przed przełączeniem do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="18ce4-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="18ce4-184">Przełącz hello udziału w tablicy hello w trybie offline, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="18ce4-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="18ce4-185">Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello tablicy wirtualnych, na których hello znajduje się udział chcesz, możesz tootake w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="18ce4-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="18ce4-186">**Wybierz** hello udziału i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **przełączyć do trybu offline**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Udostępnij w trybie offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="18ce4-188">Przejrzyj informacje hello w hello **przełączyć do trybu offline** bloku i potwierdzenie akceptacji hello operacji.</span><span class="sxs-lookup"><span data-stu-id="18ce4-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="18ce4-189">Kliknij przycisk **przełączyć do trybu offline** tootake hello udziału w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="18ce4-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="18ce4-190">Zostanie wyświetlone powiadomienie hello operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="18ce4-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="18ce4-191">tooconfirm, który hello udziału została wykonana pomyślnie toohello w trybie offline, przejdź do pozycji **udziałów** bloku.</span><span class="sxs-lookup"><span data-stu-id="18ce4-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="18ce4-192">Powinny pojawić się status hello hello udziału w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="18ce4-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="18ce4-193">Usuń udział</span><span class="sxs-lookup"><span data-stu-id="18ce4-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18ce4-194">Tylko wtedy, gdy jest w trybie offline, można usunąć udziału.</span><span class="sxs-lookup"><span data-stu-id="18ce4-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="18ce4-195">Wykonaj następujące kroki toodelete udział hello.</span><span class="sxs-lookup"><span data-stu-id="18ce4-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="18ce4-196">toodelete udziału</span><span class="sxs-lookup"><span data-stu-id="18ce4-196">toodelete a share</span></span>

1. <span data-ttu-id="18ce4-197">Z hello **udziałów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy w udziale hello, które chcesz toodelete znajduje się.</span><span class="sxs-lookup"><span data-stu-id="18ce4-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="18ce4-198">**Wybierz** hello udziału i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Usuń udział](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="18ce4-200">Sprawdź stan hello udziału hello ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="18ce4-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="18ce4-201">Jeśli chcesz toodelete udziału hello nie jest w trybie offline, przejść do trybu offline najpierw.</span><span class="sxs-lookup"><span data-stu-id="18ce4-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="18ce4-202">Wykonaj kroki hello w [Przełącz do trybu offline udział](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="18ce4-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="18ce4-203">Po wyświetleniu monitu o potwierdzenie w hello **usunąć** bloku, Zaakceptuj potwierdzenie hello i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="18ce4-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="18ce4-204">udział Hello zostanie usunięte i hello **udziałów** bloku listą udziałów w tablicy wirtualnego hello hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="18ce4-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ce4-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18ce4-205">Next steps</span></span>
<span data-ttu-id="18ce4-206">Dowiedz się, jak za[sklonować udziału StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="18ce4-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

