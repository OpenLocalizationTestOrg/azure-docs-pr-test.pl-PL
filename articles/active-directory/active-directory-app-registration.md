---
title: "aaaAzure rejestracji aplikacji w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse hello Azure tooregister portalu aplikacji w usłudze Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Zarejestrować aplikację z dzierżawą usługi Azure Active Directory

Aplikacja hello tooregister portalu Azure można użyć z dzierżawy usługi Azure Active Directory (Azure AD). Tworzy identyfikator aplikacji dla aplikacji hello i włączy ją tooreceive tokenów.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.
4. Postępuj zgodnie z monitami hello i utworzyć nową aplikację. Jeśli chcesz szczegółowe przykłady dla aplikacji sieci web lub natywnych aplikacji, zapoznaj się naszego [quickstarts](active-directory-developers-guide.md).
  * W przypadku aplikacji sieci Web, podaj hello **adres URL logowania**, która jest hello podstawowy adres URL aplikacji, w którym użytkownicy mogą rejestrować w np. `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Dla natywnych aplikacji, podaj **identyfikator URI przekierowania**, które usługi Azure AD używa tooreturn odpowiedzi tokenu. Wprowadź aplikację tooyour określonej wartości. np.`http://MyFirstAADApp`
5. Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji identyfikatorem unikatowych klientów hello identyfikator aplikacji.

## <a name="update-application-settings-from-hello-azure-portal"></a>Aktualizowanie ustawień aplikacji hello portalu Azure

Można łatwo zmodyfikować ustawienia istniejących aplikacji przy użyciu hello portalu Azure. Na przykład można tooconfigure adresu URL odpowiedzi, który jest, gdzie usługa Azure AD wystawia token odpowiedzi. Można również tooconfigure uprawnienia tooother aplikacji, dla wystąpienia tooallow Twojego tooaccess aplikacji hello interfejsu API programu Microsoft Graph. Można to zrobić wszystkich za pośrednictwem strony ustawień aplikacji hello.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i wybierz aplikację z listy hello.
4. Kliknij przycisk **ustawienia** tooopen hello stronę ustawień dla aplikacji hello.
  * Witaj **właściwości** strona umożliwia modyfikowanie hello ogólne informacje dla aplikacji hello. W tym nazwa aplikacji hello hello jednokrotnej adres URL i adresu URL wylogowania hello.
  * Witaj **adresy URL odpowiedzi** strony można tooadd adresu URL odpowiedzi, który jest, gdzie usługi Azure AD wysyła odpowiedzi tokenu.
  * Witaj **właścicieli** strony można tooadd właściciele aplikacji.
  * Witaj **uprawnienia** strony można tooconfigure uprawnień dla aplikacji hello. Na przykład hello tooaccess interfejsu API programu Graph firmy Microsoft, kliknij pozycję **Dodaj** i wybierz **Microsoft Graph** w selektora hello interfejsu API, a następnie wybierz wymagane, na przykład uprawnienie hello **Czytaj dane katalogu** .
  * Witaj **klucze** strony można tooadd hasła aplikacji. Witaj klucz tajny będą wyświetlane tylko raz natychmiast po utworzeniu, dlatego upewnij się, że toocopy dla dalszego użytku.

## <a name="use-hello-inline-manifest-editor"></a>Użyj edytora manifestu hello wbudowany

Możesz użyć hello wbudowanego edytora manifestu toomodify pewność, że właściwości aplikacji, które nie są widoczne bezpośrednio w hello portalu Azure. Na przykład można użyć identyfikator URI aplikacji hello toomodify aplikacji lub hello tooenable OAuth2.0 przepływu niejawnego zamiast autoryzacji domyślne hello Udziel przepływu kodu.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD, wybierając konto w hello prawym górnym rogu strony hello.
3. W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i wybierz aplikację z listy hello.
4. Kliknij przycisk **manifestu** z hello aplikacji tooopen hello wbudowanego manifestu Edytor stron.
5. Można tworzyć bezpośrednio toohello zmiany manifestu i zapisz go, gdy wszystko jest gotowe. Alternatywnie można pobrać manifestu tooopen hello w Twoje ulubione hello edytora i przekazywanie zaktualizować manifestu.

## <a name="next-steps"></a>Następne kroki

1. Zapoznaj się z hello [Quickstarts](active-directory-developers-guide.md) uzyskać szczegółowe wskazówki dotyczące aplikacji uwierzytelniania przy użyciu usługi Azure AD.
2. Zapoznaj się z naszą pełną listę przykłady kodu w [GitHub](https://github.com/azure-samples).
