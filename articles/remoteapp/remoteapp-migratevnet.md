---
title: "toomigrate aaaHow z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="aff31-103">Jak toomigrate kolekcji hybrydowej z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="aff31-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="aff31-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="aff31-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="aff31-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="aff31-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="aff31-106">Dobre wieści!</span><span class="sxs-lookup"><span data-stu-id="aff31-106">Good news!</span></span> <span data-ttu-id="aff31-107">Firma Microsoft włączono kolekcji usługi RemoteApp hybrydowego toodeploy bezpośrednio do użytkownika istniejących sieci wirtualnych platformy Azure (sieci wirtualne) zamiast tworzenia sieci wirtualnych specyficzne dla usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="aff31-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="aff31-108">Dzięki temu można wykorzystać hello najnowszych funkcji sieciami Wirtualnymi (na przykład ExpressRoute) i nadaj z hybrydowego kolekcje sieci bezpośredniego dostępu tooother usług platformy Azure i maszyny wirtualne wdrażane toothat sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aff31-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="aff31-109">(To pozwala lepszą wydajność i Instalator łatwiejsze niż konfiguracje sieci Wirtualnej do sieci Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="aff31-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="aff31-110">Załóżmy, że zostały już utworzone kolekcji usługi RemoteApp hybrydowe o nazwie *OriginalCollection* z sieci Wirtualnej usługi RemoteApp o nazwie *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="aff31-111">Poniżej przedstawiono toomigrate kroki hello go tooa nowej sieci Wirtualnej platformy Azure o nazwie *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="aff31-112">Na powitania **sieci** kartę w hello [portalu zarządzania](http://manage.windowsazure.com/), utworzyć sieć Wirtualną o nazwie *AzureVNET*za pomocą hello tej samej lokalizacji, konfiguracji serwera DNS i przestrzeń adresową (dla co najmniej jednego z hello *AzureVNET* podsieci) jako użyte do *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="aff31-113">Skonfiguruj *AzureVNET* tooeither hosta lub wdrożenie usługi Active Directory toohello łączności sieciowej który *OriginalCollection* jest przyłączonych do domeny do.</span><span class="sxs-lookup"><span data-stu-id="aff31-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="aff31-114">Na powitania **nimi** pozycję Utwórz kolekcję RemoteApp o nazwie *nowej kolekcji*.</span><span class="sxs-lookup"><span data-stu-id="aff31-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="aff31-115">(Użyj hello **Utwórz z sieci Wirtualnej** opcję nie **szybkie tworzenie**.)</span><span class="sxs-lookup"><span data-stu-id="aff31-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="aff31-116">Skonfiguruj *NewCollection* toobe wdrożone podsieci tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="aff31-117">Skonfiguruj *NewCollection* toouse hello takiego samego obrazu i informacji dotyczących przyłączania domeny jako użyte do *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="aff31-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="aff31-118">Po kilku godzinach *NewCollection* będą widoczne na liście kolekcji o stanie aktywnym.</span><span class="sxs-lookup"><span data-stu-id="aff31-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="aff31-119">Teraz Jeśli nie potrzebujesz toomigrate informacje o użytkowniku z hello oryginalnej kolekcji toohello nową kolekcję, zrobić dalej następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="aff31-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="aff31-120">Usuń *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="aff31-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="aff31-121">Usuń *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="aff31-122">I gotowe!</span><span class="sxs-lookup"><span data-stu-id="aff31-122">And, you’re done!</span></span>

<span data-ttu-id="aff31-123">Alternatywnie Jeśli potrzebujesz informacji o użytkowniku toomigrate z hello oryginalnej kolekcji toohello nową kolekcję, zrobić dalej następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="aff31-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="aff31-124">Wyślij wiadomość e-mail zbyt[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) z Identyfikatorem subskrypcji platformy Azure Witaj nazwy oryginalnego kolekcji i hello nazwę nowej kolekcji i poproś o toomigrate informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="aff31-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="aff31-125">W ciągu 2 dni roboczych hello RemoteApp team zostaną przeniesione listy dostępu użytkownika hello wszystkich dokumentów użytkownika i ustawień użytkownika z hello oryginalnej kolekcji toohello nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="aff31-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="aff31-126">Usuń *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="aff31-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="aff31-127">Usuń *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="aff31-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="aff31-128">I teraz wszystko gotowe!</span><span class="sxs-lookup"><span data-stu-id="aff31-128">And now, you’re done!</span></span>

<span data-ttu-id="aff31-129">Jeśli masz pytania lub potrzebujesz pomocy specjalne, Wyślij wiadomość e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="aff31-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

