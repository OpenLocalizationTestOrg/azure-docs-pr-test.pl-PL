---
title: "Usługa Azure Active Directory B2C: Konfiguracja usługi Facebook | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami usługi Facebook w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Usługa Azure Active Directory B2C: Podaj tooconsumers rejestracji i logowania z kontami usługi Facebook
## <a name="create-a-facebook-application"></a>Tworzenie aplikacji usługi Facebook
toouse usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji usługi Facebook i dostarczyć hello prawo parametrów. Niezbędne toodo konto serwisu Facebook. Jeśli nie masz, możesz pobrać go w [https://www.facebook.com/](https://www.facebook.com/).

1. Przejdź toohello [Facebook dla deweloperów](https://developers.facebook.com/) poświadczenia konta witryny sieci Web i zaloguj się przy użyciu Twojej usługi Facebook.
2. Jeśli nie zostało to jeszcze zrobione, należy tooregister jako deweloper usługi Facebook. toodo tego, kliknij **zarejestrować** (na powitania prawym górnym rogu strony hello), Zaakceptuj zasady w serwisie Facebook i wykonaj kroki rejestracji hello.
3. Kliknij przycisk **Moje aplikacje** , a następnie kliknij przycisk **Dodaj nową aplikację**. 
4. W formularzu hello podaj **Nazwa wyświetlana** i prawidłowy **E-mail kontaktu**.
5. Kliknij przycisk **utworzyć identyfikator aplikacji**. Może wymagać tooaccept Facebook platformy zasad i ukończyć sprawdzania zabezpieczeń w trybie online.
6. W kolumnie po lewej stronie powitania kliknij **ustawienia** , a następnie wybierz **podstawowe** Jeśli nie jest już wybrana.
7. Wybierz **kategorii**. 
8. Kliknij przycisk **+ Dodaj platformy** i wybierz **witryny sieci Web**.
   
    ![Facebook — ustawienia](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook — ustawienia — witryny sieci Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Wprowadź `https://login.microsoftonline.com/` w hello **adres URL witryny** pola, a następnie kliknij przycisk **Zapisz zmiany** u dołu hello hello strony.
   
    ![Facebook — adres URL witryny](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Skopiuj wartość hello **identyfikator aplikacji**. Kliknij przycisk **Pokaż** i skopiuj wartość hello **klucz tajny aplikacji**. Konieczne będzie ich tooconfigure usługi Facebook jako dostawca tożsamości w dzierżawie. **Klucz tajny aplikacji** jest ważne poświadczenie zabezpieczeń.
   
    ![Facebook - ID aplikacji i klucz tajny aplikacji](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Kliknij przycisk **+ Dodaj produktu** na hello nawigacji po lewej stronie, a następnie hello **Set Up** przycisk dla **logowania serwisu Facebook**.
   
    ![Facebook - logowania usługi Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Kliknij przycisk **ustawienia** na powitania prawo nawigacji w obszarze **logowania usługi Facebook**

    ![Facebook — ustawienia logowania usługi Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **prawidłowy OAuth przekierowania URI** w hello **ustawień klienta OAuth** sekcji. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com). Kliknij przycisk **Zapisz zmiany** u dołu hello hello strony.
    
    ![Facebook — identyfikator URI przekierowania uwierzytelniania OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake aplikacji usługi Facebook mogą być używane przez usługi Azure AD B2C, należy toomake go publicznie dostępne. Można to zrobić, klikając **aplikacji przejrzyj** hello lewy pasek nawigacyjny i przez włączenie hello przełącznika u góry strony hello hello zbyt**tak** i klikając **Potwierdź**.
    
    ![Facebook - publicznego aplikacji](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Facebook
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "Facebook".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Facebook**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i aplikacji klucz tajny aplikacji (of hello aplikacji usługi Facebook, który został utworzony wcześniej) w hello **identyfikator klienta** i **klucz tajny klienta**odpowiednio pola.
7. Kliknij przycisk **OK**, a następnie kliknij przycisk **Utwórz** toosave konfigurację usługi Facebook.

> [!NOTE]
> Dodawanie **dostawcy tożsamości** tooyour dzierżawy nie modyfikuje istniejących zasad. Należy pamiętać tooupdate zasad, umieszczając w niej hello dostawcy tożsamości, utworzony.
>