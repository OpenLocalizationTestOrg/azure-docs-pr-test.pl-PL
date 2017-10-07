---
title: "przy użyciu pamięci podręczne Redis aaaManaging hello Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage Twojego redis Azure buforuje przy użyciu hello Eksploratora Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="c775c-103">Zarządzanie za pomocą hello Eksploratora Azure dla programu Eclipse pamięci podręczne Redis</span><span class="sxs-lookup"><span data-stu-id="c775c-103">Managing Redis Caches using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c775c-104">Witaj Eksploratora Azure, który jest częścią zestawu narzędzi platformy Azure dla programu Eclipse hello, zapewnia się, że Java deweloperom łatwe w użyciu rozwiązanie do zarządzania redis pamięci podręcznych na koncie Azure z wewnątrz hello Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="c775c-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="c775c-105">Tworzenie pamięci podręcznej Redis przy użyciu programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="c775c-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="c775c-106">Witaj, wykonaj czynności umożliwia przeprowadzenie toocreate kroki hello pamięci podręcznej redis przy użyciu hello Azure Eksploratora.</span><span class="sxs-lookup"><span data-stu-id="c775c-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="c775c-107">Zaloguj się tooyour konto platformy Azure, wykonując kroki hello w hello [znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse] artykułu.</span><span class="sxs-lookup"><span data-stu-id="c775c-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="c775c-108">W hello **Eksploratora Azure** okna narzędzia, a następnie rozwiń hello **Azure** węzła, kliknij prawym przyciskiem myszy **pamięci podręczne Redis**, a następnie kliknij przycisk **Tworzenie pamięci podręcznej Redis**.</span><span class="sxs-lookup"><span data-stu-id="c775c-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Tworzenie Menu pamięci podręcznej Redis][CR01]

1. <span data-ttu-id="c775c-110">Gdy hello **nowa pamięć podręczna Redis** zostanie wyświetlone okno dialogowe, określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="c775c-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Utwórz nowe okno dialogowe pamięci podręcznej Redis][CR02]

   <span data-ttu-id="c775c-112">a.</span><span class="sxs-lookup"><span data-stu-id="c775c-112">a.</span></span> <span data-ttu-id="c775c-113">**Nazwa DNS**: Określa hello poddomenie DNS dla hello nowej pamięci podręcznej redis pamięci podręcznej, która jest reprezentowana zbyt ". redis.cache.windows .net", na przykład: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c775c-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which is prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="c775c-114">b.</span><span class="sxs-lookup"><span data-stu-id="c775c-114">b.</span></span> <span data-ttu-id="c775c-115">**Subskrypcja**: Określa hello subskrypcji platformy Azure ma toouse hello nowej pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="c775c-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="c775c-116">c.</span><span class="sxs-lookup"><span data-stu-id="c775c-116">c.</span></span> <span data-ttu-id="c775c-117">**Grupa zasobów**: Określa hello grupy zasobów dla pamięci podręcznej redis; należy toochoose hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="c775c-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="c775c-118">**Utwórz nowy**: Określa, że toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c775c-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c775c-119">**Użyj istniejącego**: Określa, że wybiorą z listy grup zasobów skojarzonych z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c775c-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="c775c-120">d.</span><span class="sxs-lookup"><span data-stu-id="c775c-120">d.</span></span> <span data-ttu-id="c775c-121">**Lokalizacja**: Określa lokalizację hello, w których tworzone jest pamięć podręczna redis; na przykład *zachodnie stany USA*.</span><span class="sxs-lookup"><span data-stu-id="c775c-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="c775c-122">e.</span><span class="sxs-lookup"><span data-stu-id="c775c-122">e.</span></span> <span data-ttu-id="c775c-123">**Warstwa cenowa**: Określa warstwy cenowej korzysta z pamięci podręcznej redis; to ustawienie określa hello liczbę połączeń klientów.</span><span class="sxs-lookup"><span data-stu-id="c775c-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="c775c-124">(Aby uzyskać więcej informacji, zobacz [cennik pamięci podręcznej Redis].)</span><span class="sxs-lookup"><span data-stu-id="c775c-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="c775c-125">f.</span><span class="sxs-lookup"><span data-stu-id="c775c-125">f.</span></span> <span data-ttu-id="c775c-126">**Port bez protokołu SSL**: Określa, czy pamięć podręczna redis zezwala na połączenia SSL nie; domyślnie są dozwolone tylko na połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="c775c-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="c775c-127">Po określeniu wszystkie ustawienia pamięci podręcznej redis, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c775c-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="c775c-128">Po utworzeniu pamięci podręcznej redis, będzie wyświetlana w hello Eksploratora Azure.</span><span class="sxs-lookup"><span data-stu-id="c775c-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Pamięci podręcznej w Eksploratorze Azure redis][CR03]

> [!NOTE]
>
> <span data-ttu-id="c775c-130">Aby uzyskać więcej informacji o konfigurowaniu Azure ustawienia pamięci podręcznej redis, zobacz [jak tooconfigure pamięć podręczna Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="c775c-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="c775c-131">Wyświetl właściwości powitania dla pamięci podręcznej Redis w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="c775c-131">Display hello properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="c775c-132">Witaj Eksploratora Azure, kliknij prawym przyciskiem myszy pamięć podręczna redis i kliknij przycisk **Pokaż właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c775c-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer właściwości menu kontekstowego toodisplay na potrzeby pamięci podręcznej redis][SP01]

1. <span data-ttu-id="c775c-134">Hello Azure Explorer wyświetla hello właściwości pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="c775c-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Właściwości pamięci podręcznej Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="c775c-136">Usuń pamięć podręczną Redis za pomocą programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="c775c-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="c775c-137">Witaj Eksploratora Azure, kliknij prawym przyciskiem myszy pamięć podręczna redis i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c775c-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Kontekst menu toodelete pamięci podręcznej redis Azure Explorer][DE01]

1. <span data-ttu-id="c775c-139">Kliknij przycisk **OK** po wyświetleniu toodelete pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="c775c-139">Click **OK** when prompted toodelete your redis cache.</span></span>

   ![Usuwanie wiersza pamięci podręcznej redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="c775c-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c775c-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="c775c-142">Aby uzyskać więcej informacji o pamięci podręcznej Azure redis, ustawienia konfiguracji i cenach Zobacz hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="c775c-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="c775c-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="c775c-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="c775c-144">[Dokumentacja pamięci podręcznej redis]</span><span class="sxs-lookup"><span data-stu-id="c775c-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="c775c-145">[cennik pamięci podręcznej Redis]</span><span class="sxs-lookup"><span data-stu-id="c775c-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="c775c-146">[jak tooconfigure pamięć podręczna Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="c775c-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[cennik pamięci podręcznej Redis]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Dokumentacja pamięci podręcznej redis]: ./redis-cache/index.md
[jak tooconfigure pamięć podręczna Redis Azure]: ./redis-cache/cache-configure.md
[znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
