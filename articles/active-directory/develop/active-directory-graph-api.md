---
title: aaaAzure interfejsu API Graph Active Directory | Dokumentacja firmy Microsoft
description: "Omówienie i szybkiego startu przewodnik hello interfejsu API Graph, dzięki czemu programistyczny dostęp tooAzure AD przez punkty końcowe interfejsu API REST."
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Interfejs API programu Graph usługi Azure Active Directory
> [!IMPORTANT]
> Zdecydowanie zaleca się używanie [Microsoft Graph](https://graph.microsoft.io/) zamiast interfejsu API usługi Azure AD Graph tooaccess zasobów usługi Azure Active Directory. Obecnie koncentrujemy nasze działania deweloperskie na programie Microsoft Graph i nie planujemy żadnych dodatkowych rozszerzeń dla interfejsu API funkcji Azure AD Graph. Istnieje bardzo ograniczoną liczbę scenariuszy, w których interfejsu API usługi Azure AD Graph nadal może być odpowiednie; Aby uzyskać więcej informacji, zobacz hello [Microsoft Graph lub hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) wpis w blogu w hello Centrum deweloperów pakietu Office.
> 
> 

Hello Azure Active Directory interfejsu API programu Graph zapewnia dostęp programistyczny tooAzure AD przez punkty końcowe interfejsu API REST. Aplikacje mogą używać tooperform interfejsu API programu Graph hello tworzenia, odczytu, aktualizacji i usuwania operacji (CRUD) w katalogu danych i obiektów. Na przykład hello interfejsu API programu Graph obsługuje hello następujące typowe operacje dla obiekt użytkownika:

* Tworzenie nowego użytkownika w katalogu
* Pobierz właściwości szczegółowe użytkownika, takie jak ich grup
* Zaktualizuj właściwości użytkownika, takie jak ich lokalizacji i numer telefonu lub zmień ich hasła
* Sprawdź członkostwo w grupie użytkownika dla dostępu opartej na rolach
* Wyłącz konto użytkownika lub usuń go całkowicie

W dodatku toouser obiektów można wykonywać podobne działania na inne obiekty, takie jak grupy i aplikacje. hello toocall interfejsu API programu Graph dla katalogu aplikacji hello musi być zarejestrowana w usłudze Azure AD i można skonfigurować tooallow dostępu toohello katalogu. Zazwyczaj jest to osiągane przez użytkownika lub administratora przepływu zgody.

przy użyciu toobegin hello Azure Active Directory interfejsu API programu Graph, zobacz hello [Przewodnik Szybki Start interfejsu API Graph](active-directory-graph-api-quickstart.md), lub widok hello [interakcyjne dokumentacji interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Funkcje
Witaj interfejsu API programu Graph zapewnia hello następujące funkcje:

* **Punkty końcowe interfejsu API REST**: hello interfejsu API programu Graph jest usługą RESTful, składającej się z punktów końcowych, które są dostępne przy użyciu standardowych żądań HTTP. Witaj interfejsu API programu Graph obsługuje XML lub Javascript Object Notation (JSON) typy zawartości dla żądań i odpowiedzi. Aby uzyskać więcej informacji, zobacz [dokumentacja interfejsu API REST usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Uwierzytelnianie za pomocą usługi Azure AD**: co toohello żądania interfejsu API programu Graph musi zostać uwierzytelniony przez dołączenie JSON Web Token (JWT) w nagłówku autoryzacji hello hello żądania. Token ten jest uzyskaną przez tworzenie punktu końcowego tokena tooAzure żądania przez usługi AD i podanie prawidłowych poświadczeń. Można użyć hello przepływ poświadczeń klienta OAuth 2.0 lub kod autoryzacji hello Udziel tooacquire przepływu tokenu toocall hello wykresu. Aby uzyskać więcej informacji [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Autoryzacji opartej na rolach (RBAC)**: grupy zabezpieczeń są używane tooperform RBAC w hello interfejsu API programu Graph. Na przykład, jeśli chcesz toodetermine, czy użytkownik ma dostęp do zasobów dla określonych tooa, aplikacja hello można wywołać hello [sprawdzić członkostwa w grupie (przechodnie)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) operacja, która zwraca wartość PRAWDA lub FAŁSZ.
* **Zapytanie różnicowej**: Jeśli chcesz toocheck dla zmian w katalogu między dwa okresy bez konieczności toomake częste toohello zapytania interfejsu API programu Graph, może wysłać żądanie różnicowej zapytania. Ten typ żądania zwróci tylko hello zmiany między hello poprzednie żądanie różnicowej zapytania i hello bieżącego żądania. Aby uzyskać więcej informacji, zobacz [Azure AD Graph API różnicowej zapytania](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Rozszerzenia katalogów**: Jeśli tworzysz aplikację, która musi mieć unikatowy właściwości tooread lub zapisu w przypadku obiektów katalogu może rejestrować i użyj wartości rozszerzenia przy użyciu hello interfejsu API programu Graph. Na przykład jeśli aplikacja wymaga właściwości Identyfikatora użytkownika Skype dla każdego użytkownika, możesz zarejestrować nową właściwość hello w katalogu hello i będą dostępne dla każdego obiektu użytkownika. Aby uzyskać więcej informacji, zobacz [Azure AD Graph interfejsu API katalogu schematu rozszerzenia](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Zabezpieczone przez zakresy uprawnień**: interfejs API programu Graph usługi AAD przedstawia zakresy uprawnień, umożliwiające bezpieczny zgodę na dostęp do danych tooAAD i obsługi różnych typów aplikacji klienta, w tym:
  
  * z interfejsem użytkownika, które są przyznawane delegowanego dostępu toodata za pośrednictwem autoryzacji hello zalogowanego użytkownika (delegowane)
  * używające aplikacji zdefiniować kontroli dostępu opartej na rolach, takich jak klienci usługi/demon (role aplikacji)
    
    Oba delegowane i zakresy uprawnień roli aplikacji reprezentują uprawnienia udostępnianych przez interfejs API programu Graph hello i może być wysłane przez aplikacje klienckie za pośrednictwem uprawnień rejestracji aplikacji [funkcji w portalu Azure hello](https://portal.azure.com). Klientów można sprawdzić zakresy uprawnień hello uzyskuje toothem sprawdzając hello zakresu ("punkt połączenia usługi") oświadczenia odebrane w tokenie dostępu hello delegowane uprawnienia i oświadczeń hello role ("ról") dla aplikacji uprawnienia roli. Dowiedz się więcej o [zakresy uprawnień interfejsu API Graph usługi Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Scenariusze
Witaj interfejsu API programu Graph umożliwia wiele scenariuszy, w aplikacji. Hello następujące scenariusze są najczęściej hello:

* **Aplikacji biznesowej (pojedynczej dzierżawy)**: W tym scenariuszu developer enterprise działa w przypadku organizacji, która ma subskrypcji usługi Office 365. Deweloper Hello jest tworzenie aplikacji sieci web, która współdziała z usługi Azure AD tooperform zadania takie przypisanie licencji użytkownika tooa. To zadanie wymaga toohello dostępu do interfejsu API programu Graph, dzięki czemu Deweloper hello rejestruje hello pojedynczej dzierżawy aplikacji w usłudze Azure AD i konfiguruje uprawnienia odczytu i zapisu dla hello interfejsu API programu Graph. Następnie hello aplikacji jest skonfigurowana toouse jest własne poświadczenia lub tych hello obecnie logowania użytkownika tooacquire tokenu toocall hello interfejsu API programu Graph.
* **Aplikacja usługi (wielodostępnej) oprogramowania jako**: W tym scenariuszu niezależnego dostawcy oprogramowania (ISV) jest tworzenie aplikacji hostowanej wielodostępnej sieci web, która zawiera funkcje zarządzania użytkownika do innych organizacji korzystających z usługi Azure AD. Tych funkcji wymaga dostępu do obiektów toodirectory, a więc aplikacja hello musi hello toocall interfejsu API programu Graph. Deweloper Hello rejestruje hello aplikacji w usłudze Azure AD, konfiguruje ją odczytu toorequire uprawnienia do interfejsu API programu Graph hello zapisu i następnie umożliwia dostęp do zewnętrznych, dzięki czemu inne organizacje mogą wyrazić zgodę aplikacji hello toouse w ich katalogu. Podczas uwierzytelniania użytkownika w innej organizacji toohello aplikacji dla powitania po raz pierwszy, są wyświetlane okno dialogowe zgody użytkownika z uprawnieniami hello, który żąda aplikacji hello.  Udzielające zgody określi aplikacji hello tymi, których uprawnienia toohello interfejsu API programu Graph w katalogu hello użytkownika. Aby uzyskać więcej informacji na powitania zgody framework, zobacz [omówienie hello zgody Framework](active-directory-integrating-applications.md).

## <a name="see-also"></a>Zobacz też
[Przewodnik Szybki Start Azure interfejs API Graph usługi AD](active-directory-graph-api-quickstart.md)

[AD Graph REST dokumentacji](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Przewodnik dewelopera usługi Azure Active Directory](active-directory-developers-guide.md)

