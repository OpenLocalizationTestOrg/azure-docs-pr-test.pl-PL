---
title: "aaaAzure Functions — Omówienie środowiska uruchomieniowego | Dokumentacja firmy Microsoft"
description: "Omówienie hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej"
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
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="6a104-103">Azure Functions — Omówienie środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="6a104-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="6a104-104">Hello środowisko uruchomieniowe Functions Azure udostępnia nową metodę możesz tootake zaletą hello prostotę i elastyczność hello Azure Functions programowania modelu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6a104-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="6a104-105">Oparty na powitania sam Otwórz katalogi główne źródła, zgodnie z usługi Azure Functions, środowisko uruchomieniowe Functions Azure jest niemal identyczne programowanie występują jako usługa w chmurze hello tooprovide wdrożonego na lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6a104-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Portal w wersji zapoznawczej usługi Azure Functions środowiska wykonawczego][1]

<span data-ttu-id="6a104-107">Hello Azure środowisko uruchomieniowe Functions umożliwia dla Ciebie tooexperience usługi Azure Functions przed zatwierdzeniem toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="6a104-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="6a104-108">W ten sposób zasobów kodu hello tworzonego można podejmowana z chmurą toohello podczas migracji.</span><span class="sxs-lookup"><span data-stu-id="6a104-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="6a104-109">środowisko uruchomieniowe Hello otwiera również nowe opcje, takie jak przy użyciu mocy obliczeniowej zapasowe hello procesów partii toorun komputerami lokalnymi noc.</span><span class="sxs-lookup"><span data-stu-id="6a104-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="6a104-110">Można też używać urządzeń w Twojej organizacji tooconditionally wysyłania tooother systemów danych, zarówno lokalnie, jak i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="6a104-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="6a104-111">Witaj środowisko uruchomieniowe Functions Azure składa się z dwóch części:</span><span class="sxs-lookup"><span data-stu-id="6a104-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="6a104-112">Rola zarządzania Azure Functions środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="6a104-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="6a104-113">Azure Functions roli procesu roboczego środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="6a104-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="6a104-114">Rola zarządzania Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6a104-114">Azure Functions Management Role</span></span>

<span data-ttu-id="6a104-115">Hello Azure funkcje zarządzania roli zawiera hosta do zarządzania hello funkcji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6a104-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="6a104-116">Ta rola wykonuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="6a104-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="6a104-117">Hosting hello funkcje portalu zarządzania Azure, czyli hello hello jednego widoczne w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a104-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6a104-118">Pozwala to utworzyć funkcji w hello sam sposób jak w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6a104-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="6a104-119">Dystrybucja funkcje na wiele funkcji pracowników.</span><span class="sxs-lookup"><span data-stu-id="6a104-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="6a104-120">Udostępnianie publikowania punktu końcowego, dzięki czemu można opublikować bezpośrednio z funkcji z programu Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a104-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="6a104-121">Środowisko Azure Functions roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="6a104-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="6a104-122">Role procesów roboczych funkcji Azure Hello są wdrażane w kontenerach systemu Windows i jest to, gdzie wykonuje kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="6a104-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="6a104-123">Można wdrożyć wiele ról procesów roboczych w całej organizacji i mocy obliczeniowej zapasowych za pomocą klucza sposób, w którym można wprowadzić klientów.</span><span class="sxs-lookup"><span data-stu-id="6a104-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="6a104-124">Minimalne wymagania</span><span class="sxs-lookup"><span data-stu-id="6a104-124">Minimum Requirements</span></span>

<span data-ttu-id="6a104-125">tooget wprowadzenie hello Azure środowisko uruchomieniowe Functions musi mieć maszyny z **systemu Windows Server 2016 lub Windows 10 twórców Update** z tooa dostępu **programu SQL Server** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="6a104-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a104-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a104-126">Next Steps</span></span>

<span data-ttu-id="6a104-127">Zainstaluj hello [środowisko uruchomieniowe Functions Azure w wersji zapoznawczej](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="6a104-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
