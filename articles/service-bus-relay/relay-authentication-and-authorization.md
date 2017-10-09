---
title: aaaAzure przekazywania uwierzytelniania i autoryzacji | Dokumentacja firmy Microsoft
description: "Omówienie uwierzytelniania dostępu do sygnatury dostępu Współdzielonego w przekaźnika usługi Azure"
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
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Azure przekazywania uwierzytelniania i autoryzacji
Aplikacje mogą uwierzytelniać tooAzure przekazywania przy użyciu uwierzytelniania dostępu do sygnatury dostępu Współdzielonego. Podobnie za[komunikatów usługi Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md), uwierzytelniania sygnatury dostępu Współdzielonego umożliwia toohello tooauthenticate aplikacji usługi Azure przekazywania danych za pomocą klawisza dostępu skonfigurowane na powitania przekazywania w przestrzeni nazw. Następnie można użyć tego klucza toogenerate token sygnatura dostępu współdzielonego, którego klienci mogą używać usługi przekazywania toohello tooauthenticate.

## <a name="shared-access-signature-authentication"></a>Uwierzytelniania sygnatury dostępu współużytkowanego
[Uwierzytelniania sygnatury dostępu Współdzielonego](../service-bus-messaging/service-bus-sas.md) umożliwia toogrant należy zasób przekazywania tooAzure dostępu użytkownika z uprawnieniami. Uwierzytelniania sygnatury dostępu Współdzielonego wymaga konfiguracji hello klucza kryptograficznego ze skojarzonymi prawami do zasobu. Klienci mogą uzyskiwać dostęp do zasobów toothat z uwzględnieniem tokenu sygnatury dostępu Współdzielonego, który składa się z zasobów hello identyfikatora URI, do której uzyskuje dostęp i wygaśnięcia podpisany hello skonfigurowany klucz.

Na przestrzeni nazw przekazywania, można skonfigurować klucze dla skojarzeń zabezpieczeń. W przeciwieństwie do komunikatów usługi Service Bus, [połączeń hybrydowych przekazywania](relay-hybrid-connections-protocol.md) obsługuje nadawców nieautoryzowani lub anonimowe. Możesz włączyć anonimowy dostęp do jednostki hello podczas tworzenia, pokazane na powitania po zrzut z portalu hello ekranu:

![][0]

toouse sygnatury dostępu Współdzielonego, można skonfigurować [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) obiektu na przekazywania przestrzeni nazw, która składa się z następujących hello:

* *KeyName* , które identyfikują regułę hello.
* *PrimaryKey* jest klucz kryptograficzny używany toosign/zweryfikować tokeny sygnatury dostępu Współdzielonego.
* *Klucz pomocniczy* jest klucz kryptograficzny używany toosign/zweryfikować tokeny sygnatury dostępu Współdzielonego.
* *Prawa* reprezentujący kolekcję hello nasłuchiwania, wysyłania lub zarządzania przyznano prawa.

Reguły autoryzacji skonfigurowana na poziomie przestrzeni nazw hello mogą udzielać dostępu tooall połączenia przekazywania w przestrzeni nazw dla klientów z tokenami podpisany przy użyciu odpowiedniego klucza hello. Zapasowej too12 takie zasady autoryzacji można skonfigurować w przestrzeni nazw przekazywania. Domyślnie [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) z dowolnymi prawami jest konfigurowana dla każdej przestrzeni nazw podczas najpierw zostanie zainicjowana.

tooaccess jednostki, powitania klienta wymaga tokenu sygnatury dostępu Współdzielonego wygenerowanych przy użyciu określonego [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token sygnatury dostępu Współdzielonego Hello jest generowana z użyciem powitalne HMAC-SHA256 ciągu zasobu, który składa się z zasobów hello dostępu toowhich identyfikatora URI jest określona i wygaśnięcia za pomocą klucza kryptograficznego skojarzonych z regułą autoryzacji hello.

Obsługę uwierzytelniania sygnatury dostępu Współdzielonego dla przekazywania Azure jest uwzględniona w hello Azure .NET SDK w wersji 2.0 lub nowszy. Sygnatury dostępu Współdzielonego zapewnia obsługę [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Wszystkich interfejsów API, które przyjmują ciąg połączenia jako parametr obsługują parametry połączenia SAS.

## <a name="next-steps"></a>Następne kroki
- Materiały [uwierzytelniania usługi Service Bus za pomocą sygnatury dostępu współdzielonego](../service-bus-messaging/service-bus-sas.md) Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego.
- Zobacz hello [przewodnik protokołu połączeń hybrydowych przekazywania Azure](relay-hybrid-connections-protocol.md) szczegółowe informacje dotyczące hello możliwości połączeń hybrydowych było możliwe.
- Dla odpowiednich informacji na temat obsługi komunikatów magistrali usług uwierzytelniania i autoryzacji, zobacz [magistrali usług uwierzytelniania i autoryzacji](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png