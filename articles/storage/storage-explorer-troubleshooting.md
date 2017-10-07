---
title: "Przewodnik rozwiązywania problemów aaaAzure Eksploratora usługi Storage | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji debugowania Witaj dwie platformy Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Podręczniku rozwiązywania problemów z Eksploratora usługi Storage platformy Azure

## <a name="introduction"></a>Wprowadzenie

Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza) jest autonomiczną aplikację, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, system macOS i Linux. Aplikacja Hello można połączyć kont toStorage hostowanych na Azure, suwerenne chmur i stosu Azure.

Ten przewodnik zawiera podsumowanie rozwiązania dla typowe problemy występujące w Eksploratorze usługi Storage.

## <a name="sign-in-issues"></a>Problemy z rejestracją

Obsługiwane są tylko konta usługi Azure Active Directory (AAD). Jeśli używasz konta usług AD FS, można oczekiwać podpisywania tooStorage Explorer nie będzie działać. Przed kontynuowaniem, spróbuj ponownie uruchomić aplikację i zobacz, czy hello problemy mogą zostać usunięte.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Błąd: Certyfikat z podpisem własnym w łańcuchu certyfikatów

Istnieje kilka przyczyn, dlaczego błąd może się pojawić i hello dwie najbardziej typowe przyczyny są następujące:

1. Aplikacja Hello jest połączony za pośrednictwem "przezroczystego obiektu pośredniczącego", co oznacza przechwycenia ruchu HTTPS, odszyfrowywania go i następnie szyfrowania za pomocą certyfikatu z podpisem własnym serwera (takich jak serwer firmy).

2. Używasz aplikacji, takich jak oprogramowanie antywirusowe, które wprowadza certyfikatu SSL z podpisem własnym do wiadomości powitania HTTPS, które otrzymujesz.

Gdy Eksploratora usługi Storage napotka jeden z problemów hello, go już wiadomo, czy została naruszona hello odebrał komunikat protokołu HTTPS. Jeśli masz kopię certyfikatu z podpisem własnym hello, możesz pozwolić, Eksploratora usługi Storage zaufania temu certyfikatowi. Jeśli nie wiesz, kto jest wprowadzenia hello certyfikatu, wykonaj te kroki toofind go:

1. Zainstaluj Otwórz protokołu SSL

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (hello wersje światła powinno wystarczyć)

    - Mac i Linux: powinien być dołączony do systemu operacyjnego

