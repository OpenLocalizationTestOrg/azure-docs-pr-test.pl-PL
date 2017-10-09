---
title: "aaaSingle logowania jednokrotnego przy użyciu serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Opisano, jak tooprovide logowanie jednokrotne przy użyciu serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Ograniczone delegowanie protokołu Kerberos dla aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji

Zapewnia rejestrację jednokrotną dla lokalnych aplikacji opublikowanych przy użyciu serwera Proxy aplikacji, które są zabezpieczone przy użyciu zintegrowanego uwierzytelniania systemu Windows. Te aplikacje wymagają biletu protokołu Kerberos dla dostępu. Serwer Proxy aplikacji używa delegowanie ograniczone protokołu Kerberos (KCD) toosupport tych aplikacji. 

Można włączyć aplikacji tooyour rejestracji jednokrotnej, przy użyciu zintegrowanego uwierzytelniania systemu Windows (IWA) przez nadanie uprawnień łączniki serwera Proxy aplikacji w usłudze Active Directory tooimpersonate użytkowników. łączniki Hello Użyj toosend to uprawnienie i odbierać tokeny w ich imieniu.

## <a name="how-single-sign-on-with-kcd-works"></a>Jak rejestracji jednokrotnej z KCD działa
Ten diagram opisano przepływ hello, gdy użytkownik próbuje tooaccess aplikacji lokalnej, która używa funkcji IWA.

