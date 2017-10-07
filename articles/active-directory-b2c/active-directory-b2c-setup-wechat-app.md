---
title: "Usługa Azure Active Directory B2C: WeChat konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami WeChat w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Usługa Azure Active Directory B2C: Udostępnianie kont WeChat tooconsumers rejestracji i logowania

> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej.
> 

## <a name="create-a-wechat-application"></a>Tworzenie aplikacji WeChat

toouse WeChat jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji WeChat i dostarczyć hello prawo parametrów. Toodo konta WeChat to konieczne. Jeśli nie masz, możesz ją uzyskać, po zarejestrowaniu się za pomocą jednego z ich aplikacji mobilnych lub za pomocą numeru q. Po wykonaniu tej Pobierz konta w zarejestrowany w programie dla deweloperów WeChat hello. Więcej informacji można znaleźć [tutaj](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Zarejestrować aplikację WeChat

1. Przejdź za[https://open.weixin.qq.com/](https://open.weixin.qq.com/) i zaloguj się.
2. Polecenie**管理中心**(management center).
3. Wykonaj tooregister niezbędne kroki hello nowej aplikacji.
4. Aby uzyskać**授权回调域**(adres URL wywołania zwrotnego), wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Znajdź i skopiuj hello **identyfikator aplikacji** i **klucz aplikacji**. Możesz będą one potrzebne później.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Skonfiguruj WeChat funkcję dostawcy tożsamości w Twojej dzierżawie
1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji. Wprowadź na przykład "WeChat".
5. Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **WeChat**i kliknij przycisk **OK**.
6. Kliknij przycisk **skonfigurować ten dostawca tożsamości**
7. Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.
8. Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.
9. Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave WeChat konfiguracji.

