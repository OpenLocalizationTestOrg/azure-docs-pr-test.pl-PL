---
title: "Uruchom i debugowania usługi w chmurze platformy Azure na komputerze lokalnym przy użyciu emulatora Express | Dokumentacja firmy Microsoft"
description: "Uruchom i debugowania usługi w chmurze na komputerze lokalnym przy użyciu emulatora Express"
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
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="78155-103">Uruchom i debugowania usługi w chmurze platformy Azure na komputerze lokalnym przy użyciu emulatora Express</span><span class="sxs-lookup"><span data-stu-id="78155-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="78155-104">Przy użyciu emulatora Express, można testowanie i debugowanie usługi w chmurze bez konieczności uruchamiania programu Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="78155-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="78155-105">Można ustawić ustawienia projektu, aby użyć emulatora Express lub pełnego emulatora, w zależności od wymagań usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="78155-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="78155-106">Aby uzyskać więcej informacji na temat pełnego emulatora, zobacz [uruchomić aplikację Azure w emulatorze obliczeniowe](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="78155-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="78155-107">Przy użyciu ekspresowej wersji emulatora w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78155-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="78155-108">Podczas tworzenia projektu platformy Azure w wersji 2.3 zestawu SDK platformy Azure lub nowszym Express emulatora automatycznie jest używany.</span><span class="sxs-lookup"><span data-stu-id="78155-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="78155-109">Dla istniejących projektów, które zostały utworzone przy użyciu starszej wersji zestawu SDK platformy Azure wykonaj następujące kroki, aby wybrać Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="78155-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="78155-110">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78155-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="78155-111">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz z menu kontekstowego **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="78155-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="78155-112">Na stronach właściwości projektów wybierz **Web** kartę.</span><span class="sxs-lookup"><span data-stu-id="78155-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Właściwości projektu usługi w chmurze Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="78155-114">W obszarze **lokalnego serwera wdrożeniowego**, wybierz pozycję **opcję Użyj usługi IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="78155-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="78155-115">W obszarze **emulatora**, wybierz pozycję **Express emulatora użyj**.</span><span class="sxs-lookup"><span data-stu-id="78155-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="78155-116">Aby uruchomić Express emulatora, uruchom następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="78155-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="78155-117">Ograniczenia Express emulatora</span><span class="sxs-lookup"><span data-stu-id="78155-117">Emulator Express limitations</span></span>
<span data-ttu-id="78155-118">Znane ograniczenia Express emulatora następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="78155-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="78155-119">Ekspresowej wersji emulatora nie jest zgodny z serwera sieci Web usług IIS.</span><span class="sxs-lookup"><span data-stu-id="78155-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="78155-120">Usługi w chmurze może zawierać wiele ról, ale jest ograniczony do jednego wystąpienia każdej roli.</span><span class="sxs-lookup"><span data-stu-id="78155-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="78155-121">Nie można uzyskać dostępu do numerów portów poniżej 1000.</span><span class="sxs-lookup"><span data-stu-id="78155-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="78155-122">Jeśli używasz dostawcę uwierzytelniania, która zwykle używa portu poniżej 1000, konieczne może zmienić tę wartość na numer portu, który jest ponad 1000.</span><span class="sxs-lookup"><span data-stu-id="78155-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="78155-123">Ograniczenia dotyczące emulatora obliczeniowe Azure dotyczą również emulatora Express.</span><span class="sxs-lookup"><span data-stu-id="78155-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="78155-124">Na przykład nie może mieć więcej niż 50 wystąpień roli dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="78155-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="78155-125">Aby uzyskać więcej informacji na temat obliczeniowe emulatora usługi Azure, zobacz [uruchomić aplikację Azure w emulatorze obliczeniowe](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="78155-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78155-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78155-126">Next steps</span></span>
[<span data-ttu-id="78155-127">Debugowanie usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="78155-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
