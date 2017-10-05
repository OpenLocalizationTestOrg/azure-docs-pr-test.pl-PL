---
title: "Azure Functions — Omówienie środowiska uruchomieniowego | Dokumentacja firmy Microsoft"
description: "Omówienie podglądu środowiska uruchomieniowego usługę Azure Functions"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="0ec74-103">Azure Functions — Omówienie środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="0ec74-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="0ec74-104">Środowisko uruchomieniowe Functions Azure udostępnia nową metodę umożliwiające wykorzystują łatwość i elastyczność funkcji Azure programowania modelu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0ec74-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="0ec74-105">Oparty na tej samej korzenie typu open source jako usługi Azure Functions, środowisko uruchomieniowe Functions Azure jest wdrożony lokalnymi zapewnia środowisko rozwoju niemal identyczne jako usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0ec74-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Portal w wersji zapoznawczej usługi Azure Functions środowiska wykonawczego][1]

<span data-ttu-id="0ec74-107">Środowisko uruchomieniowe Functions Azure udostępnia sposób środowisko Azure Functions przed zatwierdzeniem do chmury.</span><span class="sxs-lookup"><span data-stu-id="0ec74-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="0ec74-108">W ten sposób zasobów kodu, które tworzysz można podejmowana z Tobą w chmurze podczas migracji.</span><span class="sxs-lookup"><span data-stu-id="0ec74-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="0ec74-109">Środowisko uruchomieniowe otwiera również nowe opcje, takie jak przy użyciu mocy obliczeniowej zapasowe komputerów lokalnych do uruchamiania procesów partii noc.</span><span class="sxs-lookup"><span data-stu-id="0ec74-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="0ec74-110">Można też używać urządzeń w organizacji warunkowo wysyłać danych do innych systemów, zarówno lokalnie, jak i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0ec74-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="0ec74-111">Środowisko uruchomieniowe Functions Azure składa się z dwóch części:</span><span class="sxs-lookup"><span data-stu-id="0ec74-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="0ec74-112">Rola zarządzania Azure Functions środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="0ec74-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="0ec74-113">Azure Functions roli procesu roboczego środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="0ec74-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="0ec74-114">Rola zarządzania Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0ec74-114">Azure Functions Management Role</span></span>

<span data-ttu-id="0ec74-115">Rola zarządzania funkcji Azure udostępnia hosta w celu zarządzania lokalnym funkcje.</span><span class="sxs-lookup"><span data-stu-id="0ec74-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="0ec74-116">Ta rola wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="0ec74-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="0ec74-117">Hosting w portalu zarządzania Azure funkcji, która jest taka sama jak widać w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ec74-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0ec74-118">Dzięki temu można utworzyć funkcji w taki sam sposób jak w przypadku w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec74-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="0ec74-119">Dystrybucja funkcje na wiele funkcji pracowników.</span><span class="sxs-lookup"><span data-stu-id="0ec74-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="0ec74-120">Udostępnianie publikowania punktu końcowego, dzięki czemu można opublikować bezpośrednio z funkcji z programu Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ec74-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="0ec74-121">Środowisko Azure Functions roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="0ec74-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="0ec74-122">Role procesów roboczych funkcji Azure są wdrażane w kontenerach systemu Windows i jest to, gdzie wykonuje kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="0ec74-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="0ec74-123">Można wdrożyć wiele ról procesów roboczych w całej organizacji i mocy obliczeniowej zapasowych za pomocą klucza sposób, w którym można wprowadzić klientów.</span><span class="sxs-lookup"><span data-stu-id="0ec74-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="0ec74-124">Minimalne wymagania</span><span class="sxs-lookup"><span data-stu-id="0ec74-124">Minimum Requirements</span></span>

<span data-ttu-id="0ec74-125">Aby rozpocząć pracę ze środowiskiem uruchomieniowym funkcji Azure musi mieć maszyny z **systemu Windows Server 2016 lub Windows 10 twórców Update** z dostępem do **programu SQL Server** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="0ec74-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ec74-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ec74-126">Next Steps</span></span>

<span data-ttu-id="0ec74-127">Zainstaluj [środowisko uruchomieniowe Functions Azure w wersji zapoznawczej](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="0ec74-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
