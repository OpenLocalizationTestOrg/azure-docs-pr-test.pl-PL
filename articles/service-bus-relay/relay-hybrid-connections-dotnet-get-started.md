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
# <a name="get-started-with-relay-hybrid-connections"></a>Wprowadzenie do połączeń hybrydowych usługi Relay
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Ten samouczek zawiera wprowadzenie zbyt[połączeń hybrydowych przekazywania Azure](relay-what-is-it.md#hybrid-connections)i pokazuje, jak toouse .NET toocreate aplikacji klienckiej, która wysyła komunikaty tooa odpowiednich aplikacji odbiornika. 

## <a name="what-will-be-accomplished"></a>Co zostanie osiągnięte?
Połączenia hybrydowe wymaga zarówno klient, jak i składnik serwera, dlatego samouczek hello tworzy dwie aplikacje konsoli. Poniżej przedstawiono kroki hello:

1. Tworzenie przestrzeni nazw przekazywania, przy użyciu hello portalu Azure.
2. Tworzenie połączenia hybrydowego w tej przestrzeni nazw przy użyciu hello portalu Azure.
3. Pisanie komunikatów tooreceive aplikacji konsoli serwera (odbiornika).
4. Pisanie komunikatów toosend aplikacji konsoli klienta (nadawcy).

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka będziesz potrzebować hello następujące wymagania wstępne:

1. [Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com). Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.
2. Subskrypcja platformy Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure
Jeśli utworzono już przestrzeń nazw przekazywania, przejście toohello [Tworzenie połączenia hybrydowego, za pomocą portalu Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sekcji.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure
Jeśli utworzono już połączenie hybrydowe, przejście toohello [utworzyć aplikację serwer](#3-create-a-server-application-listener) sekcji.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Tworzenie aplikacji serwera (odbiornika)
toolisten i odbierania wiadomości z hello przekazywania, firma Microsoft będzie zapisywać aplikacji konsolowej C# za pomocą programu Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Tworzenie aplikacji klienta (nadawcy)
toohello wiadomości toosend przekazywania, firma Microsoft będzie zapisywać aplikacji konsolowej C# za pomocą programu Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Uruchamianie aplikacji hello
1. Uruchom powitania serwera aplikacji.
2. Uruchom powitania klienta aplikacji, a następnie wprowadź tekst.
3. Upewnij się, powitania serwera aplikacji konsoli dane wyjściowe hello tekst, który został wprowadzony w aplikacji klienckiej hello.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Gratulacje, aplikacja end-to-end do obsługi połączeń hybrydowych jest gotowa.

## <a name="next-steps"></a>Następne kroki:
* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)
* [Tworzenie przestrzeni nazw](relay-create-namespace-portal.md)
* [Wprowadzenie do programu Node](relay-hybrid-connections-node-get-started.md)

