---
title: "aaaSet się Środowisko deweloperskie do platformy Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Zainstaluj hello środowiska uruchomieniowego, zestawu SDK i narzędzia i Utwórz lokalny klaster projektowy. Po ukończeniu tej konfiguracji będzie gotowy toobuild aplikacji."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="9c2c6-104">Przygotowywanie środowiska projektowego</span><span class="sxs-lookup"><span data-stu-id="9c2c6-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c2c6-105">Windows</span><span class="sxs-lookup"><span data-stu-id="9c2c6-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="9c2c6-106">Linux</span><span class="sxs-lookup"><span data-stu-id="9c2c6-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="9c2c6-107">OSX</span><span class="sxs-lookup"><span data-stu-id="9c2c6-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="9c2c6-108">toobuild i uruchom [aplikacji usługi Azure Service Fabric] [ 1] na komputerze deweloperskim instalowanie hello środowiska uruchomieniowego, zestawu SDK i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="9c2c6-109">Należy również tooenable wykonywania skryptów programu Windows PowerShell hello objęte hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c2c6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c2c6-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="9c2c6-111">Obsługiwane wersje systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="9c2c6-111">Supported operating system versions</span></span>
<span data-ttu-id="9c2c6-112">następujące wersje systemu operacyjnego Hello są obsługiwane w przypadku rozwoju:</span><span class="sxs-lookup"><span data-stu-id="9c2c6-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="9c2c6-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="9c2c6-113">Windows 7</span></span>
* <span data-ttu-id="9c2c6-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="9c2c6-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="9c2c6-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9c2c6-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="9c2c6-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9c2c6-116">Windows Server 2016</span></span>
* <span data-ttu-id="9c2c6-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="9c2c6-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="9c2c6-118">System Windows 7 domyślnie zawiera program Windows PowerShell wyłącznie w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="9c2c6-119">Polecenia cmdlet programu PowerShell usługi Service Fabric wymagają programu PowerShell w wersji 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="9c2c6-120">Możesz [pobrać program Windows PowerShell 5.0] [ powershell5-download] z hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="9c2c6-121">Zainstaluj hello zestawu SDK i narzędzia</span><span class="sxs-lookup"><span data-stu-id="9c2c6-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="9c2c6-122">toouse programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="9c2c6-123">Service Fabric Tools są częścią hello Azure projektowania i zarządzania nimi obciążenia w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="9c2c6-124">Włącz to obciążenie w ramach instalacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="9c2c6-125">Ponadto należy hello tooinstall zestaw Microsoft Azure Service Fabric SDK, za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="9c2c6-126">[Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c2c6-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="9c2c6-127">toouse programu Visual Studio 2015 (wymaga programu Visual Studio 2015 Update 2 lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="9c2c6-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="9c2c6-128">Dla programu Visual Studio 2015 wraz z zestawu SDK, za pomocą Instalatora platformy sieci Web hello hello są zainstalowane narzędzia Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="9c2c6-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="9c2c6-129">[Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello i narzędzia][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="9c2c6-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="9c2c6-130">Instalowanie samego zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="9c2c6-130">SDK installation only</span></span>
<span data-ttu-id="9c2c6-131">Wymagane jest tylko hello zestawu SDK, po zastosowaniu tego pakietu:</span><span class="sxs-lookup"><span data-stu-id="9c2c6-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="9c2c6-132">[Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c2c6-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="9c2c6-133">bieżące wersje Hello są:</span><span class="sxs-lookup"><span data-stu-id="9c2c6-133">hello current versions are:</span></span>
* <span data-ttu-id="9c2c6-134">Zestaw SDK usługi Service Fabric w wersji 2.7.198</span><span class="sxs-lookup"><span data-stu-id="9c2c6-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="9c2c6-135">Środowisko uruchomieniowe usługi Service Fabric w wersji 5.7.198</span><span class="sxs-lookup"><span data-stu-id="9c2c6-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="9c2c6-136">Narzędzia usługi Service Fabric dla programu Visual Studio 2015 w wersji 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="9c2c6-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="9c2c6-137">Program Visual Studio 2017 Update 2 obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="9c2c6-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="9c2c6-138">Program Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) obejmuje narzędzia usługi Service Fabric dla programu Visual Studio w wersji 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="9c2c6-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="9c2c6-139">Listę obsługiwanych wersji można znaleźć na stronie [pomocy technicznej usługi Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="9c2c6-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="9c2c6-140">Włączanie wykonywania skryptów programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c2c6-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="9c2c6-141">Platforma Service Fabric korzysta ze skryptów programu Windows PowerShell do tworzenia lokalnego klastra projektowego i do wdrażania aplikacji z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="9c2c6-142">Domyślnie system Windows blokuje uruchamianie tych skryptów.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="9c2c6-143">tooenable je, należy zmodyfikować zasady wykonywania programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="9c2c6-144">Otwórz program PowerShell jako administrator i wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9c2c6-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="9c2c6-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c2c6-145">Next steps</span></span>
<span data-ttu-id="9c2c6-146">Po skonfigurowaniu środowiska projektowego możesz zacząć kompilować i uruchamiać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="9c2c6-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="9c2c6-147">Tworzenie pierwszej aplikacji platformy Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c2c6-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="9c2c6-148">Dowiedz się, jak toodeploy aplikacji w klastrze lokalnym i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="9c2c6-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="9c2c6-149">Dowiedz się więcej o hello modele programowania: Reliable Services i Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9c2c6-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="9c2c6-150">Zapoznaj się z sieci szkieletowej usług hello przykłady kodu w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="9c2c6-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="9c2c6-151">Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="9c2c6-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="9c2c6-152">Wykonaj hello learning tooget ścieżki platformy toohello obszerne wprowadzenie sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="9c2c6-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="9c2c6-153">Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="9c2c6-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Strona kampanii usługi Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI — link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI — link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI — link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
