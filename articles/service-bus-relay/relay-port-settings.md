---
title: "ustawienia portów przekazywania aaaAzure | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o wartości portu przekaźnika usługi Azure."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: e66785f786ee241c974d250f9ec29dfcc1fdc3fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-port-settings"></a>Ustawienia portów przekaźnika usługi Azure

Witaj poniższej tabeli opisano hello wymagana konfiguracja dla wartości portu dla przekaźnika usługi Azure.

## <a name="hybrid-connections"></a>Połączenia hybrydowe
Połączenia hybrydowe używa protokołu Websocket jako podstawowy mechanizm transportu, który używa hello **HTTPS** tylko. 

## <a name="wcf-relays"></a>Przekaźniki WCF
  
|Powiązanie|Zabezpieczenia transportu|Port|  
|-------------|------------------------|----------|  
|[Klasa BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (klient)|Tak|HTTPS| 
| |" |Nie|HTTP|  
|[Klasa BasicHttpRelayBinding](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (usługa)|Albo|9351/HTTP|  
|[Klasa NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (klient)|Tak|9351/HTTPS.|  
||" |Nie|9350/HTTP|  
|[Klasa NetEventRelayBinding](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (usługa)|Albo|9351/HTTP|  
|[Klasa NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (klienta/usługa)|Albo|5671/9352/HTTP (9352/9353, jeśli przy użyciu hybrydowego)|  
|[Klasa NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (klient)|Tak|9351/HTTPS.|  
||" |Nie|9350/HTTP|  
|[Klasa NetOnewayRelayBinding](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (usługa)|Albo|9351/HTTP|  
|[Klasa WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (klient)|Tak|HTTPS|  
||" |Nie|HTTP|  
|[Klasa WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (usługa)|Albo|9351/HTTP|  
|[Klasa WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (klient)|Tak|HTTPS|  
||" |Nie|HTTP|  
|[Klasa WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (usługa)|Albo|9351/HTTP|

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przekaźnika usługi Azure, odwiedź te linki:
* [Co to jest usługa Azure Relay?](relay-what-is-it.md)
* [Często zadawane pytania dotyczące usługi Relay](relay-faq.md)