---
title: "Tworzenie projektu usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz utworzyć projekt usługi w chmurze Azure z programem Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="9a333-103">Tworzenie projektu usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a333-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="9a333-104">Azure Tools dla programu Visual Studio zawiera szablon projektu umożliwiający tworzenie usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="9a333-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="9a333-105">Po utworzeniu projektu programu Visual Studio umożliwia konfigurowanie, debugowania i wdrożyć usługę w chmurze na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9a333-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="9a333-106">Kroki, aby utworzyć projekt usługi w chmurze platformy Azure w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a333-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="9a333-107">Ta sekcja przeprowadzi Cię przez proces tworzenia projektu usługi w chmurze platformy Azure w programie Visual Studio z co najmniej jedną rolę sieci web.</span><span class="sxs-lookup"><span data-stu-id="9a333-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="9a333-108">Uruchom program Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9a333-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="9a333-109">W menu głównym wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="9a333-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="9a333-110">Wybierz **chmury** z Visual C# lub Visual Basic projektu węzłów szablonu, a następnie wybierz **usługi w chmurze Azure** z listy szablonów.</span><span class="sxs-lookup"><span data-stu-id="9a333-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![Nowa usługa w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="9a333-112">Określenie, której wersji programu .NET Framework ma być używany do tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="9a333-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="9a333-113">Wprowadź nazwę i lokalizację projektu i nazwy dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9a333-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="9a333-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a333-114">Select **OK**.</span></span>

1. <span data-ttu-id="9a333-115">W **nową usługę w chmurze Azure Microsoft** okno dialogowe, wybierz role, które chcesz dodać, a następnie kliknij przycisk strzałki w prawo, aby dodać je do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9a333-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![Wybierz nowe role usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="9a333-117">Aby zmienić nazwę roli, do której dodano, umieść kursor na rolę w **nową usługę w chmurze Azure Microsoft** okna dialogowego i z menu kontekstowego wybierz **Zmień nazwę**.</span><span class="sxs-lookup"><span data-stu-id="9a333-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="9a333-118">Można również zmienić nazwy roli w ramach rozwiązania (w **Eksploratora rozwiązań**) po został dodany.</span><span class="sxs-lookup"><span data-stu-id="9a333-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![Zmień nazwę roli usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="9a333-120">Projektu programu Visual Studio Azure ma skojarzenia do roli projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="9a333-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="9a333-121">Projekt zawiera również *pliku definicji usługi* i *pliku konfiguracji usługi*:</span><span class="sxs-lookup"><span data-stu-id="9a333-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="9a333-122">**Plik definicji usługi** — definiuje ustawienia środowiska uruchomieniowego dla aplikacji, w tym, jakie role są wymagane, punktów końcowych i rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9a333-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="9a333-123">**Plik konfiguracji usługi** — konfiguruje liczbę wystąpień roli są wykonane i wartości ustawienia zdefiniowane dla roli.</span><span class="sxs-lookup"><span data-stu-id="9a333-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="9a333-124">Aby uzyskać więcej informacji o tych plikach, zobacz [konfigurowania ról dla usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="9a333-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a333-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a333-125">Next steps</span></span>
- [<span data-ttu-id="9a333-126">Zarządzanie rolami w projekty usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a333-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
