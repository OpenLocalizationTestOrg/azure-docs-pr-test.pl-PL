---
title: "Usługa Azure Active Directory B2C: Amazon konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers zapisywania się i zaloguj się przy użyciu usługi Amazon kont w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie konta Amazon tooconsumers rejestracji i logowania
## <a name="create-an-amazon-application"></a>Tworzenie aplikacji usługi Amazon
toouse Amazon jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Amazon i dostarczyć hello prawo parametrów. Toodo konta Amazon to konieczne. Jeśli nie masz, możesz pobrać go w [http://www.amazon.com/](http://www.amazon.com/).

1. Przejdź toohello [Centrum deweloperów firmy Amazon](https://login.amazon.com/) i zaloguj się przy użyciu poświadczeń konta Amazon.
2. Jeśli nie zostało to jeszcze zrobione, kliknij przycisk **Utwórz konto**, wykonaj kroki rejestracji developer hello i zaakceptuj zasady hello.
3. Kliknij przycisk **zarejestrować nową aplikację**.
   
    ![Rejestrowanie nowych aplikacji w witrynie sieci Web hello Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Podaj informacje o aplikacji (**nazwa**, **opis**, i **adres URL powiadomienia prywatności**) i kliknij przycisk **zapisać**.
   
    ![Udostępnia informacje o aplikacji do rejestrowania nowych aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. W hello **ustawień sieci Web** sekcji kopiowania wartości hello **identyfikator klienta** i **klucz tajny klienta**. (Należy tooclick hello **Pokaż klucz tajny** to przycisk toosee.) Należy ich tooconfigure Amazon funkcję dostawcy tożsamości w dzierżawie. Kliknij przycisk **Edytuj** u dołu hello hello sekcji. **Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.
   
    ![Podanie Identyfikatora klienta i klucz tajny klienta dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Wprowadź `https://login.microsoftonline.com` w hello **dozwolone źródła JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **mogą zwracać adresów URL** pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com). Kliknij pozycję **Zapisz**. Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.
   
    ![Zapewnienie źródeł JavaScript i zwracać adresów URL dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Amazon
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "Amzn".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Amazon**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello aplikacji Amazon, który został utworzony wcześniej.
7. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfigurację Amazon.

