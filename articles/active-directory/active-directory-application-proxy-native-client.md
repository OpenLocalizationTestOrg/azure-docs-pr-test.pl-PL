---
title: "aplikacje klienta natywnego aaaPublish — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób toocommunicate aplikacji klienta natywnego tooenable z łącznika serwera Proxy aplikacji w usłudze Azure AD tooprovide bezpieczny dostęp zdalny tooyour lokalnej aplikacji."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Jak toointeract aplikacji klienta natywnego tooenable przy użyciu serwera proxy aplikacji

W aplikacjach tooweb dodawania serwera Proxy usługi Azure Active Directory aplikacji może być również używane toopublish natywnego klienta aplikacji. Aplikacja Native client aplikacji różnią się od aplikacji sieci web, ponieważ są zainstalowane na urządzeniu, podczas gdy aplikacje sieci web są dostępne za pośrednictwem przeglądarki. 

Serwer Proxy aplikacji obsługuje aplikacje klientami przez akceptują usługę Azure AD wystawione tokeny, które są wysyłane w standardowych nagłówków HTTP autoryzacji.

![Relacja między użytkowników końcowych, Azure Active Directory i opublikowanych aplikacji](./media/active-directory-application-proxy-native-client/richclientflow.png)

Użyj hello Azure AD Authentication Library, która zajmuje się uwierzytelniania i obsługuje wiele środowisk klienckich, toopublish natywnych aplikacji. Serwer Proxy aplikacji jest dopasowywana do hello [scenariusza tooWeb interfejsu API aplikacji natywnej](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). W tym artykule przedstawiono hello cztery kroki toopublish aplikacji natywnej z serwera Proxy aplikacji i hello Azure AD Authentication Library. 

## <a name="step-1-publish-your-application"></a>Krok 1: Publikowanie aplikacji
Publikowanie aplikacji serwera proxy, jak w przypadku innych aplikacji i przypisz tooaccess użytkowników aplikacji. Aby uzyskać więcej informacji, zobacz [publikowania aplikacji za pomocą serwera Proxy aplikacji](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Krok 2: Konfigurowanie aplikacji
Skonfiguruj natywnych aplikacji w następujący sposób:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Przejdź za**usługi Azure Active Directory** > **rejestracji aplikacji**.
3. Wybierz **nowej rejestracji aplikacji**.
4. Określ nazwę aplikacji, wybierz pozycję **natywnego** jako typ aplikacji hello i podaj hello identyfikator URI przekierowania dla aplikacji. 

   ![Tworzenie nowej rejestracji aplikacji](./media/active-directory-application-proxy-native-client/create.png)
5. Wybierz pozycję **Utwórz**.

Aby uzyskać szczegółowe informacje dotyczące tworzenia nowej rejestracji aplikacji, zobacz [Integrowanie aplikacji z usługą Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Krok 3: Udziel dostępu tooother aplikacji
Włącz hello aplikacji natywnej toobe widoczne tooother aplikacje w katalogu:

1. Nadal **rejestracji aplikacji**, wybierz hello nowej aplikacji natywnej nowo utworzony.
2. Wybierz **wymagane uprawnienia**.
3. Wybierz pozycję **Dodaj**.
4. Pierwszym krokiem hello Otwórz **wybierz interfejs API**.
5. Używać hello wyszukiwania paska toofind hello serwera Proxy aplikacji aplikacji, która została opublikowana w pierwszej sekcji hello. Wybierz tej aplikacji, a następnie kliknij przycisk **wybierz**. 

   ![Wyszukaj powitania serwera proxy aplikacji](./media/active-directory-application-proxy-native-client/select_api.png)
6. Otwórz hello drugi etap **wybierz uprawnienia**.
7. Za pomocą toogrant wyboru hello aplikacji natywnej dostępu tooyour serwera proxy aplikacji, a następnie kliknij przycisk **wybierz**.

   ![Udziel dostępu tooproxy aplikacji](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Wybierz **gotowe**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Krok 4: Edytuj hello biblioteki uwierzytelniania usługi Active Directory
Edytuj kod natywnych aplikacji hello w kontekście uwierzytelniania hello hello tooinclude Active Directory Authentication Library (ADAL) hello następującego tekstu:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

zmienne Hello w hello przykładowy kod powinien zostać zastąpiony w następujący sposób:

* **Identyfikator dzierżawy** można znaleźć w portalu Azure hello. Przejdź za**usługi Azure Active Directory** > **właściwości** i kopiowania hello identyfikator katalogu. 
* **Zewnętrzny adres URL** jest frontonu adres URL hello wprowadzony w powitania serwera Proxy aplikacji. toofind to wartość, przejdź toohello **serwera proxy aplikacji** sekcji powitania serwera proxy aplikacji.
* **Identyfikator aplikacji** z hello aplikacji natywnej znajduje się na powitania **właściwości** strony natywnej aplikacji hello.
* **Identyfikator URI przekierowania aplikacji natywnej hello** znajduje się na powitania **identyfikator URI przekierowania** strony natywnej aplikacji hello.


## <a name="see-also"></a>Zobacz też

Aby uzyskać więcej informacji o przepływie natywnych aplikacji hello, zobacz [tooweb natywnych aplikacji interfejsu API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)
