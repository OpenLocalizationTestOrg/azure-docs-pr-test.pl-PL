---
title: 'Azure Active Directory B2C: Konfiguracja konta Microsoft | Dokumentacja firmy Microsoft'
description: "Podaj tooconsumers rejestracji i logowania z konta Microsoft w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie tooconsumers rejestracji i logowania kont Microsoft
## <a name="create-a-microsoft-account-application"></a>Tworzenie aplikacji konta Microsoft
toouse konta Microsoft, funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji konta Microsoft i dostarczyć hello prawo parametrów. Toodo konto Microsoft to konieczne. Jeśli nie masz, możesz pobrać go w [https://www.live.com/](https://www.live.com/).

1. Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) i zaloguj się przy użyciu poświadczeń konta Microsoft.
2. Kliknij przycisk **Dodaj aplikację**.
   
    ![Microsoft konta — Dodawanie nowej aplikacji](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Podaj **nazwa** dla aplikacji i kliknij przycisk **tworzenie aplikacji**.
   
    ![Konto Microsoft — Nazwa aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Skopiuj wartość hello **identyfikator aplikacji**. Będzie potrzebny tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.
   
    ![Konto Microsoft — identyfikator aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Polecenie **platformy Dodaj** i wybierz polecenie **Web**.
   
    ![Microsoft konta — Dodawanie platformy](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Konto Microsoft — sieci Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **identyfikator URI przekierowania** pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).
   
    ![Konto Microsoft — adres URL przekierowania](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Polecenie **wygenerować nowe hasło** w obszarze hello **klucze tajne aplikacji** sekcji. Skopiuj nowe hasło hello wyświetlany na ekranie. Będzie potrzebny tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie. To hasło jest ważne poświadczenie zabezpieczeń.
   
    ![Microsoft konta — wygenerować nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Konto Microsoft — nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Witaj opcję **Obsługa zestaw Live SDK** w obszarze hello **zaawansowane opcje** sekcji. Kliknij pozycję **Zapisz**.
   
    ![Konto Microsoft — Obsługa zestaw Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj konto Microsoft jako dostawca tożsamości w Twojej dzierżawie
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "MSA".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **konta Microsoft**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** i wprowadź identyfikator aplikacji hello oraz hasło hello aplikacji konta Microsoft, utworzony wcześniej.
7. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji konta Microsoft.

