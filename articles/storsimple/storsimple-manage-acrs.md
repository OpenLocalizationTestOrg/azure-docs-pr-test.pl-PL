---
title: "aaaManage rekordy kontroli dostępu w StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak kontroli dostępu toouse rekordy hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello toodetermine (ACRs)."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="03344-103">Użyj rekordy kontroli dostępu toomanage usługi Menedżer StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="03344-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="03344-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="03344-104">Overview</span></span>
<span data-ttu-id="03344-105">Rekordy kontroli dostępu (ACRs) pozwalają toospecify hosty, które mogą się łączyć tooa wolumin w urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="03344-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="03344-106">ACRs są ustawiane tooa określonego woluminu i zawierają hello iSCSI nazwy kwalifikowane (nazw IQN) hello hostów.</span><span class="sxs-lookup"><span data-stu-id="03344-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="03344-107">Gdy host podejmie próbę tooconnect tooa woluminu, hello urządzenia sprawdza powitalne ACR skojarzone z tym woluminie nazwy IQN hello i jeśli istnieje dopasowanie, a następnie hello jest nawiązywane połączenie.</span><span class="sxs-lookup"><span data-stu-id="03344-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="03344-108">Kontrola dostępu Hello rejestruje sekcji na powitania **Konfiguruj** wszystkie rekordy kontroli dostępu hello zostanie wyświetlona strona z hello odpowiadającego nazw IQN hello hostów.</span><span class="sxs-lookup"><span data-stu-id="03344-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="03344-109">W tym samouczku opisano następujące typowe zadania związane z ACR hello:</span><span class="sxs-lookup"><span data-stu-id="03344-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="03344-110">Dodaj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-110">Add an access control record</span></span> 
* <span data-ttu-id="03344-111">Edytuj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-111">Edit an access control record</span></span> 
* <span data-ttu-id="03344-112">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="03344-113">Podczas przypisywania ACR tooa woluminu, należy zadbać czy hello wolumin nie jest jednocześnie dostępna przez więcej niż jednego hosta z systemem innym niż klastrowane, ponieważ może to spowodować uszkodzenie hello woluminu.</span><span class="sxs-lookup"><span data-stu-id="03344-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="03344-114">Podczas usuwania ACR z woluminu, upewnij się, że odpowiednie hostujących hello nie uzyskuje dostęp do woluminu hello, usunięcia hello może powodować zakłócenia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="03344-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="03344-115">Dodaj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-115">Add an access control record</span></span>
<span data-ttu-id="03344-116">Użyj usługi Menedżer StorSimple hello **Konfiguruj** tooadd ACRs strony.</span><span class="sxs-lookup"><span data-stu-id="03344-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="03344-117">Zazwyczaj co ACR zostanie skojarzony z jednego woluminu.</span><span class="sxs-lookup"><span data-stu-id="03344-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="03344-118">Wykonaj następujące kroki tooadd ACR hello.</span><span class="sxs-lookup"><span data-stu-id="03344-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="03344-119">tooadd rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-119">tooadd an access control record</span></span>
1. <span data-ttu-id="03344-120">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="03344-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="03344-121">W hello tabelarycznej listę pod **rekordy kontroli dostępu**, dostawy **nazwa** dla rekordu ACR.</span><span class="sxs-lookup"><span data-stu-id="03344-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="03344-122">Podaj hello nazwę IQN hosta z systemem Windows w obszarze **Nazwa inicjatora iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="03344-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="03344-123">Witaj tooget IQN hosta z systemem Windows Server, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="03344-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="03344-124">Uruchom inicjatora iSCSI firmy Microsoft hello na hoście z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="03344-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="03344-125">W hello **właściwości inicjatora iSCSI** okna na powitania **konfiguracji** karcie zaznacz i skopiuj ciąg hello z hello **Nazwa inicjatora** pola.</span><span class="sxs-lookup"><span data-stu-id="03344-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="03344-126">Wklej ten ciąg hello **Nazwa inicjatora iSCSI** pola w tabeli ACRs hello w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="03344-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="03344-127">Kliknij przycisk **zapisać** hello toosave nowo utworzony ACR.</span><span class="sxs-lookup"><span data-stu-id="03344-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="03344-128">Witaj tabelarycznej listę zostanie zaktualizowany tooreflect można to dodawanie.</span><span class="sxs-lookup"><span data-stu-id="03344-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="03344-129">Edytuj rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-129">Edit an access control record</span></span>
<span data-ttu-id="03344-130">Użyj hello **Konfiguruj** strony w hello Azure classic portal tooedit ACRs.</span><span class="sxs-lookup"><span data-stu-id="03344-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="03344-131">Można modyfikować tylko ACRs, które nie są obecnie w użyciu.</span><span class="sxs-lookup"><span data-stu-id="03344-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="03344-132">tooedit ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="03344-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="03344-133">Wykonaj następujące kroki tooedit ACR hello.</span><span class="sxs-lookup"><span data-stu-id="03344-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="03344-134">tooedit rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-134">tooedit an access control record</span></span>
1. <span data-ttu-id="03344-135">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="03344-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="03344-136">W hello tabelarycznej listę rekordy kontroli dostępu hello, umieść kursor nad hello ACR, że chcesz toomodify.</span><span class="sxs-lookup"><span data-stu-id="03344-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="03344-137">Podaj nową nazwę i/lub IQN dla hello ACR.</span><span class="sxs-lookup"><span data-stu-id="03344-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="03344-138">Kliknij przycisk **zapisać** toosave hello zmodyfikować ACR.</span><span class="sxs-lookup"><span data-stu-id="03344-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="03344-139">Witaj tabelarycznej listę zostanie zaktualizowany tooreflect można tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="03344-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="03344-140">Usuń rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-140">Delete an access control record</span></span>
<span data-ttu-id="03344-141">Użyj hello **Konfiguruj** strony w hello Azure classic portal toodelete ACRs.</span><span class="sxs-lookup"><span data-stu-id="03344-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="03344-142">Można usunąć tylko ACRs, które nie są obecnie w użyciu.</span><span class="sxs-lookup"><span data-stu-id="03344-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="03344-143">toodelete ACR skojarzony z woluminem, który jest obecnie używany, musisz najpierw wykonać hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="03344-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="03344-144">Wykonaj hello następujące kroki toodelete rekord kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="03344-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="03344-145">toodelete rekord kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="03344-145">toodelete an access control record</span></span>
1. <span data-ttu-id="03344-146">Na powitania strony docelowej usługi, wybierz usługę, kliknij dwukrotnie nazwę usługi hello, a następnie kliknij hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="03344-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="03344-147">W hello tabelarycznej listę rekordy kontroli dostępu hello (ACRs), umieść kursor nad hello ACR, że chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="03344-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="03344-148">Ikona usuwania (**x**) będą wyświetlane w hello extreme prawej kolumnie dla hello ACR wybrany.</span><span class="sxs-lookup"><span data-stu-id="03344-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="03344-149">Kliknij przycisk hello **x** ikonę toodelete hello ACR.</span><span class="sxs-lookup"><span data-stu-id="03344-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="03344-150">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** toocontinue z hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="03344-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="03344-151">Hello tabelarycznej listę zostaną zaktualizowane tooreflect hello usunięcia.</span><span class="sxs-lookup"><span data-stu-id="03344-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03344-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03344-152">Next steps</span></span>
* <span data-ttu-id="03344-153">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="03344-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="03344-154">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="03344-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

