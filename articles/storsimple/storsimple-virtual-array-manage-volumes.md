---
title: woluminy aaaManage na tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Zawiera opis hello Menedżera urządzeń StorSimple i jak toouse on toomanage woluminach macierzy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="1c1e5-103">Użyj Menedżera urządzeń StorSimple usługi toomanage woluminy na powitania tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="1c1e5-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1c1e5-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1c1e5-104">Overview</span></span>

<span data-ttu-id="1c1e5-105">W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać woluminach macierzy wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="1c1e5-106">Witaj usługi Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="1c1e5-107">Dodanie toomanaging udziałów i woluminów można użyć tooview usługi Menedżer StorSimple urządzenia hello i zarządzanie urządzeniami, wyświetlanie alertów i wyświetlić i zarządzanie zasad tworzenia kopii zapasowych i hello katalogu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="1c1e5-108">Typy woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-108">Volume Types</span></span>

<span data-ttu-id="1c1e5-109">Woluminy StorSimple można:</span><span class="sxs-lookup"><span data-stu-id="1c1e5-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="1c1e5-110">**Przypięty lokalnie**: dane w tych woluminów pozostaje w macierzy hello przez cały czas i nie zostaną przeniesione toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="1c1e5-111">**Do warstwy**: dane w tych woluminów mogą zostaną przeniesione toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="1c1e5-112">Podczas tworzenia woluminu warstwowego około 10% miejsca hello jest inicjowana na warstwie lokalne powitania i 90% miejsca hello jest obsługiwana w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="1c1e5-113">Na przykład jeśli udostępniane wolumin 1 TB, 100 GB będzie znajdować się w lokalnej przestrzeni hello i 900 GB byłoby używanych w chmurze powitania po hello warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="1c1e5-114">Z kolei oznacza to, że jeśli zabraknie wszystkie lokalne powitania miejsce na urządzeniu hello nie można dostarczać wolumin warstwowy (ponieważ hello 10% wymaganych na lokalne powitania warstwa nie będzie dostępna).</span><span class="sxs-lookup"><span data-stu-id="1c1e5-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="1c1e5-115">Udostępnione pojemności</span><span class="sxs-lookup"><span data-stu-id="1c1e5-115">Provisioned capacity</span></span>
<span data-ttu-id="1c1e5-116">Można znaleźć w poniższej tabeli dla maksymalnej pojemności udostępnione dla każdego typu woluminu toohello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="1c1e5-117">**Identyfikator limit**</span><span class="sxs-lookup"><span data-stu-id="1c1e5-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="1c1e5-118">**Limit**</span><span class="sxs-lookup"><span data-stu-id="1c1e5-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="1c1e5-119">Minimalny rozmiar woluminu warstwowego</span><span class="sxs-lookup"><span data-stu-id="1c1e5-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="1c1e5-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="1c1e5-120">500 GB</span></span>        |
| <span data-ttu-id="1c1e5-121">Maksymalny rozmiar woluminu warstwowego</span><span class="sxs-lookup"><span data-stu-id="1c1e5-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="1c1e5-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="1c1e5-122">5 TB</span></span>          |
| <span data-ttu-id="1c1e5-123">Minimalny rozmiar woluminu przypiętego lokalnie</span><span class="sxs-lookup"><span data-stu-id="1c1e5-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="1c1e5-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="1c1e5-124">50 GB</span></span>         |
| <span data-ttu-id="1c1e5-125">Maksymalny rozmiar woluminu przypiętego lokalnie</span><span class="sxs-lookup"><span data-stu-id="1c1e5-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="1c1e5-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="1c1e5-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="1c1e5-127">Witaj woluminów bloku</span><span class="sxs-lookup"><span data-stu-id="1c1e5-127">hello Volumes blade</span></span>
<span data-ttu-id="1c1e5-128">Witaj **woluminów** menu w bloku podsumowania usługi StorSimple Wyświetla hello listę woluminów magazynu dla danej tablicy StorSimple i pozwala toomanage je.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Blok woluminów](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="1c1e5-130">Wolumin składa się z szeregu atrybuty:</span><span class="sxs-lookup"><span data-stu-id="1c1e5-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="1c1e5-131">**Nazwa woluminu** — opisową nazwą, która musi być unikatowa i ułatwia identyfikowanie hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="1c1e5-132">**Stan** — może być w trybie online lub offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="1c1e5-133">Jeśli wolumin jest w trybie offline, nie jest widoczne tooinitiators (serwery) dozwoloną dostępu toouse hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="1c1e5-134">**Typ** — wskazuje, czy wolumin hello jest **warstwowego** (hello domyślne) lub **przypięty lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="1c1e5-135">**Pojemność** — określa ilość hello danych używana jako porównaniu toohello łączna ilość danych, które mogą być przechowywane przez inicjatora hello (serwer).</span><span class="sxs-lookup"><span data-stu-id="1c1e5-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="1c1e5-136">**Kopia zapasowa** — w przypadku, gdy z hello tablicy wirtualnego StorSimple, wszystkie woluminy są włączane automatycznie do utworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="1c1e5-137">**Połączone hosty** — określa hello inicjatorów (serwerów), które mają prawo dostępu toothis woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Szczegóły ilości](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="1c1e5-139">Użyj instrukcji hello, w tym hello samouczek tooperform następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="1c1e5-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="1c1e5-140">Dodawanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-140">Add a volume</span></span>
* <span data-ttu-id="1c1e5-141">Modyfikowanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-141">Modify a volume</span></span>
* <span data-ttu-id="1c1e5-142">Przełącz do trybu offline woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-142">Take a volume offline</span></span>
* <span data-ttu-id="1c1e5-143">Usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="1c1e5-144">Dodawanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-144">Add a volume</span></span>

1. <span data-ttu-id="1c1e5-145">Witaj StorSimple podsumowania bloku usługi, kliknij **+ Dodaj wolumin** z hello paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="1c1e5-146">Spowoduje to otwarcie zapasowej hello **Dodaj wolumin** bloku.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="1c1e5-148">W hello **Dodaj wolumin** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="1c1e5-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="1c1e5-149">W hello **nazwa woluminu** wprowadź unikatową nazwę dla woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="1c1e5-150">Nazwa Hello musi być ciągiem o długości 3 znaków too127.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="1c1e5-151">W hello **typu** listy rozwijanej liście, określ, czy toocreate **warstwowego** lub **przypięty lokalnie** woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="1c1e5-152">W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **wolumin przypięty lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="1c1e5-153">Dla wszystkich innych danych wybierz **warstwowego** woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="1c1e5-154">W hello **pojemności** Określ rozmiar hello hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="1c1e5-155">Wolumin warstwowy musi należeć do zakresu od 500 GB i 5 TB i woluminu przypiętego lokalnie musi należeć do zakresu od 50 GB i 500 GB.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="1c1e5-156">Kliknij przycisk **połączone hosty**, wybierz dostępu formantu rekordu (ACR) odpowiedniego toohello inicjatora iSCSI mają tooconnect toothis woluminu, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="1c1e5-157">tooadd połączonych nowego hosta, kliknij przycisk **Dodaj nowe**, wprowadź nazwę hosta hello i jego iSCSI kwalifikowana nazwa (IQN), a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="1c1e5-159">Po zakończeniu konfigurowania woluminu, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="1c1e5-160">Wolumin zostanie utworzony z hello określonych ustawień i otrzymają powiadomienie na powitania pomyślnym utworzeniu hello takie same.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="1c1e5-161">Domyślnie kopia zapasowa zostanie włączona dla woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="1c1e5-162">tooconfirm, który hello wolumin został toohello został pomyślnie utworzony, przejdź do pozycji **woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="1c1e5-163">Powinny pojawić się hello woluminu na liście.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-163">You should see hello volume listed.</span></span>
   
    ![Powodzenie Tworzenie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="1c1e5-165">Modyfikowanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-165">Modify a volume</span></span>

<span data-ttu-id="1c1e5-166">Zmodyfikuj woluminu, gdy będziesz potrzebować toochange hello hostów, które uzyskują dostęp do woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="1c1e5-167">Witaj inne atrybuty woluminu nie można zmodyfikować po utworzeniu hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="1c1e5-168">toomodify woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-168">toomodify a volume</span></span>

1. <span data-ttu-id="1c1e5-169">Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się wolumin ma możesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="1c1e5-170">**Wybierz** hello woluminu, a następnie kliknij przycisk **połączone hosty** tooview hello aktualnie podłączonego hosta i zmodyfikuj go tooa inny serwer.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Edytuj woluminu](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="1c1e5-172">Zapisz zmiany, klikając hello **zapisać** paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="1c1e5-173">Określony ustawienia będą stosowane i zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="1c1e5-174">Przełącz do trybu offline woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-174">Take a volume offline</span></span>

<span data-ttu-id="1c1e5-175">Może być konieczne tootake woluminu w trybie offline podczas planowania toomodify albo go usunąć go.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="1c1e5-176">Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="1c1e5-177">Konieczne będzie tootake hello woluminu w trybie offline na hoście hello, a także na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="1c1e5-178">tootake woluminu w trybie offline</span><span class="sxs-lookup"><span data-stu-id="1c1e5-178">tootake a volume offline</span></span>

1. <span data-ttu-id="1c1e5-179">Upewnij się, że w woluminie hello nie jest używany przed przełączeniem do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="1c1e5-180">Zająć hello woluminu w trybie offline na hoście hello pierwszy.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="1c1e5-181">Eliminuje to potencjalne ryzyko uszkodzeniem danych na woluminie hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="1c1e5-182">Określone kroki można znaleźć toohello instrukcje dotyczące systemu operacyjnego hosta.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="1c1e5-183">Po wolumin hello na hoście hello jest w trybie offline, należy podjąć hello woluminu w macierzy hello w trybie offline, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1c1e5-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="1c1e5-184">Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello tablicy wirtualnych, na których hello znajduje się wolumin ma możesz tootake w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="1c1e5-185">**Wybierz** hello woluminu, a następnie kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **przełączyć do trybu offline**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Wolumin w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="1c1e5-187">Przejrzyj informacje hello w hello **przełączyć do trybu offline** bloku i potwierdzenie akceptacji hello operacji.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="1c1e5-188">Kliknij przycisk **przełączyć do trybu offline** tootake hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="1c1e5-189">Zostanie wyświetlone powiadomienie hello operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="1c1e5-190">tooconfirm, który wolumin hello zostało pomyślnie przełączone do trybu offline, przejdź toohello **woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="1c1e5-191">Stan hello hello woluminu powinien być widoczny jako w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Potwierdzenie woluminu w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="1c1e5-193">Usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c1e5-194">Wolumin można usunąć tylko wtedy, gdy jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="1c1e5-195">Wykonaj następujące kroki toodelete woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="1c1e5-196">toodelete woluminu</span><span class="sxs-lookup"><span data-stu-id="1c1e5-196">toodelete a volume</span></span>

1. <span data-ttu-id="1c1e5-197">Z hello **woluminów** ustawić hello bloku podsumowania usługi StorSimple, wybierz hello wirtualnego tablicy, na które hello znajduje się wolumin ma możesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="1c1e5-198">**Wybierz** hello woluminu, a następnie kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego hello **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Usuń wolumin](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="1c1e5-200">Sprawdź stan hello woluminu hello ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="1c1e5-201">Jeśli wolumin hello ma toodelete nie jest w trybie offline, przełączyć go w trybie offline hello pierwszą, następujące kroki [Przełącz do trybu offline wolumin](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="1c1e5-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="1c1e5-202">Po wyświetleniu monitu o potwierdzenie w hello **usunąć** bloku, Zaakceptuj potwierdzenie hello i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="1c1e5-203">Witaj wolumin zostanie usunięte i hello **woluminów** bloku wyświetli hello zaktualizować listę woluminów w tablicy wirtualnego hello.</span><span class="sxs-lookup"><span data-stu-id="1c1e5-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c1e5-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c1e5-204">Next steps</span></span>

<span data-ttu-id="1c1e5-205">Dowiedz się, jak za[sklonować woluminu StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="1c1e5-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

