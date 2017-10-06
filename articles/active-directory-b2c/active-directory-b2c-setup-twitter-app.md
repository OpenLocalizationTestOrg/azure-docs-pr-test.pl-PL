---
title: "Usługa Azure Active Directory B2C: Twitter konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami usługi Twitter w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Usługa Azure Active Directory B2C: Podaj tooconsumers rejestracji i logowania z kontami usługi Twitter

> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej.
> 

## <a name="create-a-twitter-application"></a>Utwórz aplikację usługi Twitter
toouse usługi Twitter jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C należy toocreate aplikacji Twitter i dostarczyć hello prawo parametrów. Toodo konta dewelopera Twitter to konieczne. Jeśli nie masz, możesz pobrać go w [https://dev.twitter.com/](https://dev.twitter.com/).

1. Przejdź toohello [dewelopera witryny sieci Web w usłudze Twitter](https://dev.twitter.com/) i zaloguj się przy użyciu poświadczeń.
2. Kliknij przycisk **Moje aplikacje** w obszarze **narzędzia i pomoc techniczna** , a następnie kliknij przycisk **Utwórz nową aplikację**. 
3. W formularzu hello, podaj wartość hello **nazwa**, **opis**, i **witryny sieci Web**.
4. Dla hello **wywołania zwrotnego adresu URL**, wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Upewnij się, że tooreplace **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).
5. Sprawdź hello pole tooagree toohello **umowy Developer** i kliknij przycisk **tworzenie aplikacji Twitter**.
6. Po utworzeniu aplikacji hello kliknij **kluczy i tokenów dostępu**.
7. Skopiuj wartość hello **konsumenta** i **klucz tajny klienta**. Konieczne będzie ich tooconfigure Twitter jako dostawca tożsamości w dzierżawie.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Twitter
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "Twitter".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Twitter**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello Twitter **konsumenta** dla hello **identyfikator klienta** i hello Twitter **klucz tajny klienta**dla hello **klucz tajny klienta**.
7. Kliknij przycisk **OK**, a następnie kliknij przycisk **Utwórz** toosave konfigurację usługi Twitter.

