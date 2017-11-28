---
title: "aplikacje App-V aaaUsing z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje toouse App-V w usłudze Azure RemoteApp."
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
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="39f35-103">Za pomocą aplikacji App-V w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="39f35-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="39f35-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="39f35-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="39f35-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="39f35-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="39f35-106">W kolekcji hybrydowej usługi Azure RemoteApp, co wymaga przyłączenie do domeny, można użyć aplikacji App-V.</span><span class="sxs-lookup"><span data-stu-id="39f35-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="39f35-107">Przed rozpoczęciem pracy należy upewnić się, że klient App-V 5.1 hello tooinstall o hello najnowsze aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="39f35-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="39f35-108">Konieczne będzie toocreate [niestandardowego obrazu](remoteapp-create-custom-image.md) zawierającą klienta hello App-V.</span><span class="sxs-lookup"><span data-stu-id="39f35-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="39f35-109">Jest łatwy toouse istniejącej infrastruktury programu App-V z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="39f35-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="39f35-110">Ponieważ kolekcji hybrydowej jest wdrażana na sieć Wirtualną platformy Azure ma kontroler domeny tooyour dostępu i maszyn wirtualnych hello są przyłączone do domeny, można wykorzystać istniejące App-v infrastruktury i wdrożenie metody tooeasyily App-V aplikacji hosta w usłudze Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="39f35-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="39f35-111">Poniżej przedstawiono pewne kwestie, które należy zwrócić uwagę na podstawie hello typu wdrożenia App-V, które obecnie ma:</span><span class="sxs-lookup"><span data-stu-id="39f35-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="39f35-112">Opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="39f35-112">Configuration options</span></span> |  | <span data-ttu-id="39f35-113">Dodatnią</span><span class="sxs-lookup"><span data-stu-id="39f35-113">Positive</span></span> | <span data-ttu-id="39f35-114">Ujemna</span><span class="sxs-lookup"><span data-stu-id="39f35-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39f35-115">Metoda dostarczania</span><span class="sxs-lookup"><span data-stu-id="39f35-115">Delivery method</span></span> |<span data-ttu-id="39f35-116">Przesyłania strumieniowego (na żądanie)</span><span class="sxs-lookup"><span data-stu-id="39f35-116">Streaming (on-demand)</span></span> |<span data-ttu-id="39f35-117">Aplikacja jest zawsze hello najnowsze i gotowości do pracy</span><span class="sxs-lookup"><span data-stu-id="39f35-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="39f35-118">Pierwszy opóźnienia</span><span class="sxs-lookup"><span data-stu-id="39f35-118">First time latency</span></span> |
| <span data-ttu-id="39f35-119">Zainstalowany</span><span class="sxs-lookup"><span data-stu-id="39f35-119">Mounted</span></span> |<span data-ttu-id="39f35-120">Najszybszym; Aplikacja jest już obecny na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="39f35-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="39f35-121">Rozrostu - ma miejsce obrazu (limit 127 GB)</span><span class="sxs-lookup"><span data-stu-id="39f35-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="39f35-122">Aplikacja lokalizacji magazynu</span><span class="sxs-lookup"><span data-stu-id="39f35-122">App location storage</span></span> |<span data-ttu-id="39f35-123">Zawartość udostępniona</span><span class="sxs-lookup"><span data-stu-id="39f35-123">Shared content</span></span> |<span data-ttu-id="39f35-124">Aplikacja jest uruchamiana w pamięci wystąpienia usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="39f35-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="39f35-125">Eats pamięci i dobre połączenie serwera toostreaming (plik), w którym znajduje się aplikacja hello</span><span class="sxs-lookup"><span data-stu-id="39f35-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="39f35-126">Dysku (buforowanej)</span><span class="sxs-lookup"><span data-stu-id="39f35-126">Disk (Cached)</span></span> |<span data-ttu-id="39f35-127">Szybkie wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="39f35-127">Fast execution.</span></span> <span data-ttu-id="39f35-128">Aplikacja nie jest zależna od dostępności źródła zawartości</span><span class="sxs-lookup"><span data-stu-id="39f35-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="39f35-129">Rozrostu - ma miejsce obrazu (limit 127 GB)</span><span class="sxs-lookup"><span data-stu-id="39f35-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="39f35-130">Określanie wartości docelowej</span><span class="sxs-lookup"><span data-stu-id="39f35-130">Targeting</span></span> |<span data-ttu-id="39f35-131">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="39f35-131">User</span></span> |<span data-ttu-id="39f35-132">Wymaga infrastruktury App-V pełne autonomiczny</span><span class="sxs-lookup"><span data-stu-id="39f35-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="39f35-133">Global (komputer)</span><span class="sxs-lookup"><span data-stu-id="39f35-133">Global (machine)</span></span> |<span data-ttu-id="39f35-134">Wstępnie publikowania lub docelowych przy użyciu publikowania serwera</span><span class="sxs-lookup"><span data-stu-id="39f35-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="39f35-135">Musi tooupdate obrazu platformy Azure, jeśli chcesz aplikacji hello tooupdate (dużych).</span><span class="sxs-lookup"><span data-stu-id="39f35-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="39f35-136">Zajmie trochę miejsca na obrazie.</span><span class="sxs-lookup"><span data-stu-id="39f35-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="39f35-137">Po utworzeniu niestandardowego obrazu i kolekcji hybrydowej opublikować aplikację, Przypisz użytkowników i korzystać z istniejących aplikacji App-V hostowanych w usłudze Azure RemoteApp dostarczyć urządzenia tooany w dowolnym miejscu.</span><span class="sxs-lookup"><span data-stu-id="39f35-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

