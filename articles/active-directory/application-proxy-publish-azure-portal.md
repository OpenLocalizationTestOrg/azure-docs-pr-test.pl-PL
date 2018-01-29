---
title: "Publikowanie aplikacji przy użyciu serwera proxy aplikacji usługi Azure AD | Microsoft Docs"
description: "Publikowanie aplikacji lokalnych do chmury z serwera Proxy aplikacji usługi Azure AD w portalu Azure."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2017
ms.author: daveba
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 43cabb03a698dd87f12fef8e9a4dd54ee42c3ec9
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publikowanie aplikacji przy użyciu serwera proxy aplikacji usługi Azure AD

Serwer Proxy aplikacji usługi Azure Active Directory (AD) pomaga obsługuje pracowników zdalnych przez publikowania lokalnych aplikacji można uzyskać dostęp za pośrednictwem Internetu. Możesz opublikować te aplikacje za pośrednictwem portalu Azure w celu zapewnienia bezpiecznego dostępu zdalnego spoza sieci.

W tym artykule przedstawiono kroki publikowania aplikacji lokalnej za pomocą serwera Proxy aplikacji. Po ukończeniu tego artykułu użytkowników będzie można zdalnego dostępu aplikacji. I będzie gotowa skonfigurować dodatkowe funkcje dla aplikacji, takich jak logowanie jednokrotne, spersonalizowane informacje i wymagania dotyczące zabezpieczeń.

