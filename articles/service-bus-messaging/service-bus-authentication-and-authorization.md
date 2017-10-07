---
title: "aaaAzure magistrali usług uwierzytelniania i autoryzacji | Dokumentacja firmy Microsoft"
description: "Uwierzytelnianie tooService aplikacji magistrali z uwierzytelnianiem dostępu sygnatury dostępu Współdzielonego."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Uwierzytelnianie i autoryzacja w usłudze Service Bus

Aplikacje mogą uwierzytelniać tooAzure usługi Service Bus przy użyciu dostępu sygnatury dostępu Współdzielonego uwierzytelniania. Udostępnione sygnatury dostępu uwierzytelniania umożliwia aplikacji tooauthenticate tooService magistrali przy użyciu klawisza dostępu skonfigurowane na powitania przestrzeni nazw lub w jednostce hello, z którym są skojarzone określonych praw. Następnie można użyć tego klucza toogenerate token sygnatura dostępu współdzielonego, którego klienci mogą używać tooService tooauthenticate magistrali.

> [!IMPORTANT]
> Sygnatury dostępu Współdzielonego należy używać zamiast usługi Azure Active Directory kontroli dostępu (znanej także jako usługa kontroli dostępu lub ACS), ponieważ ACS jest przestarzałe. Sygnatury dostępu Współdzielonego zapewnia schemat uwierzytelniania prostego, elastyczne i łatwe w użyciu dla usługi Service Bus. Aplikacje mogą używać SAS w scenariuszach, w których nie potrzebują oni pojęcie hello toomanage autoryzowanych "użytkownika". Aby uzyskać więcej informacji, zobacz [ten wpis w blogu](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Uwierzytelniania sygnatury dostępu współużytkowanego

[Uwierzytelniania sygnatury dostępu Współdzielonego](service-bus-sas.md) umożliwia toogrant należy zasób magistrali tooService dostępu użytkownika z uprawnieniami. Skojarzenia zabezpieczeń uwierzytelniania w usłudze Service Bus wymaga konfiguracji hello klucza kryptograficznego ze skojarzonymi prawami do zasobu usługi Service Bus. Klienci mogą uzyskiwać dostęp do zasobów toothat z uwzględnieniem tokenu sygnatury dostępu Współdzielonego, który składa się z zasobów hello identyfikatora URI, do której uzyskuje dostęp i wygaśnięcia podpisany hello skonfigurowany klucz.

Na przestrzeni nazw usługi Service Bus, można skonfigurować klucze dla skojarzeń zabezpieczeń. klucz Hello stosuje tooall jednostek obsługi komunikatów w tej przestrzeni nazw. Klucze można również skonfigurować na tematów i kolejek usługi Service Bus. Sygnatury dostępu Współdzielonego jest również obsługiwany na [przekazywania Azure](../service-bus-relay/relay-authentication-and-authorization.md).

toouse sygnatury dostępu Współdzielonego, można skonfigurować [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) obiektu w przestrzeni nazw, kolejka lub temat. Ta reguła zawiera hello następujące elementy:

* *KeyName* , które identyfikują regułę hello.
* *PrimaryKey* jest klucz kryptograficzny używany toosign/zweryfikować tokeny sygnatury dostępu Współdzielonego.
* *Klucz pomocniczy* jest klucz kryptograficzny używany toosign/zweryfikować tokeny sygnatury dostępu Współdzielonego.
* *Prawa* reprezentujący kolekcję hello nasłuchiwania, wysyłania lub zarządzania przyznano prawa.

Reguły autoryzacji skonfigurowana na poziomie przestrzeni nazw hello mogą udzielać dostępu tooall jednostki w przestrzeni nazw dla klientów z tokenami podpisany przy użyciu odpowiedniego klucza hello. Zapasowej too12 takie zasady autoryzacji można skonfigurować w przestrzeni nazw usługi Service Bus, kolejka lub temat. Domyślnie [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) z dowolnymi prawami jest konfigurowana dla każdej przestrzeni nazw podczas najpierw zostanie zainicjowana.

tooaccess jednostki, powitania klienta wymaga tokenu sygnatury dostępu Współdzielonego wygenerowanych przy użyciu określonego [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token sygnatury dostępu Współdzielonego Hello jest generowana z użyciem powitalne HMAC-SHA256 ciągu zasobu, który składa się z zasobów hello dostępu toowhich identyfikatora URI jest określona i wygaśnięcia za pomocą klucza kryptograficznego skojarzonych z regułą autoryzacji hello.

Obsługę uwierzytelniania sygnatury dostępu Współdzielonego dla usługi Service Bus jest uwzględniona w hello Azure .NET SDK w wersji 2.0 lub nowszej. Sygnatury dostępu Współdzielonego zapewnia obsługę [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Wszystkich interfejsów API, które przyjmują ciąg połączenia jako parametr obsługują parametry połączenia SAS.

## <a name="next-steps"></a>Następne kroki

- Materiały [uwierzytelniania usługi Service Bus za pomocą sygnatury dostępu współdzielonego](service-bus-sas.md) Aby uzyskać więcej informacji na temat sygnatury dostępu Współdzielonego.
- [Zmienia tooACS włączone w przestrzeni nazw.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Dla odpowiednich informacji na temat przekaźnika usługi Azure uwierzytelniania i autoryzacji, zobacz [Azure przekazywania uwierzytelniania i autoryzacji](../service-bus-relay/relay-authentication-and-authorization.md). 

