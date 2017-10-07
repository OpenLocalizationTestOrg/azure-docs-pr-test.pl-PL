---
title: "aaaGet pracę z połączeń hybrydowych przekazywania Azure w węźle | Dokumentacja firmy Microsoft"
description: "Napisz aplikację konsolową w środowisku Node.js do obsługi połączeń hybrydowych usługi Azure Relay."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="b7579-103">Wprowadzenie do połączeń hybrydowych usługi Relay</span><span class="sxs-lookup"><span data-stu-id="b7579-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="b7579-104">Ten samouczek zawiera wprowadzenie zbyt[połączeń hybrydowych przekazywania Azure](relay-what-is-it.md#hybrid-connections)i pokazuje, jak toouse Node.js toocreate aplikacji klienckiej, która wysyła komunikaty tooa odpowiednich aplikacji odbiornika.</span><span class="sxs-lookup"><span data-stu-id="b7579-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b7579-105">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="b7579-105">What will be accomplished</span></span>

<span data-ttu-id="b7579-106">Połączenia hybrydowe wymagają zarówno składnika klienta, jak i składnika serwera, dlatego w tym samouczku utworzymy dwie aplikacje konsolowe.</span><span class="sxs-lookup"><span data-stu-id="b7579-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="b7579-107">Poniżej przedstawiono kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b7579-107">Here are hello steps:</span></span>

1. <span data-ttu-id="b7579-108">Tworzenie przestrzeni nazw przekazywania, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7579-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="b7579-109">Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7579-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="b7579-110">Wpisz serwer komunikatów tooreceive aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="b7579-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="b7579-111">Zapis klienta komunikatów toosend aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="b7579-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7579-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7579-112">Prerequisites</span></span>

1. <span data-ttu-id="b7579-113">Środowisko [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="b7579-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="b7579-114">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b7579-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="b7579-115">1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b7579-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="b7579-116">Jeśli masz już przestrzeń nazw przekazywania utworzone, przejście toohello [Tworzenie połączenia hybrydowego, za pomocą portalu Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sekcji.</span><span class="sxs-lookup"><span data-stu-id="b7579-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="b7579-117">2. Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b7579-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="b7579-118">Jeśli masz już połączenie hybrydowe utworzone, przejście toohello [utworzyć aplikację serwer](#3-create-a-server-application-listener) sekcji.</span><span class="sxs-lookup"><span data-stu-id="b7579-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="b7579-119">3. Tworzenie aplikacji serwera (odbiornika)</span><span class="sxs-lookup"><span data-stu-id="b7579-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="b7579-120">toolisten i odbierania wiadomości z hello przekazywania, firma Microsoft będzie zapisywać aplikacja konsolowa Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7579-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="b7579-121">4. Tworzenie aplikacji klienta (nadawcy)</span><span class="sxs-lookup"><span data-stu-id="b7579-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="b7579-122">toosend komunikatów toohello przekazywania, firma Microsoft będzie zapisywać aplikacja konsolowa Node.js.</span><span class="sxs-lookup"><span data-stu-id="b7579-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="b7579-123">5. Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b7579-123">5. Run hello applications</span></span>

1. <span data-ttu-id="b7579-124">Uruchom aplikację serwera hello: z typu wiersza polecenia Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="b7579-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="b7579-125">Uruchom aplikację klienta hello: z typu wiersza polecenia Node.js `node sender.js`i wprowadź tekst.</span><span class="sxs-lookup"><span data-stu-id="b7579-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="b7579-126">Upewnij się, powitania serwera aplikacji konsoli dane wyjściowe hello tekst, który został wprowadzony w aplikacji klienckiej hello.</span><span class="sxs-lookup"><span data-stu-id="b7579-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="b7579-128">Gratulacje! Aplikacja typu end-to-end do obsługi połączeń hybrydowych korzystająca ze środowiska Node.js jest gotowa.</span><span class="sxs-lookup"><span data-stu-id="b7579-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7579-129">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="b7579-129">Next steps:</span></span>

* [<span data-ttu-id="b7579-130">Często zadawane pytania dotyczące usługi Relay</span><span class="sxs-lookup"><span data-stu-id="b7579-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="b7579-131">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="b7579-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="b7579-132">Wprowadzenie do programu .NET</span><span class="sxs-lookup"><span data-stu-id="b7579-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="b7579-133">Wprowadzenie do programu Node</span><span class="sxs-lookup"><span data-stu-id="b7579-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

