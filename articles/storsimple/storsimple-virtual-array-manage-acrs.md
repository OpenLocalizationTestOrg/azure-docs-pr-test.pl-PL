---
title: "aaaManage rekordy kontroli dostępu dla tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toomanage rekordy toodetermine (ACRs), których hostów można połączyć tooa woluminu na powitania tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="80f1d-103">Toomanage StorSimple za pomocą Menedżera urządzeń rekordy kontroli dostępu dla tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="80f1d-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="80f1d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="80f1d-104">Overview</span></span>

<span data-ttu-id="80f1d-105">Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa woluminu na powitania tablicy wirtualnego StorSimple (znanej także jako hello lokalnej urządzenia wirtualnego StorSimple).</span><span class="sxs-lookup"><span data-stu-id="80f1d-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="80f1d-106">ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów.</span><span class="sxs-lookup"><span data-stu-id="80f1d-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="80f1d-107">Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza hello ACR skojarzone z tym woluminie dla nazwy IQN hello i jeśli istnieje dopasowanie, hello połączenie zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="80f1d-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="80f1d-108">Witaj **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji usługi Menedżer urządzeń wyświetla wszystkie rekordy kontroli dostępu hello hello odpowiadającego nazw IQN hello hostów.</span><span class="sxs-lookup"><span data-stu-id="80f1d-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Zarządzanie rekordami kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="80f1d-110">W tym samouczku opisano następujące typowe zadania związane z ACR hello:</span><span class="sxs-lookup"><span data-stu-id="80f1d-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="80f1d-111">Pobierz hello IQN</span><span class="sxs-lookup"><span data-stu-id="80f1d-111">Get hello IQN</span></span>
* <span data-ttu-id="80f1d-112">Dodaj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="80f1d-112">Add an access control record</span></span>
* <span data-ttu-id="80f1d-113">Edytuj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="80f1d-113">Edit an access control record</span></span>
* <span data-ttu-id="80f1d-114">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="80f1d-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="80f1d-115">Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="80f1d-116">Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="80f1d-117">Pobierz hello IQN</span><span class="sxs-lookup"><span data-stu-id="80f1d-117">Get hello IQN</span></span>

<span data-ttu-id="80f1d-118">Wykonaj następujące kroki tooget hello IQN hosta z systemem Windows z systemem Windows Server 2012 hello.</span><span class="sxs-lookup"><span data-stu-id="80f1d-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="80f1d-119">Dodaj ACR</span><span class="sxs-lookup"><span data-stu-id="80f1d-119">Add an ACR</span></span>

<span data-ttu-id="80f1d-120">Możesz użyć **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji z tooadd usługi Menedżer StorSimple urządzenia ACRs.</span><span class="sxs-lookup"><span data-stu-id="80f1d-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="80f1d-121">Zazwyczaj należy skojarzyć jedną ACR z jednego woluminu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="80f1d-122">Informacji o kojarzeniu ACR z woluminem, przejdź zbyt[Dodaj wolumin](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="80f1d-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80f1d-123">Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="80f1d-124">Wykonaj następujące kroki tooadd ACR hello.</span><span class="sxs-lookup"><span data-stu-id="80f1d-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="80f1d-125">tooadd ACR</span><span class="sxs-lookup"><span data-stu-id="80f1d-125">tooadd an ACR</span></span>

1. <span data-ttu-id="80f1d-126">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="80f1d-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="80f1d-127">W hello **rekordy kontroli dostępu** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="80f1d-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="80f1d-128">W hello **dodać ACR** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="80f1d-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="80f1d-129">Wypełnij pole **Nazwa** dla rekordu ACR.</span><span class="sxs-lookup"><span data-stu-id="80f1d-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="80f1d-130">W obszarze **Nazwa inicjatora iSCSI**, podaj hello nazwę IQN hosta z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="80f1d-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="80f1d-131">Witaj tooget IQN hosta z systemem Windows Server, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="80f1d-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="80f1d-132">Uruchom inicjatora iSCSI firmy Microsoft hello na hoście z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="80f1d-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="80f1d-133">W oknie właściwości inicjatora iSCSI hello, na powitania **konfiguracji** karcie zaznacz i skopiuj ciąg hello z hello **Nazwa inicjatora** pola.</span><span class="sxs-lookup"><span data-stu-id="80f1d-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="80f1d-134">Wklej ten ciąg hello **IQN** w hello **dodać ACR** bloku.</span><span class="sxs-lookup"><span data-stu-id="80f1d-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="80f1d-135">Kliknij przycisk **Dodaj** tooadd hello ACR.</span><span class="sxs-lookup"><span data-stu-id="80f1d-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Dodaj rekordy kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="80f1d-137">Witaj tabelarycznej listę jest zaktualizowane tooreflect tego dodatku.</span><span class="sxs-lookup"><span data-stu-id="80f1d-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="80f1d-138">Edytuj ACR</span><span class="sxs-lookup"><span data-stu-id="80f1d-138">Edit an ACR</span></span>