2. Uruchom Otwórz protokołu SSL

    - System Windows: Otwórz katalog instalacyjny hello, kliknij pozycję **/bin/**, a następnie kliknij dwukrotnie **openssl.exe**.
    - Mac i Linux: Uruchom **openssl** z terminalu.

3. Wykonanie s_client - showcerts-Połącz microsoft.com:443

4. Poszukaj certyfikaty z podpisem własnym. Jeśli nie wiesz, które są podpisem, poszukaj dowolnym hello podmiotu ("s:") i wystawcy ("i") są takie same hello.

5. Znalezione wszystkie certyfikaty z podpisem własnym dla każdego z nich, skopiować i wkleić wszystkie elementy z tym **---BEGIN CERTIFICATE---** za**---END CERTIFICATE---** tooa nowy plik cer.

6. Otwórz Eksploratora usługi Storage, kliknij pozycję **Edytuj** > **certyfikaty SSL** > **importu certyfikatów**, a następnie użyj hello pliku selektora toofind, wybierz, i otwierać pliki .cer hello, które zostały utworzone.

Jeśli nie można znaleźć żadnych certyfikatów z podpisem własnym za pomocą hello powyżej czynności, skontaktuj się z nami za pomocą narzędzia opinii hello, aby uzyskać dalszą pomoc.

### <a name="unable-tooretrieve-subscriptions"></a>Nie można tooretrieve subskrypcji

Jeśli tooretrieve subskrypcji po pomyślnym zalogowaniu w, wykonaj te kroki tootroubleshoot ten problem:

- Sprawdź, czy Twoje konto ma subskrypcje toohello dostęp po zalogowaniu się do hello portalu Azure.

- Upewnij się, że zalogowano się za pomocą hello poprawne środowisko (Azure, chińskiej wersji platformy Azure, platformy Azure w Niemczech, Azure instytucji rządowych Stanów Zjednoczonych lub niestandardowe stosu środowiska/Azure).

- Jeśli używasz serwera proxy, upewnij się, poprawnie skonfigurowany serwer proxy Eksploratora usługi Storage hello.

- Spróbuj usunąć i ponowne dodawanie hello konta.

- Spróbuj usuwanie hello następujące pliki z katalogu głównego (czyli C:\Users\ContosoUser), a następnie ponowne dodanie konta hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Obejrzyj hello developer narzędzia konsoli (naciskając klawisz F12) Jeśli logujesz dla komunikatów o błędach:

![Narzędzia dla deweloperów](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Strona uwierzytelniania hello toosee

Jeśli strony uwierzytelniania hello toosee, wykonaj te kroki tootroubleshoot ten problem:

- W zależności od prędkości połączenia hello może potrwać hello tooload strony logowania, zaczekaj co najmniej jedną minutę przed zamknięciem okno dialogowe hello uwierzytelniania.

- Jeśli używasz serwera proxy, upewnij się, poprawnie skonfigurowany serwer proxy Eksploratora usługi Storage hello.

- Widok hello konsoli dla deweloperów, naciskając klawisz F12 hello. Obejrzyj hello odpowiedzi z konsoli dla deweloperów hello i zobacz, czy można znaleźć żadnych clue Dlaczego uwierzytelniania nie działa.

### <a name="cannot-remove-account"></a>Nie można usunąć konta

Jeśli jesteś tooremove konta lub łącze Uwierzytelnij ponownie hello wykonywać żadnych czynności, wykonaj te kroki tootroubleshoot ten problem:

- Spróbuj usuwanie hello następujące pliki z katalogu głównego, a następnie ponowne dodawanie konta hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Jeśli chcesz tooremove SAS dołączony zasobów magazynu, należy usunąć hello następujące pliki:

    - Folder %appdata%/StorageExplorer dla systemu Windows

    - /Users/ < twoje_imie >/biblioteki/komputerze Obsługa/StorageExplorer dla komputerów Mac

    - ~/.config/StorageExplorer dla systemu Linux

> [!NOTE]
>  Konieczne będzie tooreenter swoje poświadczenia po usunięciu tych plików.

## <a name="proxy-issues"></a>Problemy z serwera proxy

Najpierw upewnij się, ten powitania po wprowadzone informacje są wszystkie prawidłowe:

- Witaj, adres URL serwera proxy i port numer

- Nazwa użytkownika i hasło, jeśli jest to wymagane przez serwer proxy hello

### <a name="common-solutions"></a>Typowe rozwiązania

Jeśli nadal występują problemy, wykonaj te kroki tootroubleshoot je:

- Jeśli łączysz toohello Internet bez użycia serwera proxy, sprawdź, czy Eksploratora usługi Storage działa bez włączone ustawienia serwera proxy. Jeśli hello tak jest, może istnieć problem z ustawieniami serwera proxy. Współpraca z problemów hello tooidentify administratora serwera proxy.

- Sprawdź, czy inne aplikacje korzystające z serwera proxy hello działają zgodnie z oczekiwaniami.

- Sprawdź, czy masz połączenie toohello portalu Microsoft Azure za pomocą przeglądarki sieci web

- Sprawdź, czy możesz odbierać odpowiedzi z punktami końcowymi usługi. Wprowadź jeden z adresami URL punktu końcowego w przeglądarce. Jeśli można połączyć, powinien zostać wyświetlony InvalidQueryParameterValue lub podobne odpowiedzi XML.

- Jeśli ktoś inny korzysta również Eksploratora usługi Storage z serwerem proxy, sprawdź, czy można połączyć. Jeśli można się połączyć, może być toocontact administratorem serwera proxy

### <a name="tools-for-diagnosing-issues"></a>Narzędzia do diagnozowania problemów

Jeśli masz sieci narzędzi, takich jak Fiddler dla systemu Windows może toodiagnose hello problemy mogą się następująco:

- Jeśli masz toowork za pośrednictwem serwera proxy, może być tooconfigure Twojego sieci tooconnect narzędzia za pośrednictwem serwera proxy hello.

- Sprawdź hello numeru portu używanego przez narzędzie do sieci.

- Wprowadź adres URL hosta lokalnego hello i hello sieci jako ustawienia serwera proxy w Eksploratorze usługi Storage narzędzia numer portu. Jeśli odbywa się prawidłowo, narzędzie sieci uruchamia rejestrowanie żądań sieci przez punkty końcowe usług i toomanagement Eksploratora usługi Storage. Na przykład wprowadź https://cawablobgrs.blob.core.windows.net/ dla punktu końcowego obiektu blob w przeglądarce, a otrzymasz odpowiedź podobne następującego hello, które sugeruje hello zasób istnieje, mimo że nie można do niego dostęp.

![Przykładowy kod](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Skontaktuj się z administratorem serwera proxy

Jeśli ustawienia serwera proxy są prawidłowe, może być toocontact administratora serwera proxy i

- Upewnij się, że serwer proxy blokuje ruch tooAzure zarządzania lub zasobu punktów końcowych.

- Sprawdź hello protokół uwierzytelniania używany przez serwer proxy. Eksplorator usługi Storage aktualnie nie obsługuje serwerów proxy NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Komunikat o błędzie "tooRetrieve dzieci"

Jeśli jesteś tooAzure połączonych za pośrednictwem serwera proxy, sprawdź, czy ustawienia serwera proxy są poprawne. Jeśli dostęp do zasobów tooa zostały przyznane przez właściciela hello hello subskrypcji lub konta, sprawdź, czy znasz, lub listę uprawnień dla tego zasobu.

### <a name="issues-with-sas-url"></a>Problemy z adresem URL SAS
W przypadku łączenia tooa usługi przy użyciu adresu URL SAS i występuje błąd:

- Upewnij się, że adres URL hello dostarcza niezbędne uprawnienia hello tooread lub listy zasobów.

- Sprawdź powitalne tego adresu URL nie wygasł.

- Jeśli adres URL SAS hello jest oparta na zasadach dostępu, sprawdź, czy zasady dostępu hello nie został odwołany.

## <a name="next-steps"></a>Następne kroki

Jeśli hello rozwiązania nie działają dla Ciebie, przesłać problem za pomocą narzędzia opinii hello z poczty e-mail i szczegółów o problemie hello uwzględnione podczas można tak, aby firma Microsoft może skontaktować się z Tobą ustalania hello problem.

toodo tego, kliknij **pomocy** menu, a następnie kliknij przycisk **Prześlij opinię**.

![Opinia](./media/storage-explorer-troubleshooting/4022503_en_1.png)
