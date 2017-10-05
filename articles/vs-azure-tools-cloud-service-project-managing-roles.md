---
title: "Zarządzanie rolami w usług w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie dodawania i usuwania ról w usług w chmurze Azure z programem Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="abe7d-103">Zarządzanie rolami w usług w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abe7d-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="abe7d-104">Po utworzeniu usługi w chmurze platformy Azure, można dodać do niego nowych ról lub usuwać istniejących ról.</span><span class="sxs-lookup"><span data-stu-id="abe7d-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="abe7d-105">Możesz także zaimportować istniejący projekt i przekształcić ją do roli.</span><span class="sxs-lookup"><span data-stu-id="abe7d-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="abe7d-106">Można na przykład zaimportować aplikację sieci web platformy ASP.NET i wyznaczanie roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="abe7d-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="abe7d-107">Dodawanie roli do usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="abe7d-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="abe7d-108">Poniższe kroki prowadzące przez Dodawanie roli sieci web lub procesu roboczego do projektu usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe7d-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe7d-109">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe7d-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe7d-110">W **Eksploratora rozwiązań**, rozwiń węzeł projektu</span><span class="sxs-lookup"><span data-stu-id="abe7d-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="abe7d-111">Kliknij prawym przyciskiem myszy **ról** węzeł, aby wyświetlić menu kontekstowe.</span><span class="sxs-lookup"><span data-stu-id="abe7d-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="abe7d-112">Wybierz z menu kontekstowego **Dodaj**, następnie wybierz istniejącą rolę sieci web lub roli proces roboczy z bieżącego rozwiązania lub Utwórz projekt roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="abe7d-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="abe7d-113">Można również wybrać odpowiedni projekt, takich jak projekt aplikacji sieci web platformy ASP.NET i skojarzyć go z projektu roli.</span><span class="sxs-lookup"><span data-stu-id="abe7d-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Opcje menu, aby dodać rolę do projektu usługi w chmurze Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="abe7d-115">Usunięcie roli z usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="abe7d-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="abe7d-116">Poniższe kroki prowadzące przez usunięcie roli sieci web lub procesu roboczego z projektu usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe7d-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe7d-117">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe7d-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe7d-118">W **Eksploratora rozwiązań**, rozwiń węzeł projektu</span><span class="sxs-lookup"><span data-stu-id="abe7d-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="abe7d-119">Rozwiń węzeł **ról** węzła.</span><span class="sxs-lookup"><span data-stu-id="abe7d-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="abe7d-120">Kliknij prawym przyciskiem myszy węzeł, który chcesz usunąć, a z menu kontekstowego wybierz **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="abe7d-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![Opcje menu, aby dodać rolę do usługi w chmurze Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="abe7d-122">Ponowne Dodawanie roli do projektu usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="abe7d-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="abe7d-123">Jeśli usunąć rolę z projektu usługi w chmurze, ale później zdecyduje się Dodaj rolę projektu, tylko deklaracji roli i Podstawowe atrybuty, takie jak punkty końcowe i informacje diagnostyczne, zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="abe7d-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="abe7d-124">Nie dodatkowe zasoby lub odwołania zostały dodane do `ServiceDefinition.csdef` pliku lub `ServiceConfiguration.cscfg` pliku.</span><span class="sxs-lookup"><span data-stu-id="abe7d-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="abe7d-125">Jeśli chcesz dodać te informacje, należy ręcznie dodać do tych plików.</span><span class="sxs-lookup"><span data-stu-id="abe7d-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="abe7d-126">Na przykład można usunąć roli usługi sieci web, a później zdecydujesz się dodać tej roli do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="abe7d-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="abe7d-127">Jeśli to zrobisz, występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="abe7d-127">If you do this, an error occurs.</span></span> <span data-ttu-id="abe7d-128">Aby uniknąć tego błędu, należy dodać `<LocalResources>` pokazano w poniższych XML do elementu `ServiceDefinition.csdef` pliku.</span><span class="sxs-lookup"><span data-stu-id="abe7d-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="abe7d-129">Użyj nazwy roli usługi sieci web, który został dodany do projektu jako część atrybutu nazwy dla  **<LocalStorage>**  elementu.</span><span class="sxs-lookup"><span data-stu-id="abe7d-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="abe7d-130">W tym przykładzie nazwa roli usługi sieci web jest **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="abe7d-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="abe7d-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abe7d-131">Next steps</span></span>
- [<span data-ttu-id="abe7d-132">Konfigurowanie ról dla usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abe7d-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
