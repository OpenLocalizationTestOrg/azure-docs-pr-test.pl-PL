---
title: "Zarządzanie za pomocą Eksploratora Azure dla programu Eclipse pamięci podręczne Redis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać pamięci podręczne Azure redis za pomocą Eksploratora Azure dla programu Eclipse."
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
ms.openlocfilehash: dc1ed15cb83e6ddc8cf84f5c52a0482231f75e40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="fbca9-103">Zarządzanie za pomocą Eksploratora Azure dla programu Eclipse pamięci podręczne Redis</span><span class="sxs-lookup"><span data-stu-id="fbca9-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="fbca9-104">Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse, zapewnia się, że Java deweloperom łatwe w użyciu rozwiązanie do zarządzania redis pamięci podręcznych na koncie Azure z poziomu środowiska Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="fbca9-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="fbca9-105">Tworzenie pamięci podręcznej Redis przy użyciu programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="fbca9-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="fbca9-106">W poniższych krokach objaśniono kroków w celu tworzenia pamięci podręcznej redis przy użyciu Eksploratora Azure.</span><span class="sxs-lookup"><span data-stu-id="fbca9-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="fbca9-107">Zaloguj się do konta platformy Azure, korzystając z procedury w [znak w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse] artykułu.</span><span class="sxs-lookup"><span data-stu-id="fbca9-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="fbca9-108">W **Eksploratora Azure** okna narzędzia, a następnie rozwiń **Azure** węzła, kliknij prawym przyciskiem myszy **pamięci podręczne Redis**, a następnie kliknij przycisk **Tworzenie pamięci podręcznej Redis**.</span><span class="sxs-lookup"><span data-stu-id="fbca9-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Tworzenie Menu pamięci podręcznej Redis][CR01]

1. <span data-ttu-id="fbca9-110">Gdy **nowa pamięć podręczna Redis** zostanie wyświetlone okno dialogowe, określ następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="fbca9-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Utwórz nowe okno dialogowe pamięci podręcznej Redis][CR02]

   <span data-ttu-id="fbca9-112">a.</span><span class="sxs-lookup"><span data-stu-id="fbca9-112">a.</span></span> <span data-ttu-id="fbca9-113">**Nazwa DNS**: Określa poddomenie DNS nowej pamięci podręcznej redis, który jest dołączany na początku ". redis.cache.windows.net", na przykład: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="fbca9-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="fbca9-114">b.</span><span class="sxs-lookup"><span data-stu-id="fbca9-114">b.</span></span> <span data-ttu-id="fbca9-115">**Subskrypcja**: Określa subskrypcji platformy Azure, którego chcesz użyć dla nowej pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="fbca9-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="fbca9-116">c.</span><span class="sxs-lookup"><span data-stu-id="fbca9-116">c.</span></span> <span data-ttu-id="fbca9-117">**Grupa zasobów**: Określa grupę zasobów dla pamięci podręcznej redis; musisz wybrać jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="fbca9-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="fbca9-118">**Utwórz nowy**: Określa, czy chcesz utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="fbca9-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="fbca9-119">**Użyj istniejącego**: Określa, że wybiorą z listy grup zasobów skojarzonych z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fbca9-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="fbca9-120">d.</span><span class="sxs-lookup"><span data-stu-id="fbca9-120">d.</span></span> <span data-ttu-id="fbca9-121">**Lokalizacja**: Określa lokalizację, w której utworzono pamięć podręczną redis; na przykład *zachodnie stany USA*.</span><span class="sxs-lookup"><span data-stu-id="fbca9-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="fbca9-122">e.</span><span class="sxs-lookup"><span data-stu-id="fbca9-122">e.</span></span> <span data-ttu-id="fbca9-123">**Warstwa cenowa**: Określa warstwy cenowej korzysta z pamięci podręcznej redis; to ustawienie określa liczbę połączeń klientów.</span><span class="sxs-lookup"><span data-stu-id="fbca9-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="fbca9-124">(Aby uzyskać więcej informacji, zobacz [cennik pamięci podręcznej Redis].)</span><span class="sxs-lookup"><span data-stu-id="fbca9-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="fbca9-125">f.</span><span class="sxs-lookup"><span data-stu-id="fbca9-125">f.</span></span> <span data-ttu-id="fbca9-126">**Port bez protokołu SSL**: Określa, czy pamięć podręczna redis zezwala na połączenia SSL nie; domyślnie są dozwolone tylko na połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="fbca9-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="fbca9-127">Po określeniu wszystkie ustawienia pamięci podręcznej redis, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbca9-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="fbca9-128">Po utworzeniu pamięci podręcznej redis, będzie on wyświetlany w Eksploratorze Azure.</span><span class="sxs-lookup"><span data-stu-id="fbca9-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Pamięci podręcznej w Eksploratorze Azure redis][CR03]

