---
title: "aaaIIS uwierzytelniania i serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to strona uwierzytelnianie wieloskładnikowe Azure hello przydatnej wdrażania uwierzytelniania IIS i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Konfigurowanie serwera usługi Azure Multi-Factor Authentication na potrzeby aplikacji sieci Web usług IIS

Użyj sekcji uwierzytelniania w usługach IIS hello hello tooenable serwera usługi Azure Multi-Factor Authentication (MFA) i skonfiguruj uwierzytelniania usług IIS w celu integracji z aplikacjami sieci web Microsoft IIS. powitania serwera usługi Azure MFA instaluje wtyczkę, która pozwala na filtrowanie żądań wysyłanych toohello IIS sieci web serwera tooadd Azure Multi-Factor Authentication. Witaj wtyczki programu IIS zapewnia obsługę uwierzytelniania za pomocą formularza i zintegrowane uwierzytelnianie HTTP systemu Windows. Zaufanych adresów IP mogą być również skonfigurowany tooexempt adresów IP z uwierzytelniania dwuskładnikowego.

![Uwierzytelnianie usług IIS](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Używanie uwierzytelniania usług IIS opartego na formularzach z serwerem usługi Azure Multi-Factor Authentication
toosecure IIS sieci web aplikacji korzystającej z uwierzytelniania opartego na formularzu, zainstalować powitania serwera usługi Azure Multi-Factor Authentication na serwerze sieci web usług IIS hello i skonfigurować hello serwera na powitania następujące procedury:

1. Na powitania serwera usługi Azure Multi-Factor Authentication kliknij ikonę uwierzytelnianie usług IIS hello w menu po lewej stronie powitania.
2. Kliknij przycisk hello **opartej na formularzu** kartę.
3. Kliknij pozycję **Dodaj**.
4. zmienne nazwy użytkownika, hasło i domenę toodetect automatycznie, wprowadź hello adresu URL logowania (na przykład https://localhost/contoso/auth/login.aspx) w ramach okno dialogowe hello automatyczna konfiguracja witryny i kliknij przycisk **OK**.
5. Sprawdź hello **dopasowania użytkownika wymagają uwierzytelniania wieloskładnikowego** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane na powitania serwera i uwierzytelniania wieloskładnikowego toomulti podmiotu. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z uwierzytelniania wieloskładnikowego, nie zaznaczaj hello pola wyboru.
6. Nie można automatycznie wykryć hello zmiennych strony, kliknij przycisk **Określ ręcznie** w oknie dialogowym hello automatyczna konfiguracja witryny.
7. Okno dialogowe Dodawanie witryny opartej hello, strony logowania toohello adres URL hello hello adresu URL przesyłania pola i wprowadź nazwę aplikacji (opcjonalnie). Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.
8. Wybierz hello poprawny format żądania. Ta opcja jest ustawiona zbyt**POST lub GET** dla większości aplikacji sieci web.
9. Wprowadź hello zmienna nazwy użytkownika, zmienna hasła i zmienna domeny (jeśli jest on wyświetlany na stronie logowania hello). nazwy hello toofind hello pól wejściowych, przejdź toohello stronę logowania w przeglądarce sieci web, kliknij prawym przyciskiem myszy na stronie powitania i wybierz **Wyświetl źródło**.
10. Sprawdź hello **dopasowania użytkownika wymagane uwierzytelnianie wieloskładnikowe Azure** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane na powitania serwera i uwierzytelniania wieloskładnikowego toomulti podmiotu. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z uwierzytelniania wieloskładnikowego, nie zaznaczaj hello pola wyboru.
11. Kliknij przycisk **zaawansowane** tooreview Zaawansowane ustawienia, w tym:

  - Wybór pliku niestandardowej strony odmowy
  - Pamięć podręczna informacji o pomyślnym uwierzytelnieniu toohello witryny sieci Web w danym okresie czasu plików cookie
  - Określ, czy poświadczenia podstawowego hello tooauthenticate względem domeny systemu Windows, katalogiem LDAP. czy serwera RADIUS.

12. Kliknij przycisk **OK** okno dialogowe Dodawanie witryny opartej toohello tooreturn.
13. Kliknij przycisk **OK**.
14. Raz hello adresu URL i zmienne strony zostały wykryte lub wprowadzony, hello witryny sieci Web dane są wyświetlane w hello panelu opartej na formularzu.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Używanie zintegrowanego uwierzytelniania systemu Windows z serwerem usługi Azure Multi-Factor Authentication
toosecure IIS sieci web aplikacji wykorzystującej uwierzytelnianie zintegrowane systemu Windows HTTP, zainstalować powitania serwera usługi Azure MFA na serwerze sieci web usług IIS hello, a następnie skonfigurować hello serwera z hello następujące kroki:

1. Na powitania serwera usługi Azure Multi-Factor Authentication kliknij ikonę uwierzytelnianie usług IIS hello w menu po lewej stronie powitania.
2. Kliknij przycisk hello **HTTP** kartę.
3. Kliknij pozycję **Dodaj**.
4. W powitalne okno dialogowe Dodawanie podstawowego adresu URL wprowadź adres URL hello hello witryny sieci Web, którym jest przeprowadzana uwierzytelniania HTTP (na przykład http://localhost/owa) i podaj nazwę aplikacji (opcjonalnie). Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.
5. Dostosuj hello limit czasu bezczynności i maksymalnej długości sesji Jeśli hello domyślne nie są wystarczające.
6. Sprawdź hello **dopasowania użytkownika wymagają uwierzytelniania wieloskładnikowego** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane na powitania serwera i uwierzytelniania wieloskładnikowego toomulti podmiotu. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z uwierzytelniania wieloskładnikowego, nie zaznaczaj hello pola wyboru.
7. Sprawdź hello **pamięci podręcznej plików Cookie** polu w razie potrzeby.
8. Kliknij przycisk **OK**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Włączanie wtyczek IIS dla serwera usługi Azure Multi-Factor Authentication
Po skonfigurowaniu hello opartej na formularzu lub adresów URL protokołu HTTP uwierzytelniania i ustawienia, wybierz opcję hello którym załadowane i włączone w usługach IIS hello Azure Multi-Factor Authentication w usługach IIS dodatków plug-in. Użyj hello następujące procedury:

1. Jeśli uruchomiony w usługach IIS 6, kliknij hello **ISAPI** kartę. Wybierz hello witryny sieci Web, która hello aplikacji sieci web jest uruchomiona w obszarze (np. Domyślna witryna sieci Web) tooenable hello Azure usługi Multi-Factor Authentication filtru ISAPI wtyczki dla tej lokacji.
2. Jeśli uruchomiony w usługach IIS 7 lub nowszego, kliknij hello **modułu macierzystego** kartę. Wybierz powitania serwera, witryny sieci Web lub aplikacji hello tooenable wtyczki usług IIS na potrzeby hello poziomach.
3. Kliknij przycisk hello **uwierzytelniania Włącz usługi IIS** pole u góry hello hello ekranu. Uwierzytelnianie wieloskładnikowe platformy Azure jest teraz zabezpieczanie hello wybrane aplikacji usług IIS. Upewnij się, że użytkownicy zostały zaimportowane na powitania serwera.

## <a name="trusted-ips"></a>Zaufane adresy IP
Witaj zaufanych adresów IP umożliwia użytkownikom toobypass Azure Multi-Factor Authentication dla żądań witryny sieci Web pochodzących z określonych adresów IP lub podsieci. Na przykład można tooexempt użytkowników z usługi Azure Multi-Factor Authentication podczas logowania się z hello pakietu office. W tym celu należy określić podsieć biura hello jako wpis zaufanych adresów IP. tooconfigure zaufanych adresów IP, należy użyć hello następujące procedury:

1. W hello sekcji uwierzytelnianie usług IIS, kliknij przycisk hello **zaufanych adresów IP** kartę.
2. Kliknij pozycję **Dodaj**.
3. Gdy pojawi się okno dialogowe Dodawanie adresów IP zaufanych hello, wybierz hello **pojedynczy adres IP**, **zakres adresów IP**, lub **podsieci** przycisk radiowy.
4. Wprowadź adres IP hello, zakres adresów IP lub podsieci, która powinna być białej. Wprowadzanie podsieci, wybierz hello odpowiednią maskę sieci, a następnie kliknij przycisk **OK**. Lista dozwolonych adresów Hello został dodany.
