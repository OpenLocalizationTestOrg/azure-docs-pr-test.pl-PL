---
title: "Zarządzanie kontenerów woluminu StorSimple na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Menedżer urządzeń StorSimple usługi woluminu kontenery strona służy do dodawania, modyfikowania i usuwania kontenera woluminów."
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
ms.openlocfilehash: 0f8e00d6d07224f56625482f339e612e68914be2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="ccbfa-103">Zarządzanie kontenery woluminów StorSimple przy użyciu usługi Menedżer StorSimple urządzenia</span><span class="sxs-lookup"><span data-stu-id="ccbfa-103">Use the StorSimple Device Manager service to manage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="ccbfa-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ccbfa-104">Overview</span></span>
<span data-ttu-id="ccbfa-105">W tym samouczku wyjaśniono, jak korzystać z usługi Menedżera urządzeń StorSimple, tworzenie i zarządzanie nimi kontenery woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="ccbfa-106">Kontener woluminów na urządzeniu Microsoft Azure StorSimple zawiera jeden lub więcej woluminów, które mają konta magazynu, szyfrowania i ustawienia zużycie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="ccbfa-107">Urządzenie może mieć wiele kontenerów woluminu dla jego woluminów.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="ccbfa-108">Kontener woluminów obejmuje następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="ccbfa-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="ccbfa-109">**Woluminy** — warstwowy lub woluminów StorSimple, które znajdują się w kontenerze wolumin przypięty lokalnie.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> 
* <span data-ttu-id="ccbfa-110">**Szyfrowanie** — klucz szyfrowania, które mogą być definiowane dla każdego kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="ccbfa-111">Ten klucz służy do szyfrowania danych, które są wysyłane z urządzenia StorSimple w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-111">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="ccbfa-112">Z klasy zbrojnych AES 256-bitowym kluczem jest używany z kluczem wprowadzonych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-112">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="ccbfa-113">Aby zabezpieczyć dane, zalecamy zawsze włączone szyfrowanie magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-113">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="ccbfa-114">**Konto magazynu** — konta magazynu Azure, który jest używany do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-114">**Storage account** – The Azure storage account that is used to store the data.</span></span> <span data-ttu-id="ccbfa-115">Wszystkie woluminy znajdującej się w kontenerze woluminów udostępnić to konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-115">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="ccbfa-116">Wybierz konto magazynu z istniejącej listy lub Utwórz nowe konto, podczas tworzenia kontenera woluminu, a następnie określ poświadczenia dostępu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-116">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="ccbfa-117">**Chmury przepustowości** — przepustowości przez urządzenie po wysłaniu danych z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-117">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="ccbfa-118">Można wymusić kontroli przepustowości, określając wartość z zakresu od 1 MB/s do 1000 MB/s, podczas tworzenia tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="ccbfa-119">Jeśli chcesz, aby urządzenia pełną dostępną przepustowość, ustaw tego pola **nieograniczone**.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-119">If you want the device to consume all available bandwidth, set this field to **Unlimited**.</span></span> <span data-ttu-id="ccbfa-120">Można również utworzyć i zastosować szablon przepustowości przydzielić przepustowość zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-120">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

<span data-ttu-id="ccbfa-121">W poniższych procedurach opisano sposób użycia StorSimple **kontenery woluminów** bloku, aby ukończyć następujące typowe operacje:</span><span class="sxs-lookup"><span data-stu-id="ccbfa-121">The following procedures explain how to use the StorSimple **Volume containers** blade to complete the following common operations:</span></span>

* <span data-ttu-id="ccbfa-122">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-122">Add a volume container</span></span>
* <span data-ttu-id="ccbfa-123">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-123">Modify a volume container</span></span>
* <span data-ttu-id="ccbfa-124">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="ccbfa-125">Dodaj kontener woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-125">Add a volume container</span></span>
<span data-ttu-id="ccbfa-126">Wykonaj poniższe kroki, aby dodać kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-126">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="ccbfa-127">Modyfikowanie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-127">Modify a volume container</span></span>
<span data-ttu-id="ccbfa-128">Wykonaj poniższe kroki, aby zmodyfikować kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-128">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="ccbfa-129">Usunięcie kontenera woluminów</span><span class="sxs-lookup"><span data-stu-id="ccbfa-129">Delete a volume container</span></span>
<span data-ttu-id="ccbfa-130">Kontener woluminów obejmuje woluminy znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-130">A volume container has volumes within it.</span></span> <span data-ttu-id="ccbfa-131">Można usunąć tylko wtedy, gdy wszystkie woluminy, które są zawarte w niej najpierw zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-131">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="ccbfa-132">Wykonaj poniższe kroki, aby usunąć kontener woluminów.</span><span class="sxs-lookup"><span data-stu-id="ccbfa-132">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="ccbfa-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccbfa-133">Next steps</span></span>
* <span data-ttu-id="ccbfa-134">Dowiedz się więcej o [zarządzania woluminami StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="ccbfa-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="ccbfa-135">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple urządzenia do administrowania urządzeniem StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ccbfa-135">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

