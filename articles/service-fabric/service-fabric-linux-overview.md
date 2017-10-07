---
title: "aaaAzure sieci szkieletowej usług w systemie Linux | Dokumentacja firmy Microsoft"
description: "Klastry usługi sieć szkieletowa obsługują systemu Linux i Java, co oznacza, że będziesz w stanie toodeploy i aplikacji sieci szkieletowej usług hosta napisany w języku Java i C# w systemie Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="3bf3c-103">Sieć szkieletowa usług w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="3bf3c-103">Service Fabric on Linux</span></span>
<span data-ttu-id="3bf3c-104">Podgląd Hello sieci szkieletowej usług w systemie Linux pozwala toobuild, wdrażania i zarządzania wysoce skalowalne, wysoko dostępne aplikacje w systemie Linux, tak jak w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="3bf3c-105">platformy Service Fabric Hello (Reliable Services i Reliable Actors) są dostępne w języku Java w systemie Linux w dodanie tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="3bf3c-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="3bf3c-106">Można również tworzyć [usługi pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md) z dowolnego języka lub struktury.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="3bf3c-107">Ponadto hello preview obsługuje również organizowanie kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="3bf3c-108">Kontenery docker można uruchamiać pliki wykonywalne gościa lub macierzysty usług sieci szkieletowej usług, korzystających z platformy Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="3bf3c-109">Sieć szkieletowa usług w systemie Linux jest koncepcyjnie równoważne tooService sieci szkieletowej w systemie Windows (z wyjątkiem charakterystyki systemu operacyjnego i obsługa języka programowania).</span><span class="sxs-lookup"><span data-stu-id="3bf3c-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="3bf3c-110">W związku z tym większość naszego [istniejąca dokumentacja](http://aka.ms/servicefabricdocs) ma zastosowanie w myśl należy zapoznać się z technologii hello.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="3bf3c-111">Obsługiwane systemy operacyjne i języki programowania</span><span class="sxs-lookup"><span data-stu-id="3bf3c-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="3bf3c-112">Hello ograniczone w wersji zapoznawczej obsługuje hello tworzenia rozwoju jednego pola Ponadto klastry klastrów maszyny toomulti na platformie Azure z systemem Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="3bf3c-113">obsługuje podglądu Hello hello Reliable Actors i hello usługi bezstanowej niezawodnej struktury w języku Java i C# w pliki wykonywalne tooguest dodanie i organizowanie kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="3bf3c-114">Niezawodne kolekcje nie są obsługiwane w systemie Linux jeszcze.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="3bf3c-115">Nie są obsługiwane tylko klastry wstrzymania albo - tylko jedno pole, jak i Azure Linux klastrach obejmujących wiele maszyn są obsługiwane w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="3bf3c-116">Obsługiwane narzędzi</span><span class="sxs-lookup"><span data-stu-id="3bf3c-116">Supported tooling</span></span>
<span data-ttu-id="3bf3c-117">Podgląd Hello obsługuje interakcji z hello klastra za pomocą interfejsu wiersza polecenia usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="3bf3c-118">Dla deweloperów języka Java Integracja z Eclipse i narzędzia Yeoman jest dostarczany z Eclipse obsługiwane w systemie Linux i OS x.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="3bf3c-119">Witaj integracji systemu OS x używa Maszynę wirtualną systemu Linux pod maską hello za pośrednictwem vagrant.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="3bf3c-120">C# deweloperom integracji z narzędzia Yeoman podano toogenerate szablonów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bf3c-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf3c-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bf3c-121">Next steps</span></span>

* <span data-ttu-id="3bf3c-122">Zapoznaj się z hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) i [niezawodne usługi](service-fabric-reliable-services-introduction.md) programowania struktur</span><span class="sxs-lookup"><span data-stu-id="3bf3c-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="3bf3c-123">Przygotowywanie środowiska projektowego w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="3bf3c-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="3bf3c-124">Przygotowywanie środowiska projektowego w systemie OSX</span><span class="sxs-lookup"><span data-stu-id="3bf3c-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="3bf3c-125">Tworzenie pierwszej aplikacji usługi sieci szkieletowej Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="3bf3c-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="3bf3c-126">Instalator usługi sieć szkieletowa ciągłej integracji i wdrażania z Wpięć i GitHub</span><span class="sxs-lookup"><span data-stu-id="3bf3c-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="3bf3c-127">Różnice w usłudze Service Fabric w systemie Windows i Linux</span><span class="sxs-lookup"><span data-stu-id="3bf3c-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