Jeśli jesteś nowym użytkownikiem serwera Proxy aplikacji, więcej informacji na temat tej funkcji z artykułem [jak zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publikowanie aplikacji lokalnych dla funkcji dostępu zdalnego

Wykonaj poniższe kroki publikowania aplikacji przy użyciu serwera Proxy aplikacji. Jeśli nie zostały już pobrane i skonfigurować łącznik w organizacji, przejdź do [rozpoczęcie pracy z serwerem Proxy aplikacji i zainstalować łącznik](active-directory-application-proxy-enable.md) najpierw, a następnie opublikować aplikację.

> [!TIP]
> Jeśli testujesz się serwera Proxy aplikacji po raz pierwszy, wybierz aplikację, który jest skonfigurowany do uwierzytelniania opartego na hasłach. Serwer Proxy aplikacji obsługuje inne typy uwierzytelniania, ale aplikacje oparte na hasłach są najłatwiejsze do uruchomienia i szybko uruchomić. 

1. Zaloguj się jako administrator w [portalu Azure](https://portal.azure.com/).
2. Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **nowej aplikacji**.

  ![Dodawanie aplikacji dla przedsiębiorstw](./media/application-proxy-publish-azure-portal/add-app.png)

3. Wybierz **wszystkie**, a następnie wybierz pozycję **lokalnej aplikacji**.  

  ![Dodawanie własnej aplikacji](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Podaj następujące informacje dotyczące aplikacji:

   - **Nazwa**: Nazwa aplikacji, która będzie wyświetlana na panelu dostępu i w portalu Azure. 

   - **Wewnętrzny adres URL**: adres URL, który umożliwia dostęp do aplikacji z poziomu sieci prywatnej. Możesz wprowadzić określoną ścieżkę na serwerze zaplecza, która zostanie opublikowana, podczas gdy pozostała część serwera pozostanie nieopublikowana. W ten sposób można publikować różne Lokacje na tym samym serwerze co różnych aplikacji i nadaj każdej z nich własnej nazwy i reguły dostępu.

     > [!TIP]
     > W przypadku publikowania ścieżki upewnij się, że zawiera ona wszystkie niezbędne obrazy, skrypty i arkusze stylów dla aplikacji. Na przykład jeśli aplikacja znajduje się w katalogu https://yourapp/app i korzysta z obrazów znajdujących się w katalogu https://yourapp/media, należy opublikować https://yourapp/ jako ścieżkę. Ten wewnętrzny adres URL nie musi być strony docelowej, które użytkownicy zobaczą. Aby uzyskać więcej informacji, zobacz [ustawić niestandardową stronę główną dla opublikowanych aplikacji](application-proxy-office365-app-launcher.md).

   - **Zewnętrzny adres URL**: adres Użytkownicy przechodzą do Aby uzyskać dostęp do aplikacji z spoza sieci. Jeśli nie chcesz użyć domyślnej domeny serwera Proxy aplikacji, przeczytaj o [domen niestandardowych w serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-custom-domains.md).
   - **Wstępne uwierzytelnianie**: jak serwer Proxy aplikacji zweryfikuje użytkowników przed udzieleniem im dostępu do aplikacji. 

     - Azure Active Directory: serwer proxy aplikacji przekierowuje użytkowników, aby zalogowali się w usłudze Azure AD, co umożliwia uwierzytelnienie ich uprawnień do katalogu i aplikacji. Zaleca się pozostawienie tej opcji jako domyślny, tak aby można było korzystać z funkcji zabezpieczeń usługi Azure AD, takich jak dostęp warunkowy i usługa Multi-Factor Authentication.
     - Przekazywanie: Użytkownicy nie mają do uwierzytelniania usługi Azure Active Directory dostępu do aplikacji. Nadal można skonfigurować uwierzytelniania wymogi do wewnętrznej bazy danych.
   - **Łącznik grupy**: łączników przetwarzania zdalnego dostępu do aplikacji i łącznika grup pomocy organizowanie łączniki i aplikacje według obszaru, sieci lub cel. Jeśli nie masz jeszcze utworzony łącznik grupy aplikacji jest przypisany do **domyślne**.

   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Jeśli to konieczne, należy skonfigurować dodatkowe ustawienia. W przypadku większości aplikacji należy zachować te ustawienia w ich domyślne Stany. 
   - **Limit czasu aplikacji zaplecza**: Ustaw tę wartość na **długi** tylko wtedy, gdy aplikacja jest powolne uwierzytelnienia i połączenia. 
   - **Tłumaczenie adresów URL w nagłówkach**: Zachowaj tę wartość jako **tak** chyba, że aplikacja wymagane oryginalny nagłówek hosta w żądaniu uwierzytelnienia.
   - **Tłumaczenie adresów URL w treści aplikacji**: Zachowaj tę wartość jako **nr** chyba że zostały zapisane na stałe HTML linki do innych aplikacji lokalnych, a nie używaj domen niestandardowych. Aby uzyskać więcej informacji, zobacz [Link tłumaczenia z serwerem Proxy aplikacji](application-proxy-link-translation.md).
   
   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Wybierz pozycję **Dodaj**.


## <a name="add-a-test-user"></a>Dodaj użytkownika testowego 

Aby przetestować aplikację został poprawnie opublikowany, należy dodać konto użytkownika testu. Sprawdź, czy to konto ma już uprawnienia na dostęp do aplikacji z wewnątrz sieci firmowej.

1. W bloku szybki start wybierz **przypisać użytkownika do testowania**.

  ![Przypisz użytkownika do testowania](./media/application-proxy-publish-azure-portal/assign-user.png)

2. Dla użytkowników i grup bloku, wybierz **Dodaj**.

  ![Dodaj użytkownika lub grupę](./media/application-proxy-publish-azure-portal/add-user.png)

3. W bloku przypisania Dodaj, wybierz **użytkowników i grup** następnie wybierz konto, które chcesz dodać. 
4. Wybierz opcję **Przypisz**.

## <a name="test-your-published-app"></a>Testowanie opublikowanych aplikacji

W przeglądarce przejdź do zewnętrznego adresu URL skonfigurowanego w kroku publikowania. Należy wyświetlić ekranu startowego i być w stanie zalogować się przy użyciu konta testowego skonfigurowane.

![Testowanie opublikowanych aplikacji](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Kolejne kroki
- [Pobierz łączniki](active-directory-application-proxy-enable.md) i [tworzenie grup łącznika](active-directory-application-proxy-connectors-azure-portal.md) do publikowania aplikacji w różnych sieciach i lokalizacji.

- [Konfigurowanie rejestracji jednokrotnej](application-proxy-sso-azure-portal.md) nowo opublikowanych aplikacji
