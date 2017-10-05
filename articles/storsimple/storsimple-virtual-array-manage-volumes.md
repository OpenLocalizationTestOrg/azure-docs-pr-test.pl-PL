---
title: "Zarządzanie woluminami w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "Zawiera opis Menedżera urządzeń StorSimple i wyjaśniono, jak przy jego użyciu zarządzać woluminach macierzy wirtualne StorSimple."
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
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="c3815-103">Usługa StorSimple za pomocą Menedżera urządzeń, aby zarządzać woluminy na tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="c3815-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="c3815-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c3815-104">Overview</span></span>

<span data-ttu-id="c3815-105">W tym samouczku opisano sposób korzystania z usługi Menedżer StorSimple urządzenia do tworzenia i zarządzania woluminach macierzy wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c3815-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="c3815-106">Usługę Menedżer StorSimple urządzenia jest rozszerzeniem w portalu Azure, która umożliwia zarządzanie rozwiązania StorSimple z interfejsem sieci web jednej.</span><span class="sxs-lookup"><span data-stu-id="c3815-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="c3815-107">Oprócz zarządzania udziałami i woluminami, można użyć usługi Menedżer StorSimple urządzenia, wyświetlanie i zarządzanie urządzeniami, wyświetlanie alertów i wyświetlić oraz zarządzanie nimi zasady tworzenia kopii zapasowej i kopii zapasowej wykazu.</span><span class="sxs-lookup"><span data-stu-id="c3815-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="c3815-108">Typy woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-108">Volume Types</span></span>

