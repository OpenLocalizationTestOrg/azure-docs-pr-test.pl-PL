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
# <a name="get-started-with-relay-hybrid-connections"></a>Wprowadzenie do połączeń hybrydowych usługi Relay

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Ten samouczek zawiera wprowadzenie zbyt[połączeń hybrydowych przekazywania Azure](relay-what-is-it.md#hybrid-connections)i pokazuje, jak toouse Node.js toocreate aplikacji klienckiej, która wysyła komunikaty tooa odpowiednich aplikacji odbiornika. 

## <a name="what-will-be-accomplished"></a>Co zostanie osiągnięte?

Połączenia hybrydowe wymagają zarówno składnika klienta, jak i składnika serwera, dlatego w tym samouczku utworzymy dwie aplikacje konsolowe. Poniżej przedstawiono kroki hello:

1. Tworzenie przestrzeni nazw przekazywania, przy użyciu hello portalu Azure.
2. Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure.
3. Wpisz serwer komunikatów tooreceive aplikacji konsoli.
4. Zapis klienta komunikatów toosend aplikacji konsoli.

## <a name="prerequisites"></a>Wymagania wstępne

1. Środowisko [Node.js](https://nodejs.org/en/).
2. Subskrypcja platformy Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure

Jeśli masz już przestrzeń nazw przekazywania utworzone, przejście toohello [Tworzenie połączenia hybrydowego, za pomocą portalu Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sekcji.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Tworzenie połączenia hybrydowego, przy użyciu hello portalu Azure

Jeśli masz już połączenie hybrydowe utworzone, przejście toohello [utworzyć aplikację serwer](#3-create-a-server-application-listener) sekcji.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Tworzenie aplikacji serwera (odbiornika)

toolisten i odbierania wiadomości z hello przekazywania, firma Microsoft będzie zapisywać aplikacja konsolowa Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Tworzenie aplikacji klienta (nadawcy)

toosend komunikatów toohello przekazywania, firma Microsoft będzie zapisywać aplikacja konsolowa Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Uruchamianie aplikacji hello

1. Uruchom aplikację serwera hello: z typu wiersza polecenia Node.js `node listener.js`.
2. Uruchom aplikację klienta hello: z typu wiersza polecenia Node.js `node sender.js`i wprowadź tekst.
3. Upewnij się, powitania serwera aplikacji konsoli dane wyjściowe hello tekst, który został wprowadzony w aplikacji klienckiej hello.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Gratulacje! Aplikacja typu end-to-end do obsługi połączeń hybrydowych korzystająca ze środowiska Node.js jest gotowa.

## <a name="next-steps"></a>Następne kroki:

* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)
* [Tworzenie przestrzeni nazw](relay-create-namespace-portal.md)
* [Wprowadzenie do programu .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Wprowadzenie do programu Node](relay-hybrid-connections-node-get-started.md)