> [!NOTE]
>
> <span data-ttu-id="fbca9-130">Aby uzyskać więcej informacji o konfigurowaniu Azure ustawienia pamięci podręcznej redis, zobacz [Konfigurowanie pamięci podręcznej Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="fbca9-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="fbca9-131">Wyświetl właściwości dla pamięci podręcznej Redis w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="fbca9-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="fbca9-132">W Eksploratorze Azure, kliknij prawym przyciskiem myszy pamięci podręcznej redis, a następnie kliknij przycisk **Pokaż właściwości**.</span><span class="sxs-lookup"><span data-stu-id="fbca9-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure menu kontekstowe Eksploratora, aby wyświetlić właściwości pamięci podręcznej redis][SP01]

1. <span data-ttu-id="fbca9-134">W Eksploratorze Azure Wyświetla właściwości dla pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="fbca9-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Właściwości pamięci podręcznej Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="fbca9-136">Usuń pamięć podręczną Redis za pomocą programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="fbca9-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="fbca9-137">W Eksploratorze Azure, kliknij prawym przyciskiem myszy pamięci podręcznej redis, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="fbca9-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure menu kontekstowego Eksploratora można usunąć pamięci podręcznej redis][DE01]

1. <span data-ttu-id="fbca9-139">Kliknij przycisk **OK** po wyświetleniu monitu, aby usunąć pamięć podręczną redis.</span><span class="sxs-lookup"><span data-stu-id="fbca9-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Usuwanie wiersza pamięci podręcznej redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="fbca9-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbca9-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="fbca9-142">Aby uzyskać więcej informacji o pamięci podręcznej Azure redis, ustawienia konfiguracji i cenach zobacz następujące linki:</span><span class="sxs-lookup"><span data-stu-id="fbca9-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="fbca9-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="fbca9-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="fbca9-144">[Dokumentacja pamięci podręcznej redis]</span><span class="sxs-lookup"><span data-stu-id="fbca9-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="fbca9-145">[cennik pamięci podręcznej Redis]</span><span class="sxs-lookup"><span data-stu-id="fbca9-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="fbca9-146">[Konfigurowanie pamięci podręcznej Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="fbca9-146">[How to configure Azure Redis Cache]</span></span>

<!-- URL List -->

<span data-ttu-id="fbca9-147">[cennik pamięci podręcznej Redis]: https://azure.microsoft.com/pricing/details/cache/</span><span class="sxs-lookup"><span data-stu-id="fbca9-147">[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/</span></span>
<span data-ttu-id="fbca9-148">[Azure Redis Cache]: https://azure.microsoft.com/services/cache/</span><span class="sxs-lookup"><span data-stu-id="fbca9-148">[Azure Redis Cache]: https://azure.microsoft.com/services/cache/</span></span>
<span data-ttu-id="fbca9-149">[Dokumentacja pamięci podręcznej redis]: ./redis-cache/index.md</span><span class="sxs-lookup"><span data-stu-id="fbca9-149">[Redis Cache Documentation]: ./redis-cache/index.md</span></span>
<span data-ttu-id="fbca9-150">[Konfigurowanie pamięci podręcznej Redis Azure]: ./redis-cache/cache-configure.md</span><span class="sxs-lookup"><span data-stu-id="fbca9-150">[How to configure Azure Redis Cache]: ./redis-cache/cache-configure.md</span></span>
<span data-ttu-id="fbca9-151">[znak w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="fbca9-151">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
