---
title: "aaaConfigure projekt usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure platformy Azure w chmurze projekt usługi w programie Visual Studio, w zależności od wymagań dla tego projektu."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="16473-103">Konfigurowanie projektu usługi w chmurze platformy Azure przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16473-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="16473-104">Projekt usługi w chmurze platformy Azure, można skonfigurować w zależności od wymagań dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="16473-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="16473-105">Można ustawić właściwości hello projektu dla hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="16473-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="16473-106">**Publikowanie tooAzure usługi chmury** — można ustawić właściwości toomake się upewnić, że istniejące tooAzure wdrożone usługi chmury nie jest przypadkowo usunięte.</span><span class="sxs-lookup"><span data-stu-id="16473-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="16473-107">**Uruchomić ani debugować usługi w chmurze na komputerze lokalnym hello** — możesz wybrać toouse konfiguracji usługi i wskazuje, czy emulatora magazynu Azure hello toostart.</span><span class="sxs-lookup"><span data-stu-id="16473-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="16473-108">**Sprawdzanie poprawności pakietu usług chmury po utworzeniu** — można określić tootreat wszystkie ostrzeżenia jako błędy, dzięki czemu można zapewnić tym pakiecie usługi chmury hello wdraża bez żadnych problemów.</span><span class="sxs-lookup"><span data-stu-id="16473-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="16473-109">Kroki tooconfigure projekt usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="16473-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="16473-110">Otwarcia lub utworzenia projektu usługi w chmurze w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16473-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="16473-111">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="16473-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="16473-112">Na stronie właściwości projektu hello, wybierz hello **programowanie** kartę.</span><span class="sxs-lookup"><span data-stu-id="16473-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menu Właściwości projektu](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="16473-114">Ustaw **Monituj przed usunięciem istniejącego wdrożenia** za**True**.</span><span class="sxs-lookup"><span data-stu-id="16473-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="16473-115">To ustawienie pomaga tooensure nie przypadkowo usuwaj istniejącego wdrożenia na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="16473-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="16473-116">Wybierz hello potrzeby **konfiguracji usługi** tooindicate konfigurację usługi, która ma toouse podczas uruchamiania lub debugowania usługi w chmurze lokalnie.</span><span class="sxs-lookup"><span data-stu-id="16473-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="16473-117">Aby uzyskać więcej informacji na temat toomodify z konfiguracją usługi roli, zobacz [jak tooconfigure hello ról platformy Azure w chmurze usługi z programem Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="16473-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="16473-118">Ustaw **emulatora magazynu Start Azure** za**True** toostart hello emulatora magazynu Azure podczas uruchamiania lub debugowania usługi w chmurze lokalnie.</span><span class="sxs-lookup"><span data-stu-id="16473-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="16473-119">Ustaw **Traktuj ostrzeżenia jako błędy** za**True** toomake się, że nie można opublikować, jeśli występują błędy sprawdzania poprawności pakietu.</span><span class="sxs-lookup"><span data-stu-id="16473-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="16473-120">Ustaw **korzystania z portów projektu sieci web** za**True** toomake się, że roli sieci web używany hello sam każdy port czasu rozpoczyna się lokalnie w usługach IIS Express.</span><span class="sxs-lookup"><span data-stu-id="16473-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="16473-121">Z hello narzędzi Visual Studio, wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="16473-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16473-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16473-122">Next steps</span></span>
- [<span data-ttu-id="16473-123">Konfigurowanie projektu platformy Azure przy użyciu wielu konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="16473-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

