---
title: "Omówienie usługi Azure StorSimple danych Manager aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie hello usługi Menedżer StorSimple danych (w podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="a9916-103">Omówienie Menedżera danych StorSimple (podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="a9916-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="a9916-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a9916-104">Overview</span></span>

<span data-ttu-id="a9916-105">Microsoft Azure StorSimple jest rozwiązanie magazynu hybrydowego chmury, które adresy hello złożoności danych niestrukturalnych zwykle powiązanych ze udziałów plików.</span><span class="sxs-lookup"><span data-stu-id="a9916-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="a9916-106">StorSimple używa magazynu w chmurze, jak rozszerzenie hello lokalnego rozwiązania i automatycznie warstwy danych przez Magazyn lokalne powitania i magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a9916-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="a9916-107">Zintegrowana ochrony danych z lokalnego i w chmurze migawek, eliminuje potrzebę hello sprawling infrastruktury magazynu.</span><span class="sxs-lookup"><span data-stu-id="a9916-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="a9916-108">Archiwalne i odzyskiwanie po awarii jest również bezproblemowe z chmurą hello działający jako lokalizacji poza siedzibą firmy.</span><span class="sxs-lookup"><span data-stu-id="a9916-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="a9916-109">Hello usługi przekształcania danych, która wprowadzamy w tym dokumencie umożliwia możesz tooseamlessly dostępu hello danych StorSimple w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a9916-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="a9916-110">Ta usługa udostępnia interfejsy API tooextract dane z StorSimple i prezentować tooother Azure usług w formatach, które mogą być łatwo używane.</span><span class="sxs-lookup"><span data-stu-id="a9916-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="a9916-111">w tej wersji zapoznawczej obsługiwane formaty Hello są obiekty BLOB platformy Azure i zasoby usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a9916-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="a9916-112">Ta transformacja umożliwia możesz tooeasily przewodowy usług, takich jak usługi Azure Media Services, Azure HDInsight uczenie maszynowe Azure i usługi Azure Search dane toooperate na urządzeniu lokalnym serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="a9916-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="a9916-113">Poniżej przedstawiono diagram blokowy wysokiego poziomu pokazujący to.</span><span class="sxs-lookup"><span data-stu-id="a9916-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagram ogólny](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="a9916-115">W tym dokumencie opisano, jak można założyć prywatnej wersji zapoznawczej tej usługi.</span><span class="sxs-lookup"><span data-stu-id="a9916-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="a9916-116">Wyjaśniono również, jak skorzystać z tej aplikacji toowrite usługi, które używają danych StorSimple i innymi usługami Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a9916-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="a9916-117">Załóż Data Manager w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="a9916-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="a9916-118">Przed zarejestrowaniem się usługi Menedżera danych hello Przejrzyj hello następujące wymagania wstępne.</span><span class="sxs-lookup"><span data-stu-id="a9916-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a9916-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9916-119">Prerequisites</span></span>

<span data-ttu-id="a9916-120">Tym ćwiczeniu przyjęto założenie, że masz</span><span class="sxs-lookup"><span data-stu-id="a9916-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="a9916-121">Aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9916-121">an active Azure subscription.</span></span>
* <span data-ttu-id="a9916-122">Access tooa zarejestrowane urządzenia serii StorSimple 8000 z aktualizacją</span><span class="sxs-lookup"><span data-stu-id="a9916-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="a9916-123">Witaj wszystkie klucze skojarzone z urządzenia z serii StorSimple 8000 hello.</span><span class="sxs-lookup"><span data-stu-id="a9916-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="a9916-124">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="a9916-124">Sign up</span></span>

<span data-ttu-id="a9916-125">Witaj Menedżer StorSimple danych znajduje się w prywatnej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a9916-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="a9916-126">Wykonaj hello następujące kroki toosign konto w prywatnej wersji zapoznawczej tej usługi:</span><span class="sxs-lookup"><span data-stu-id="a9916-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="a9916-127">Zaloguj się do hello portalu Azure z rozszerzeniem Menedżer StorSimple danych hello w: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="a9916-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="a9916-128">Użyj toolog Twoje poświadczenia platformy Azure w.</span><span class="sxs-lookup"><span data-stu-id="a9916-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="a9916-129">Kliknij przycisk hello  **+**  toocreate ikonę usługi.</span><span class="sxs-lookup"><span data-stu-id="a9916-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="a9916-130">Kliknij przycisk **magazynu** , a następnie kliknij przycisk **Zobacz wszystkie** w otwartym bloku hello.</span><span class="sxs-lookup"><span data-stu-id="a9916-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Ikona danych Menedżera StorSimple wyszukiwania](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="a9916-132">Ikona Menedżer StorSimple danych hello jest widoczna.</span><span class="sxs-lookup"><span data-stu-id="a9916-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Wybierz ikonę Menedżera StorSimple danych](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="a9916-134">Kliknij ikonę Menedżer StorSimple danych, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a9916-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="a9916-135">Wybierz subskrypcję hello mają tooenable hello prywatnej wersji zapoznawczej, a następnie kliknij przycisk **Zapisz się!**</span><span class="sxs-lookup"><span data-stu-id="a9916-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Zapisz się](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="a9916-137">To wysyła tooonboard żądania użytkownik.</span><span class="sxs-lookup"><span data-stu-id="a9916-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="a9916-138">Firma Microsoft będzie dołączyć należy jak najszybciej.</span><span class="sxs-lookup"><span data-stu-id="a9916-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="a9916-139">Po włączeniu subskrypcji można utworzyć usługi Menedżer StorSimple danych.</span><span class="sxs-lookup"><span data-stu-id="a9916-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="a9916-140">tooeasily dostępu do usługi Menedżer StorSimple danych hello, kliknij przycisk toopin ikonę gwiazdki hello go tooyour Ulubione.</span><span class="sxs-lookup"><span data-stu-id="a9916-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Dostęp do danych StorSimple menedżerów](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="a9916-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9916-142">Next steps</span></span>

<span data-ttu-id="a9916-143">[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a9916-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
