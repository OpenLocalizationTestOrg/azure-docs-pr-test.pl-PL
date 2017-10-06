---
title: "Usługa Azure Active Directory B2C: Weibo konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami Weibo w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie kont Weibo tooconsumers rejestracji i logowania

> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej. Ten dostawca tożsamości nie należy używać w środowisku produkcyjnym.
> 

## <a name="create-a-weibo-application"></a>Tworzenie aplikacji Weibo

toouse Weibo jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Weibo i dostarczyć hello prawo parametrów. Toodo konta Weibo to konieczne. Jeśli nie masz, możesz ją uzyskać, w [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Zarejestruj w programie dla deweloperów Weibo hello

1. Przejdź toohello [portalu dla deweloperów Weibo](http://open.weibo.com/) i zaloguj się przy użyciu poświadczeń konta Weibo.
2. Po zalogowaniu kliknij swoją nazwę wyświetlaną w hello prawym górnym rogu.
3. Z listy rozwijanej hello, wybierz**编辑开发者信息**(Edytuj informacje dla deweloperów).
4. Wprowadź informacje wymagane hello do postaci hello i kliknij**提交**(Prześlij).
5. Ukończ proces weryfikacji wiadomości e-mail hello.
6. Przejdź toohello [strony weryfikacji tożsamości](http://open.weibo.com/developers/identity/edit).
7. Wprowadź informacje wymagane hello do postaci hello i kliknij**提交**(Prześlij).

### <a name="register-a-weibo-application"></a>Zarejestrować aplikację Weibo

1. Przejdź toohello [nowej strony rejestracji aplikacji Weibo](http://open.weibo.com/apps/new).
2. Wprowadź informacje niezbędne aplikacji hello.
3. Kliknij przycisk**创建**(Utwórz).
4. Skopiuj wartości hello **klucz aplikacji** i **klucz tajny aplikacji**. Będzie on potrzebny później.
5. Przekaż zdjęć hello wymagane, a następnie wprowadź niezbędne informacje hello.
6. Kliknij przycisk**保存以上信息**(Zapisz).
7. Kliknij przycisk**高级信息**(zaawansowane informacje).
8. Kliknij przycisk**编辑**(Edytuj) następnego toohello pola OAuth2.0**授权设置**(adres URL przekierowania).
9. Wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` dla OAuth2.0**授权设置**(adres URL przekierowania). Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Kliknij przycisk**提交**(Prześlij).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj Weibo funkcję dostawcy tożsamości w Twojej dzierżawie
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "Weibo".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Weibo**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości**
7. Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.
8. Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.
9. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave Weibo konfiguracji.

