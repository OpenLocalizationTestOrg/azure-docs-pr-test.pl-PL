---
title: "aaaManage Twojego kontenery woluminów StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak używasz hello Menedżer StorSimple kontenery woluminów usługi strony tooadd, zmodyfikować lub usunąć kontener woluminów."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="3d676-103">Użyj kontenery woluminów StorSimple toomanage usługi Menedżer StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="3d676-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="3d676-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3d676-104">Overview</span></span>
<span data-ttu-id="3d676-105">W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple i zarządzanie nimi kontenery woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3d676-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="3d676-106">Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="3d676-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="3d676-107">Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów.</span><span class="sxs-lookup"><span data-stu-id="3d676-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="3d676-108">Kontener woluminów obejmuje hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="3d676-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="3d676-109">**Woluminy** — hello warstwowej lub woluminów StorSimple, które znajdują się w kontenerze woluminów hello przypięty lokalnie.</span><span class="sxs-lookup"><span data-stu-id="3d676-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="3d676-110">Kontener woluminów mogą zawierać zapasowe too256 woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3d676-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="3d676-111">**Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="3d676-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="3d676-112">Ten klucz jest używany do szyfrowania hello dane są przesyłane z chmury toohello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3d676-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="3d676-113">Z klasy zbrojnych AES 256-bitowym kluczem służy kluczem hello wprowadzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3d676-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="3d676-114">toosecure danych, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3d676-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="3d676-115">**Konto magazynu** — Witaj konto magazynu dostawcy usług magazynu tooyour połączonych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3d676-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="3d676-116">Wszystkie woluminy hello znajdującej się w kontenerze woluminów udostępnić to konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="3d676-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="3d676-117">Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, jeśli Tworzenie kontenera woluminów hello, a następnie określisz hello poświadczeń dostępu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="3d676-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="3d676-118">**Chmury przepustowości** — Witaj przepustowości przez urządzenie hello, gdy hello dane z urządzenia hello są wysyłane toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="3d676-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="3d676-119">Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 do 1000 MB/s podczas definiowania tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="3d676-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="3d676-120">Tooconsume urządzenia hello pełną dostępną przepustowość, ustawić tooUnlimited tego pola.</span><span class="sxs-lookup"><span data-stu-id="3d676-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="3d676-121">Można również utworzyć i zastosować przepustowości przepustowości tooallocate szablonu na podstawie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="3d676-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Strona kontenery woluminów](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="3d676-123">Ta poniższe procedury wyjaśniają, jak toouse hello StorSimple **kontenery woluminów** hello toocomplete strony następujące typowe operacje:</span><span class="sxs-lookup"><span data-stu-id="3d676-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="3d676-124">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-124">Add a volume container</span></span> 
* <span data-ttu-id="3d676-125">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-125">Modify a volume container</span></span> 
* <span data-ttu-id="3d676-126">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="3d676-127">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-127">Add a volume container</span></span>
<span data-ttu-id="3d676-128">Wykonaj następujące kroki tooadd kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="3d676-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="3d676-129">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-129">Modify a volume container</span></span>
<span data-ttu-id="3d676-130">Wykonaj następujące kroki toomodify kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="3d676-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="3d676-131">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="3d676-131">Delete a volume container</span></span>
<span data-ttu-id="3d676-132">Kontener woluminów obejmuje woluminy znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="3d676-132">A volume container has volumes within it.</span></span> <span data-ttu-id="3d676-133">Można usunąć tylko wtedy, gdy wszystkie woluminy hello zawarte w niej najpierw zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="3d676-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="3d676-134">Wykonaj następujące kroki toodelete kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="3d676-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="3d676-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d676-135">Next steps</span></span>
* <span data-ttu-id="3d676-136">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="3d676-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="3d676-137">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3d676-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

