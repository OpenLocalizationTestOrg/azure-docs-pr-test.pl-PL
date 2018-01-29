---
title: "Serwer MFA z usługami AD FS w systemie Windows Server | Microsoft Docs"
description: "Ten artykuł zawiera wprowadzenie do usługi Azure Multi-Factor Authentication i usług AD FS w systemie Windows Server 2012 R2 i 2016."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60e6737533e946512ae9b8e1e251e7bd6c9d0fe5
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="configure-azure-multi-factor-authentication-server-to-work-with-ad-fs-in-windows-server"></a>Konfigurowanie serwera usługi Azure Multi-Factor Authentication do współdziałania z usługami AD FS w systemie Windows Server
Jeśli korzystasz z usług federacyjnych Active Directory (AD FS) i chcesz zabezpieczyć zasoby chmurowe lub lokalne, możesz skonfigurować serwer Azure Multi-Factor Authentication do pracy z usługami AD FS. Ta konfiguracja wyzwala weryfikację dwuetapową dla punktów końcowych o wysokiej wartości.

W tym artykule omawiane jest korzystanie z serwera usługi Azure Multi-Factor Authentication oraz usług AD FS w systemie Windows Server 2012 R2 lub Windows Server 2016. Aby uzyskać dodatkowe informacje, przeczytaj o sposobie [zabezpieczania zasobów w chmurze i zasobów lokalnych przy użyciu serwera Azure Multi-Factor Authentication z usługami AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Zabezpieczanie usług AD FS systemu Windows Server za pomocą serwera usługi Azure Multi-Factor Authentication
Podczas instalowania serwera usługi Azure Multi-Factor Authentication dostępne są następujące opcje:

* Lokalna instalacja serwera usługi Azure Multi-Factor Authentication na tym samym serwerze, na którym zainstalowano usługi AD FS.
* Lokalna instalacja adaptera usługi Azure Multi-Factor Authentication na serwerze usług AD FS, a następnie instalacja serwera Multi-Factor Authentication na innym komputerze.

Przed rozpoczęciem należy uwzględnić następujące informacje:

* Nie musisz instalować serwera usługi Azure Multi-Factor Authentication na serwerze usług AD FS. Należy jednak zainstalować adapter usługi Multi-Factor Authentication dla usług AD FS w systemie Windows Server 2012 R2 lub Windows Server 2016, w którym działa usługa AD FS. Serwer można zainstalować na innym komputerze, jeśli przeprowadzisz instalację adaptera AD FS na oddzielnym serwerze federacyjnym usług AD FS. Zapoznaj się z poniższymi procedurami, aby dowiedzieć się, jak oddzielnie zainstalować adapter.
* Jeśli organizacja używa weryfikacji za pomocą wiadomości tekstowych lub aplikacji mobilnej, ciągi zdefiniowane w ustawieniach firmy zawierają symbol zastępczy <$*application_name*$>. Na serwerze usługi MFA w wersji 7.1 możesz podać nazwę aplikacji, która zastępuje ten symbol zastępczy. W wersji 7.0 i starszych ten symbol zastępczy nie jest automatycznie zastępowany w przypadku korzystania z adaptera usług AD FS. W przypadku starszych wersji usuń symbol zastępczy z odpowiednich ciągów podczas zabezpieczania usług AD FS.
* Konto używane do logowania musi mieć uprawnienia użytkownika do tworzenia grup zabezpieczeń w usłudze Active Directory.
* Kreator instalacji adaptera AD FS usługi Multi-Factor Authentication tworzy grupę zabezpieczeń o nazwie PhoneFactor Admins w Twoim wystąpieniu usługi Active Directory. Następnie do tej grupy zostaje dodane konto usług AD FS usługi federacyjnej. Sprawdź, czy grupa PhoneFactor Admins została utworzona na kontrolerze domeny oraz czy konto usług AD FS jest członkiem tej grupy. W razie potrzeby ręcznie dodaj konto usług AD FS do grupy PhoneFactor Admins w ramach kontrolera domeny.
* Informacje dotyczące instalowania zestawu SDK usługi internetowej w portalu użytkownika można znaleźć w temacie [Deploying the user portal for the Azure Multi-Factor Authentication Server (Wdrażanie portalu użytkownika dla serwera Azure Multi-Factor Authentication)](multi-factor-authentication-get-started-portal.md).

### <a name="install-azure-multi-factor-authentication-server-locally-on-the-ad-fs-server"></a>Instalowanie serwera Azure Multi-Factor Authentication lokalnie na serwerze usług AD FS
1. Pobierz serwer Azure Multi-Factor Authentication i zainstaluj go na serwerze usług AD FS. Aby uzyskać informacje dotyczące instalacji, przeczytaj o [wprowadzeniu do serwera Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. W konsoli zarządzania serwerem usługi Azure Multi-Factor Authentication kliknij ikonę **AD FS**. Wybierz opcje **Zezwalaj na rejestrację użytkownika** i **Zezwalaj użytkownikom na wybór metody**.
3. Wybierz wszystkie dodatkowe opcje, które chcesz określić dla Twojej organizacji.
4. Kliknij pozycję **Zainstaluj adapter ADFS**.
   
   <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Jeśli zostanie wyświetlone okno usługi Active Directory, oznacza to dwie rzeczy. Komputer jest przyłączony do domeny, a konfiguracja usługi Active Directory pod kątem zabezpieczenia komunikacji między adapterem AD FS a usługą Multi-Factor Authentication nie została ukończona. Kliknij przycisk **Dalej**, aby przeprowadzić tę konfigurację automatycznie, lub zaznacz pole wyboru **Pomiń automatyczną konfigurację usługi Active Directory i skonfiguruj ustawienia ręcznie**. Kliknij przycisk **Dalej**.
6. Jeśli zostanie wyświetlone okno grupy lokalnej, oznacza to dwie rzeczy. Komputer nie jest przyłączony do domeny, a konfiguracja grupy lokalnej pod kątem zabezpieczenia komunikacji między adapterem AD FS a usługą Multi-Factor Authentication nie została ukończona. Kliknij przycisk **Dalej**, aby przeprowadzić tę konfigurację automatycznie, lub zaznacz pole wyboru **Pomiń automatyczną konfigurację grupy lokalnej i skonfiguruj ustawienia ręcznie**. Kliknij przycisk **Dalej**.
7. W Kreatorze instalacji kliknij przycisk **Dalej**. Serwer Azure Multi-Factor Authentication tworzy grupę PhoneFactor Admins i dodaje do niej konto usług AD FS.
   <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Na stronie **Uruchamianie instalatora** kliknij przycisk **Dalej**.
9. W oknie instalatora adaptera AD FS usługi Multi-Factor Authentication kliknij przycisk **Dalej**.
10. Po zakończeniu instalacji kliknij przycisk **Zamknij**.
11. Po zainstalowaniu adaptera należy zarejestrować go za pomocą usług AD FS. Uruchom program Windows PowerShell i uruchom następujące polecenie:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. Aby używać nowo zarejestrowanego adaptera, edytuj globalne zasady uwierzytelniania w usługach AD FS. W konsoli zarządzania usług AD FS przejdź do węzła **Zasady uwierzytelniania**. W sekcji **Uwierzytelnianie wieloskładnikowe** kliknij link **Edytuj** obok sekcji **Ustawienia globalne**. W oknie **Edytowanie globalnych zasad uwierzytelniania** wybierz pozycję **Uwierzytelnianie wieloskładnikowe** jako dodatkową metodę uwierzytelniania, a następnie kliknij przycisk **OK**. Adapter zostanie zarejestrowany jako element WindowsAzureMultiFactorAuthentication. Uruchom ponownie usługę AD FS, aby zmiany wprowadzone w ramach rejestracji zaczęły obowiązywać.

<center>![Chmura](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

Serwer usługi Multi-Factor Authentication jest teraz skonfigurowany jako dodatkowy dostawca uwierzytelniania do używania z usługami AD FS.

## <a name="install-a-standalone-instance-of-the-ad-fs-adapter-by-using-the-web-service-sdk"></a>Instalowanie wystąpienia autonomicznego adaptera AD FS za pomocą zestawu SDK usługi sieci Web
1. Zainstaluj zestaw SDK usługi sieci Web na serwerze z uruchomionym serwerem Multi-Factor Authentication.
2. Skopiuj następujące pliki z katalogu \Program Files\Multi-Factor Authentication Server na serwer, na którym planujesz zainstalować adapter AD FS:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Uruchom plik instalacyjny MultiFactorAuthenticationAdfsAdapterSetup64.msi.
4. W oknie instalatora adaptera AD FS usługi Multi-Factor Authentication kliknij przycisk **Dalej**, aby rozpocząć instalację.
5. Po zakończeniu instalacji kliknij przycisk **Zamknij**.

## <a name="edit-the-multifactorauthenticationadfsadapterconfig-file"></a>Edytowanie pliku MultiFactorAuthenticationAdfsAdapter.config
Edytuj plik MultiFactorAuthenticationAdfsAdapter.config, wykonując następujące czynności:

1. Dla węzła **UseWebServiceSdk** ustaw wartość **true**.  
2. Dla węzła **WebServiceSdkUrl** ustaw adres URL zestawu SDK usługi sieci Web usługi Multi-Factor Authentication. Na przykład: *https://contoso.com/&lt;nazwa_certyfikatu&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, gdzie *nazwa_certyfikatu* to nazwa certyfikatu.  
3. Zmodyfikuj skrypt Register-MultiFactorAuthenticationAdfsAdapter.ps1, dodając ciąg `-ConfigurationFilePath &lt;path&gt;` na końcu polecenia `Register-AdfsAuthenticationProvider`, gdzie *&lt;path&gt;* jest pełną ścieżką do pliku MultiFactorAuthenticationAdfsAdapter.config.

### <a name="configure-the-web-service-sdk-with-a-username-and-password"></a>Konfigurowanie zestawu SDK usługi sieci Web przy użyciu nazwy użytkownika i hasła
Istnieją dwie opcje konfigurowania zestawu SDK usługi sieci Web. Pierwsza opcja to konfiguracja przy użyciu nazwy użytkownika i hasła, a druga — przy użyciu certyfikatu klienta. Wykonaj następujące kroki, aby skorzystać z pierwszej opcji, lub przejdź dalej, aby skorzystać z drugiej opcji.  

1. Jako wartość węzła **WebServiceSdkUsername** ustaw konto należące do grupy zabezpieczeń PhoneFactor Admins. Użyj formatu &lt;domena&gt;&#92;&lt;nazwa_użytkownika&gt;.  
2. Jako wartość węzła **WebServiceSdkPassword** ustaw odpowiednie hasło do konta.

### <a name="configure-the-web-service-sdk-with-a-client-certificate"></a>Konfigurowanie zestawu SDK usługi sieci Web przy użyciu certyfikatu klienta
Jeśli nie chcesz używać nazwy użytkownika i hasła, wykonaj następujące czynności, aby skonfigurować zestaw SDK usługi sieci Web przy użyciu certyfikatu klienta.

1. Uzyskaj certyfikat klienta z urzędu certyfikacji dla serwera, na którym uruchomiony jest zestaw SDK usługi sieci Web. Dowiedz się, jak [uzyskać certyfikaty klientów](https://technet.microsoft.com/library/cc770328.aspx).  
2. Zaimportuj certyfikat klienta do osobistego magazynu certyfikatów komputera lokalnego na serwerze, na którym uruchomiony jest zestaw SDK usługi sieci Web. Upewnij się, że certyfikat publiczny urzędu certyfikacji znajduje się w magazynie certyfikatów zaufanych certyfikatów głównych.  
3. Wyeksportuj klucz publiczny i prywatny certyfikatu klienta do pliku pfx.  
4. Wyeksportuj klucz publiczny do pliku cer w formacie Base64.  
5. W Menedżerze serwera sprawdź, czy zainstalowana jest funkcja Serwer sieci Web (IIS)\Serwer sieci Web\Zabezpieczenia\Uwierzytelnianie mapowań certyfikatów klientów za pośrednictwem usług IIS. Jeśli ta funkcja nie jest zainstalowana, wybierz pozycję **Dodaj role i funkcje**, aby ją dodać.  
6. W Menedżerze usług IIS kliknij dwukrotnie składnik **Edytor konfiguracji** w witrynie sieci Web, która zawiera katalog wirtualny zestawu SDK usługi sieci Web. Ważne jest, aby wybrać witrynę sieci Web, a nie katalog wirtualny.  
7. Przejdź do sekcji **system.webServer/security/authentication/iisClientCertificateMappingAuthentication**.  
8. Ustaw węzeł enabled na wartość **true**.  
9. Ustaw węzeł oneToOneCertificateMappingsEnabled na wartość **true**.  
10. Kliknij przycisk **...** obok pozycji oneToOneMappings, a następnie kliknij link **Dodaj**.  
11. Otwórz wyeksportowany wcześniej plik cer w formacie Base64. Usuń wiersze *-----BEGIN CERTIFICATE-----* i *-----END CERTIFICATE-----* oraz wszystkie podziały wierszy. Skopiuj ciąg wynikowy.  
12. Jako wartość węzła certificate ustaw ciąg skopiowany w poprzednim kroku.  
13. Ustaw węzeł enabled na wartość **true**.  
14. Dla węzła userName ustaw konto należące do grupy zabezpieczeń PhoneFactor Admins. Użyj formatu &lt;domena&gt;&#92;&lt;nazwa_użytkownika&gt;.  
15. Ustaw hasło na odpowiednie hasło do konta, a następnie zamknij składnik Edytor konfiguracji.  
16. Kliknij link **Zastosuj**.  
17. W katalogu wirtualnym zestawu SDK usługi sieci Web kliknij dwukrotnie pozycję **Uwierzytelnianie**.  
18. Sprawdź, czy opcje Personifikacja ASP.NET i Uwierzytelnianie podstawowe są ustawione na wartość **Włączone**, a wszystkie inne opcje — na wartość **Wyłączone**.  
19. W katalogu wirtualnym zestawu SDK usługi sieci Web kliknij dwukrotnie pozycję **Ustawienia SSL**.  
20. Ustaw opcję Certyfikaty klientów na wartość **Akceptuj**, a następnie kliknij pozycję **Zastosuj**.  
21. Skopiuj wyeksportowany wcześniej plik pfx na serwer, na którym uruchomiony jest adapter AD FS.  
22. Zaimportuj plik pfx do osobistego magazynu certyfikatów komputera lokalnego.  
23. Kliknij prawym przyciskiem myszy i wybierz pozycję **Zarządzaj kluczami prywatnymi**, a następnie przyznaj dostęp do odczytu do konta użytego do zalogowania się do usług AD FS.  
24. Otwórz certyfikat klienta i skopiuj odcisk palca z karty **Szczegóły**.  
25. W pliku MultiFactorAuthenticationAdfsAdapter.config jako wartość węzła **WebServiceSdkCertificateThumbprint** ustaw ciąg skopiowany w poprzednim kroku.  

Następnie, aby zarejestrować adapter, uruchom skrypt \Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 w programie PowerShell. Adapter zostanie zarejestrowany jako element WindowsAzureMultiFactorAuthentication. Uruchom ponownie usługę AD FS, aby zmiany wprowadzone w ramach rejestracji zaczęły obowiązywać.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS
Aby zabezpieczyć zasób w chmurze, skonfiguruj regułę oświadczeń, tak aby usługi Active Directory Federation Services emitowały oświadczenie multipleauthn, gdy użytkownik pomyślnie przeprowadzi weryfikację dwuetapową. To oświadczenie jest przekazywane do usługi Azure AD. Wykonaj tę procedurę w celu przejścia przez poszczególne kroki:

1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie wybierz pozycję **Relacje zaufania jednostek zależnych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Przekazywanie lub filtrowanie oświadczenia przychodzącego**, a następnie kliknij przycisk **Dalej**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nadaj regule nazwę.
7. Wybierz wartość **Odwołania metod uwierzytelniania** jako typ oświadczenia przychodzącego.
8. Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.
    ![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Kliknij przycisk **Zakończ**. Zamknij konsolę zarządzania usługami AD FS.

## <a name="related-topics"></a>Powiązane tematy
Aby uzyskać pomoc przy rozwiązywaniu problemów, zobacz [Azure Multi-Factor Authentication — często zadawane pytania](multi-factor-authentication-faq.md)
