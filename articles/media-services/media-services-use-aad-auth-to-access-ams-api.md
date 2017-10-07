---
title: "aaaAccess interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat pojęć i kroki tootake toouse usługi Azure Active Directory (Azure AD) tooauthenticate dostępu toohello interfejsu API usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Witaj dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD
 
Witaj interfejsu API usługi Azure Media Services jest interfejs API RESTful. Służy on tooperform operacje na zasobach nośnika przy użyciu interfejsu API REST lub przy użyciu zestawów SDK klienta dostępne. Usługa Azure Media Services udostępnia klienta usługi Media Services SDK dla programu Microsoft .NET. toobe autoryzowanych zasobów usługi Media Services tooaccess i hello Media Services API, musisz najpierw musi zostać uwierzytelniony. 

Usługa Media Services obsługuje [usługi Azure Active Directory (Azure AD)-uwierzytelniania opartego na](../active-directory/active-directory-whatis.md). Witaj usługi Azure Media REST musi mieć hello użytkownika lub aplikacji, która sprawia, że żądania interfejsu API REST hello albo hello **współautora** lub **właściciela** tooaccess roli hello zasobów. Aby uzyskać więcej informacji, zobacz [wprowadzenie opartej na rolach kontrola dostępu w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Obecnie usługa Media Services obsługuje hello Azure kontroli dostępu usługi uwierzytelniania modelu. Jednak na 1 czerwca 2018 zostaną wycofane autoryzacji kontroli dostępu. Zaleca się, jak najszybciej migracji model uwierzytelniania toohello usługi Azure AD.

Ten dokument zawiera omówienie sposobu tooaccess hello interfejsu API usług Media Services przy użyciu REST lub interfejsów API architektury .NET.

## <a name="access-control"></a>Kontrola dostępu

Hello Azure Media REST żądania toosucceed hello wywoływania użytkownik musi mieć rolę współautora lub właściciela do hello jest próby tooaccess konta usługi Media Services.  
Tylko użytkownik mający rolę właściciela hello można przekazać nośnika zasobów (konto) dostępu toonew użytkowników lub aplikacji. Rola współautora Hello mogą uzyskiwać dostęp tylko hello zasobu multimediów.
Nieautoryzowanych żądań zakończyć się niepowodzeniem z kodem stanu 401. Jeśli widzisz tego kodu błędu, sprawdź, czy użytkownika ma hello współautora lub rolę właściciela przypisane do konta usługi Media Services hello użytkownika. Można to sprawdzić, w hello portalu Azure. Wyszukaj konta nośnika, a następnie kliknij hello **kontrola dostępu** kartę. 

![Karta kontroli dostępu](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Typy uwierzytelniania 
 
Korzystając z uwierzytelniania usługi Azure AD z usługi Azure Media Services, masz dwie opcje uwierzytelniania:

- **Uwierzytelnianie użytkownika**. Uwierzytelnianie osoby, która używa toointeract aplikacji hello z zasobami usługi Media Services. Interaktywna aplikacja Hello należy najpierw Monituj użytkownika o hello na powitania poświadczeń. Przykładem jest aplikacja konsoli zarządzania używane przez zadania kodowania toomonitor autoryzowanych użytkowników lub transmisji strumieniowej na żywo. 
- **Uwierzytelnianie głównej usługi**. Uwierzytelniania usługi. Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych demon usługi, usługi warstwy środkowej lub zaplanowanych zadań. Przykłady są aplikacje sieci web, aplikacje funkcji aplikacji logiki, interfejsu API i mikrousług.

### <a name="user-authentication"></a>Uwierzytelnianie użytkowników 

Aplikacje, które powinny używać metody uwierzytelniania użytkownika hello są zarządzanie i monitorowanie natywnych aplikacji: aplikacje mobilne, aplikacje systemu Windows i aplikacji konsoli. Tego typu rozwiązanie jest przydatne, gdy chcesz interakcji z usługą hello w jednym z hello następujące scenariusze:

- Pulpit nawigacyjny do kodowania zadań monitorowania.
- Monitorowanie, odwiedź pulpit nawigacyjny strumienie na żywo.
- Aplikacji do zarządzania desktop lub mobile użytkownikom tooadminister zasobów w ramach konta usługi Media Services.

> [!NOTE]
> Nie można używać tej metody uwierzytelniania dla aplikacji dla użytkowników. 

Natywnych aplikacji musi najpierw uzyskać token dostępu z usługi Azure AD, a następnie użyć go po wprowadzeniu HTTP żądania toohello nośnika interfejsu API REST usług. Dodaj nagłówek żądania toohello tokenu dostępu hello. 

powitania po diagram przedstawia przepływ uwierzytelniania typowych aplikacji: 

![Diagram aplikacje natywne](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

W hello poprzedzających diagramu hello liczby reprezentują hello przepływ żądań hello w kolejności chronologicznej.

> [!NOTE]
> Korzystając z metody uwierzytelniania użytkownika hello, wszystkie aplikacje udostępnianie hello tego samego Identyfikatora klienta aplikacji natywnej (ustawienie domyślne) i aplikacji natywnej identyfikator URI przekierowania. 

1. Monituj użytkownika o poświadczenia.
2. Żądanie tokenu dostępu usługi Azure AD z hello następujące parametry:  

    * Punkt końcowy dzierżawy usługi Azure AD.

        Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure. Umieść kursor nad nazwą hello hello zalogowanego użytkownika w prawym górnym rogu hello.
    * Identyfikator URI zasobu usługi Media Services. 

        Ten identyfikator URI jest hello takie same dla konta usługi Media Services, które znajdują się w hello tego samego środowiska platformy Azure (na przykład https://rest.media.azure.net).

    * Identyfikator klienta aplikacji usługi Media Services (macierzysty).
    * Identyfikator URI przekierowania aplikacji usługi Media Services (macierzysty).
    * Identyfikator URI dla usługi REST Media Services zasobu.
        
        Witaj identyfikator URI reprezentuje punkt końcowy interfejsu API REST hello (na przykład https://test03.restv2.westus.media.azure.net/api/).

    tooget wartości tych parametrów, zobacz [za pomocą ustawień uwierzytelniania Azure tooaccess portalu usługi Azure AD hello](media-services-portal-get-started-with-aad.md) przy użyciu opcji uwierzytelniania użytkownika hello.

3. token dostępu Hello Azure AD jest wysyłany toohello klienta.
4. Witaj klient wysyła żądanie toohello interfejsu API REST multimediów Azure z tokenem dostępu hello Azure AD.
5. powitania klienta pobiera ponownie hello dane z usługi Media Services.

Aby dowiedzieć się jak toocommunicate uwierzytelniania toouse usługi Azure AD z pozostałych żądań przy użyciu powitania klienta Media Services na platformie .NET SDK, zobacz [użycia usługi Azure AD authentication tooaccess hello Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md). 

Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu dostępu do usługi Azure AD przy użyciu parametrów hello opisany w kroku 2. Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Uwierzytelnianie jednostki usługi

Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych usług warstwy środkowej i zaplanowanych zadań: sieci web aplikacji, aplikacje funkcji aplikacji logiki, interfejsów API i mikrousług. Ta metoda uwierzytelniania jest również odpowiedni dla aplikacji interaktywnych, w których można toouse toomanage zasobów konta usługi.

Gdy używasz scenariusze konsumenckie toobuild hello usługi uwierzytelniania główna — metoda uwierzytelniania zwykle odbywa się hello warstwy środkowej (za pośrednictwem niektórych interfejsu API), a nie bezpośrednio w aplikacji mobilnych lub komputerowych. 

toouse ta metoda tworzy aplikację usługi Azure AD i dodatki service principal w jego własnej dzierżawy. Po utworzeniu aplikacji hello nadaj hello aplikacji współautora lub właściciela roli dostępu toohello konta usługi Media Services. Można to zrobić w hello portalu Azure za pomocą wiersza polecenia platformy Azure lub za pomocą skryptu programu PowerShell. Można również użyć istniejącej aplikacji usługi Azure AD. Możesz zarejestrować i zarządzanie aplikacji usługi Azure AD i nazwę główną usługi [w portalu Azure hello](media-services-portal-get-started-with-aad.md). Możesz również można to zrobić przy użyciu [Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) lub [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Aplikacje warstwy środkowej](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Po utworzeniu aplikacji usługi Azure AD, możesz uzyskać wartości hello następujące ustawienia. Te wartości są wymagane do uwierzytelniania:

- Identyfikator klienta 
- Klucz tajny klienta 

W powyższej ilustracji hello hello liczby reprezentują hello przepływ żądań hello w kolejności chronologicznej:
    
1. Aplikacja warstwy środkowej (interfejs API sieci web lub aplikacji sieci web) żądania tokenu dostępu usługi Azure AD, który ma następujące parametry hello:  

    * Punkt końcowy dzierżawy usługi Azure AD.

        Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure. Umieść kursor nad nazwą hello hello zalogowanego użytkownika w prawym górnym rogu hello.
    * Identyfikator URI zasobu usługi Media Services. 

        Ten identyfikator URI jest hello takie same dla konta usługi Media Services, które znajdują się w hello tego samego środowiska platformy Azure (na przykład https://rest.media.azure.net).

    * Identyfikator URI dla usługi REST Media Services zasobu.

        Witaj identyfikator URI reprezentuje punkt końcowy interfejsu API REST hello (na przykład https://test03.restv2.westus.media.azure.net/api/).

    * Wartości aplikacji w usłudze Azure AD: hello identyfikator klienta i klucz tajny klienta.
    
    tooget wartości tych parametrów, zobacz [za pomocą ustawień uwierzytelniania Azure tooaccess portalu usługi Azure AD hello](media-services-portal-get-started-with-aad.md) przy użyciu opcji uwierzytelniania głównej usługi hello.

2. token dostępu Hello Azure AD jest wysyłany toohello warstwy środkowej.
4. warstwy środkowej Hello wysyła żądanie toohello interfejsu API REST multimediów Azure tokenem hello Azure AD.
5. warstwy środkowej Hello pobiera ponownie hello dane z usługi Media Services.

Aby uzyskać więcej informacji dotyczących sposobu toocommunicate uwierzytelniania toouse usługi Azure AD z POZOSTAŁĄ żądań przy użyciu powitania klienta Media Services na platformie .NET SDK, zobacz [użycia usługi Azure AD authentication tooaccess Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md). 

Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu usługi Azure AD przy użyciu parametrów opisanych w kroku 1. Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Wyjątek: "hello serwer zdalny zwrócił błąd: Brak autoryzacji (401)."

Rozwiązanie: Hello Media Services REST żądania toosucceed, hello wywoływania użytkownik musi być Rola współautora lub właściciela hello konto usługi Media Services, które chce tooaccess. Aby uzyskać więcej informacji, zobacz hello [kontrola dostępu](media-services-use-aad-auth-to-access-ams-api.md#access-control) sekcji.

## <a name="resources"></a>Zasoby

następujące artykuły Hello są omówienie pojęć dotyczących uwierzytelniania usługi Azure AD: 

- [Uwierzytelnianie scenariusze związane z usługą Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Dodawanie, aktualizowanie lub usuwanie aplikacji w usłudze Azure AD](../active-directory/develop/active-directory-integrating-applications.md)
- [Konfigurowanie i zarządzanie nimi kontroli dostępu opartej na rolach przy użyciu programu PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)

## <a name="next-steps"></a>Następne kroki

* Za pomocą hello portalu Azure[dostęp do usługi Azure AD authentication tooconsume interfejsu API usługi Azure Media Services](media-services-portal-get-started-with-aad.md).
* Za pomocą uwierzytelniania usługi Azure AD[dostępu Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md).

