---
title: "toorun Express emulatora aaaUsing i debugowania platformy Azure w chmurze usługi na komputerze lokalnym | Dokumentacja firmy Microsoft"
description: "Przy użyciu emulatora Express toorun i debugowania usługi w chmurze, na komputerze lokalnym"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="1487a-103">Przy użyciu emulatora Express toorun i debugowania platformy Azure usługa w chmurze na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="1487a-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="1487a-104">Przy użyciu emulatora Express, można testowanie i debugowanie usługi w chmurze bez konieczności uruchamiania programu Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1487a-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="1487a-105">Możesz ustawić toouse ustawienia Twojego projektu albo Express emulatora lub hello pełnego emulatora, w zależności od wymagań hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1487a-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="1487a-106">Aby uzyskać więcej informacji na temat pełnego emulatora hello, zobacz [uruchomić aplikację Azure w hello obliczeniowe emulatora](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1487a-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="1487a-107">Przy użyciu ekspresowej wersji emulatora w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1487a-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="1487a-108">Podczas tworzenia projektu platformy Azure w wersji 2.3 zestawu SDK platformy Azure lub nowszym Express emulatora automatycznie jest używany.</span><span class="sxs-lookup"><span data-stu-id="1487a-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="1487a-109">Dla istniejących projektów, które zostały utworzone przy użyciu starszej wersji hello Azure SDK Użyj hello następujące kroki tooselect emulatora Express:</span><span class="sxs-lookup"><span data-stu-id="1487a-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="1487a-110">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1487a-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="1487a-111">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1487a-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="1487a-112">Na stronach właściwości projektów hello, wybierz hello **Web** kartę.</span><span class="sxs-lookup"><span data-stu-id="1487a-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Właściwości projektu usługi w chmurze Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="1487a-114">W obszarze **lokalnego serwera wdrożeniowego**, wybierz pozycję **opcję Użyj usługi IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="1487a-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="1487a-115">W obszarze **emulatora**, wybierz pozycję **Express emulatora użyj**.</span><span class="sxs-lookup"><span data-stu-id="1487a-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="1487a-116">toolaunch hello emulatora Express, uruchom następujące polecenie w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1487a-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="1487a-117">Ograniczenia Express emulatora</span><span class="sxs-lookup"><span data-stu-id="1487a-117">Emulator Express limitations</span></span>
<span data-ttu-id="1487a-118">znane ograniczenia Express emulatora Hello następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="1487a-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="1487a-119">Ekspresowej wersji emulatora nie jest zgodny z serwera sieci Web usług IIS.</span><span class="sxs-lookup"><span data-stu-id="1487a-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="1487a-120">Usługi w chmurze może zawierać wiele ról, ale każda rola jest ograniczona tooone wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="1487a-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="1487a-121">Nie można uzyskać dostępu do numerów portów poniżej 1000.</span><span class="sxs-lookup"><span data-stu-id="1487a-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="1487a-122">Jeśli używasz dostawcę uwierzytelniania, która zwykle używa portu poniżej 1000, może być konieczne toochange tego numeru portu tooa wartość przekracza 1000.</span><span class="sxs-lookup"><span data-stu-id="1487a-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="1487a-123">Ograniczenia dotyczące toohello obliczeniowe emulatora usługi Azure mają zastosowanie również tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="1487a-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="1487a-124">Na przykład nie może mieć więcej niż 50 wystąpień roli dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1487a-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="1487a-125">Aby uzyskać więcej informacji na temat hello obliczeniowe emulatora usługi Azure, zobacz [uruchomić aplikację Azure w hello obliczeniowe emulatora](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="1487a-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1487a-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1487a-126">Next steps</span></span>
[<span data-ttu-id="1487a-127">Debugowanie usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="1487a-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
