---
title: "Wprowadzenie do połączeń hybrydowych usługi Azure Relay na platformie .NET | Microsoft Docs"
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="fb2e4-103">Wprowadzenie do połączeń hybrydowych usługi Relay</span><span class="sxs-lookup"><span data-stu-id="fb2e4-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="fb2e4-104">Ten samouczek zawiera wprowadzenie do [połączeń hybrydowych usługi Azure Relay](relay-what-is-it.md#hybrid-connections). Pokazano w nim, jak na platformie .NET utworzyć aplikację kliencką, która wysyła komunikaty do odpowiadającej jej aplikacji odbiornika.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="fb2e4-105">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="fb2e4-105">What will be accomplished</span></span>
<span data-ttu-id="fb2e4-106">Ponieważ połączenia hybrydowe wymagają zarówno składnika klienta, jak i składnika serwera, w tym samouczku zostaną utworzone dwie aplikacje konsolowe.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="fb2e4-107">Oto konkretne kroki:</span><span class="sxs-lookup"><span data-stu-id="fb2e4-107">Here are the steps:</span></span>

1. <span data-ttu-id="fb2e4-108">Utworzenie przestrzeni nazw usługi Relay za pomocą witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="fb2e4-109">Utwórz połączenie hybrydowe w tej przestrzeni nazw za pomocą witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="fb2e4-110">Napisanie aplikacji konsolowej serwera (odbiornika) służącej do odbierania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="fb2e4-111">Napisanie aplikacji konsolowej klienta (nadawcy) służącej do wysyłania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb2e4-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fb2e4-112">Prerequisites</span></span>

<span data-ttu-id="fb2e4-113">Do wykonania kroków tego samouczka niezbędne jest spełnienie następujących wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="fb2e4-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="fb2e4-114">[Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="fb2e4-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="fb2e4-115">W przykładach znajdujących się w tym samouczku używany jest program Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="fb2e4-116">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="fb2e4-117">1. Tworzenie przestrzeni nazw za pomocą usługi Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fb2e4-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="fb2e4-118">Jeśli przestrzeń nazw usługi Relay została już utworzona, przejdź do sekcji [Tworzenie połączenia hybrydowego za pomocą witryny Azure Portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="fb2e4-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="fb2e4-119">2. Tworzenie połączenia hybrydowego za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fb2e4-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="fb2e4-120">Jeśli połączenie hybrydowe zostało już utworzone, przejdź do sekcji [Tworzenie aplikacji serwera](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="fb2e4-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="fb2e4-121">3. Tworzenie aplikacji serwera (odbiornika)</span><span class="sxs-lookup"><span data-stu-id="fb2e4-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="fb2e4-122">Aby nasłuchiwać i odbierać komunikaty z usługi Relay, napiszemy aplikację konsolową w języku C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="fb2e4-123">4. Tworzenie aplikacji klienta (nadawcy)</span><span class="sxs-lookup"><span data-stu-id="fb2e4-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="fb2e4-124">Aby wysyłać komunikaty do usługi Relay, napiszemy aplikację konsolową w języku C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="fb2e4-125">5. Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fb2e4-125">5. Run the applications</span></span>
1. <span data-ttu-id="fb2e4-126">Uruchom aplikację serwera.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-126">Run the server application.</span></span>
2. <span data-ttu-id="fb2e4-127">Uruchom aplikację klienta i wprowadź jakiś tekst.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="fb2e4-128">Upewnij się, że w konsoli aplikacji serwera pojawia się tekst wprowadzony w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="fb2e4-130">Gratulacje, aplikacja end-to-end do obsługi połączeń hybrydowych jest gotowa.</span><span class="sxs-lookup"><span data-stu-id="fb2e4-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb2e4-131">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="fb2e4-131">Next steps:</span></span>
* [<span data-ttu-id="fb2e4-132">Często zadawane pytania dotyczące usługi Relay</span><span class="sxs-lookup"><span data-stu-id="fb2e4-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="fb2e4-133">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="fb2e4-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="fb2e4-134">Wprowadzenie do programu Node</span><span class="sxs-lookup"><span data-stu-id="fb2e4-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

