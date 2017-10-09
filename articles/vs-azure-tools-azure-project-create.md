---
title: "aaaCreating projekt usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz toocreate projekt usługi w chmurze Azure z programem Visual Studio"
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
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="564c6-103">Tworzenie projektu usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="564c6-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="564c6-104">Hello Azure Tools dla programu Visual Studio zawiera szablon projektu umożliwiający tworzenie usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="564c6-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="564c6-105">Po utworzeniu hello projektu programu Visual Studio umożliwia tooconfigure, debugowania i wdrażania tooAzure usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="564c6-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="564c6-106">Kroki toocreate projekt usługi w chmurze platformy Azure w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="564c6-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="564c6-107">Ta sekcja przeprowadzi Cię przez proces tworzenia projektu usługi w chmurze platformy Azure w programie Visual Studio z co najmniej jedną rolę sieci web.</span><span class="sxs-lookup"><span data-stu-id="564c6-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="564c6-108">Uruchom program Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="564c6-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="564c6-109">W menu głównym hello wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="564c6-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="564c6-110">Wybierz **chmury** z hello Visual C# lub Visual Basic projektu węzłów szablonu, a następnie wybierz **usługi w chmurze Azure** z hello listę szablonów.</span><span class="sxs-lookup"><span data-stu-id="564c6-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Nowa usługa w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="564c6-112">Określ wersję hello .NET Framework ma toouse toodevelop Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="564c6-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="564c6-113">Wprowadź nazwę i lokalizację projektu i nazwę hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="564c6-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="564c6-114">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="564c6-114">Select **OK**.</span></span>

1. <span data-ttu-id="564c6-115">W hello **nową usługę w chmurze Azure Microsoft** okno dialogowe, wybierz hello role mają tooadd i wybierz tooadd przycisk strzałki w prawo hello ich tooyour rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="564c6-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Wybierz nowe role usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="564c6-117">toorename roli zostały dodane, aktywowania roli hello w hello **nową usługę w chmurze Azure Microsoft** okna dialogowego i wybierz z menu kontekstowego hello, **zmienić**.</span><span class="sxs-lookup"><span data-stu-id="564c6-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="564c6-118">Można również zmienić nazwy roli w ramach rozwiązania (w hello **Eksploratora rozwiązań**) po został dodany.</span><span class="sxs-lookup"><span data-stu-id="564c6-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Zmień nazwę roli usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="564c6-120">Projekt programu Visual Studio Azure Hello ma skojarzenia toohello roli projektów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="564c6-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="564c6-121">Projekt Hello zawiera również hello *pliku definicji usługi* i *pliku konfiguracji usługi*:</span><span class="sxs-lookup"><span data-stu-id="564c6-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="564c6-122">**Plik definicji usługi** — definiuje ustawienia środowiska uruchomieniowego hello aplikacji, w tym, jakie role są wymagane, punktów końcowych i rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="564c6-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="564c6-123">**Plik konfiguracji usługi** — konfiguruje liczbę wystąpień roli są uruchamiane i hello wartości hello ustawienia zdefiniowane dla roli.</span><span class="sxs-lookup"><span data-stu-id="564c6-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="564c6-124">Aby uzyskać więcej informacji o tych plikach, zobacz [konfigurowania ról hello na potrzeby usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="564c6-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="564c6-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="564c6-125">Next steps</span></span>
- [<span data-ttu-id="564c6-126">Zarządzanie rolami w projekty usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="564c6-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
