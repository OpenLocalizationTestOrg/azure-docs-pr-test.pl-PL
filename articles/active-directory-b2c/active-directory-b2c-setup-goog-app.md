---
title: "Usługa Azure Active Directory B2C: Google + konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z konta Google + w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie kont Google + tooconsumers rejestracji i logowania
## <a name="create-a-google-application"></a>Tworzenie aplikacji Google +
toouse Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Google + i dostarczyć hello prawo parametrów. Toodo konto Google + to konieczne. Jeśli nie masz, możesz pobrać go w [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Przejdź toohello [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.
2. Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.
   
    ![Google + — wprowadzenie](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + — nowy projekt](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** w hello lewy pasek nawigacyjny.
4. Kliknij przycisk hello **ekranu zgoda OAuth** u góry hello.
   
    ![Google + - poświadczeń](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w hello **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzowanych przekierowania URI**pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com). Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter. Kliknij przycisk **Utwórz**.
   
    ![Google + - Utwórz identyfikator klienta](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**. Konieczne będzie ich tooconfigure Google + funkcję dostawcy tożsamości w dzierżawie. **Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.
   
    ![Google + - klucz tajny klienta](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj Google + funkcję dostawcy tożsamości w Twojej dzierżawie
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Na przykład wprowadź "G +".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Google**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello Google + aplikacji, który został utworzony wcześniej.
7. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji Google +.

