---
title: "O usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak DevTest Labs może ułatwić do tworzenia, zarządzania i monitorowania maszyn wirtualnych platformy Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="55398-103">O usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="55398-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="55398-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="55398-104">Overview</span></span>
<span data-ttu-id="55398-105">Deweloperzy i testerzy chce się dowiedzieć, aby rozwiązać problem z opóźnieniami dotyczącymi tworzenia i zarządzania środowiskami, przechodząc do chmury.</span><span class="sxs-lookup"><span data-stu-id="55398-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="55398-106">Azure rozwiązuje problem opóźnienia środowiska i umożliwia samoobsługi w ramach nowej struktury wydajne kosztów.</span><span class="sxs-lookup"><span data-stu-id="55398-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="55398-107">Jednak deweloperów i testerów nadal muszą poświęcić wiele czasu Konfigurowanie środowiskami własnym obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="55398-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="55398-108">Inne osoby podejmujące decyzje są także wiedzą o tym, jak skorzystać z chmury, aby zmaksymalizować ich oszczędności bez dodawania zbyt dużo koszty procesu.</span><span class="sxs-lookup"><span data-stu-id="55398-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="55398-109">Azure DevTest Labs to usługa, która pomaga deweloperom i testerom szybko utworzyć środowiska na platformie Azure podczas zminimalizować odpady i kontrolować koszty.</span><span class="sxs-lookup"><span data-stu-id="55398-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="55398-110">Możesz przetestować najnowszą wersję aplikacji dzięki możliwości szybkiej aprowizacji środowisk systemów Windows i Linux przy użyciu szablonów i artefaktów z możliwością ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="55398-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="55398-111">Łatwo zintegrować z procesu wdrażania z DevTest Labs do udostępniania na żądanie środowiska.</span><span class="sxs-lookup"><span data-stu-id="55398-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="55398-112">Skalowanie w górę obciążenia testowania przez Inicjowanie obsługi wielu agentów testowych i utworzyć wstępnie przygotowany środowiska szkolenia i pokazy.</span><span class="sxs-lookup"><span data-stu-id="55398-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="55398-113">DevTest Labs zapewnia następujące korzyści podczas tworzenia, konfigurowania i zarządzania środowiska dewelopera i testowe w chmurze</span><span class="sxs-lookup"><span data-stu-id="55398-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="55398-114">Obaw samoobsługi</span><span class="sxs-lookup"><span data-stu-id="55398-114">Worry-free self-service</span></span>
<span data-ttu-id="55398-115">DevTest Labs ułatwia kontrolę kosztów, umożliwiając określenie zasad w laboratorium — takie jak liczba maszyn wirtualnych (VM) na użytkownika i liczbę maszyn wirtualnych dla laboratorium.</span><span class="sxs-lookup"><span data-stu-id="55398-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="55398-116">DevTest Labs umożliwia także tworzenie zasad, aby automatycznie zamknąć i uruchomić maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="55398-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="55398-117">Szybki dostęp do gotowe do testów</span><span class="sxs-lookup"><span data-stu-id="55398-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="55398-118">DevTest Labs umożliwia tworzenie środowisk wstępnie przygotowany z wszystko, czego zespołu musi uruchomić projektowania i testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55398-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="55398-119">Po prostu oświadczeń środowisk zainstalowanym ostatniego dobra Kompilacja aplikacji i uzyskać pracy od razu.</span><span class="sxs-lookup"><span data-stu-id="55398-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="55398-120">Możesz też użyć kontenery nawet szybsze i leaner środowisko tworzenia.</span><span class="sxs-lookup"><span data-stu-id="55398-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="55398-121">Utwórz raz, używaj wszędzie</span><span class="sxs-lookup"><span data-stu-id="55398-121">Create once, use everywhere</span></span>
<span data-ttu-id="55398-122">Przechwytywania i udostępniania szablonów środowiska i artefaktów w obrębie zespołu lub organizacji - all w kontroli źródła - tworzenie deweloperów i łatwe testowanie środowisk.</span><span class="sxs-lookup"><span data-stu-id="55398-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="55398-123">Integracja z istniejącym łańcuchem narzędzi</span><span class="sxs-lookup"><span data-stu-id="55398-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="55398-124">Korzystaj z wstępnie przygotowanych dodatków plug-in i interfejsie API, aby udostępnić środowiska i testowania bezpośrednio z własnych narzędzi preferowanych ciągłej integracji (CI), zintegrowane środowisko programistyczne (IDE) lub automatyczne potoku wersji.</span><span class="sxs-lookup"><span data-stu-id="55398-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="55398-125">Umożliwia także Nasze kompleksowe narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="55398-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="55398-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55398-126">Next steps</span></span>
[<span data-ttu-id="55398-127">DevTest Labs — pojęcia</span><span class="sxs-lookup"><span data-stu-id="55398-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

