---
title: "Omówienie usługi Azure API centra zdarzeń | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="bde23-103">Interfejsy API centra zdarzeń dostępne</span><span class="sxs-lookup"><span data-stu-id="bde23-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="bde23-104">Interfejsy API środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="bde23-104">Runtime APIs</span></span>

<span data-ttu-id="bde23-105">Poniżej znajduje się opis wszystkich aktualnie dostępnych klientów środowiska uruchomieniowego usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bde23-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="bde23-106">Chociaż niektóre z tych bibliotek zawiera również funkcje zarządzania ograniczone, dostępne są także [biblioteki określonej](#management-apis) przeznaczone do obsługi operacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="bde23-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="bde23-107">Podstawowe tych bibliotek koncentruje się na wysyłanie i odbieranie komunikatów z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bde23-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="bde23-108">Zobacz [dodatkowe informacje](#additional-information) więcej szczegółów na bieżący stan wszystkich bibliotek środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="bde23-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="bde23-109">Język/Platform</span><span class="sxs-lookup"><span data-stu-id="bde23-109">Language/Platform</span></span> | <span data-ttu-id="bde23-110">Pakiet klienta</span><span class="sxs-lookup"><span data-stu-id="bde23-110">Client package</span></span> | <span data-ttu-id="bde23-111">EventProcessorHost pakietu</span><span class="sxs-lookup"><span data-stu-id="bde23-111">EventProcessorHost package</span></span> | <span data-ttu-id="bde23-112">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="bde23-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bde23-113">.NET standard</span><span class="sxs-lookup"><span data-stu-id="bde23-113">.NET Standard</span></span> | [<span data-ttu-id="bde23-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="bde23-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="bde23-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="bde23-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="bde23-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="bde23-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="bde23-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="bde23-117">.NET Framework</span></span> | [<span data-ttu-id="bde23-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="bde23-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="bde23-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="bde23-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="bde23-120">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="bde23-120">N/A</span></span> |
| <span data-ttu-id="bde23-121">Java</span><span class="sxs-lookup"><span data-stu-id="bde23-121">Java</span></span> | [<span data-ttu-id="bde23-122">Maven</span><span class="sxs-lookup"><span data-stu-id="bde23-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="bde23-123">Maven</span><span class="sxs-lookup"><span data-stu-id="bde23-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="bde23-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="bde23-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="bde23-125">Węzeł</span><span class="sxs-lookup"><span data-stu-id="bde23-125">Node</span></span> | [<span data-ttu-id="bde23-126">NPM</span><span class="sxs-lookup"><span data-stu-id="bde23-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="bde23-127">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="bde23-127">N/A</span></span> | [<span data-ttu-id="bde23-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="bde23-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="bde23-129">C</span><span class="sxs-lookup"><span data-stu-id="bde23-129">C</span></span> | <span data-ttu-id="bde23-130">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="bde23-130">N/A</span></span> | <span data-ttu-id="bde23-131">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="bde23-131">N/A</span></span> | [<span data-ttu-id="bde23-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="bde23-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="bde23-133">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="bde23-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="bde23-134">.NET</span><span class="sxs-lookup"><span data-stu-id="bde23-134">.NET</span></span>
<span data-ttu-id="bde23-135">Ekosystemu platformy .NET ma wiele środowisk uruchomieniowych, więc istnieje wiele bibliotek .NET dla usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bde23-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="bde23-136">Biblioteki standardowe .NET mogą być uruchamiane przy użyciu platformy .NET Core lub .NET Framework, gdy biblioteka programu .NET Framework może być uruchamiany tylko w środowisku .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="bde23-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="bde23-137">Aby uzyskać więcej informacji dotyczących platformy .NET Framework, zobacz [framework w wersji](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="bde23-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="bde23-138">Węzeł</span><span class="sxs-lookup"><span data-stu-id="bde23-138">Node</span></span>

<span data-ttu-id="bde23-139">Biblioteka języka Node.js jest obecnie w wersji zapoznawczej i są obsługiwane jako projekt po stronie przez pracowników firmy Microsoft i zewnętrznych współpracowników.</span><span class="sxs-lookup"><span data-stu-id="bde23-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="bde23-140">Wszystkie udziały wraz z kodem źródłowym Zapraszamy i zostanie zweryfikowana.</span><span class="sxs-lookup"><span data-stu-id="bde23-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="bde23-141">Interfejsy API Management</span><span class="sxs-lookup"><span data-stu-id="bde23-141">Management APIs</span></span>

<span data-ttu-id="bde23-142">Poniżej znajduje się lista wszystkich obecnie zarządzania określone biblioteki.</span><span class="sxs-lookup"><span data-stu-id="bde23-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="bde23-143">Żadna z tych bibliotek zawierają operacji środowiska uruchomieniowego i są wyłącznie w celu zarządzania jednostek usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bde23-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="bde23-144">Język/Platform</span><span class="sxs-lookup"><span data-stu-id="bde23-144">Language/Platform</span></span> | <span data-ttu-id="bde23-145">Pakiet zarządzania</span><span class="sxs-lookup"><span data-stu-id="bde23-145">Management package</span></span> | <span data-ttu-id="bde23-146">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="bde23-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bde23-147">.NET standard</span><span class="sxs-lookup"><span data-stu-id="bde23-147">.NET Standard</span></span> | [<span data-ttu-id="bde23-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="bde23-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="bde23-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="bde23-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="bde23-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bde23-150">Next steps</span></span>
<span data-ttu-id="bde23-151">Następujące linki pozwalają dowiedzieć się więcej na temat usługi Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="bde23-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="bde23-152">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bde23-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="bde23-153">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="bde23-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="bde23-154">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="bde23-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)