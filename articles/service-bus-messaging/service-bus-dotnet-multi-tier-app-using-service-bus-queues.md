---
title: "aaa.NET wielowarstwową aplikację przy użyciu usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Samouczek platformy .NET, która pomaga utworzyć aplikację wielowarstwową na platformie Azure, która używa toocommunicate kolejek usługi Service Bus między warstwami."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="d00f8-103">Aplikacja wielowarstwowa platformy .NET używająca kolejek usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="d00f8-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="d00f8-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d00f8-104">Introduction</span></span>
<span data-ttu-id="d00f8-105">Tworzenie dla Microsoft Azure jest łatwy w użyciu programu Visual Studio i hello wolne zestawu Azure SDK dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="d00f8-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="d00f8-106">W tym samouczku przedstawiono hello kroki toocreate aplikacji, która używa wielu zasobów platformy Azure działa w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d00f8-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="d00f8-107">Dowiesz się hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d00f8-107">You will learn hello following:</span></span>

* <span data-ttu-id="d00f8-108">Jak tooenable komputera dla rozwoju platformy Azure za pomocą jednej pobrać i zainstalować.</span><span class="sxs-lookup"><span data-stu-id="d00f8-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="d00f8-109">Jak toouse toodevelop programu Visual Studio dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d00f8-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="d00f8-110">Jak toocreate wielowarstwową aplikację na platformie Azure przy użyciu ról sieci web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="d00f8-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="d00f8-111">W jaki sposób toocommunicate między warstwami przy użyciu kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="d00f8-112">W tym samouczku możesz utworzyć i uruchomić aplikację wielowarstwową hello Azure w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d00f8-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="d00f8-113">Fronton Hello jest roli sieci web platformy ASP.NET MVC i hello zaplecze rolę procesu roboczego, który korzysta z kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="d00f8-114">Możesz utworzyć hello samą aplikację wielowarstwową z frontonu hello jako projekt sieci web, który jest wdrożony tooan witrynie systemu Azure zamiast usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d00f8-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="d00f8-115">Możesz również wypróbować hello [.NET na lokalnej/w chmurze hybrydowej aplikacji](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="d00f8-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="d00f8-116">Witaj Poniższy zrzut ekranu przedstawia aplikacji hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="d00f8-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="d00f8-117">Omówienie scenariusza: komunikacja między rolami</span><span class="sxs-lookup"><span data-stu-id="d00f8-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="d00f8-118">toosubmit zamówienie do przetworzenia hello frontonu składnik interfejsu użytkownika w roli sieć web hello musi współdziałać z logiką warstwy środkowej hello uruchomionej w roli procesu roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="d00f8-119">W tym przykładzie użyto komunikatów usługi Service Bus hello komunikacji między warstwami hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="d00f8-120">Przy użyciu usługi Service Bus wysyłanie komunikatów między hello sieci web i warstwą środkową oddziela dwa składniki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="d00f8-121">Z kolei hello toodirect wiadomości (czyli TCP lub HTTP), warstwa sieci web nie łączy z warstwy środkowej toohello bezpośrednio; Zamiast tego wypycha jednostki pracy jako komunikaty do usługi Service Bus, która w niezawodny sposób je przechowuje do momentu hello Środkowa warstwa będzie gotowa tooconsume i przetwarzanie ich.</span><span class="sxs-lookup"><span data-stu-id="d00f8-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="d00f8-122">Usługa Service Bus zapewnia dwie jednostki toosupport obsługiwanych przez brokera komunikatów: kolejki i tematy.</span><span class="sxs-lookup"><span data-stu-id="d00f8-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="d00f8-123">W przypadku kolejek każdy komunikat wysłane toohello kolejki jest używany przez jednego odbiorcę.</span><span class="sxs-lookup"><span data-stu-id="d00f8-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="d00f8-124">Tematy obsługują wzorzec publikowania/subskrypcji hello w którym każdy opublikowany komunikat staje się dostępne tooa subskrypcji zarejestrowanej hello tematu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="d00f8-125">Każda subskrypcja logicznie zachowuje własną kolejkę komunikatów.</span><span class="sxs-lookup"><span data-stu-id="d00f8-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="d00f8-126">Subskrypcje można również skonfigurować przy użyciu reguł filtrowania, ograniczających hello zestaw komunikatów przesyłany do toothose kolejki subskrypcji hello pasujące hello filtru.</span><span class="sxs-lookup"><span data-stu-id="d00f8-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="d00f8-127">Witaj poniższym przykładzie użyto kolejek usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="d00f8-128">Ten mechanizm komunikacji ma kilka zalet w stosunku do komunikatów bezpośrednich:</span><span class="sxs-lookup"><span data-stu-id="d00f8-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="d00f8-129">**Rozdzielenie czasowe.**</span><span class="sxs-lookup"><span data-stu-id="d00f8-129">**Temporal decoupling.**</span></span> <span data-ttu-id="d00f8-130">Z hello asynchroniczny wzorzec przesyłania komunikatów, producenci i konsumenci nie muszą być online na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="d00f8-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="d00f8-131">Usługa Service Bus niezawodny sposób przechowuje komunikaty do momentu hello odbierająca jest gotowa do ich odebrania.</span><span class="sxs-lookup"><span data-stu-id="d00f8-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="d00f8-132">Dzięki temu składniki hello toobe aplikacji hello rozproszonych rozłączone zarówno dobrowolnie, na przykład w celu przeprowadzenia konserwacji lub powodu tooa awarii składników, bez wywierania wpływu na system jako całość.</span><span class="sxs-lookup"><span data-stu-id="d00f8-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="d00f8-133">Ponadto korzystanie z aplikacji hello może być konieczne toocome online pewnych porach dnia hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="d00f8-134">**Wyrównywanie obciążenia.**</span><span class="sxs-lookup"><span data-stu-id="d00f8-134">**Load leveling.**</span></span> <span data-ttu-id="d00f8-135">W wielu aplikacjach obciążenie systemu różni się w czasie, gdy czas przetwarzania hello wymagany dla każdej jednostki pracy jest zwykle stały.</span><span class="sxs-lookup"><span data-stu-id="d00f8-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="d00f8-136">Pośredniczenie producentami a konsumentami komunikatów z kolejki oznacza, że udostępniane tego hello korzystanie z aplikacji (proces roboczy hello) tylko potrzeb toobe tooaccommodate średni obciążenia, a nie obciążeniem szczytowym.</span><span class="sxs-lookup"><span data-stu-id="d00f8-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="d00f8-137">głębokość kolejki hello Hello rośnie i zmniejsza się w zależności od zmian obciążenia przychodzącego hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="d00f8-138">To jest zapisywany bezpośrednio oszczędność pieniędzy hello ilość obciążenia aplikacji hello wymagane tooservice infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="d00f8-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="d00f8-139">**Równoważenie obciążenia.**</span><span class="sxs-lookup"><span data-stu-id="d00f8-139">**Load balancing.**</span></span> <span data-ttu-id="d00f8-140">W miarę wzrostu obciążenia więcej procesów roboczych można dodać tooread z hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="d00f8-141">Każdy komunikat jest przetwarzany przez tylko jeden z procesów roboczych hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="d00f8-142">Ponadto to Równoważenie obciążenia oparte na ściąganiu umożliwia optymalnie wykorzystać maszyny procesów roboczych hello nawet wtedy, gdy maszyny procesów roboczych różnią się pod względem mocy przetwarzania, ponieważ każda będzie ściągać komunikaty własnych maksymalną szybkością.</span><span class="sxs-lookup"><span data-stu-id="d00f8-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="d00f8-143">Ten wzorzec jest często nazywany hello *konkurujących konsumentów* wzorca.</span><span class="sxs-lookup"><span data-stu-id="d00f8-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="d00f8-144">Hello w następujących sekcjach omówiono w nim hello kodu, który implementuje tę architekturę.</span><span class="sxs-lookup"><span data-stu-id="d00f8-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="d00f8-145">Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="d00f8-145">Set up hello development environment</span></span>
<span data-ttu-id="d00f8-146">Przed rozpoczęciem tworzenia aplikacji platformy Azure Pobierz narzędzia hello i konfigurowanie środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="d00f8-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="d00f8-147">Zainstaluj hello Azure SDK dla platformy .NET z hello SDK [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d00f8-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d00f8-148">W hello **.NET** kolumny, kliknij wersję hello [programu Visual Studio](http://www.visualstudio.com) używasz.</span><span class="sxs-lookup"><span data-stu-id="d00f8-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="d00f8-149">Witaj czynnościach w ramach tego samouczka użyj programu Visual Studio 2015, ale współpracują oni również z programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d00f8-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="d00f8-150">Gdy monit toorun lub zapisać hello Instalatora, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="d00f8-151">W hello **Instalatora platformy sieci Web**, kliknij przycisk **zainstalować** i kontynuować hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="d00f8-152">Po zakończeniu instalacji hello będzie mieć wszystko niezbędne toostart toodevelop hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="d00f8-153">Hello SDK zawiera narzędzia, które pozwalają w łatwy sposób tworzyć aplikacje platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d00f8-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="d00f8-154">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="d00f8-154">Create a namespace</span></span>
<span data-ttu-id="d00f8-155">Witaj, następnym krokiem jest toocreate przestrzeni nazw usługi i uzyskiwanie klucza dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d00f8-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="d00f8-156">Przestrzeń nazw wyznacza granice każdej aplikacji uwidacznianej za pośrednictwem usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="d00f8-157">Klucz sygnatury dostępu Współdzielonego jest generowany przez system powitania po utworzeniu przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d00f8-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="d00f8-158">Hello kombinacja przestrzeni nazw i klucza sygnatury dostępu Współdzielonego zapewnia poświadczenia hello usługi Service Bus tooauthenticate dostępu tooan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="d00f8-159">Tworzenie roli sieci Web</span><span class="sxs-lookup"><span data-stu-id="d00f8-159">Create a web role</span></span>
<span data-ttu-id="d00f8-160">W tej sekcji zostanie utworzony hello frontonu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="d00f8-161">Najpierw należy utworzyć hello stron, które będą wyświetlane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="d00f8-162">Następnie dodaj kod, który przesyła kolejki usługi Service Bus tooa elementów i wyświetla informacje o stanie dotyczące hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="d00f8-163">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="d00f8-163">Create hello project</span></span>
1. <span data-ttu-id="d00f8-164">Korzystając z uprawnień administratora, uruchom program Visual Studio: kliknij prawym przyciskiem myszy hello **programu Visual Studio** ikonę programu, a następnie kliknij przycisk **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="d00f8-165">Witaj emulatora obliczeń platformy Azure, omówiony w dalszej części tego artykułu, wymaga uruchomienia programu Visual Studio z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="d00f8-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="d00f8-166">W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="d00f8-167">W pozycji **Zainstalowane szablony** w obszarze **Visual C#** kliknij pozycję **Chmura**, a następnie kliknij pozycję **Usługa w chmurze Azure**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="d00f8-168">Nazwa projektu hello **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="d00f8-169">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="d00f8-170">Wśród ról platformy **.NET Framework 4.5** kliknij dwukrotnie pozycję **Role sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="d00f8-171">Umieść kursor nad **WebRole1** w obszarze **rozwiązania usługi w chmurze Azure**, kliknij ikonę ołówka hello i Zmień nazwę roli sieci web hello zbyt**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="d00f8-172">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-172">Then click **OK**.</span></span> <span data-ttu-id="d00f8-173">(Upewnij się, że wpisana nazwa to „Frontend”, pisana przez małe „e”, a nie „FrontEnd”.)</span><span class="sxs-lookup"><span data-stu-id="d00f8-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="d00f8-174">Z hello **nowy projekt ASP.NET** okno dialogowe, w hello **wybierz szablon** kliknij **MVC**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="d00f8-175">Nadal w hello **nowy projekt ASP.NET** okna dialogowego kliknij hello **Zmień uwierzytelnianie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d00f8-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="d00f8-176">W hello **Zmień uwierzytelnianie** okno dialogowe, kliknij przycisk **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="d00f8-177">W tym samouczku wdrożysz aplikację, która nie wymaga logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d00f8-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="d00f8-178">Po powrocie do hello **nowy projekt ASP.NET** okno dialogowe, kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="d00f8-179">W **Eksploratora rozwiązań**, w hello **FrontendWebRole** projektu, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="d00f8-180">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="d00f8-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="d00f8-181">Wybierz hello **WindowsAzure.ServiceBus** pakiet, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="d00f8-182">Należy zauważyć, że ten hello wymagane zestawy klientów są teraz przywoływane i dodano kilka nowych plików kodu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="d00f8-183">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Modele** i kliknij pozycję **Dodaj**, następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="d00f8-184">W hello **nazwa** okno, nazwa typu hello **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="d00f8-185">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="d00f8-186">Pisanie kodu powitania dla roli sieci web</span><span class="sxs-lookup"><span data-stu-id="d00f8-186">Write hello code for your web role</span></span>
<span data-ttu-id="d00f8-187">W tej sekcji utworzysz hello różne strony, które będą wyświetlane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="d00f8-188">W pliku OnlineOrder.cs hello w programie Visual Studio Zastąp istniejącą definicję przestrzeni nazw hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d00f8-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="d00f8-189">W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="d00f8-190">Dodaj następujące hello **przy użyciu** instrukcji u góry hello hello pliku przestrzenie nazw hello tooinclude modelu utworzony, a także usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="d00f8-191">Również w pliku HomeController.cs hello w programie Visual Studio, Zastąp istniejącą definicję przestrzeni nazw z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="d00f8-192">Ten kod zawiera metody obsługi przesyłania hello elementów toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="d00f8-193">Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tootest hello dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="d00f8-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="d00f8-194">Teraz Utwórz widok hello hello `Submit()` została utworzona wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d00f8-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="d00f8-195">Kliknij prawym przyciskiem myszy w obrębie hello `Submit()` — metoda (przeciążenia hello `Submit()` który nie przyjmuje żadnych parametrów), a następnie wybierz pozycję **Dodaj widok**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="d00f8-196">Okno dialogowe tworzenia widoku hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="d00f8-197">W hello **szablonu** wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="d00f8-198">W hello **klasa modelu** kliknij hello **OnlineOrder** klasy.</span><span class="sxs-lookup"><span data-stu-id="d00f8-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="d00f8-199">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-199">Click **Add**.</span></span>
8. <span data-ttu-id="d00f8-200">Teraz Zmień nazwę hello wyświetlany w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d00f8-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="d00f8-201">W **Eksploratora rozwiązań**, kliknij dwukrotnie **Views\Shared\\_Layout.cshtml** pliku tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="d00f8-202">Zamień wszystkie wystąpienia hasła **My ASP.NET Application** na hasło **LITWARE'S Products**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="d00f8-203">Usuń hello **Home**, **o**, i **skontaktuj się z** łącza.</span><span class="sxs-lookup"><span data-stu-id="d00f8-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="d00f8-204">Usuń hello wyróżniony kod:</span><span class="sxs-lookup"><span data-stu-id="d00f8-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="d00f8-205">Na koniec zmodyfikuj hello przesłanie strony tooinclude niektóre informacje na temat hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="d00f8-206">W **Eksploratora rozwiązań**, kliknij dwukrotnie **Views\Home\Submit.cshtml** pliku tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="d00f8-207">Dodaj hello następującego wiersza po `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="d00f8-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="d00f8-208">Na razie hello `ViewBag.MessageCount` jest pusta.</span><span class="sxs-lookup"><span data-stu-id="d00f8-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="d00f8-209">Wypełnisz ją później.</span><span class="sxs-lookup"><span data-stu-id="d00f8-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="d00f8-210">Twój interfejs użytkownika został zaimplementowany.</span><span class="sxs-lookup"><span data-stu-id="d00f8-210">You now have implemented your UI.</span></span> <span data-ttu-id="d00f8-211">Możesz nacisnąć przycisk **F5** toorun aplikacji i upewnij się, że jej wygląd zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="d00f8-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="d00f8-212">Pisanie kodu hello składania kolejki usługi Service Bus tooa elementów</span><span class="sxs-lookup"><span data-stu-id="d00f8-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="d00f8-213">Teraz Dodaj kod przesyłający elementy tooa kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="d00f8-214">Najpierw utwórz klasę, która zawiera informacje o połączeniu kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d00f8-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="d00f8-215">Następnie zainicjuj połączenie z pliku Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="d00f8-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="d00f8-216">Koniec zaktualizuj kod przesyłania hello, utworzony wcześniej w kolejki usługi Service Bus tooa HomeController.cs tooactually przesyłania elementów.</span><span class="sxs-lookup"><span data-stu-id="d00f8-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="d00f8-217">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **FrontendWebRole** (kliknij prawym przyciskiem myszy projekt hello, nie hello roli).</span><span class="sxs-lookup"><span data-stu-id="d00f8-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="d00f8-218">Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="d00f8-219">Nazwa klasy hello **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="d00f8-220">Kliknij przycisk **Dodaj** toocreate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="d00f8-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="d00f8-221">Teraz Dodaj kod, który hermetyzuje informacje o połączeniu hello i inicjuje kolejki usługi Service Bus tooa połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="d00f8-222">Zastąp całą zawartość pliku QueueConnector.cs hello hello następującego kodu i wprowadź wartości w polach `your Service Bus namespace` (przestrzeni nazw) i `yourKey`, która jest hello **klucz podstawowy** uzyskanym wcześniej z hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d00f8-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="d00f8-223">Teraz upewnij się, że wywoływanie metody **Initialize** działa.</span><span class="sxs-lookup"><span data-stu-id="d00f8-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="d00f8-224">W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="d00f8-225">Dodaj następujące wiersz kodu na końcu hello hello hello **Application_Start** metody.</span><span class="sxs-lookup"><span data-stu-id="d00f8-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="d00f8-226">Na koniec zaktualizuj kod sieci web hello został utworzony wcześniej, aby przesłać elementy toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="d00f8-227">W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="d00f8-228">Aktualizacja hello `Submit()` — metoda (hello przeciążenie, które nie przyjmuje żadnych parametrów) w następujący sposób wiadomość hello tooget liczba hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="d00f8-229">Aktualizacja hello `Submit(OnlineOrder order)` — metoda (hello przeciążenie, które przyjmuje jeden parametr) w następujący sposób toosubmit kolejność informacji toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="d00f8-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="d00f8-230">Teraz możesz uruchomić ponownie aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-230">You can now run hello application again.</span></span> <span data-ttu-id="d00f8-231">Zwiększa liczbę wiadomości powitania zawsze przesyłania zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d00f8-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="d00f8-232">Tworzenie roli procesu roboczego hello</span><span class="sxs-lookup"><span data-stu-id="d00f8-232">Create hello worker role</span></span>
<span data-ttu-id="d00f8-233">Teraz utworzysz hello roli procesu roboczego, który przetwarza zgłoszenia zamówień hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="d00f8-234">W tym przykładzie użyto hello **roli proces roboczy z kolejką usługi Service Bus** szablon projektu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d00f8-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="d00f8-235">Witaj wymagane poświadczenia zostały już uzyskane z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="d00f8-236">Upewnij się, że nawiązano połączenie programu Visual Studio tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d00f8-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="d00f8-237">W programie Visual Studio w **Eksploratora rozwiązań** kliknij prawym przyciskiem myszy **ról** folder hello **MultiTierApp** projektu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="d00f8-238">Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Nowy projekt roli procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="d00f8-239">Witaj **Dodawanie nowego projektu roli** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d00f8-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="d00f8-240">W hello **Dodawanie nowego projektu roli** okno dialogowe, kliknij przycisk **roli proces roboczy z kolejką usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="d00f8-241">W hello **nazwa** okno, nazwa projektu hello **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="d00f8-242">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-242">Then click **Add**.</span></span>
6. <span data-ttu-id="d00f8-243">Skopiuj parametry połączenia hello uzyskany w kroku 9 Schowka toohello sekcji "Tworzenie przestrzeni nazw usługi Service Bus" hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="d00f8-244">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **OrderProcessingRole** został utworzony w kroku 5 (Upewnij się, że prawym przyciskiem myszy **OrderProcessingRole** w obszarze **Ról**, a nie hello klasy).</span><span class="sxs-lookup"><span data-stu-id="d00f8-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="d00f8-245">Następnie kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="d00f8-246">Na powitania **ustawienia** kartę hello **właściwości** okno dialogowe, kliknij wewnątrz hello **wartość** pole **Microsoft.ServiceBus.ConnectionString**, a następnie wklej skopiowany w kroku 6 wartość punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="d00f8-247">Utwórz **OnlineOrder** klasy toorepresent hello zamówień ich przetwarzania z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="d00f8-248">Możesz ponownie użyć klasy, która została już utworzona.</span><span class="sxs-lookup"><span data-stu-id="d00f8-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="d00f8-249">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **OrderProcessingRole** klasy (ikonę klasy powitania kliknij prawym przyciskiem myszy, nie hello roli).</span><span class="sxs-lookup"><span data-stu-id="d00f8-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="d00f8-250">Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="d00f8-251">Przeglądaj podfolderu toohello **FrontendWebRole\Models**, a następnie kliknij dwukrotnie **OnlineOrder.cs** tooadd on toothis projektu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="d00f8-252">W **WorkerRole.cs**, zmień wartość hello hello **QueueName** zmienną z `"ProcessingQueue"` zbyt`"OrdersQueue"` pokazane na powitania następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="d00f8-253">Dodaj następujące hello za pomocą instrukcji u góry pliku WorkerRole.cs hello hello.</span><span class="sxs-lookup"><span data-stu-id="d00f8-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="d00f8-254">W hello `Run()` funkcja wewnątrz hello `OnMessage()` wywołać, Zastąp zawartość hello hello `try` klauzuli z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="d00f8-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="d00f8-255">Aplikacja hello została ukończona.</span><span class="sxs-lookup"><span data-stu-id="d00f8-255">You have completed hello application.</span></span> <span data-ttu-id="d00f8-256">Można przetestować pełnej aplikacji hello, klikając prawym przyciskiem myszy projekt MultiTierApp hello w Eksploratorze rozwiązań, wybierając **Ustaw jako projekt startowy**, a następnie naciśnij klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="d00f8-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="d00f8-257">Należy pamiętać, że liczba komunikatów nie zwiększa się, ponieważ hello roli procesu roboczego przetwarza elementy z kolejki hello i oznacza je jako ukończone.</span><span class="sxs-lookup"><span data-stu-id="d00f8-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="d00f8-258">Można zobaczyć wyniki śledzenia hello swojej roli procesu roboczego, wyświetlając hello interfejs użytkownika emulatora obliczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d00f8-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="d00f8-259">Aby to zrobić, prawym przyciskiem myszy ikonę emulatora hello w obszarze powiadomień paska zadań hello i wybierając **Pokaż interfejs użytkownika emulatora obliczeń**.</span><span class="sxs-lookup"><span data-stu-id="d00f8-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="d00f8-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d00f8-260">Next steps</span></span>
<span data-ttu-id="d00f8-261">toolearn więcej informacji na temat usługi Service Bus, zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="d00f8-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="d00f8-262">[Dokumentacja usługi Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="d00f8-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="d00f8-263">[Service Bus service page][sbacom] (Strona usługi Service Bus)</span><span class="sxs-lookup"><span data-stu-id="d00f8-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="d00f8-264">[Jak tooUse kolejek usługi Service Bus][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="d00f8-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="d00f8-265">toolearn więcej informacji na temat wielowarstwowych scenariuszy, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d00f8-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="d00f8-266">[Wielowarstwowa aplikacja platformy .NET korzystająca z tabel, kolejek i obiektów Blob magazynu][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="d00f8-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