<span data-ttu-id="80f1d-139">Użyj hello **rekordy kontroli dostępu** bloku w hello **konfiguracji** sekcji usługi Menedżera urządzeń w hello ACRs tooedit portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="80f1d-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="80f1d-140">Nie należy modyfikować ACR, który jest aktualnie używany.</span><span class="sxs-lookup"><span data-stu-id="80f1d-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="80f1d-141">tooedit ACR skojarzony z woluminem, który jest aktualnie używana, należy najpierw wziąć hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="80f1d-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="80f1d-142">Wykonaj następujące kroki tooedit ACR hello.</span><span class="sxs-lookup"><span data-stu-id="80f1d-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="80f1d-143">tooedit ACR</span><span class="sxs-lookup"><span data-stu-id="80f1d-143">tooedit an ACR</span></span>

1. <span data-ttu-id="80f1d-144">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** sekcji **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="80f1d-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="80f1d-145">W hello **rekordy kontroli dostępu** bloku z hello Tabelaryczny spis hello rekordy kontroli dostępu, kliknij dwukrotnie hello ACR, że chcesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="80f1d-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="80f1d-146">W hello **rekordy kontroli dostępu do edycji** bloku hello następujące:</span><span class="sxs-lookup"><span data-stu-id="80f1d-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="80f1d-147">Podaj hello IQN dla hello ACR.</span><span class="sxs-lookup"><span data-stu-id="80f1d-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="80f1d-148">Kliknij przycisk **zapisać** u góry hello toosave bloku hello hello zmodyfikowane ACR.</span><span class="sxs-lookup"><span data-stu-id="80f1d-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="80f1d-149">Zostanie wyświetlony powitania po komunikat potwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="80f1d-149">You see hello following confirmation message:</span></span>
   
        ![Edytuj rekordy kontroli dostępu](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="80f1d-151">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="80f1d-151">Delete an access control record</span></span>

<span data-ttu-id="80f1d-152">Użyj hello **konfiguracji** strony w hello ACRs toodelete portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="80f1d-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="80f1d-153">Nie należy usuwać ACR, który jest aktualnie używany.</span><span class="sxs-lookup"><span data-stu-id="80f1d-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="80f1d-154">toodelete ACR skojarzony z woluminem, który jest aktualnie używana, należy najpierw wziąć hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="80f1d-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="80f1d-155">Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="80f1d-156">Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="80f1d-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="80f1d-157">toodelete rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="80f1d-157">toodelete an access control record</span></span>

1. <span data-ttu-id="80f1d-158">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** sekcji **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="80f1d-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="80f1d-159">W hello **rekordy kontroli dostępu** bloku z hello Tabelaryczny spis hello rekordy kontroli dostępu, kliknij dwukrotnie hello ACR, że chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="80f1d-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="80f1d-160">W bloku rekordów hello edycji dostępu formantu, kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="80f1d-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Usuń ACRS](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="80f1d-162">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **usunąć** toocontinue z hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="80f1d-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="80f1d-163">Tworzenie listy tabelarycznym Hello jest zaktualizowane tooreflect hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="80f1d-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Komunikat ostrzegawczy](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="80f1d-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80f1d-165">Next steps</span></span>

* <span data-ttu-id="80f1d-166">Dowiedz się więcej o [Dodawanie woluminów i konfigurowanie ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="80f1d-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

