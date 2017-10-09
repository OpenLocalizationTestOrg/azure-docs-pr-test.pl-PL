---
title: aaaCreate aplikacji funkcji z hello portalu Azure | Dokumentacja firmy Microsoft
description: "Tworzenie nowej aplikacji funkcji w usłudze Azure App Service przy użyciu portalu hello."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="0a9c3-103">Tworzenie aplikacji funkcji z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0a9c3-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="0a9c3-104">Aplikacje platformy Azure funkcji używa hello infrastruktury usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="0a9c3-105">W tym temacie opisano sposób toocreate aplikacji funkcji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="0a9c3-106">Aplikacja funkcji jest hello obsługujący wykonanie hello poszczególnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="0a9c3-107">Po utworzeniu aplikacji funkcji w hostingu planu usługi aplikacji hello aplikacji funkcji można korzystać ze wszystkich funkcji hello usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="0a9c3-108">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="0a9c3-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="0a9c3-109">Podczas tworzenia aplikacji funkcji, podaj prawidłową **Nazwa aplikacji**, która może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="0a9c3-110">Podkreślenie (**_**) nie jest dozwolonym znakiem.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="0a9c3-111">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="0a9c3-112">Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="0a9c3-113">Po utworzeniu hello funkcji aplikacji, można utworzyć pojedynczych funkcji w różnych językach co najmniej jeden.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="0a9c3-114">Tworzenie funkcji [przy użyciu portalu hello](functions-create-first-azure-function.md#create-function), [ciągłe wdrażanie](functions-continuous-deployment.md), lub [przekazywanie z FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="0a9c3-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="0a9c3-115">Plany usługi</span><span class="sxs-lookup"><span data-stu-id="0a9c3-115">Service plans</span></span>

<span data-ttu-id="0a9c3-116">Usługa Azure Functions oferuje dwa pakiety różnych usług: plan zużycia i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="0a9c3-117">plan zużycie Hello automatycznie przydzieli moc obliczeniową, gdy kod działa, możliwość skalowania w poziomie jako niezbędne toohandle obciążenia, a następnie skali w kodu nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="0a9c3-118">plan usługi aplikacji Hello zapewnia funkcji urządzeniami hello tooall dostępu aplikacji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="0a9c3-119">Musisz wybrać plan usługi po utworzeniu aplikacji funkcji, a obecnie nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="0a9c3-120">Aby uzyskać więcej informacji, zobacz [wybierz usługi Azure Functions plan hostingu](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0a9c3-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="0a9c3-121">Jeśli planujesz funkcji JavaScript toorun plan usługi aplikacji, należy wybrać plan o mniejszej liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="0a9c3-122">Aby uzyskać więcej informacji, zobacz hello [JavaScript — odwołanie do funkcji](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="0a9c3-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="0a9c3-123">Wymagania dotyczące konta magazynu</span><span class="sxs-lookup"><span data-stu-id="0a9c3-123">Storage account requirements</span></span>

<span data-ttu-id="0a9c3-124">Podczas tworzenia aplikacji funkcji w usłudze App Service, należy utworzyć lub połączyć tooa ogólnego przeznaczenia konta usługi Magazyn Azure obsługującym magazynu obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="0a9c3-125">Wewnętrznie funkcji używa magazynu dla operacji, takich jak zarządzanie wyzwalaczy i rejestrowanie wykonania funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="0a9c3-126">Niektóre konta magazynu nie obsługują kolejek i tabel, takich jak konta magazynu tylko do obiektów blob, usługa Azure Premium Storage i kont magazynu ogólnego przeznaczenia z replikacją ZRS.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="0a9c3-127">Te konta są filtrowane z z hello bloku konto magazynu podczas tworzenia aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="0a9c3-128">Podczas korzystania z planu obsługi zużycia hello, plików konfiguracji kod i powiązanie funkcji są przechowywane w na koncie magazynu głównego hello usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="0a9c3-129">Podczas usuwania konta magazynu głównego hello ta zawartość zostanie usunięta i nie może zostać odzyskany.</span><span class="sxs-lookup"><span data-stu-id="0a9c3-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="0a9c3-130">toolearn więcej informacji na temat typów kont magazynu, zobacz [wprowadzenie do usług magazynu Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="0a9c3-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0a9c3-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0a9c3-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



