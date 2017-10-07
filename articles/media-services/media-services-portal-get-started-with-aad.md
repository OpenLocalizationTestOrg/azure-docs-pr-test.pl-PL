---
title: "aaaGet do korzystania z usługi Azure AD authentication przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Azure tooaccess portalu tooconsume uwierzytelniania usługi Azure Active Directory (Azure AD) hello Azure Media Services API."
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Wprowadzenie do uwierzytelniania usługi Azure AD przy użyciu hello portalu Azure

Dowiedz się, jak toouse hello Azure tooaccess portalu usługi Azure Active Directory (Azure AD) uwierzytelniania tooaccess hello Azure Media Services API.

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Jeśli nie masz konta, Rozpocznij od [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). 
- Konto usługi Media Services. Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).
- Upewnij się, że przegląd hello [podczas uzyskiwania dostępu do usługi Azure Media usług interfejsu API za pomocą omówienie uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

Korzystając z uwierzytelniania usługi Azure AD z usługi Azure Media Services, masz dwie opcje uwierzytelniania:

- **Uwierzytelnianie użytkownika**. Uwierzytelnianie osoby, która używa toointeract aplikacji hello z zasobami usługi Media Services. Interaktywna aplikacja Hello należy najpierw monitują hello poświadczenia użytkownika. Przykładem jest aplikacja konsoli zarządzania używane przez zadania kodowania toomonitor autoryzowanych użytkowników lub transmisji strumieniowej na żywo. 
- **Uwierzytelnianie głównej usługi**. Uwierzytelniania usługi. Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych demon usługi, usługi warstwy środkowej lub zaplanowane zadania: aplikacje sieci web funkcji aplikacji, aplikacji logiki, interfejsów API albo mikrousługi.

> [!IMPORTANT]
> Obecnie usługa Media Services obsługuje hello Azure kontroli dostępu usługi uwierzytelniania modelu. Jednak na 1 czerwca 2018 zostaną wycofane autoryzacji kontroli dostępu. Zaleca się, jak najszybciej migracji model uwierzytelniania toohello usługi Azure AD.

## <a name="select-hello-authentication-method"></a>Wybierz metodę uwierzytelniania hello

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Media Services.
2. Wybierz jak toohello tooconnect Media Services API.

    ![Wybierz połączenie stronę — metoda](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Uwierzytelnianie użytkowników

tooconnect toohello interfejsu API usług Media Services przy użyciu hello opcji uwierzytelniania użytkownika, powitania klienta aplikacja potrzebuje toorequest token usługi Azure AD, który ma hello następujące parametry:  

* Punktu końcowego dzierżawcy usługi Azure AD
* Identyfikator URI zasobu usługi Media Services
* Identyfikator klienta aplikacji usługi Media Services (native) 
* Identyfikator URI przekierowania aplikacji usługi Media Services (native) 
* Identyfikator URI dla usługi REST Media Services

Można uzyskać hello wartości dla parametrów na powitania **Media Services API z uwierzytelnieniem użytkownika** strony. 

![Uzyskuj dostęp do strony uwierzytelniania użytkownika](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Jeśli łączysz toohello interfejsu API usług Media Services przy użyciu hello zestawu .NET SDK nośnika usługi Microsoft hello wymaganych wartości tooyou dostępne jako część hello zestawu SDK. Aby uzyskać więcej informacji, zobacz [użycia usługi Azure AD authentication tooaccess hello Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md).

Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu usługi Azure AD przy użyciu parametrów hello wcześniejszym opisem. Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Uwierzytelnianie jednostki usługi

tooconnect toohello interfejsu API usług Media Services przy użyciu hello opcji głównej usługi, aplikacji warstwy środkowej (interfejs API sieci web lub aplikacji sieci web) musi toorequest token usługi Azure AD, który ma hello następujące parametry:  

* Punktu końcowego dzierżawcy usługi Azure AD
* Identyfikator URI zasobu usługi Media Services 
* Identyfikator URI dla usługi REST Media Services
* Wartości aplikacji w usłudze Azure AD: hello **identyfikator klienta** i **klucz tajny klienta**

Można uzyskać hello wartości dla parametrów na powitania **tooMedia interfejsu API usług Uzyskuj dostęp do nazwy głównej usługi** strony. Użyj tej strony toocreate Azure nowej aplikacji usługi AD lub tooselect już istniejący. Po wybraniu hello aplikacji usługi Azure AD, możesz pobrać hello Identyfikatora klienta (identyfikator aplikacji) i generowanie wartości (klucz) klucz tajny klienta hello. 

![Uzyskuj dostęp do strony głównej usługi](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Gdy hello **nazwy głównej usługi** zostanie otwarty blok, zostanie wybrana hello pierwszej aplikacji usługi Azure AD spełniającego hello następujące kryteria:

- Jest zarejestrowaną aplikację usługi Azure AD.
- Na powitania konto ma uprawnienia współautora lub Owner Role-Based kontroli dostępu.

Po utworzeniu, lub wybierz aplikację usługi Azure AD, można tworzyć i skopiować klucza tajnego klienta (klucz) i hello Identyfikatora klienta (identyfikator aplikacji). Identyfikator klucza tajnego i klienta klienta Hello są token dostępu hello tooget wymaganego w tym scenariuszu.

Jeśli nie masz aplikacji usługi Azure AD toocreate uprawnienia w domenie kontroli aplikacji usługi Azure AD hello hello bloku nie są wyświetlane, a następnie zostanie wyświetlony komunikat ostrzegawczy.

Jeśli łączysz toohello interfejsu API usług Media Services przy użyciu hello .NET SDK usługi Media Services, zobacz [użycia usługi Azure AD authentication tooaccess hello Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md).

Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu usługi Azure AD przy użyciu parametrów hello wcześniejszym opisem. Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Pobierz klucz tajny identyfikator i klienta powitania klienta

Po wybraniu istniejącej aplikacji usługi Azure AD lub hello wybierz opcję toocreate nowy, są wyświetlane następujące przyciski hello:

![Zarządzanie przyciski uprawnienia i zarządzanie aplikacji](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

Witaj tooopen bloku aplikacji usługi Azure AD, kliknij przycisk **Zarządzanie aplikacją**. Na powitania **Zarządzanie aplikacją** bloku można uzyskać Identyfikatora klienta aplikacji hello (identyfikator aplikacji). toogenerate klucz tajny klienta (key), wybierz opcję **klucze**.

![Zarządzanie aplikacji bloku klucze opcji](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Zarządzanie uprawnieniami i aplikacji hello

Po wybraniu hello aplikacji usługi Azure AD, można zarządzać aplikacji hello i uprawnienia. tooset się tooaccess aplikacji z usługą Azure AD innych aplikacji, kliknij przycisk **zarządzania uprawnieniami**. Dla zadań zarządzania, takich jak zmiana kluczy i adresy URL odpowiedzi lub manifest aplikacji hello tooedit, kliknij przycisk **Zarządzanie aplikacją**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Edytuj ustawienia aplikacji hello lub manifestu

Ustawienia aplikacji hello tooedit lub manifestu, kliknij przycisk **Zarządzanie aplikacją**.

![Zarządzanie strony aplikacji](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Następne kroki

Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).
