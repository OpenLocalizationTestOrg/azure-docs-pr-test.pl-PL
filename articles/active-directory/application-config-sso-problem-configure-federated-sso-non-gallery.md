---
title: "Konfigurowanie federacyjnych logowanie jednokrotne dla aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Niektóre hello typowych problemów, które można napotkać podczas konfigurowania federacyjnych pojedynczego logowania jednokrotnego tooyour niestandardową SAML aplikację, która nie jest wymieniony w galerii aplikacji usługi Azure AD hello adresów"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii

Jeśli napotkasz problem podczas konfigurowania aplikacji. Sprawdź zostały wykonane wszystkie kroki hello w artykule hello [konfigurowania pojedynczego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Nie można dodać inne wystąpienie aplikacji hello

tooadd drugiego wystąpienia aplikacji, należy toobe stanie:

-   Skonfiguruj Unikatowy identyfikator hello drugie wystąpienie. Nie można tego samego identyfikatora używane dla pierwszego wystąpienia hello powitalne tooconfigure stanie.

-   Skonfiguruj inny certyfikat niż hello używane jako hello pierwszego wystąpienia.

Jeśli hello aplikacji nie obsługuje żadnego z hello powyżej. Następnie nie będzie możliwe tooconfigure drugiego wystąpienia.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Gdzie ustawić hello format EntityID (identyfikator użytkownika)

Możesz nie być w formacie EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.

Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format. Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sekcji hello NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Gdzie uzyskać metadanych aplikacji hello lub certyfikatu z usługi Azure AD

metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.

7.  Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie. W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.

Usługi Azure AD nie udostępnia metadane hello tooget adresu URL. można pobrać metadanych Hello jako plik XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Nie wiadomo, jak toocustomize SAML oświadczenia wysyłane tooan aplikacji

toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
