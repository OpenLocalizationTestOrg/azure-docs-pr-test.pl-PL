---
title: "aaaGet pracę z połączeń hybrydowych przekazywania Azure w programie .NET | Dokumentacja firmy Microsoft"
description: "Napisz aplikację konsolową w języku C# dla połączeń hybrydowych usługi Azure Relay."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="46bd7-103">Wprowadzenie do połączeń hybrydowych usługi Relay</span><span class="sxs-lookup"><span data-stu-id="46bd7-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="46bd7-104">Ten samouczek zawiera wprowadzenie zbyt[połączeń hybrydowych przekazywania Azure](relay-what-is-it.md#hybrid-connections)i pokazuje, jak toouse .NET toocreate aplikacji klienckiej, która wysyła komunikaty tooa odpowiednich aplikacji odbiornika.</span><span class="sxs-lookup"><span data-stu-id="46bd7-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="46bd7-105">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="46bd7-105">What will be accomplished</span></span>
<span data-ttu-id="46bd7-106">Połączenia hybrydowe wymaga zarówno klient, jak i składnik serwera, dlatego samouczek hello tworzy dwie aplikacje konsoli.</span><span class="sxs-lookup"><span data-stu-id="46bd7-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="46bd7-107">Poniżej przedstawiono kroki hello:</span><span class="sxs-lookup"><span data-stu-id="46bd7-107">Here are hello steps:</span></span>

1. <span data-ttu-id="46bd7-108">Tworzenie przestrzeni nazw przekazywania, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46bd7-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="46bd7-109">Tworzenie połączenia hybrydowego w tej przestrzeni nazw przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46bd7-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="46bd7-110">Pisanie komunikatów tooreceive aplikacji konsoli serwera (odbiornika).</span><span class="sxs-lookup"><span data-stu-id="46bd7-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="46bd7-111">Pisanie komunikatów toosend aplikacji konsoli klienta (nadawcy).</span><span class="sxs-lookup"><span data-stu-id="46bd7-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46bd7-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="46bd7-112">Prerequisites</span></span>

<span data-ttu-id="46bd7-113">toocomplete tego samouczka będziesz potrzebować hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="46bd7-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="46bd7-114">[Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="46bd7-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="46bd7-115">Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="46bd7-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="46bd7-116">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="46bd7-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="46bd7-117">1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="46bd7-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="46bd7-118">Jeśli utworzono już przestrzeń nazw przekazywania, przejście toohello [Tworzenie połączenia hybrydowego, za pomocą portalu Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sekcji.</span><span class="sxs-lookup"><span data-stu-id="46bd7-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="46bd7-119">2. Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="46bd7-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="46bd7-120">Jeśli utworzono już połączenie hybrydowe, przejście toohello [utworzyć aplikację serwer](#3-create-a-server-application-listener) sekcji.</span><span class="sxs-lookup"><span data-stu-id="46bd7-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="46bd7-121">3. Tworzenie aplikacji serwera (odbiornika)</span><span class="sxs-lookup"><span data-stu-id="46bd7-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="46bd7-122">toolisten i odbierania wiadomości z hello przekazywania, firma Microsoft będzie zapisywać aplikacji konsolowej C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46bd7-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="46bd7-123">4. Tworzenie aplikacji klienta (nadawcy)</span><span class="sxs-lookup"><span data-stu-id="46bd7-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="46bd7-124">toohello wiadomości toosend przekazywania, firma Microsoft będzie zapisywać aplikacji konsolowej C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46bd7-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="46bd7-125">5. Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="46bd7-125">5. Run hello applications</span></span>
1. <span data-ttu-id="46bd7-126">Uruchom powitania serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46bd7-126">Run hello server application.</span></span>
2. <span data-ttu-id="46bd7-127">Uruchom powitania klienta aplikacji, a następnie wprowadź tekst.</span><span class="sxs-lookup"><span data-stu-id="46bd7-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="46bd7-128">Upewnij się, powitania serwera aplikacji konsoli dane wyjściowe hello tekst, który został wprowadzony w aplikacji klienckiej hello.</span><span class="sxs-lookup"><span data-stu-id="46bd7-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="46bd7-130">Gratulacje, aplikacja end-to-end do obsługi połączeń hybrydowych jest gotowa.</span><span class="sxs-lookup"><span data-stu-id="46bd7-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46bd7-131">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="46bd7-131">Next steps:</span></span>
* [<span data-ttu-id="46bd7-132">Często zadawane pytania dotyczące usługi Relay</span><span class="sxs-lookup"><span data-stu-id="46bd7-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="46bd7-133">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="46bd7-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="46bd7-134">Wprowadzenie do programu Node</span><span class="sxs-lookup"><span data-stu-id="46bd7-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

