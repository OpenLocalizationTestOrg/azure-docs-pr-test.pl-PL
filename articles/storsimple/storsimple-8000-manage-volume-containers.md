---
title: "aaaManage Twojego kontenery woluminów StorSimple na urządzeniu z serii StorSimple 8000 hello | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak używasz hello Menedżera urządzeń StorSimple kontenery woluminów usługi strony tooadd, zmodyfikować lub usunąć kontener woluminów."
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
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="c6b3e-103">Użyj kontenery woluminów StorSimple toomanage hello Menedżera urządzeń StorSimple usługi</span><span class="sxs-lookup"><span data-stu-id="c6b3e-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="c6b3e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c6b3e-104">Overview</span></span>
<span data-ttu-id="c6b3e-105">W tym samouczku wyjaśniono, jak toouse hello toocreate usługi Menedżer StorSimple urządzenia i zarządzać kontenery woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="c6b3e-106">Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="c6b3e-107">Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="c6b3e-108">Kontener woluminów obejmuje hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="c6b3e-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="c6b3e-109">**Woluminy** — hello warstwowej lub woluminów StorSimple, które znajdują się w kontenerze woluminów hello przypięty lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="c6b3e-110">**Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="c6b3e-111">Ten klucz jest używany do szyfrowania hello dane są przesyłane z chmury toohello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="c6b3e-112">Z klasy zbrojnych AES 256-bitowym kluczem służy kluczem hello wprowadzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="c6b3e-113">toosecure danych, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="c6b3e-114">**Konto magazynu** — Witaj konta magazynu platformy Azure, które jest używane toostore hello danych.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="c6b3e-115">Wszystkie woluminy hello znajdującej się w kontenerze woluminów udostępnić to konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="c6b3e-116">Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, jeśli Tworzenie kontenera woluminów hello, a następnie określisz hello poświadczeń dostępu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="c6b3e-117">**Chmury przepustowości** — Witaj przepustowości przez urządzenie hello, gdy hello dane z urządzenia hello są wysyłane toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="c6b3e-118">Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 MB/s do 1000 MB/s, podczas tworzenia tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="c6b3e-119">Tooconsume urządzenia hello pełną dostępną przepustowość, ustawić tego pola zbyt**nieograniczone**.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="c6b3e-120">Można również utworzyć i zastosować przepustowości przepustowości tooallocate szablonu na podstawie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="c6b3e-121">Witaj poniższe procedury wyjaśniają, jak toouse hello StorSimple **kontenery woluminów** hello toocomplete bloku następujące typowe operacje:</span><span class="sxs-lookup"><span data-stu-id="c6b3e-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="c6b3e-122">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-122">Add a volume container</span></span>
* <span data-ttu-id="c6b3e-123">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-123">Modify a volume container</span></span>
* <span data-ttu-id="c6b3e-124">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="c6b3e-125">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-125">Add a volume container</span></span>
<span data-ttu-id="c6b3e-126">Wykonaj następujące kroki tooadd kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="c6b3e-127">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-127">Modify a volume container</span></span>
<span data-ttu-id="c6b3e-128">Wykonaj następujące kroki toomodify kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="c6b3e-129">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="c6b3e-129">Delete a volume container</span></span>
<span data-ttu-id="c6b3e-130">Kontener woluminów obejmuje woluminy znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-130">A volume container has volumes within it.</span></span> <span data-ttu-id="c6b3e-131">Można usunąć tylko wtedy, gdy wszystkie woluminy hello zawarte w niej najpierw zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="c6b3e-132">Wykonaj następujące kroki toodelete kontenera woluminów hello.</span><span class="sxs-lookup"><span data-stu-id="c6b3e-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="c6b3e-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6b3e-133">Next steps</span></span>
* <span data-ttu-id="c6b3e-134">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="c6b3e-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="c6b3e-135">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c6b3e-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

