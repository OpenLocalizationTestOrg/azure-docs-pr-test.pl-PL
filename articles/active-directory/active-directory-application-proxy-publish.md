---
title: "aaaPublish aplikacji za pomocą serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowanie chmury toohello aplikacji lokalnie z serwera Proxy aplikacji usługi Azure AD w klasycznym portalu hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publikowanie aplikacji przy użyciu serwera proxy aplikacji usługi Azure AD

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-application-proxy-publish.md)

Serwer Proxy aplikacji usługi Azure AD pomaga obsługuje pracowników zdalnych, publikując lokalnymi toobe aplikacji udostępnianych za pośrednictwem hello internet. W tym punkcie powinna mieć już [włączono serwer Proxy aplikacji w hello klasycznego portalu Azure](active-directory-application-proxy-enable.md). W tym artykule przedstawiono hello kroki toopublish aplikacji, które są uruchomione w sieci lokalnej i zapewniania bezpiecznego dostępu zdalnego z spoza sieci. Po zakończeniu pracy w tym artykule, będzie gotowy tooconfigure aplikacji hello spersonalizowanych informacji lub wymagania dotyczące zabezpieczeń.

> [!NOTE]
> Serwer Proxy aplikacji jest funkcją, która jest dostępna tylko w przypadku uaktualnienia toohello Premium lub podstawowa edition usługi Azure Active Directory. Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md). Jeśli chcesz toouse serwera Proxy aplikacji, możesz [publikowanie aplikacji w portalu Azure hello](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Publikowanie aplikacji przy użyciu Kreatora hello
1. Zaloguj się jako administrator w hello [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Przejdź tooActive katalog i wybierz katalog hello, w którym włączono serwer Proxy aplikacji.
   
    ![Active Directory — ikona](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Kliknij przycisk hello **aplikacji** , a następnie kliknij pozycję hello **Dodaj** przycisk u dołu hello hello ekranu
   
    ![Dodawanie aplikacji](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Wybierz pozycję **Opublikuj aplikację dostępną spoza sieci**.
   
    ![Opublikuj aplikację dostępną spoza sieci](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Podaj następujące informacje na temat aplikacji hello:
   
   * **Nazwa**: hello przyjazna nazwa aplikacji. Nazwa musi być unikatowa w katalogu.
   * **Wewnętrzny adres URL**: hello adres, który łącznika serwera Proxy aplikacji hello używa aplikacji hello tooaccess z poziomu sieci prywatnej. Na powitania toopublish serwera wewnętrznej bazy danych, można wprowadzić określoną ścieżkę, zablokowaniu nieopublikowane rest hello powitania serwera. W ten sposób można publikować różne Lokacje hello na tym samym serwerze i nadaj każdej z nich własnej nazwy i reguły dostępu.
     
     > [!TIP]
     > Po opublikowaniu ścieżki, upewnij się, czy zawiera wszystkie obrazy niezbędne hello, skrypty i arkusze stylów dla aplikacji. Na przykład jeśli aplikacja jest w https://yourapp/app i przy użyciu obrazów znajdujący się w https://yourapp/media, następnie należy opublikować https://yourapp/ jako ścieżka hello.
     > 
     > 
   * **Metoda uwierzytelniania wstępnego**: jak serwer Proxy aplikacji zweryfikuje użytkowników przed udzieleniem im dostępu tooyour aplikacji. Wybierz jedną z opcji hello z menu rozwijanego hello.
     
     * Azure Active Directory: Serwer Proxy aplikacji przekierowuje toosign użytkowników za pomocą usługi Azure AD, które umożliwi uwierzytelnienie ich uprawnień dla katalogu hello i aplikacji.
     * Przekazywanie: Użytkownicy nie mają tooauthenticate tooaccess hello aplikacji.
     
     ![Właściwości aplikacji](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. toofinish hello kreatora, kliknij znacznik wyboru hello u dołu hello hello ekranu. Aplikacja Hello jest teraz zdefiniowana w usłudze Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Przypisywanie użytkowników i grup toohello aplikacji
W kolejności dla użytkowników tooaccess opublikowanej aplikacji, należy tooassign je pojedynczo lub w grupach. (Pamiętaj tooassign sobie dostępu zbyt.) Każdy przypisany użytkownik musi mieć licencję platformy Azure w warstwie Podstawowa lub wyższej. Licencje można przypisywać indywidualnie lub toogroups. Aby uzyskać więcej informacji, zobacz [przypisywanie użytkowników aplikacji tooan](active-directory-applications-guiding-developers-assigning-users.md). 

W przypadku aplikacji wymagających uwierzytelnienia wstępnego przypisanie użytkownika daje aplikacji hello toouse uprawnienia. Dla aplikacji, które nie wymagają uwierzytelniania wstępnego, przypisanie użytkownika oznacza, że użytkownik hello mają dostęp do aplikacji hello przez hello panelu dostępu.

1. Po zakończenia kreatora Dodawanie aplikacji hello zobacz temat hello Szybki Start strony aplikacji. Wybierz toomanage, kto ma dostęp do aplikacji toohello, **użytkowników i grup**.
   
    ![Przypisywanie użytkowników na stronie Szybki start serwera proxy aplikacji — zrzut ekranu](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Wyszukaj określonych użytkowników w katalogu lub wyświetl wszystkich użytkowników. wyniki wyszukiwania hello toodisplay, kliknij znacznik wyboru hello.
   
      ![Wyszukiwanie grup lub użytkowników — zrzut ekranu.](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Wybierz użytkowników lub grupy tooassign toothis aplikacji i kliknij **przypisać**. Jesteś zadawane tooconfirm tej akcji.

> [!NOTE]
> W przypadku aplikacji korzystających ze zintegrowanego uwierzytelniania systemu Windows można przypisywać wyłącznie użytkowników synchronizowanych z lokalnej usługi Active Directory i grupy takich użytkowników. Użytkowników logujących się za pomocą konta Microsoft i gości nie można przypisywać do aplikacji opublikowanych przy użyciu serwera proxy aplikacji usługi Azure Active Directory. Upewnij się, zaloguj się przy użyciu poświadczeń, które są częścią hello użytkowników tej samej domenie co w przypadku publikowania aplikacji hello.
> 
> 

## <a name="test-your-published-application"></a>Testowanie opublikowanej aplikacji
Po opublikowaniu aplikacji, można przetestować go przechodząc toohello adres URL, który został opublikowany. Upewnij się, że można uzyskać do niej dostęp, jest poprawnie renderowana i wszystko działa zgodnie z oczekiwaniami. Jeśli masz problemy lub komunikat o błędzie, spróbuj hello [przewodnik rozwiązywania problemów](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Konfigurowanie aplikacji
Można modyfikować opublikowane aplikacje lub konfigurować opcje zaawansowane, na stronie Konfiguruj hello. Na tej stronie można dostosować aplikację, zmiana nazwy hello lub przekazując logo. Można także zarządzać regułami dostępu, takich jak hello metoda uwierzytelniania wstępnego czy uwierzytelnianie wieloskładnikowe.

![Konfiguracja zaawansowana](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Po opublikowaniu aplikacji za pomocą usługi Azure Active Directory serwera Proxy aplikacji, pojawią się one na liście aplikacji hello w usłudze Azure AD i można zarządzać nimi.

Jeśli wyłączysz usługi serwera Proxy aplikacji po opublikowaniu aplikacji, aplikacji hello nie są już dostępne spoza sieci prywatnej. Użytkownicy nadal mogą dostępu hello aplikacji lokalnej w zwykły sposób.

tooview aplikacji i upewnij się, że ten jest dostępny, kliknij dwukrotnie nazwę hello aplikacji hello. Jeśli powitania serwera Proxy aplikacji usługi jest wyłączona i aplikacja hello nie jest dostępna, pojawi się ostrzeżenie u góry hello hello ekranu.

toodelete aplikacji, wybierz aplikacji hello listy, a następnie kliknij przycisk **usunąć**.

## <a name="next-steps"></a>Następne kroki
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)
* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Włączanie dostępu warunkowego](active-directory-application-proxy-conditional-access.md)
* [Praca z aplikacjami obsługującymi oświadczenia](active-directory-application-proxy-claims-aware-apps.md)

Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)

