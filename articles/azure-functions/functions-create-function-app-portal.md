---
title: "Tworzenie aplikacji funkcji przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Utwórz nową aplikację funkcji w usłudze Azure App Service z portalu."
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
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="f5a9d-103">Tworzenie aplikacji funkcji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f5a9d-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="f5a9d-104">Aplikacje platformy Azure funkcja używa infrastruktury usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="f5a9d-105">W tym temacie przedstawiono sposób tworzenia aplikacji funkcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="f5a9d-106">Aplikacja funkcji jest kontener, który obsługuje wykonywanie poszczególnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="f5a9d-107">Po utworzeniu aplikacji funkcji w usłudze App Service, plan hostingu aplikacji funkcji można korzystać ze wszystkich funkcji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="f5a9d-108">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="f5a9d-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="f5a9d-109">Podczas tworzenia aplikacji funkcji, podaj prawidłową **Nazwa aplikacji**, która może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="f5a9d-110">Podkreślenie (**_**) nie jest dozwolonym znakiem.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="f5a9d-111">Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="f5a9d-112">Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="f5a9d-113">Po utworzeniu aplikacji funkcji, można utworzyć pojedynczych funkcji w różnych językach jeden lub więcej.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="f5a9d-114">Tworzenie funkcji [przy użyciu portalu](functions-create-first-azure-function.md#create-function), [ciągłe wdrażanie](functions-continuous-deployment.md), lub [przekazywanie z FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="f5a9d-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="f5a9d-115">Plany usługi</span><span class="sxs-lookup"><span data-stu-id="f5a9d-115">Service plans</span></span>

<span data-ttu-id="f5a9d-116">Usługa Azure Functions oferuje dwa pakiety różnych usług: plan zużycia i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="f5a9d-117">Plan zużycie automatycznie przydzieli moc obliczeniową, gdy kod jest uruchomiona, możliwość skalowania w poziomie jako niezbędne do obsługi obciążenia, a następnie skale — w gdy kodu nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="f5a9d-118">Plan usługi aplikacji umożliwia funkcja dostęp aplikacji do wszystkie urządzenia z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="f5a9d-119">Musisz wybrać plan usługi po utworzeniu aplikacji funkcji, a obecnie nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="f5a9d-120">Aby uzyskać więcej informacji, zobacz [wybierz usługi Azure Functions plan hostingu](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="f5a9d-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="f5a9d-121">Jeśli planujesz uruchamianie funkcji JavaScript na plan usługi aplikacji, należy wybrać plan o mniejszej liczby rdzeni.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="f5a9d-122">Aby uzyskać więcej informacji, zobacz [JavaScript — odwołanie do funkcji](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="f5a9d-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="f5a9d-123">Wymagania dotyczące konta magazynu</span><span class="sxs-lookup"><span data-stu-id="f5a9d-123">Storage account requirements</span></span>

<span data-ttu-id="f5a9d-124">Podczas tworzenia aplikacji funkcji w usłudze App Service, należy utworzyć lub połączyć konto usługi Azure Storage ogólnego przeznaczenia, które obsługuje magazynu obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="f5a9d-125">Wewnętrznie funkcji używa magazynu dla operacji, takich jak zarządzanie wyzwalaczy i rejestrowanie wykonania funkcji.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="f5a9d-126">Niektóre konta magazynu nie obsługują kolejek i tabel, takich jak konta magazynu tylko do obiektów blob, usługa Azure Premium Storage i kont magazynu ogólnego przeznaczenia z replikacją ZRS.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="f5a9d-127">Te konta są filtrowane z z bloku konto magazynu podczas tworzenia aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="f5a9d-128">Korzystając z zużycie plan hostingu, plików konfiguracji kod i powiązania funkcji są przechowywane w magazyn plików Azure w ramach konta głównego magazynu.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="f5a9d-129">Podczas usuwania konta magazynu głównego ta zawartość zostanie usunięta i nie może zostać odzyskany.</span><span class="sxs-lookup"><span data-stu-id="f5a9d-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="f5a9d-130">Aby dowiedzieć się więcej na temat typów kont magazynu, zobacz [wprowadzenie do usług magazynu Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="f5a9d-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f5a9d-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5a9d-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



