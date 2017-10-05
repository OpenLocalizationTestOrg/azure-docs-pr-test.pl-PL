---
title: "Usługa Azure Active Directory B2C: Amazon konfiguracji | Dokumentacja firmy Microsoft"
description: "Umożliwiają tworzenie kont i logowania użytkowników z kontami usługi Amazon w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
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
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a>Azure Active Directory B2C: Umożliwiają tworzenie kont i logowania użytkowników z kontami usługi Amazon
## <a name="create-an-amazon-application"></a>Tworzenie aplikacji usługi Amazon
Aby używać usługi Amazon funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy utworzyć aplikację usługi Amazon i dostarczyć prawo parametrów. Musisz mieć konto Amazon, w tym celu. Jeśli nie masz, możesz pobrać go w [http://www.amazon.com/](http://www.amazon.com/).

1. Przejdź do [Centrum deweloperów firmy Amazon](https://login.amazon.com/) i zaloguj się przy użyciu poświadczeń konta Amazon.
2. Jeśli nie zostało to jeszcze zrobione, kliknij przycisk **Utwórz konto**, wykonaj kroki rejestracji deweloperów i zaakceptuj zasady.
3. Kliknij przycisk **zarejestrować nową aplikację**.
   
    ![Rejestrowanie nowych aplikacji w witrynie sieci Web firmy Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Podaj informacje o aplikacji (**nazwa**, **opis**, i **adres URL powiadomienia prywatności**) i kliknij przycisk **zapisać**.
   
    ![Udostępnia informacje o aplikacji do rejestrowania nowych aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. W **ustawień sieci Web** sekcji, skopiowanie wartości **identyfikator klienta** i **klucz tajny klienta**. (Należy kliknąć przycisk **Pokaż klucz tajny** przycisk, aby wyświetlić to.) Należy dysponować je, aby skonfigurować funkcję dostawcy tożsamości w dzierżawie usługi Amazon. Kliknij przycisk **Edytuj** w dolnej części sekcji. **Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.
   
    ![Podanie Identyfikatora klienta i klucz tajny klienta dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Wprowadź `https://login.microsoftonline.com` w **dozwolone źródła JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **mogą zwracać adresów URL** pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com). Kliknij pozycję **Zapisz**. **{Dzierżawa}** wartość jest rozróżniana wielkość liter.
   
    ![Zapewnienie źródeł JavaScript i zwracać adresów URL dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Amazon
1. Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.
2. W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij pozycję **+Dodaj** w górnej części bloku.
4. Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości. Wprowadź na przykład "Amzn".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Amazon**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź identyfikator klienta i klucz tajny klienta aplikacji Amazon, utworzony wcześniej.
7. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** Aby zapisać konfigurację Amazon.

