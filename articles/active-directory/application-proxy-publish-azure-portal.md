---
title: "aaaPublish aplikacji za pomocą serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowanie chmury toohello aplikacji lokalnie z serwera Proxy aplikacji usługi Azure AD w hello portalu Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publikowanie aplikacji przy użyciu serwera proxy aplikacji usługi Azure AD

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-application-proxy-publish.md)

Serwer Proxy aplikacji usługi Azure Active Directory (AD) pomaga obsługuje pracowników zdalnych, publikując lokalnymi toobe aplikacji udostępnianych za pośrednictwem hello internet. Możesz opublikować te aplikacje za pomocą hello Azure tooprovide portalu bezpiecznego dostępu zdalnego spoza sieci.

W tym artykule przedstawiono hello kroki toopublish aplikacji lokalnej za pomocą serwera Proxy aplikacji. Po zakończeniu pracy w tym artykule, użytkownicy będą się tooaccess mogli zdalnie aplikacji. I gotowe tooconfigure będzie dodatkowe funkcje dla aplikacji hello, takie jak pojedyncze logowania jednokrotnego, spersonalizowane informacje i wymagania dotyczące zabezpieczeń.

Jeśli masz tooApplication nowego serwera Proxy, więcej informacji na temat tej funkcji z artykułem hello [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publikowanie aplikacji lokalnych dla funkcji dostępu zdalnego

Wykonaj te kroki toopublish aplikacjami za pomocą serwera Proxy aplikacji. Jeśli nie zostały już pobrane i skonfigurować łącznik w organizacji, należy przejść za[rozpoczęcie pracy z serwerem Proxy aplikacji i zainstalować łącznik hello](active-directory-application-proxy-enable.md) najpierw, a następnie opublikować aplikację.

> [!TIP]
> Jeśli testujesz się serwera Proxy aplikacji dla powitania po raz pierwszy, wybierz aplikację, który jest skonfigurowany do uwierzytelniania opartego na hasłach. Serwer Proxy aplikacji obsługuje inne typy uwierzytelniania, ale są oparte na hasłach aplikacji hello najprostszym tooget się i szybko uruchomić. 

1. Zaloguj się jako administrator w hello [portalu Azure](https://portal.azure.com/).
2. Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **nowej aplikacji**.

  ![Dodawanie aplikacji dla przedsiębiorstw](./media/application-proxy-publish-azure-portal/add-app.png)

3. Wybierz **wszystkie**, a następnie wybierz pozycję **lokalnej aplikacji**.  

  ![Dodawanie aplikacji](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Podaj następujące informacje na temat aplikacji hello:

   - **Nazwa**: hello nazwę aplikacji hello, która będzie wyświetlana na panelu dostępu hello i w hello portalu Azure. 

   - **Wewnętrzny adres URL**: hello adres URL, którego używasz aplikacji hello tooaccess z poziomu sieci prywatnej. Na powitania toopublish serwera wewnętrznej bazy danych, można wprowadzić określoną ścieżkę, zablokowaniu nieopublikowane rest hello powitania serwera. W ten sposób można publikować różne Lokacje na tym samym serwerze co różnych aplikacji hello i nadaj każdej z nich własnej nazwy i reguły dostępu.

     > [!TIP]
     > Po opublikowaniu ścieżki, upewnij się, czy zawiera wszystkie obrazy niezbędne hello, skrypty i arkusze stylów dla aplikacji. Na przykład jeśli aplikacja jest w https://yourapp/app i przy użyciu obrazów znajdujący się w https://yourapp/media, następnie należy opublikować https://yourapp/ jako ścieżka hello. Ten wewnętrzny adres URL nie ma strony docelowej hello toobe, które użytkownicy zobaczą. Aby uzyskać więcej informacji, zobacz [ustawić niestandardową stronę główną dla opublikowanych aplikacji](application-proxy-office365-app-launcher.md).

   - **Zewnętrzny adres URL**: hello adres Użytkownicy przechodzą tooin kolejności tooaccess hello aplikacji z spoza sieci. Jeśli nie chcesz toouse hello domyślny serwer Proxy aplikacji domeny, przeczytaj o [domen niestandardowych w serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-custom-domains.md).
   - **Wstępne uwierzytelnianie**: jak serwer Proxy aplikacji zweryfikuje użytkowników przed udzieleniem im dostępu tooyour aplikacji. 

     - Azure Active Directory: Serwer Proxy aplikacji przekierowuje toosign użytkowników za pomocą usługi Azure AD, które umożliwi uwierzytelnienie ich uprawnień dla katalogu hello i aplikacji. Zaleca się pozostawienie tej opcji jako domyślny hello tak, aby można było korzystać z funkcji zabezpieczeń usługi Azure AD, takich jak dostęp warunkowy i usługa Multi-Factor Authentication.
     - Przekazywanie: Użytkownicy nie mają tooauthenticate względem aplikacji hello tooaccess usługi Azure Active Directory. Nadal można skonfigurować uwierzytelniania wymogi hello wewnętrznej bazy danych.
   - **Łącznik grupy**: łączników hello dostępu zdalnego tooyour aplikacji i grup łącznika ułatwić organizowanie łączniki i aplikacje według obszaru, sieci lub cel. Jeśli nie masz jeszcze utworzony łącznik grupy aplikacji przypisano zbyt**domyślne**.

   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Jeśli to konieczne, należy skonfigurować dodatkowe ustawienia. W przypadku większości aplikacji należy zachować te ustawienia w ich domyślne Stany. 
   - **Limit czasu aplikacji zaplecza**: Ustaw tę wartość za**długi** tylko wtedy, gdy aplikacja jest powolne tooauthenticate i nawiąż połączenie. 
   - **Tłumaczenie adresów URL w nagłówkach**: Zachowaj tę wartość jako **tak** , chyba że hello oryginalnego nagłówka hosta w żądaniu uwierzytelniania hello wymaganych aplikacji.
   - **Tłumaczenie adresów URL w aplikacji treści**: Zachowaj tę wartość jako **nr** chyba, że masz aplikacji lokalnych tooother łącza HTML zapisane na stałe, a nie używaj domen niestandardowych. Aby uzyskać więcej informacji, zobacz [Link tłumaczenia z serwerem Proxy aplikacji](application-proxy-link-translation.md).
   
   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Wybierz pozycję **Dodaj**.


## <a name="add-a-test-user"></a>Dodaj użytkownika testowego 

tootest, że aplikacja została opublikowana poprawnie, Dodaj konto użytkownika testu. Sprawdź, czy to konto ma już aplikacji hello tooaccess uprawnienia z wewnątrz sieci firmowej hello.

1. W bloku szybki start hello, wybierz **przypisać użytkownika do testowania**.

  ![Przypisz użytkownika do testowania](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Na powitania użytkowników i grup bloku, wybierz **Dodaj**.

  ![Dodaj użytkownika lub grupę](./media/application-proxy-publish-azure-portal/add-user.png)

3. W bloku przypisania Dodaj hello, wybierz **użytkowników i grup** następnie wybierz konto hello ma tooadd. 
4. Wybierz **przypisać**.

## <a name="test-your-published-app"></a>Testowanie opublikowanych aplikacji

W przeglądarce Przejdź toohello zewnętrzny adres URL, skonfigurowanego podczas hello publikowania kroku. Powinny pojawić się ekranu startowego hello i można toosign stanie się przy użyciu hello testowe konto można skonfigurować.

![Testowanie opublikowanych aplikacji](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Następne kroki
- [Pobierz łączniki](active-directory-application-proxy-enable.md) i [tworzenie grup łącznika](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplikacji w różnych sieciach i lokalizacje.

- [Konfigurowanie rejestracji jednokrotnej](application-proxy-sso-azure-portal.md) nowo opublikowanych aplikacji
