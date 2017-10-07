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
# <a name="available-relay-apis"></a>Interfejsy API dostępne przekazywania

## <a name="runtime-apis"></a>Interfejsy API środowiska wykonawczego

Witaj Poniższa tabela zawiera listę wszystkich aktualnie dostępnych klientów środowiska uruchomieniowego przekazywania.

Witaj [dodatkowe informacje](#additional-information) sekcja zawiera więcej informacji o stanie hello wszystkich bibliotek środowiska uruchomieniowego.

| Język/Platform | Funkcja | Pakiet klienta | Repozytorium |
| --- | --- | --- | --- |
| .NET standard | Połączenia hybrydowe | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET framework | Przekaźnik WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | Nie dotyczy |
| Węzeł | Połączenia hybrydowe | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Dodatkowe informacje

#### <a name="net"></a>.NET
Witaj ekosystemu platformy .NET ma wiele środowisk uruchomieniowych, więc istnieje wiele bibliotek .NET dla usługi Event Hubs. Biblioteka .NET Standard Hello mogą być uruchamiane przy użyciu platformy .NET Core lub hello .NET Framework podczas hello Biblioteka programu .NET Framework może być uruchamiany tylko w środowisku .NET Framework. Aby uzyskać więcej informacji dotyczących platformy .NET Framework, zobacz [framework w wersji](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:
* [Co to jest usługa Azure Relay?](relay-what-is-it.md)
* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)