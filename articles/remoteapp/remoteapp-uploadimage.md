---
title: "Przekaż obraz niestandardowy usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przekazać obraz niestandardowy usługi Azure RemoteApp"
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="f40b9-103">Przekaż obraz niestandardowy usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f40b9-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f40b9-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f40b9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f40b9-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="f40b9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f40b9-106">Teraz, gdy utworzono obrazu niestandardowego szablonu lub zaktualizować go ze zmianami, musisz przekazać go do biblioteki obrazu usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f40b9-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="f40b9-107">Wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f40b9-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f40b9-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="f40b9-108">Before you start</span></span>
1. <span data-ttu-id="f40b9-109">Upewnij się, niestandardowy obraz spełnia [wymagania dotyczące obrazu](remoteapp-imagereqs.md) i [wymagań aplikacji](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="f40b9-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="f40b9-110">Zainstaluj [modułu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f40b9-110">Install the [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="f40b9-111">Krok po kroku na temat przekazywania niestandardowego obrazu</span><span class="sxs-lookup"><span data-stu-id="f40b9-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="f40b9-112">Otwórz Portal zarządzania Azure i przejdź do strony usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f40b9-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="f40b9-113">Na **obrazy szablonów** , kliknij pozycję **przekazać** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="f40b9-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="f40b9-114">Wprowadź przyjazną nazwę dla obrazu i określ lokalizację konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f40b9-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="f40b9-115">Upewnij się, że lokalizacja jest tej samej lokalizacji co kolekcji usługi RemoteApp lub lokalizację, w której chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="f40b9-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="f40b9-116">Po wyświetleniu monitu można pobrać skryptu do komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f40b9-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="f40b9-117">Skopiuj parametry polecenia w polu tekstowym do Schowka.</span><span class="sxs-lookup"><span data-stu-id="f40b9-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="f40b9-118">Otwórz okno programu Windows PowerShell z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="f40b9-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="f40b9-119">W oknie programu Windows PowerShell z podwyższonym poziomem uprawnień przejdź do katalogu, w której pobrano skrypt.</span><span class="sxs-lookup"><span data-stu-id="f40b9-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="f40b9-120">Wklej skopiowane polecenie i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f40b9-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="f40b9-121">Rozpocznie się proces przekazywania i czas trwania może zależeć od wielu czynników, takich jak szybkość sieci, a rozmiar obrazu</span><span class="sxs-lookup"><span data-stu-id="f40b9-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="f40b9-122">W przypadku przekazania nie powiedzie się z powodu przerwy w działaniu sieci lub rzeczy jak, zawsze można wznowić procesu przekazywania zostanie rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="f40b9-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="f40b9-123">Aby wznowić przekazywania, uruchom skrypt ponownie, używając tego samego wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f40b9-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="f40b9-124">Nigdy nie zmodyfikować skrypt przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f40b9-124">Never modify the upload script.</span></span> <span data-ttu-id="f40b9-125">Aby upewnić się, że obraz spełnia wymagania dotyczące obrazów i wymagania dotyczące aplikacji została zaimplementowana konkretnych testów.</span><span class="sxs-lookup"><span data-stu-id="f40b9-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="f40b9-126">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="f40b9-126">Common problems</span></span>
* <span data-ttu-id="f40b9-127">Upewnij się, że używasz programu Windows PowerShell, nie programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f40b9-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="f40b9-128">Musisz zainstalować moduł Azure PowerShell, ponieważ niektóre moduły są wymagane podczas procesu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f40b9-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="f40b9-129">Nigdy nie zmodyfikować skrypt, sprawdzanie poprawności istnieją dla Twojej wygody.</span><span class="sxs-lookup"><span data-stu-id="f40b9-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="f40b9-130">Jeśli plik vhd pobiera zablokowane podczas przekazywania, skopiuj plik, lub przenieś go do nowego przekazywania lokalizacji, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="f40b9-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="f40b9-131">Może to być niektórych procesu systemu Windows, który uniemożliwia przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f40b9-131">There might be some Windows process that is preventing upload.</span></span>  

