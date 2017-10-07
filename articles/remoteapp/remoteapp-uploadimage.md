---
title: "aaaUpload niestandardowego obrazu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupload niestandardowego obrazu usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="c23ae-103">Przekaż obraz niestandardowy usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c23ae-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c23ae-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c23ae-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c23ae-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c23ae-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c23ae-106">Utworzono obrazu niestandardowego szablonu lub zaktualizować go ze zmianami, trzeba tooupload biblioteki obrazu usługi Azure RemoteApp tooyour obrazu.</span><span class="sxs-lookup"><span data-stu-id="c23ae-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="c23ae-107">Wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="c23ae-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c23ae-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c23ae-108">Before you start</span></span>
1. <span data-ttu-id="c23ae-109">Upewnij się, niestandardowy obraz spełnia hello [wymagania dotyczące obrazu](remoteapp-imagereqs.md) i [wymagań aplikacji](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="c23ae-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="c23ae-110">Zainstaluj hello [modułu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c23ae-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="c23ae-111">Krok po kroku na temat tooupload niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="c23ae-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="c23ae-112">Otwórz Portal zarządzania Azure i przejdź toohello RemoteApp strony.</span><span class="sxs-lookup"><span data-stu-id="c23ae-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="c23ae-113">Na powitania **obrazy szablonów** , kliknij pozycję **przekazać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c23ae-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="c23ae-114">Wprowadź przyjazną nazwę dla obrazu i określ lokalizację konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="c23ae-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="c23ae-115">Upewnij się, lokalizacja hello jest hello tej samej lokalizacji co kolekcji usługi RemoteApp lub lokalizację, gdzie ma zostać toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="c23ae-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="c23ae-116">Po wyświetleniu monitu, Pobierz hello skryptu tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c23ae-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="c23ae-117">Skopiuj parametry polecenia hello w Schowku tooyour pole tekstowe hello.</span><span class="sxs-lookup"><span data-stu-id="c23ae-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="c23ae-118">Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="c23ae-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="c23ae-119">Z hello z podwyższonym poziomem uprawnień okno programu Windows PowerShell Przejdź toohello tym samym katalogu, którego pobrano hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="c23ae-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="c23ae-120">Witaj Wklej skopiowane polecenie i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c23ae-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="c23ae-121">rozpocznie się proces przekazywania Hello i czas trwania może zależeć od wielu czynników, takich jak szybkość sieci, a rozmiar obrazu hello</span><span class="sxs-lookup"><span data-stu-id="c23ae-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="c23ae-122">Jeśli Twoje przekazywania nie powiedzie się z powodu przerwy w działaniu sieci lub rzeczy jak, zawsze można wznowić procesu przekazywania hello rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="c23ae-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="c23ae-123">tooresume przekazanie, uruchom ponownie, używając skrypt hello hello sam wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c23ae-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="c23ae-124">Nigdy nie należy zmodyfikować skrypt przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="c23ae-124">Never modify hello upload script.</span></span> <span data-ttu-id="c23ae-125">Sprawdzania wymagań zostać zaimplementowany tooensure, który hello obraz spełnia hello obrazu wymagania i wymagania dotyczące aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c23ae-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="c23ae-126">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="c23ae-126">Common problems</span></span>
* <span data-ttu-id="c23ae-127">Upewnij się, że używasz programu Windows PowerShell, nie programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c23ae-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="c23ae-128">Moduł Azure PowerShell hello tooinstall jest potrzebna, ponieważ niektóre moduły są potrzebne podczas procesu przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="c23ae-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="c23ae-129">Nigdy nie zmienia hello skryptu, sprawdzanie poprawności istnieją dla Twojej wygody.</span><span class="sxs-lookup"><span data-stu-id="c23ae-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="c23ae-130">Jeśli plik vhd hello pobiera zablokowane podczas przekazywania, skopiuj plik hello, lub przenieś go tooa nowe przekazywania lokalizacji, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="c23ae-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="c23ae-131">Może to być niektórych procesu systemu Windows, który uniemożliwia przekazywania.</span><span class="sxs-lookup"><span data-stu-id="c23ae-131">There might be some Windows process that is preventing upload.</span></span>  

