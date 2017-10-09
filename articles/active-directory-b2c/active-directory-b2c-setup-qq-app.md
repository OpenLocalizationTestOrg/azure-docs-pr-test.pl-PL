---
title: "Usługa Azure Active Directory B2C: Q konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami q w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie kont q tooconsumers rejestracji i logowania

> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej.
> 

## <a name="create-a-qq-application"></a>Tworzenie aplikacji q

toouse q jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji q i dostarczyć hello prawo parametrów. Toodo konta q to konieczne. Jeśli nie masz, możesz ją uzyskać, w [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Zarejestruj w programie dla deweloperów q hello

1. Przejdź toohello [portalu dla deweloperów q](http://open.qq.com) i zaloguj się przy użyciu poświadczeń konta q.
2. Po zalogowaniu Przejdź zbyt[http://open.qq.com/reg](http://open.qq.com/reg) tooregister samodzielnie dewelopera.
3. Wybierz hello menu**个人**(poszczególnych deweloperów).
4. Wprowadź informacje wymagane hello do postaci hello i kliknij**下一步**(następny krok).
5. Ukończ proces weryfikacji wiadomości e-mail hello.

> [!NOTE]
> Konieczne będzie toowait kilka toobe dni zatwierdzone po zarejestrowaniu dewelopera. 

### <a name="register-a-qq-application"></a>Zarejestrować aplikację q

1. Przejdź za[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Polecenie**应用管理**(Zarządzanie aplikacjami).
3. Polecenie**创建应用**(Tworzenie aplikacji).
4. Wprowadź informacje niezbędne aplikacji hello.
5. Polecenie**创建应用**(Tworzenie aplikacji).
6. Wprowadź informacje wymagane hello.
7. Dla hello**授权回调域**(adres URL wywołania zwrotnego) wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Polecenie**创建应用**(Tworzenie aplikacji).
9. Na stronie potwierdzenia hello, kliknij**应用管理**strony zarządzania aplikacji toohello tooreturn (Zarządzanie aplikacjami).
10. Polecenie**查看**dalej aplikacji toohello (Widok), został utworzony.
11. Polecenie**修改**(Edycja).
12. Z góry hello hello strony, skopiuj hello **identyfikator aplikacji** i **klucz aplikacji**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj funkcję dostawcy tożsamości w dzierżawie q
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "Q".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **q**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości**
7. Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.
8. Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.
9. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfigurację q.