![Diagram przepływu uwierzytelniania firmy Microsoft AAD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. Witaj, użytkownik wprowadza hello aplikacji lokalnych hello tooaccess adresu URL za pośrednictwem serwera Proxy aplikacji.
2. Serwer Proxy aplikacji przekierowuje hello żądania tooAzure AD uwierzytelniania usługi toopreauthenticate. W tym momencie usługi Azure AD stosuje odpowiednie uwierzytelnianie, a zasady autoryzacji, takie jak uwierzytelnianie wieloskładnikowe. Jeśli użytkownik hello jest weryfikowane, usługi Azure AD tworzy token i wysyła je toohello użytkownika.
3. Użytkownik Hello przekazuje token tooApplication powitania serwera Proxy.
4. Serwer Proxy aplikacji weryfikuje hello token i pobiera hello główną nazwę użytkownika (UPN) z niego, a następnie wysyła hello żądania, hello UPN, hello toohello nazwy usługi (SPN) łącznika za pośrednictwem uwierzytelnionego dually bezpiecznego kanału.
5. Hello łącznika przeprowadza negocjowanie delegowanie ograniczone protokołu Kerberos (KCD) z hello lokalnego AD personifikacji hello użytkownika tooget aplikacji token toohello protokołu Kerberos.
6. Usługi Active Directory wysyła hello token protokołu Kerberos dla toohello aplikacji hello łącznika.
7. Witaj łącznika wysyła hello oryginalnego żądania toohello serwera aplikacji, za pomocą hello token protokołu Kerberos, który otrzymał z usługi AD.
8. Aplikacja Hello wysyła hello odpowiedzi toohello łącznik, który jest następnie zwracany toohello serwera Proxy aplikacji usługi, a na koniec toohello użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem pracy z logowanie jednokrotne dla aplikacji IWA, upewnij się, środowisko jest gotowe z hello następujące ustawienia i konfiguracje:

* Aplikacji, takich jak aplikacje sieci Web programu SharePoint są ustawione toouse zintegrowane uwierzytelnianie systemu Windows. Aby uzyskać więcej informacji, zobacz [włączyć obsługę uwierzytelniania Kerberos](https://technet.microsoft.com/library/dd759186.aspx), lub dla programu SharePoint, zobacz [planowanie uwierzytelniania Kerberos w programie SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Wszystkie Twoje aplikacje mają [główne nazwy usług](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* uruchomione powitania serwera Hello łącznika i powitania serwera z systemem aplikacji hello są przyłączone do domeny i część hello tej samej domenie lub domenach ufających. Aby uzyskać więcej informacji dotyczących przyłączania do domeny, zobacz [przyłączyć komputer tooa domeny](https://technet.microsoft.com/library/dd807102.aspx).
* Witaj serwerem hello łącznika ma atrybutu TokenGroupsGlobalAndUniversal hello tooread dostępu dla użytkowników. To ustawienie domyślne może negatywnie przez ograniczenie funkcjonalności hello środowiska zabezpieczeń.

### <a name="configure-active-directory"></a>Konfigurowanie usługi Active Directory
Konfiguracja usługi Active Directory Hello różni, hello w zależności od tego, czy łącznik serwera Proxy aplikacji, a serwer aplikacji hello znajdują się w tej samej domenie lub nie.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Łącznik i serwera aplikacji hello — w tej samej domenie
1. W usłudze Active Directory, przejdź zbyt**narzędzia** > **użytkownicy i komputery**.
2. Wybierz serwer hello systemem hello łącznika.
3. Kliknij prawym przyciskiem myszy i wybierz **właściwości** > **delegowania**.
4. Wybierz **Ufaj temu komputerowi w delegowania toospecified tylko usług**. 
5. W obszarze **toowhich usług to konto może okazywać delegowane poświadczenia** dodać wartość hello hello tożsamością SPN serwera aplikacji hello. Dzięki temu użytkownicy tooimpersonate łącznika serwera Proxy aplikacji hello w usłudze AD dla aplikacji hello zdefiniowane na liście hello.

   ![Zrzut ekranu okna właściwości SVR łącznika](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Łącznik i serwera aplikacji w różnych domenach
1. Aby uzyskać listę wymagań wstępnych dotyczących pracy z KCD między domenami, zobacz [ograniczone delegowanie protokołu Kerberos między domenami](https://technet.microsoft.com/library/hh831477.aspx).
2. Użyj hello `principalsallowedtodelegateto` właściwość hello łącznika serwera tooenable powitania serwera Proxy aplikacji toodelegate hello łącznika serwera. Serwer aplikacji Hello `sharepointserviceaccount` i delegowanie serwera hello jest `connectormachineaccount`. W systemie Windows 2012 R2 Użyj tego kodu na przykład:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount może być konto komputera SPS hello lub konta usługi, które hello SPS działa puli aplikacji.

## <a name="configure-single-sign-on"></a>Konfigurowanie rejestracji jednokrotnej 
1. Publikowanie aplikacji zgodnie z instrukcjami toohello opisanego w [publikowania aplikacji za pomocą serwera Proxy aplikacji](application-proxy-publish-azure-portal.md). Upewnij się, że tooselect **usługi Azure Active Directory** jako hello **metoda uwierzytelniania wstępnego**.
2. Po wyświetleniu aplikacji hello listy aplikacji przedsiębiorstwa, zaznacz go i kliknij **logowanie jednokrotne**.
3. Ustaw zbyt hello logowania jednokrotnego w tryb jednego**zintegrowane uwierzytelnianie systemu Windows**.  
4. Wprowadź hello **wewnętrzny SPN aplikacji** powitania serwera aplikacji. W tym przykładzie hello SPN dla opublikowanych aplikacji jest http/www.contoso.com. Ten toobe potrzeb SPN liście hello usług toowhich hello łącznika może okazywać delegowane poświadczenia. 
5. Wybierz hello **delegowane tożsamości logowania** dla toouse łącznika hello w imieniu użytkowników. Aby uzyskać więcej informacji, zobacz [Praca z różnych lokalnymi i tożsamościami w chmurze](#Working-with-different-on-premises-and-cloud-identities)

   ![Konfiguracja zaawansowanych aplikacji](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Logowanie Jednokrotne dla aplikacji z systemem innym niż Windows
Hello przepływ delegowania protokołu Kerberos w serwera Proxy aplikacji usługi Azure AD rozpoczyna się, gdy usługa Azure AD uwierzytelnia użytkownika hello w chmurze hello. Po hello żądanie dociera lokalnymi, hello aplikacji serwera Proxy Azure AD connector wystawia biletu protokołu Kerberos w imieniu użytkownika hello przez interakcji z hello lokalnej usługi Active Directory. Ten proces jest określony tooas, delegowanie ograniczone protokołu Kerberos (KCD). W hello następnej fazy, żądanie zostanie wysłane toohello wewnętrznej bazy danych aplikacji przy użyciu tego biletu protokołu Kerberos. Istnieje kilka protokołów, które definiują sposób toosend takich żądań. Większość serwerów z systemem innym niż Windows oczekiwać Negotiate/SPNego, która jest teraz obsługiwana na serwera Proxy aplikacji usługi Azure AD.

Aby uzyskać więcej informacji o protokole Kerberos, zobacz [wszystkie mają tooknow o protokołu Kerberos ograniczonego delegowania (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Aplikacje systemu Windows bez zwykle użytkownika nazwy użytkowników lub nazwy konta SAM zamiast domeny adresów e-mail. Tej sytuacji tooyour aplikacji, należy tooconfigure hello delegowane logowania tożsamości pola tooconnect Twojej tożsamości aplikacji w chmurze tożsamości tooyour. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Praca z różnych lokalnymi i tożsamościami w chmurze
Serwer Proxy aplikacji zakłada, że użytkownicy mają dokładnie hello tej samej tożsamości w chmurze hello i lokalnych. Jeśli nie jest to przypadek hello, można nadal służy KCD dla logowania jednokrotnego. Skonfiguruj **delegowane tożsamości logowania** dla każdego toospecify aplikacji powinny być używane tożsamość, podczas wykonywania logowania jednokrotnego.  

Ta funkcja umożliwia wiele organizacji, które mają różne lokalnymi i w chmurze tożsamości toohave rejestracji Jednokrotnej z aplikacji tooon lokalne powitania w chmurze bez konieczności hello użytkowników tooenter różne nazwy użytkowników i hasła. Dotyczy to również organizacjom który:

* Wewnętrznie mają kilka domen (joe@us.contoso.com, joe@eu.contoso.com) i w chmurze hello pojedynczej domeny (joe@contoso.com).
* Wewnętrznie mają nazwy domeny bez obsługi routingu (joe@contoso.usa) i prawnych w chmurze hello.
* Nie używaj nazw domen wewnętrznie (Jan)
* Użyj innych aliasów lokalnych i w chmurze hello. Na przykład joe-johns@contoso.com vs.joej@contoso.com  

Dzięki serwerowi Proxy aplikacji można wybrać które tożsamości toouse tooobtain hello biletu Kerberos. To ustawienie jest na aplikację. Niektóre z tych opcji nadają się do systemów, które nie akceptują format adresu e-mail, inne są zaprojektowane dla alternatywnej nazwy logowania.

![Zrzut ekranu parametr tożsamości delegowanego logowania](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Jeśli używana jest tożsamość delegowanego logowania, wartość hello nie muszą być unikatowe we wszystkich domenach hello lub lasom w organizacji. Aby uniknąć tego problemu, należy publikowania aplikacji, te dwa razy przy użyciu dwóch różnych grup łącznika. Ponieważ każda aplikacja ma odbiorców innego użytkownika, możesz ponadto dołączyć do jego łączniki tooa inną domenę.

### <a name="configure-sso-for-different-identities"></a>Konfigurowanie logowania jednokrotnego dla różnych tożsamości
1. Konfigurowanie ustawień usługi Azure AD Connect tożsamość główna hello jest adresem e-mail hello (poczta). Jest to realizowane jako część hello dostosowania procesu, zmieniając hello **główna nazwa użytkownika** w hello ustawień synchronizacji. Te ustawienia określają również, jak użytkownicy logują się tooOffice365, Windows10 urządzenia i inne aplikacje, które używają usługi Azure AD jako magazynu ich tożsamości.  
   ![Identyfikowanie użytkowników zrzut ekranu — Lista rozwijana główna nazwa użytkownika](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. W ustawieniach konfiguracji aplikacji hello aplikacji hello chcesz toomodify, wybierz opcję hello **delegowane tożsamości logowania** toobe używany:

   * Nazwa główna użytkownika (na przykład joe@contoso.com)
   * Alternatywna nazwa główna użytkownika (na przykład joed@contoso.local)
   * Nazwa użytkownika, część główna nazwa użytkownika (na przykład Jan)
   * Część nazwy użytkownika alternatywna nazwa główna użytkownika (na przykład joed)
   * Nazwa konta SAM lokalnymi (zależy od konfiguracji kontrolera domeny hello)

### <a name="troubleshooting-sso-for-different-identities"></a>Rozwiązywanie problemów z logowania jednokrotnego dla różnych tożsamości
Jeśli występuje błąd w hello procesu logowania jednokrotnego, wydaje się w dzienniku zdarzeń maszyny łącznika hello zgodnie z objaśnieniem w [Rozwiązywanie problemów](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Jednak w niektórych przypadkach hello pomyślnie wysłaniu żądania toohello zaplecza aplikacji podczas odpowiada tej aplikacji w różnych odpowiedzi HTTP. Rozwiązywanie problemów z tych przypadkach należy zacząć od badanie numer zdarzenia 24029 na maszynie łącznika hello w dzienniku zdarzeń w sesji serwera Proxy aplikacji hello. pole "użytkownika" hello w ramach szczegółów zdarzenia hello zostanie Hello tożsamości użytkownika, którego użyto do delegowania. Wybierz tooturn na dziennika sesji **wyświetlanie analityczne i debugowania dzienniki** w menu Widok podglądu zdarzeń hello.

## <a name="next-steps"></a>Następne kroki

* [Jak tooconfigure toouse aplikacji serwera Proxy aplikacji ograniczone delegowanie protokołu Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)


Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)

