---
title: "Omówienie przekaźnika API aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd informacji o dostępnych interfejsach API przekaźnika usługi Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="fb1d3-103">Interfejsy API dostępne przekazywania</span><span class="sxs-lookup"><span data-stu-id="fb1d3-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="fb1d3-104">Interfejsy API środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="fb1d3-104">Runtime APIs</span></span>

<span data-ttu-id="fb1d3-105">Witaj Poniższa tabela zawiera listę wszystkich aktualnie dostępnych klientów środowiska uruchomieniowego przekazywania.</span><span class="sxs-lookup"><span data-stu-id="fb1d3-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="fb1d3-106">Witaj [dodatkowe informacje](#additional-information) sekcja zawiera więcej informacji o stanie hello wszystkich bibliotek środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="fb1d3-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="fb1d3-107">Język/Platform</span><span class="sxs-lookup"><span data-stu-id="fb1d3-107">Language/Platform</span></span> | <span data-ttu-id="fb1d3-108">Funkcja</span><span class="sxs-lookup"><span data-stu-id="fb1d3-108">Available feature</span></span> | <span data-ttu-id="fb1d3-109">Pakiet klienta</span><span class="sxs-lookup"><span data-stu-id="fb1d3-109">Client package</span></span> | <span data-ttu-id="fb1d3-110">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="fb1d3-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb1d3-111">.NET standard</span><span class="sxs-lookup"><span data-stu-id="fb1d3-111">.NET Standard</span></span> | <span data-ttu-id="fb1d3-112">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="fb1d3-112">Hybrid Connections</span></span> | [<span data-ttu-id="fb1d3-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="fb1d3-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="fb1d3-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="fb1d3-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="fb1d3-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="fb1d3-115">.NET Framework</span></span> | <span data-ttu-id="fb1d3-116">Przekaźnik WCF</span><span class="sxs-lookup"><span data-stu-id="fb1d3-116">WCF Relay</span></span> | [<span data-ttu-id="fb1d3-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="fb1d3-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="fb1d3-118">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="fb1d3-118">N/A</span></span> |
| <span data-ttu-id="fb1d3-119">Węzeł</span><span class="sxs-lookup"><span data-stu-id="fb1d3-119">Node</span></span> | <span data-ttu-id="fb1d3-120">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="fb1d3-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="fb1d3-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="fb1d3-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="fb1d3-122">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="fb1d3-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="fb1d3-123">.NET</span><span class="sxs-lookup"><span data-stu-id="fb1d3-123">.NET</span></span>
<span data-ttu-id="fb1d3-124">Witaj ekosystemu platformy .NET ma wiele środowisk uruchomieniowych, więc istnieje wiele bibliotek .NET dla usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fb1d3-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="fb1d3-125">Biblioteka .NET Standard Hello mogą być uruchamiane przy użyciu platformy .NET Core lub hello .NET Framework podczas hello Biblioteka programu .NET Framework może być uruchamiany tylko w środowisku .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fb1d3-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="fb1d3-126">Aby uzyskać więcej informacji dotyczących platformy .NET Framework, zobacz [framework w wersji](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="fb1d3-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb1d3-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb1d3-127">Next steps</span></span>
<span data-ttu-id="fb1d3-128">toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:</span><span class="sxs-lookup"><span data-stu-id="fb1d3-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="fb1d3-129">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="fb1d3-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="fb1d3-130">Często zadawane pytania dotyczące usługi Relay</span><span class="sxs-lookup"><span data-stu-id="fb1d3-130">Relay FAQ</span></span>](relay-faq.md)