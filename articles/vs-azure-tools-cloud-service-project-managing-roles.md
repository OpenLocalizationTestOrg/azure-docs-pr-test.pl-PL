---
title: "aaaManaging ról na platformie Azure cloud services z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd i usuwanie ról na platformie Azure cloud services z programem Visual Studio."
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
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="abe1e-103">Zarządzanie rolami w usług w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abe1e-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="abe1e-104">Po utworzeniu usługi w chmurze platformy Azure, można dodać nowe role tooit lub usuwać istniejących ról.</span><span class="sxs-lookup"><span data-stu-id="abe1e-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="abe1e-105">Można także zaimportować istniejący projekt i przekonwertować go tooa roli.</span><span class="sxs-lookup"><span data-stu-id="abe1e-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="abe1e-106">Można na przykład zaimportować aplikację sieci web platformy ASP.NET i wyznaczanie roli sieci web.</span><span class="sxs-lookup"><span data-stu-id="abe1e-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="abe1e-107">Dodawanie tooan roli usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="abe1e-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="abe1e-108">Hello następujące kroki prowadzące przez dodawanie sieci web lub procesu roboczego roli tooan Azure projektu usługi w chmurze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe1e-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe1e-109">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe1e-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe1e-110">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello</span><span class="sxs-lookup"><span data-stu-id="abe1e-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="abe1e-111">Kliknij prawym przyciskiem myszy hello **ról** menu kontekstowe hello toodisplay węzłów.</span><span class="sxs-lookup"><span data-stu-id="abe1e-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="abe1e-112">Wybierz z menu kontekstowego hello **Dodaj**, następnie wybierz istniejącą rolę sieci web lub roli proces roboczy z bieżącego rozwiązania hello lub Utwórz projekt roli sieci web lub procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="abe1e-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="abe1e-113">Można również wybrać odpowiedni projekt, takich jak projekt aplikacji sieci web platformy ASP.NET i skojarzyć go z projektu roli.</span><span class="sxs-lookup"><span data-stu-id="abe1e-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Menu Opcje tooadd projektu usługi w chmurze Azure tooan roli](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="abe1e-115">Usunięcie roli z usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="abe1e-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="abe1e-116">Witaj następujące kroki prowadzące przez usunięcie roli sieci web lub procesu roboczego z projektu usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe1e-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe1e-117">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abe1e-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="abe1e-118">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello</span><span class="sxs-lookup"><span data-stu-id="abe1e-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="abe1e-119">Rozwiń węzeł hello **ról** węzła.</span><span class="sxs-lookup"><span data-stu-id="abe1e-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="abe1e-120">Kliknij prawym przyciskiem myszy hello węzła tooremove, a następnie, wybierz z menu kontekstowego hello **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="abe1e-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Menu Opcje tooadd tooan roli usługi w chmurze Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="abe1e-122">Ponowne dodawanie projektu usługi w chmurze Azure tooan roli</span><span class="sxs-lookup"><span data-stu-id="abe1e-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="abe1e-123">Usuń rolę z projektu usługi w chmurze, ale później zdecyduje tooadd hello powrotem rolę toohello projektu, tylko hello roli deklaracji i Podstawowe atrybuty, takie jak punkty końcowe i informacje diagnostyczne, zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="abe1e-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="abe1e-124">Nie dodatkowe zasoby lub odwołania są dodawane toohello `ServiceDefinition.csdef` pliku lub toohello `ServiceConfiguration.cscfg` pliku.</span><span class="sxs-lookup"><span data-stu-id="abe1e-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="abe1e-125">Jeśli chcesz tooadd te informacje, należy toomanually go z powrotem dodać do tych plików.</span><span class="sxs-lookup"><span data-stu-id="abe1e-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="abe1e-126">Na przykład można usunąć roli usługi sieci web, a później zdecyduje tooadd kopii tej roli w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="abe1e-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="abe1e-127">Jeśli to zrobisz, występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="abe1e-127">If you do this, an error occurs.</span></span> <span data-ttu-id="abe1e-128">tooprevent ten błąd, masz tooadd hello `<LocalResources>` element pokazano powitania po XML z powrotem do hello `ServiceDefinition.csdef` pliku.</span><span class="sxs-lookup"><span data-stu-id="abe1e-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="abe1e-129">Użyj nazwy hello hello roli usługi sieci web, która dodane do projektu hello jako część atrybut nazwy hello hello  **<LocalStorage>**  elementu.</span><span class="sxs-lookup"><span data-stu-id="abe1e-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="abe1e-130">W tym przykładzie nazwa hello roli usługi sieci web hello jest **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="abe1e-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="abe1e-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abe1e-131">Next steps</span></span>
- [<span data-ttu-id="abe1e-132">Konfigurowanie ról powitania dla usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abe1e-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
