---
title: "Przegląd interfejsu API centra zdarzeń aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd informacji o dostępnych interfejsach API centra zdarzeń platformy Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="8ed97-103">Interfejsy API centra zdarzeń dostępne</span><span class="sxs-lookup"><span data-stu-id="8ed97-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="8ed97-104">Interfejsy API środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="8ed97-104">Runtime APIs</span></span>

<span data-ttu-id="8ed97-105">Witaj poniżej znajduje się opis wszystkich aktualnie dostępnych klientów środowiska uruchomieniowego usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8ed97-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="8ed97-106">Chociaż niektóre z tych bibliotek zawiera również funkcje zarządzania ograniczone, dostępne są także [biblioteki określonej](#management-apis) toomanagement operacji w wersji dedykowanej.</span><span class="sxs-lookup"><span data-stu-id="8ed97-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="8ed97-107">fokus core Hello te biblioteki jest toosend i odbieranie komunikatów z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8ed97-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="8ed97-108">Zobacz [dodatkowe informacje](#additional-information) więcej szczegółów na powitania bieżący stan wszystkich bibliotek środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="8ed97-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="8ed97-109">Język/Platform</span><span class="sxs-lookup"><span data-stu-id="8ed97-109">Language/Platform</span></span> | <span data-ttu-id="8ed97-110">Pakiet klienta</span><span class="sxs-lookup"><span data-stu-id="8ed97-110">Client package</span></span> | <span data-ttu-id="8ed97-111">EventProcessorHost pakietu</span><span class="sxs-lookup"><span data-stu-id="8ed97-111">EventProcessorHost package</span></span> | <span data-ttu-id="8ed97-112">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="8ed97-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8ed97-113">.NET standard</span><span class="sxs-lookup"><span data-stu-id="8ed97-113">.NET Standard</span></span> | [<span data-ttu-id="8ed97-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="8ed97-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="8ed97-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="8ed97-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="8ed97-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="8ed97-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="8ed97-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="8ed97-117">.NET Framework</span></span> | [<span data-ttu-id="8ed97-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="8ed97-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="8ed97-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="8ed97-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="8ed97-120">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="8ed97-120">N/A</span></span> |
| <span data-ttu-id="8ed97-121">Java</span><span class="sxs-lookup"><span data-stu-id="8ed97-121">Java</span></span> | [<span data-ttu-id="8ed97-122">Maven</span><span class="sxs-lookup"><span data-stu-id="8ed97-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="8ed97-123">Maven</span><span class="sxs-lookup"><span data-stu-id="8ed97-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="8ed97-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="8ed97-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="8ed97-125">Węzeł</span><span class="sxs-lookup"><span data-stu-id="8ed97-125">Node</span></span> | [<span data-ttu-id="8ed97-126">NPM</span><span class="sxs-lookup"><span data-stu-id="8ed97-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="8ed97-127">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="8ed97-127">N/A</span></span> | [<span data-ttu-id="8ed97-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="8ed97-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="8ed97-129">C</span><span class="sxs-lookup"><span data-stu-id="8ed97-129">C</span></span> | <span data-ttu-id="8ed97-130">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="8ed97-130">N/A</span></span> | <span data-ttu-id="8ed97-131">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="8ed97-131">N/A</span></span> | [<span data-ttu-id="8ed97-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="8ed97-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="8ed97-133">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="8ed97-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="8ed97-134">.NET</span><span class="sxs-lookup"><span data-stu-id="8ed97-134">.NET</span></span>
<span data-ttu-id="8ed97-135">Witaj ekosystemu platformy .NET ma wiele środowisk uruchomieniowych, więc istnieje wiele bibliotek .NET dla usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8ed97-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="8ed97-136">Biblioteka .NET Standard Hello mogą być uruchamiane przy użyciu platformy .NET Core lub hello .NET Framework podczas hello Biblioteka programu .NET Framework może być uruchamiany tylko w środowisku .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8ed97-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="8ed97-137">Aby uzyskać więcej informacji dotyczących platformy .NET Framework, zobacz [framework w wersji](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="8ed97-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="8ed97-138">Węzeł</span><span class="sxs-lookup"><span data-stu-id="8ed97-138">Node</span></span>

<span data-ttu-id="8ed97-139">biblioteka języka Node.js Hello jest obecnie w wersji zapoznawczej i są obsługiwane jako projekt po stronie przez pracowników firmy Microsoft i zewnętrznych współpracowników.</span><span class="sxs-lookup"><span data-stu-id="8ed97-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="8ed97-140">Wszystkie udziały wraz z kodem źródłowym Zapraszamy i zostanie zweryfikowana.</span><span class="sxs-lookup"><span data-stu-id="8ed97-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="8ed97-141">Interfejsy API Management</span><span class="sxs-lookup"><span data-stu-id="8ed97-141">Management APIs</span></span>

<span data-ttu-id="8ed97-142">Hello poniżej znajduje się lista wszystkich obecnie zarządzania określone biblioteki.</span><span class="sxs-lookup"><span data-stu-id="8ed97-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="8ed97-143">Żadna z tych bibliotek zawierać operacje środowiska uruchomieniowego i są hello wyłącznie w celu zarządzania jednostek usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8ed97-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="8ed97-144">Język/Platform</span><span class="sxs-lookup"><span data-stu-id="8ed97-144">Language/Platform</span></span> | <span data-ttu-id="8ed97-145">Pakiet zarządzania</span><span class="sxs-lookup"><span data-stu-id="8ed97-145">Management package</span></span> | <span data-ttu-id="8ed97-146">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="8ed97-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8ed97-147">.NET standard</span><span class="sxs-lookup"><span data-stu-id="8ed97-147">.NET Standard</span></span> | [<span data-ttu-id="8ed97-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="8ed97-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="8ed97-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="8ed97-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="8ed97-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ed97-150">Next steps</span></span>
<span data-ttu-id="8ed97-151">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="8ed97-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="8ed97-152">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8ed97-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="8ed97-153">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8ed97-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8ed97-154">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="8ed97-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)