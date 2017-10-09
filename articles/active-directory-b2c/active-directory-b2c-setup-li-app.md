---
title: "Usługa Azure Active Directory B2C: LinkedIn konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami LinkedIn w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie kont LinkedIn tooconsumers rejestracji i logowania
## <a name="create-a-linkedin-application"></a>Tworzenie aplikacji LinkedIn
toouse LinkedIn jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji LinkedIn i dostarczyć hello prawo parametrów. Toodo konta LinkedIn to konieczne. Jeśli nie masz, możesz pobrać go w [https://www.linkedin.com/](https://www.linkedin.com/).

1. Przejdź toohello [deweloperzy LinkedIn witryny sieci Web](https://www.developer.linkedin.com/) i zaloguj się przy użyciu poświadczeń konta LinkedIn.
2. Kliknij przycisk **Moje aplikacje** w hello paska menu u góry, a następnie kliknij przycisk **tworzenie aplikacji**.
   
    ![LinkedIn — nowej aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. W hello **Utwórz nową aplikację** tworzą, wprowadź odpowiednie informacje hello (**nazwa firmy**, **nazwa**, **opis**, **Adres URL Logo aplikacji**, **stosowania**, **adres URL witryny sieci Web**, **służbowy adres E-mail** i **Telefon służbowy**).
4. Akceptuję toohello **LinkedIn interfejsu API warunki użytkowania** i kliknij przycisk **przesyłania**.
   
    ![LinkedIn - rejestrowania aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**. (Można znaleźć je w obszarze **klucze uwierzytelniania**.) Konieczne będzie ich tooconfigure LinkedIn funkcję dostawcy tożsamości w dzierżawie.
   
   > [!NOTE]
   > **Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.
   > 
   > 
6. Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzacji adresów URL przekierowań** pola (w obszarze **OAuth 2.0**). Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com). Kliknij przycisk **Dodaj**, a następnie kliknij przycisk **aktualizacji**. Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.
   
    ![LinkedIn — ustawienia aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj LinkedIn funkcję dostawcy tożsamości w Twojej dzierżawie
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "LI".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **LinkedIn**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello LinkedIn aplikacji, który został utworzony wcześniej.
7. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji LinkedIn.