<span data-ttu-id="c3815-109">Woluminy StorSimple można:</span><span class="sxs-lookup"><span data-stu-id="c3815-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="c3815-110">**Przypięty lokalnie**: dane w tych woluminów pozostaje w macierzy przez cały czas i nie zostaną przeniesione do chmury.</span><span class="sxs-lookup"><span data-stu-id="c3815-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="c3815-111">**Do warstwy**: dane w tych woluminów mogą zostaną przeniesione do chmury.</span><span class="sxs-lookup"><span data-stu-id="c3815-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="c3815-112">Podczas tworzenia woluminu warstwowego około 10% miejsca jest inicjowana na warstwie lokalnej i 90% miejsca jest udostępniony w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c3815-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="c3815-113">Na przykład jeśli zainicjowano obsługę administracyjną wolumin 1 TB, 100 GB, czy znajdują się w lokalnej przestrzeni i 900 GB byłoby używanych w chmurze po warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="c3815-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="c3815-114">Z kolei oznacza to, że jeśli całe lokalne miejsce na urządzeniu nie można dostarczać wolumin warstwowy (ponieważ 10%, wymagane w warstwie lokalnej nie będzie dostępna).</span><span class="sxs-lookup"><span data-stu-id="c3815-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="c3815-115">Udostępnione pojemności</span><span class="sxs-lookup"><span data-stu-id="c3815-115">Provisioned capacity</span></span>
<span data-ttu-id="c3815-116">Zapoznaj się z poniższej tabeli maksymalną pojemność udostępnione dla każdego typu woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="c3815-117">**Identyfikator limit**</span><span class="sxs-lookup"><span data-stu-id="c3815-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="c3815-118">**Limit**</span><span class="sxs-lookup"><span data-stu-id="c3815-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="c3815-119">Minimalny rozmiar woluminu warstwowego</span><span class="sxs-lookup"><span data-stu-id="c3815-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="c3815-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="c3815-120">500 GB</span></span>        |
| <span data-ttu-id="c3815-121">Maksymalny rozmiar woluminu warstwowego</span><span class="sxs-lookup"><span data-stu-id="c3815-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="c3815-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="c3815-122">5 TB</span></span>          |
| <span data-ttu-id="c3815-123">Minimalny rozmiar woluminu przypiętego lokalnie</span><span class="sxs-lookup"><span data-stu-id="c3815-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="c3815-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="c3815-124">50 GB</span></span>         |
| <span data-ttu-id="c3815-125">Maksymalny rozmiar woluminu przypiętego lokalnie</span><span class="sxs-lookup"><span data-stu-id="c3815-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="c3815-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="c3815-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="c3815-127">Blok woluminów</span><span class="sxs-lookup"><span data-stu-id="c3815-127">The Volumes blade</span></span>
<span data-ttu-id="c3815-128">**Woluminów** menu w bloku podsumowania usługi StorSimple Wyświetla listę woluminów magazynu dla danej tablicy StorSimple i umożliwia zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="c3815-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Blok woluminów](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="c3815-130">Wolumin składa się z szeregu atrybuty:</span><span class="sxs-lookup"><span data-stu-id="c3815-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="c3815-131">**Nazwa woluminu** — opisową nazwę, która musi być unikatowa i pomaga w identyfikacji woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="c3815-132">**Stan** — może być w trybie online lub offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="c3815-133">Jeśli wolumin jest w trybie offline, nie jest widoczny dla inicjatorów (serwerów), które mają dostęp do korzystać z woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="c3815-134">**Typ** — wskazuje, czy wolumin jest **warstwowego** (ustawienie domyślne) lub **przypięty lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="c3815-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="c3815-135">**Pojemność** — określa ilość danych używanych w porównaniu z łączną ilość danych, które mogą być przechowywane przez inicjatora (serwer).</span><span class="sxs-lookup"><span data-stu-id="c3815-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="c3815-136">**Kopia zapasowa** — w przypadku tablicy wirtualnego StorSimple, wszystkie woluminy są włączane automatycznie do kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3815-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="c3815-137">**Połączone hosty** — określa inicjatorów (serwerów), które mają prawo dostępu do tego woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Szczegóły ilości](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="c3815-139">Wykonaj instrukcje w tym samouczku, aby wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c3815-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="c3815-140">Dodawanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-140">Add a volume</span></span>
* <span data-ttu-id="c3815-141">Modyfikowanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-141">Modify a volume</span></span>
* <span data-ttu-id="c3815-142">Przełącz do trybu offline woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-142">Take a volume offline</span></span>
* <span data-ttu-id="c3815-143">Usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="c3815-144">Dodawanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-144">Add a volume</span></span>

1. <span data-ttu-id="c3815-145">W bloku podsumowania usługi StorSimple, kliknij **+ Dodaj wolumin** z paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="c3815-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="c3815-146">Spowoduje to otwarcie **Dodaj wolumin** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3815-146">This opens up the **Add volume** blade.</span></span>
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="c3815-148">W **Dodaj wolumin** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c3815-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="c3815-149">W **nazwa woluminu** wprowadź unikatową nazwę dla woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="c3815-150">Nazwa musi być ciągiem o długości 3 do 127 znaków.</span><span class="sxs-lookup"><span data-stu-id="c3815-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="c3815-151">W **typu** listy rozwijanej liście, określ, czy można utworzyć **warstwowego** lub **przypięty lokalnie** woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="c3815-152">W przypadku obciążeń, które wymagają lokalnych gwarancji, małych opóźnień i większej wydajności, wybierz **wolumin przypięty lokalnie**.</span><span class="sxs-lookup"><span data-stu-id="c3815-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="c3815-153">Dla wszystkich innych danych wybierz **warstwowego** woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="c3815-154">W **pojemności** Określ rozmiar woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="c3815-155">Wolumin warstwowy musi należeć do zakresu od 500 GB i 5 TB i woluminu przypiętego lokalnie musi należeć do zakresu od 50 GB i 500 GB.</span><span class="sxs-lookup"><span data-stu-id="c3815-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="c3815-156">Kliknij przycisk **połączone hosty**, zaznacz rekord kontroli dostępu (ACR) odpowiadający inicjatora iSCSI, który chcesz połączyć do tego woluminu, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="c3815-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="c3815-157">Aby dodać nowy host połączony, kliknij przycisk **Dodaj nowe**, wprowadź nazwę hosta i jego iSCSI kwalifikowana nazwa (IQN), a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c3815-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Dodawanie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="c3815-159">Po zakończeniu konfigurowania woluminu, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c3815-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="c3815-160">Wolumin zostanie utworzony przy użyciu określonych ustawień i otrzymają powiadomienie o pomyślnym utworzeniu tego samego.</span><span class="sxs-lookup"><span data-stu-id="c3815-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="c3815-161">Domyślnie kopia zapasowa zostanie włączona dla woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="c3815-162">Aby upewnić się, że wolumin został utworzony pomyślnie, przejdź do **woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3815-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="c3815-163">Powinny pojawić się woluminu na liście.</span><span class="sxs-lookup"><span data-stu-id="c3815-163">You should see the volume listed.</span></span>
   
    ![Powodzenie Tworzenie woluminu](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="c3815-165">Modyfikowanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-165">Modify a volume</span></span>

<span data-ttu-id="c3815-166">Jeśli musisz zmienić hosty, które uzyskują dostęp do woluminu, należy zmodyfikować woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="c3815-167">Inne atrybuty woluminu nie można zmodyfikować po utworzeniu woluminu.</span><span class="sxs-lookup"><span data-stu-id="c3815-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="c3815-168">Aby zmodyfikować woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-168">To modify a volume</span></span>

1. <span data-ttu-id="c3815-169">Z **woluminów** ustawić bloku podsumowania usługi StorSimple, wybierz tablicy wirtualny, na którym znajduje się wolumin ma modyfikowania.</span><span class="sxs-lookup"><span data-stu-id="c3815-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="c3815-170">**Wybierz** wolumin i kliknij przycisk **połączone hosty** Aby wyświetlić aktualnie połączonych hosta, a następnie zmodyfikować go na innym serwerze.</span><span class="sxs-lookup"><span data-stu-id="c3815-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Edytuj woluminu](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="c3815-172">Zapisz zmiany, klikając **zapisać** paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="c3815-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="c3815-173">Określony ustawienia będą stosowane i zostanie wyświetlone powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="c3815-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="c3815-174">Przełącz do trybu offline woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-174">Take a volume offline</span></span>

<span data-ttu-id="c3815-175">Konieczne może być Przełącz wolumin do trybu offline podczas planowania go zmodyfikować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="c3815-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="c3815-176">Gdy wolumin jest w trybie offline, nie jest dostępny do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="c3815-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="c3815-177">Należy podjąć woluminu w trybie offline na hoście, a także na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="c3815-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="c3815-178">Wolumin przełączenia do trybu offline</span><span class="sxs-lookup"><span data-stu-id="c3815-178">To take a volume offline</span></span>

1. <span data-ttu-id="c3815-179">Upewnij się, że w danym woluminie nie jest używany przed przełączeniem do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="c3815-180">Zająć pierwszy woluminu w trybie offline na hoście.</span><span class="sxs-lookup"><span data-stu-id="c3815-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="c3815-181">Eliminuje to potencjalne ryzyko uszkodzeniem danych na woluminie.</span><span class="sxs-lookup"><span data-stu-id="c3815-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="c3815-182">Aby poznać konkretne kroki zapoznaj się z instrukcjami dla systemu operacyjnego hosta.</span><span class="sxs-lookup"><span data-stu-id="c3815-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="c3815-183">Po wolumin hosta jest w trybie offline, należy podjąć woluminu w macierzy w trybie offline, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c3815-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="c3815-184">Z **woluminów** ustawić bloku podsumowania usługi StorSimple, wybierz tablicy wirtualny, na którym znajduje się wolumin ma można przełączyć do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="c3815-185">**Wybierz** wolumin i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego **przełączyć do trybu offline**.</span><span class="sxs-lookup"><span data-stu-id="c3815-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Wolumin w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="c3815-187">Przejrzyj informacje w **przełączyć do trybu offline** bloku i potwierdzenie akceptacji wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="c3815-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="c3815-188">Kliknij przycisk **przełączyć do trybu offline** woluminu przełączenia do trybu offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="c3815-189">Zostanie wyświetlone powiadomienie operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="c3815-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="c3815-190">Aby upewnić się, że wolumin został pomyślnie przełączony w tryb offline, przejdź do **woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3815-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="c3815-191">Stan woluminu powinien być widoczny jako w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-191">You should see the status of the volume as offline.</span></span>
     
       ![Potwierdzenie woluminu w trybie offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="c3815-193">Usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="c3815-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3815-194">Wolumin można usunąć tylko wtedy, gdy jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="c3815-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="c3815-195">Wykonaj poniższe kroki, aby usunąć wolumin.</span><span class="sxs-lookup"><span data-stu-id="c3815-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="c3815-196">Aby usunąć wolumin</span><span class="sxs-lookup"><span data-stu-id="c3815-196">To delete a volume</span></span>

1. <span data-ttu-id="c3815-197">Z **woluminów** ustawić bloku podsumowania usługi StorSimple, wybierz tablicy wirtualny, na którym znajduje się wolumin ma na usuwanie.</span><span class="sxs-lookup"><span data-stu-id="c3815-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="c3815-198">**Wybierz** wolumin i kliknij przycisk **...**  (Alternatywnie kliknij prawym przyciskiem myszy w tym wierszu) i wybierz z menu kontekstowego **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c3815-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Usuń wolumin](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="c3815-200">Sprawdź stan woluminu, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="c3815-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="c3815-201">Jeśli wolumin do usunięcia nie jest w trybie offline, przejść do trybu offline należy wykonać kroki opisane w [Przełącz do trybu offline wolumin](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="c3815-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="c3815-202">Po wyświetleniu monitu o potwierdzenie w **usunąć** bloku, Zaakceptuj potwierdzenie i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c3815-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="c3815-203">Wolumin zostanie usunięte i **woluminów** bloku wyświetli zaktualizowaną listę woluminów w tablicy wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="c3815-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3815-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3815-204">Next steps</span></span>

<span data-ttu-id="c3815-205">Dowiedz się, jak [sklonować woluminu StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="c3815-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

