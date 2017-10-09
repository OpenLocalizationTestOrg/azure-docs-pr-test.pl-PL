---
title: "aaaWhat przekazywania Azure jest i dlaczego warto używać go — omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie usługi Azure Relay"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>Co to jest usługa Azure Relay?

Witaj przekaźnika usługi Azure service ułatwia hybrydowych aplikacji przez włączenie toosecurely można ujawnić usług, które znajdują się w korporacyjnym środowisku sieci toohello chmury publicznej, bez konieczności tooopen połączenie zapory lub wymagają niepożądanych zmian tooa Infrastruktura sieci firmowej. Usługa przekazywania obsługuje wiele różnych protokołów transportowych i standardów usług sieci Web.

Usługa przekaźnika Hello obsługuje tradycyjne jednokierunkowe żądanie/odpowiedź, a ruch peer-to-peer. Obsługuje ona również dystrybucję zdarzeń w zakresie Internetu tooenable publikowania/subskrypcji scenariuszy i komunikacji poprzez gniazdo dwukierunkowe dla zwiększonej wydajności point-to-point. 

We wzorcu transferu danych hello obsługiwanych przez przekaźnik Usługa lokalna łączy toohello przekaźnika usługi za pomocą portu wychodzącego i tworzy gniazdo dwukierunkowe dla komunikacji powiązanej tooa konkretnym adresem spotkania. powitania klienta następnie może komunikować się z usługą lokalne powitania wysyłając usługi przekazywania toohello ruchu kierującej hello adresu spotkania. Hello usługi przekazywania następnie "przekazuje" Usługa lokalna toohello danych za pomocą klienta dedykowanych tooeach gniazd dwukierunkowych. Witaj klient nie potrzebuje bezpośredniego połączenia usługi lokalnej toohello, nie jest wymagane tooknow, w którym znajduje się usługa hello i hello Usługa lokalna nie wymaga żadnych portów przychodzących otwarty na zaporze hello.

elementy klucza możliwości Hello udostępniane przez przekaźnik jest komunikacja dwukierunkowa, Niebuforowane bariery sieciowe ograniczania przypominającej TCP, odnajdowania punktu końcowego, stanu łączności i umieszczenia zabezpieczenia punktu końcowego. możliwości przekazywania Hello różnią się od technologii integracji na poziomie sieci, takich jak sieć VPN, w tym przekazywania można zakresie tooa endpoint pojedynczej aplikacji na jednym komputerze, gdy technologii sieci VPN jest znacznie bardziej natrętnych, opiera się na zmiany w środowisku sieciowym hello .

Usługa Azure Relay ma dwie funkcje:

1. [Połączenia hybrydowe](#hybrid-connections) — używa hello Otwórz standardowe websocket włączenie scenariuszy wieloplatformowych.
2. [Przekaźniki WCF](#wcf-relays) -korzysta z systemu Windows Communication Foundation (WCF) tooenable zdalnych wywołań procedur. Przekaźnik WCF jest hello przekazywania starszych oferty, w których wielu klientów już używać z ich WCF modele programowania.

Połączenia hybrydowe i przekaźników WCF Włącz tooassets bezpiecznego połączenia, który istnieje w korporacyjnym środowisku sieciowym. Używanie jednego za pośrednictwem innych hello jest zależne od określonych potrzeb, zgodnie z opisem w poniższej tabeli hello:

|  | Przekaźnik WCF | Połączenia hybrydowe |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Otwarty protokół oparty na standardach** | |x |
| **Wiele modeli programowania RPC** | |x |

## <a name="hybrid-connections"></a>Połączenia hybrydowe

Witaj [połączeń hybrydowych przekaźnika usługi Azure](relay-hybrid-connections-protocol.md) funkcja jest bezpieczne, protokołu open ewolucji hello istniejących funkcji przekazywania, które można wdrożyć na dowolnej platformie i w dowolnym języku, który zawiera podstawowe możliwości protokołu WebSocket, który jawnie zawiera hello interfejs API protokołu WebSocket w popularne przeglądarki sieci web. Połączenia hybrydowe są oparte na protokole HTTP i WebSocket.

### <a name="service-history"></a>Historia usługi

Połączenia hybrydowe otrzymuje pierwsze hello, podobnie o nazwie "Usługi BizTalk Services" funkcji, które było oparte na hello Azure Service Bus WCF przekazywania. nowe możliwości połączeń hybrydowych Hello uzupełnia hello istniejących funkcji przekazywania WCF i możliwości te dwie usługi istnieje side-by-side hello Azure przekaźnika usługi. Korzystają one ze wspólnej bramy, ale pod innymi względami są to różne implementacje.

## <a name="wcf-relays"></a>Przekaźniki WCF

Witaj WCF przekazywania działa w przypadku hello pełne .NET Framework (NETFX) i usług WCF. Inicjuje hello połączenie między usługą lokalną i hello przekaźnika usługi przy użyciu zestawu powiązań "przekazuje" usługi WCF. Tle hello hello powiązania przekaźników są mapowane toonew transportu powiązanie elementy toocreate składników kanału WCF integrujące się z magistralą usług w chmurze hello.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Architektura: przetwarzanie przychodzących żądań przekaźnika
Gdy klient wysyła żądanie toohello [przekazywania Azure](/azure/service-bus-relay/) usługi, usługi równoważenia obciążenia Azure hello kieruje tooany hello węzłów bramy. Jeśli hello żądanie jest żądaniem nasłuchiwania, węzeł bramy hello tworzy nowy przekaźnik. Jeśli Żądanie hello jest konkretnego przekaźnika tooa żądania połączenia, węzeł bramy hello przekazuje hello połączenia żądania toohello węzeł bramy będący właścicielem przekaźnika hello. Witaj węzła bramy, który jest właścicielem przekaźnika hello wysyła spotkania żądania toohello nasłuchującego klienta, prosząc toocreate odbiornika hello węzeł bramy toohello tymczasowego kanału, który odebrał żądanie połączenia hello.

Po nawiązaniu połączenia przekaźnika hello, hello klienci mogą wymieniać komunikaty za pośrednictwem hello węzła bramy, który służy do hello spotkania.

![Przetwarzanie przychodzących żądań przekaźnika WCF](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Następne kroki

* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)
* [Tworzenie przestrzeni nazw](relay-create-namespace-portal.md)
* [Wprowadzenie do programu .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Wprowadzenie do programu Node](relay-hybrid-connections-node-get-started.md)

