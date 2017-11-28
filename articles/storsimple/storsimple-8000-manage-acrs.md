---
title: "aaaManage rekordy kontroli dostępu w StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toouse rekordy hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello toodetermine (ACRs)."
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="edfea-103">Użyj rekordy kontroli dostępu toomanage usługi Menedżer StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="edfea-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="edfea-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="edfea-104">Overview</span></span>
<span data-ttu-id="edfea-105">Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="edfea-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="edfea-106">ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów.</span><span class="sxs-lookup"><span data-stu-id="edfea-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="edfea-107">Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza powitalne ACR skojarzone z tym woluminie nazwy IQN hello i jeśli istnieje dopasowanie, a następnie hello jest nawiązywane połączenie.</span><span class="sxs-lookup"><span data-stu-id="edfea-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="edfea-108">Witaj rekordy kontroli dostępu w hello **konfiguracji** sekcji z bloku usługi Menedżer StorSimple urządzenia wyświetlić wszystkie rekordy kontroli dostępu hello z hello odpowiadającego nazw IQN hello hostów.</span><span class="sxs-lookup"><span data-stu-id="edfea-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="edfea-109">W tym samouczku opisano następujące typowe zadania związane z ACR hello:</span><span class="sxs-lookup"><span data-stu-id="edfea-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="edfea-110">Dodaj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-110">Add an access control record</span></span>
* <span data-ttu-id="edfea-111">Edytuj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-111">Edit an access control record</span></span>
* <span data-ttu-id="edfea-112">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="edfea-113">Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="edfea-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="edfea-114">Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="edfea-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="edfea-115">Pobierz hello IQN</span><span class="sxs-lookup"><span data-stu-id="edfea-115">Get hello IQN</span></span>

<span data-ttu-id="edfea-116">Wykonaj następujące kroki tooget hello IQN hosta z systemem Windows z systemem Windows Server 2012 hello.</span><span class="sxs-lookup"><span data-stu-id="edfea-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="edfea-117">Dodaj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-117">Add an access control record</span></span>
<span data-ttu-id="edfea-118">Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku tooadd ACRs.</span><span class="sxs-lookup"><span data-stu-id="edfea-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="edfea-119">Zazwyczaj co ACR zostanie skojarzony z jednego woluminu.</span><span class="sxs-lookup"><span data-stu-id="edfea-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="edfea-120">Wykonaj następujące kroki tooadd ACR hello.</span><span class="sxs-lookup"><span data-stu-id="edfea-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="edfea-121">tooadd ACR</span><span class="sxs-lookup"><span data-stu-id="edfea-121">tooadd an ACR</span></span>

1. <span data-ttu-id="edfea-122">Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="edfea-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="edfea-123">W hello **rekordy kontroli dostępu** bloku, kliknij przycisk **+ Dodaj ACR**.</span><span class="sxs-lookup"><span data-stu-id="edfea-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="edfea-125">W hello **dodać ACR** bloku hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="edfea-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="edfea-126">Podaj nazwę dla rekordu ACR.</span><span class="sxs-lookup"><span data-stu-id="edfea-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="edfea-127">Podaj nazwę IQN hello danego hosta systemu Windows Server, w obszarze **iSCSI Nazwa inicjatora (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="edfea-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="edfea-128">Kliknij przycisk **Dodaj** toocreate hello ACR.</span><span class="sxs-lookup"><span data-stu-id="edfea-128">Click **Add** toocreate hello ACR.</span></span>

        ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="edfea-130">Witaj nowo dodanych ACR będą wyświetlane na powitania Tabelaryczny spis ACRs.</span><span class="sxs-lookup"><span data-stu-id="edfea-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Kliknij przycisk Dodaj ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="edfea-132">Edytuj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-132">Edit an access control record</span></span>
<span data-ttu-id="edfea-133">Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku tooedit ACRs.</span><span class="sxs-lookup"><span data-stu-id="edfea-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="edfea-134">Zalecane jest zmodyfikowanie tych ACRs, które nie są obecnie w użyciu.</span><span class="sxs-lookup"><span data-stu-id="edfea-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="edfea-135">tooedit ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="edfea-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="edfea-136">Wykonaj następujące kroki tooedit ACR hello.</span><span class="sxs-lookup"><span data-stu-id="edfea-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="edfea-137">tooedit rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="edfea-138">Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="edfea-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="edfea-140">W hello tabelarycznej listę rekordy kontroli dostępu hello, kliknij i zaznacz hello ACR, że chcesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="edfea-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="edfea-142">W hello **rekord kontroli dostępu edycji** bloku, podaj inny host tooanother odpowiedniego IQN.</span><span class="sxs-lookup"><span data-stu-id="edfea-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="edfea-144">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="edfea-144">Click **Save**.</span></span> <span data-ttu-id="edfea-145">Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.</span><span class="sxs-lookup"><span data-stu-id="edfea-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Edytuj rekordy kontroli dostępu](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="edfea-147">Użytkownik jest powiadamiany o zaktualizowaniu hello ACR.</span><span class="sxs-lookup"><span data-stu-id="edfea-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="edfea-148">Lista tabelarycznym Hello aktualizuje również tooreflect hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="edfea-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="edfea-149">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-149">Delete an access control record</span></span>
<span data-ttu-id="edfea-150">Użyj hello **konfiguracji** części hello Menedżera urządzeń StorSimple usługi bloku toodelete ACRs.</span><span class="sxs-lookup"><span data-stu-id="edfea-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="edfea-151">Można usunąć tylko ACRs, które nie są obecnie w użyciu.</span><span class="sxs-lookup"><span data-stu-id="edfea-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="edfea-152">toodelete ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="edfea-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="edfea-153">Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="edfea-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="edfea-154">toodelete rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="edfea-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="edfea-155">Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij dwukrotnie usługę hello nazwę, a następnie w hello **konfiguracji** kliknij **rekordy kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="edfea-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="edfea-157">W hello tabelarycznej listę rekordy kontroli dostępu hello, kliknij i zaznacz hello ACR, że chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="edfea-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="edfea-159">Kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke i wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="edfea-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="edfea-161">Po wyświetleniu monitu o potwierdzenie, przejrzyj informacje hello, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="edfea-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="edfea-163">Użytkownik jest powiadamiany o zakończeniu hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="edfea-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="edfea-164">Tworzenie listy tabelarycznym Hello jest zaktualizowane tooreflect hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="edfea-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Przejdź tooaccess kontrolować rekordy](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="edfea-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="edfea-166">Next steps</span></span>
* <span data-ttu-id="edfea-167">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="edfea-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="edfea-168">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="edfea-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

