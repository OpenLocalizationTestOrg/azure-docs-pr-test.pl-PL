---
title: "Zarządzanie kontenerów woluminu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak służy strony kontenery woluminów usługi Menedżer StorSimple do dodawania, modyfikowania i usuwania kontenera woluminów."
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="03f01-103">Usługę Menedżer StorSimple umożliwia zarządzanie kontenery woluminów StorSimple</span><span class="sxs-lookup"><span data-stu-id="03f01-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="03f01-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="03f01-104">Overview</span></span>
<span data-ttu-id="03f01-105">W tym samouczku opisano sposób korzystania z usługi Menedżer StorSimple, tworzenie i zarządzanie nimi kontenery woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03f01-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="03f01-106">Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="03f01-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="03f01-107">Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów.</span><span class="sxs-lookup"><span data-stu-id="03f01-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="03f01-108">Kontener woluminów obejmuje następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="03f01-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="03f01-109">**Woluminy** — warstwowy lub woluminów StorSimple, które znajdują się w kontenerze wolumin przypięty lokalnie.</span><span class="sxs-lookup"><span data-stu-id="03f01-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="03f01-110">Kontener woluminów może zawierać maksymalnie 256 woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03f01-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="03f01-111">**Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="03f01-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="03f01-112">Ten klucz służy do szyfrowania danych, które są wysyłane z urządzenia StorSimple w chmurze.</span><span class="sxs-lookup"><span data-stu-id="03f01-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="03f01-113">Z klasy zbrojnych AES 256-bitowym kluczem jest używany z kluczem wprowadzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03f01-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="03f01-114">Aby zabezpieczyć dane, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="03f01-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="03f01-115">**Konto magazynu** — konta magazynu, które jest połączone z dostawcą usług magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="03f01-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="03f01-116">Wszystkie woluminy znajdującej się w kontenerze woluminów udostępnić to konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="03f01-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="03f01-117">Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, podczas tworzenia kontenera woluminu, a następnie określ poświadczenia dostępu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="03f01-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="03f01-118">**Chmury przepustowości** — przepustowości przez urządzenie po wysłaniu danych z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="03f01-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="03f01-119">Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 do 1000 MB/s podczas definiowania tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="03f01-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="03f01-120">Jeśli chcesz, aby urządzenie, aby korzystać z całej dostępnej przepustowości, ustaw nieograniczone tego pola.</span><span class="sxs-lookup"><span data-stu-id="03f01-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="03f01-121">Można również utworzyć i zastosować szablon przepustowości przydzielić przepustowość zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="03f01-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![Strona kontenery woluminów](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="03f01-123">Ta poniższe procedury dotyczą sposobu używania StorSimple **kontenery woluminów** stronie, aby wykonać następujące operacje wspólne:</span><span class="sxs-lookup"><span data-stu-id="03f01-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="03f01-124">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-124">Add a volume container</span></span> 
* <span data-ttu-id="03f01-125">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-125">Modify a volume container</span></span> 
* <span data-ttu-id="03f01-126">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="03f01-127">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-127">Add a volume container</span></span>
<span data-ttu-id="03f01-128">Wykonaj poniższe kroki, aby dodać kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="03f01-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="03f01-129">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-129">Modify a volume container</span></span>
<span data-ttu-id="03f01-130">Wykonaj poniższe kroki, aby zmodyfikować kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="03f01-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="03f01-131">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="03f01-131">Delete a volume container</span></span>
<span data-ttu-id="03f01-132">Kontener woluminów obejmuje woluminy znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="03f01-132">A volume container has volumes within it.</span></span> <span data-ttu-id="03f01-133">Można usunąć tylko wtedy, gdy wszystkie woluminy, które są zawarte w niej najpierw zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="03f01-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="03f01-134">Wykonaj poniższe kroki, aby usunąć kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="03f01-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="03f01-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03f01-135">Next steps</span></span>
* <span data-ttu-id="03f01-136">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="03f01-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="03f01-137">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple do administrowania urządzeniem StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="03f01-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

