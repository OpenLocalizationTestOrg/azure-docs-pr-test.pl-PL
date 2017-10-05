---
title: "Za pomocą aplikacji App-V z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z aplikacji App-V w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="1b50c-103">Za pomocą aplikacji App-V w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1b50c-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b50c-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="1b50c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1b50c-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="1b50c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1b50c-106">W kolekcji hybrydowej usługi Azure RemoteApp, co wymaga przyłączenie do domeny, można użyć aplikacji App-V.</span><span class="sxs-lookup"><span data-stu-id="1b50c-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="1b50c-107">Przed rozpoczęciem pracy, upewnij się zainstalować klienta App-V 5.1 z najnowszymi aktualizacjami.</span><span class="sxs-lookup"><span data-stu-id="1b50c-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="1b50c-108">Musisz utworzyć [niestandardowego obrazu](remoteapp-create-custom-image.md) zawierającą klienta App-V.</span><span class="sxs-lookup"><span data-stu-id="1b50c-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="1b50c-109">Jest to łatwe w użyciu istniejącej infrastruktury programu App-V z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1b50c-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="1b50c-110">Kolekcja hybrydowa jest wdrażana na sieć Wirtualną platformy Azure, który ma dostęp do kontrolera domeny i maszyn wirtualnych są przyłączone do domeny, można wykorzystać istniejące App-v infrastruktury i wdrożenie metody do aplikacji App-V host easyily w usłudze Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1b50c-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="1b50c-111">Poniżej przedstawiono pewne kwestie, które należy zwrócić uwagę na podstawie typu wdrożenia App-V, które obecnie ma:</span><span class="sxs-lookup"><span data-stu-id="1b50c-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="1b50c-112">Opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1b50c-112">Configuration options</span></span> |  | <span data-ttu-id="1b50c-113">Dodatnią</span><span class="sxs-lookup"><span data-stu-id="1b50c-113">Positive</span></span> | <span data-ttu-id="1b50c-114">Ujemna</span><span class="sxs-lookup"><span data-stu-id="1b50c-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b50c-115">Metoda dostarczania</span><span class="sxs-lookup"><span data-stu-id="1b50c-115">Delivery method</span></span> |<span data-ttu-id="1b50c-116">Przesyłania strumieniowego (na żądanie)</span><span class="sxs-lookup"><span data-stu-id="1b50c-116">Streaming (on-demand)</span></span> |<span data-ttu-id="1b50c-117">Aplikacja jest zawsze r i świeża</span><span class="sxs-lookup"><span data-stu-id="1b50c-117">App is always the latest and fresh</span></span> |<span data-ttu-id="1b50c-118">Pierwszy opóźnienia</span><span class="sxs-lookup"><span data-stu-id="1b50c-118">First time latency</span></span> |
| <span data-ttu-id="1b50c-119">Zainstalowany</span><span class="sxs-lookup"><span data-stu-id="1b50c-119">Mounted</span></span> |<span data-ttu-id="1b50c-120">Najszybszym; Aplikacja jest już obecny w maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b50c-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="1b50c-121">Rozrostu - ma miejsce obrazu (limit 127 GB)</span><span class="sxs-lookup"><span data-stu-id="1b50c-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1b50c-122">Aplikacja lokalizacji magazynu</span><span class="sxs-lookup"><span data-stu-id="1b50c-122">App location storage</span></span> |<span data-ttu-id="1b50c-123">Zawartość udostępniona</span><span class="sxs-lookup"><span data-stu-id="1b50c-123">Shared content</span></span> |<span data-ttu-id="1b50c-124">Aplikacja jest uruchamiana w pamięci wystąpienia usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1b50c-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="1b50c-125">Eats pamięci i dobre połączenie przesyłania strumieniowego serwera (plik), w którym znajduje się aplikacja</span><span class="sxs-lookup"><span data-stu-id="1b50c-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="1b50c-126">Dysku (buforowanej)</span><span class="sxs-lookup"><span data-stu-id="1b50c-126">Disk (Cached)</span></span> |<span data-ttu-id="1b50c-127">Szybkie wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="1b50c-127">Fast execution.</span></span> <span data-ttu-id="1b50c-128">Aplikacja nie jest zależna od dostępności źródła zawartości</span><span class="sxs-lookup"><span data-stu-id="1b50c-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="1b50c-129">Rozrostu - ma miejsce obrazu (limit 127 GB)</span><span class="sxs-lookup"><span data-stu-id="1b50c-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="1b50c-130">Określanie wartości docelowej</span><span class="sxs-lookup"><span data-stu-id="1b50c-130">Targeting</span></span> |<span data-ttu-id="1b50c-131">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="1b50c-131">User</span></span> |<span data-ttu-id="1b50c-132">Wymaga infrastruktury App-V pełne autonomiczny</span><span class="sxs-lookup"><span data-stu-id="1b50c-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="1b50c-133">Global (komputer)</span><span class="sxs-lookup"><span data-stu-id="1b50c-133">Global (machine)</span></span> |<span data-ttu-id="1b50c-134">Wstępnie publikowania lub docelowych przy użyciu publikowania serwera</span><span class="sxs-lookup"><span data-stu-id="1b50c-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="1b50c-135">Należy zaktualizować obrazu platformy Azure, jeśli chcesz zaktualizować aplikację (dużych).</span><span class="sxs-lookup"><span data-stu-id="1b50c-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="1b50c-136">Zajmie trochę miejsca na obrazie.</span><span class="sxs-lookup"><span data-stu-id="1b50c-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="1b50c-137">Po utworzeniu niestandardowego obrazu i kolekcji hybrydowej opublikować aplikację, Przypisz użytkowników i korzystać z istniejących aplikacji App-V hostowanych w usłudze Azure RemoteApp dostarczane na dowolnych urządzeniach w dowolnym miejscu.</span><span class="sxs-lookup"><span data-stu-id="1b50c-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

