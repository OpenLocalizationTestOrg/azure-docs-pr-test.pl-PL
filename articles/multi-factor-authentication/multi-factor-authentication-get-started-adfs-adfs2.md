---
title: "aaaUse serwera usługi Azure MFA z usługami AD FS 2.0 | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA i usług AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Konfigurowanie serwera usługi Azure Multi-Factor Authentication toowork z usługami AD FS 2.0
W tym artykule jest przeznaczony dla organizacji, które są Sfederowanych z usługą Azure Active Directory i chcesz toosecure zasoby, które są lokalnie lub w chmurze hello. Ochrona zasobów z wykorzystaniem powitania serwera usługi Azure Multi-Factor Authentication i konfigurowania jej toowork z usługami AD FS co weryfikacji dwuetapowej zostanie wywołany przez punkty końcowe wysokiej wartości.

Ta dokumentacja obejmuje przy użyciu powitania serwera usługi Azure Multi-Factor Authentication z usługami AD FS 2.0. Aby dowiedzieć się więcej na temat usług AD FS, zobacz [Zabezpieczanie zasobów w chmurze i lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS systemu Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Zabezpieczanie usługi AD FS 2.0 przy użyciu serwera proxy
toosecure usług AD FS 2.0 z serwera proxy, zainstaluj powitania serwera usługi Azure Multi-Factor Authentication na serwerze proxy hello AD FS.

### <a name="configure-iis-authentication"></a>Konfigurowanie uwierzytelniania usług IIS
1. Na powitania serwera usługi Azure Multi-Factor Authentication kliknij hello **uwierzytelniania usług IIS** ikonę w menu po lewej stronie powitania.
2. Kliknij przycisk hello **opartej na formularzu** kartę.
3. Kliknij pozycję **Dodaj**.

   <center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. zmienne nazwy użytkownika, hasło i domenę toodetect automatycznie, wprowadź adres URL logowania hello (na przykład https://sso.contoso.com/adfs/ls) w ramach okno dialogowe hello automatyczna konfiguracja witryny i kliknij przycisk **OK**.
5. Sprawdź hello **dopasowania użytkownika wymagane uwierzytelnianie wieloskładnikowe Azure** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane do powitania serwera i podmiotu tootwo krok weryfikacji. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z weryfikacji dwuetapowej, nie zaznaczaj hello pola wyboru.
6. Jeśli nie można automatycznie wykryć hello zmiennych strony, kliknij przycisk hello **Określ ręcznie...** przycisk w oknie dialogowym hello automatyczna konfiguracja witryny.
7. Okno dialogowe Dodawanie witryny opartej hello wprowadź strony logowania hello adresu URL toohello AD FS w polu Prześlij adres URL hello (na przykład https://sso.contoso.com/adfs/ls), a następnie wprowadź nazwę aplikacji (opcjonalnie). Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.
8. Ustaw format żądania hello zbyt**POST lub GET**.
9. Wprowadź hello zmienna nazwy użytkownika (UsernameTextBox$ $ContentPlaceHolder1 ctl00) i zmienna hasła (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Jeśli Twoja strona logowania opartej na formularzu są wyświetlane pole tekstowe domeny, wprowadź hello domeny oraz zmienną. toofind hello nazwy pól wejściowych hello na powitania strony logowania, strony logowania toohello Przejdź w przeglądarce sieci web, kliknij prawym przyciskiem myszy na stronie powitania i wybierz **Wyświetl źródło**.
10. Sprawdź hello **dopasowania użytkownika wymagane uwierzytelnianie wieloskładnikowe Azure** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane do powitania serwera i podmiotu tootwo krok weryfikacji. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z weryfikacji dwuetapowej, nie zaznaczaj hello pola wyboru.
    <center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Kliknij pozycję **Zaawansowane**, tooreview ustawienia zaawansowane. Ustawienia, które można skonfigurować, to:

    - Wybór pliku niestandardowej strony odmowy
    - Pamięć podręczna informacji o pomyślnym uwierzytelnieniu toohello witryny internetowej przy użyciu plików cookie
    - Wybierz sposób tooauthenticate hello poświadczenia podstawowego

12. Ponieważ serwer proxy hello AD FS nie jest to prawdopodobnie toobe przyłączone do domeny toohello, można użyć kontrolera domeny tooyour tooconnect LDAP dla użytkownika i wstępnego uwierzytelniania. W powitalne okno dialogowe Zaawansowana witryna sieci Web, kliknij przycisk hello **uwierzytelniania podstawowego** i wybierz **wiązania LDAP** dla hello typ uwierzytelniania wstępnego uwierzytelniania.
13. Po zakończeniu kliknij przycisk **OK** okno dialogowe Dodawanie witryny opartej toohello tooreturn.
14. Kliknij przycisk **OK** hello tooclose — okno dialogowe.
15. Raz hello adresu URL i zmienne strony zostały wykryte lub wprowadzony, hello witryny sieci Web dane są wyświetlane w hello panelu opartej na formularzu.
16. Kliknij przycisk hello **modułu macierzystego** karcie i wybierz powitania serwera, witryny hello hello AD FS z serwera proxy jest uruchomiona w obszarze (takich jak "Default Web Site"), lub hello usług AD FS serwera proxy aplikacji (na przykład "ls" w obszarze "usług AD FS") tooenable hello wtyczki na powitania usług IIS żądany poziom.
17. Kliknij przycisk hello **uwierzytelniania Włącz usługi IIS** pole u góry hello hello ekranu.

Uwierzytelnianie usług IIS Hello jest teraz włączony.

### <a name="configure-directory-integration"></a>Konfigurowanie integracji katalogu
Włączona uwierzytelnianie usług IIS, ale tooperform hello wstępnego uwierzytelniania tooyour Active Directory (AD) za pośrednictwem protokołu LDAP, należy skonfigurować hello kontrolera domeny toohello połączenia LDAP.

1. Kliknij przycisk hello **integracji katalogów** ikony.
2. Na karcie Ustawienia hello wybierz hello **użyj konkretnej konfiguracji LDAP** przycisk radiowy.

   <center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Kliknij pozycję **Edytuj**.
4. Okno dialogowe Edycja konfiguracji katalogu LDAP hello należy wypełnić pola hello z kontrolerem domeny hello informacje wymagane tooconnect toohello AD. Opisy hello pola znajdują się w pliku pomocy powitania serwera usługi Azure Multi-Factor Authentication.
5. Testuj połączenie LDAP hello klikając hello **testu** przycisku.

   <center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Jeśli test połączenia LDAP hello zakończyło się pomyślnie, kliknij przycisk **OK**.

### <a name="configure-company-settings"></a>Konfigurowanie ustawień firmy
1. Następnie kliknij przycisk hello **ustawienia firmy** ikony, jak i wybierz hello **rozpoznawanie nazwy użytkownika** kartę.
2. Wybierz hello **atrybutu unikatowego identyfikatora użyj katalogu LDAP w celu dopasowania nazw użytkowników** przycisk radiowy.
3. Jeśli użytkownicy wprowadzić swoją nazwę użytkownika w formacie "domena azwa_użytkownika", powitania serwera musi toobe toostrip stanie hello domeny poza hello username podczas tworzenia zapytania LDAP hello. Można to skonfigurować za pomocą ustawienia rejestru.
4. Otwórz Edytor rejestru hello i przejdź tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/dodatnie sieci/PhoneFactor na serwerze 64-bitowym. Jeśli na serwerze 32-bitowych zająć hello "Wow6432Node" poza hello ścieżki. Utwórz DWORD klucza rejestru o nazwie "UsernameCxz_stripPrefixDomain" i ustaw hello too1 wartość. Uwierzytelnianie wieloskładnikowe platformy Azure jest teraz zabezpieczanie proxy hello usług AD FS.

Upewnij się, że użytkownicy zostały zaimportowane z usługi Active Directory na powitania serwera. Zobacz hello [sekcji zaufanych adresów IP](#trusted-ips) Jeśli chcesz toowhitelist wewnętrznych adresów IP, weryfikację dwuetapową nie jest wymagana podczas logowania w witrynie sieci Web toohello z tych lokalizacjach.

<center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>Bezpośrednie używanie usług AD FS 2.0 bez serwera proxy
Serwer proxy hello AD FS nie jest używana, można zabezpieczyć usług AD FS. Zainstaluj powitania serwera usługi Azure Multi-Factor Authentication na serwerze hello usług AD FS i skonfigurować powitalne serwera na powitania następujące kroki:

1. W ramach hello Azure aplikacji serwer Multi-Factor Authentication, kliknij przycisk hello **uwierzytelniania usług IIS** ikonę w menu po lewej stronie powitania.
2. Kliknij przycisk hello **HTTP** kartę.
3. Kliknij pozycję **Dodaj**.
4. W powitalne okno dialogowe Dodawanie podstawowego adresu URL wprowadź adres URL hello hello witryny sieci Web usług AD FS gdzie HTTP uwierzytelniania (na przykład https://sso.domain.com/adfs/ls/auth/integrated) do hello pole podstawowego adresu URL. Następnie wprowadź nazwę aplikacji (opcjonalnie). Nazwa aplikacji Hello jest wyświetlana w raportach usługi Azure Multi-Factor Authentication i może być wyświetlany w komunikatach uwierzytelniania wiadomości SMS lub aplikacji mobilnej.
5. W razie potrzeby można dostosować limit czasu bezczynności hello i maksymalnej długości sesji.
6. Sprawdź hello **dopasowania użytkownika wymagane uwierzytelnianie wieloskładnikowe Azure** Jeśli wszyscy użytkownicy zostały lub zostaną zaimportowane do powitania serwera i podmiotu tootwo krok weryfikacji. Jeśli duża liczba użytkowników nie zostały zaimportowane na powitania serwera i/lub będą wykluczone z weryfikacji dwuetapowej, nie zaznaczaj hello pola wyboru.
7. Zaznacz pole pamięci podręcznej plików cookie hello, w razie potrzeby.

   <center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Kliknij przycisk **OK**.
9. Kliknij przycisk hello **modułu macierzystego** kartę i hello wybierz serwer, hello witryny sieci Web (takie jak "Default Web Site") lub hello usług AD FS aplikację (na przykład "ls" w obszarze "usług AD FS") tooenable hello IIS wtyczki na powitania żądany poziom.
10. Kliknij przycisk hello **uwierzytelniania Włącz usługi IIS** pole u góry hello hello ekranu.

Po wykonaniu tych czynności usługi AD FS są chronione przez usługę Azure Multi-Factor Authentication.

Upewnij się, że użytkownicy zostały zaimportowane z usługi Active Directory na powitania serwera. Zobacz adresy hello sekcji zaufanych adresów IP, jeśli chcesz toowhitelist wewnętrznym adresem IP, aby weryfikacji dwuetapowej nie jest wymagana podczas logowania w witrynie sieci Web toohello z tych lokalizacjach.

## <a name="trusted-ips"></a>Zaufane adresy IP
Listę zaufanych adresów IP umożliwiają użytkownikom toobypass Azure Multi-Factor Authentication dla żądań witryny sieci Web pochodzących z określonych adresów IP lub podsieci. Na przykład można tooexempt użytkownikom weryfikacji dwuetapowej podczas logowania się biurze hello. W tym celu należy określić podsieć biura hello jako wpis zaufanych adresów IP.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure zaufanych adresów IP
1. W hello sekcji uwierzytelnianie usług IIS, kliknij przycisk hello **zaufanych adresów IP** kartę.
2. Kliknij przycisk hello **Dodaj...** Dodaj...
3. Gdy pojawi się okno dialogowe Dodawanie adresów IP zaufanych hello, wybierz jedną z hello **pojedynczy adres IP**, **zakres adresów IP**, lub **podsieci** przyciski radiowe.
4. Wprowadź hello adres IP, zakresu adresów IP lub podsieci, która powinna być białej. Wprowadzania podsieci, wybierz hello odpowiednią maskę sieci, a następnie kliknij przycisk hello **OK** przycisku. Witaj zaufanych IP zostali dodani.

<center>![Konfiguracja](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
