---
title: "Konfiguracja zabezpieczeń scalania aaaSplit | Dokumentacja firmy Microsoft"
description: Konfigurowanie x409 certyfikaty szyfrowania
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Konfiguracja zabezpieczeń scalania podziału
toouse hello podziału/Merge usługi, należy poprawnie skonfigurować zabezpieczeń. Usługa Hello jest częścią hello funkcji elastycznego skalowania bazy danych SQL Azure firmy Microsoft. Aby uzyskać więcej informacji, zobacz [elastycznej podziału skali i scal samouczek usługi](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Konfigurowanie certyfikatów
Certyfikaty są skonfigurowane na dwa sposoby. 

1. [Witaj tooConfigure certyfikat SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure certyfikaty klienta](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>Certyfikaty tooobtain
Certyfikaty można uzyskać z publicznych urzędów certyfikacji (CA) lub hello [usługi certyfikatów systemu Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Są to hello preferowanych metod tooobtain certyfikatów.

Jeśli te opcje nie są dostępne, można wygenerować **certyfikaty z podpisem własnym**.

## <a name="tools-toogenerate-certificates"></a>Narzędzia toogenerate certyfikatów
* [MakeCert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>narzędzia hello toorun
* Z wiersz polecenia dla deweloperów programu Visual Studio, zobacz [wiersz polecenia programu Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Jeśli zainstalowany, przejdź do:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Pobierz hello WDK z [Windows 8.1: Pobieranie zestawów i narzędzi](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certyfikat SSL hello tooconfigure
Certyfikat SSL jest wymagany tooencrypt hello komunikacji i uwierzytelniania serwera hello. Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:

### <a name="create-a-new-self-signed-certificate"></a>Utwórz nowy certyfikat z podpisem własnym
1. [Utwórz certyfikat z podpisem własnym](#create-a-self-signed-certificate)
2. [Utwórz plik PFX dla certyfikatu SSL z podpisem własnym](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Przekaż certyfikat SSL tooCloud usługi](#upload-ssl-certificate-to-cloud-service)
4. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)
5. [Urząd certyfikacji SSL importu](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>przechowywanie istniejącego certyfikatu z certyfikatu hello toouse
1. [Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów](#export-ssl-certificate-from-certificate-store)
2. [Przekaż certyfikat SSL tooCloud usługi](#upload-ssl-certificate-to-cloud-service)
3. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse istniejącego certyfikatu w pliku PFX
1. [Przekaż certyfikat SSL tooCloud usługi](#upload-ssl-certificate-to-cloud-service)
2. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certyfikaty klienta tooconfigure
Certyfikaty klienta są wymagane w kolejności tooauthenticate żądań toohello usługi. Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:

### <a name="turn-off-client-certificates"></a>Wyłącz certyfikaty klienta
1. [Wyłącz uwierzytelnianie oparte na certyfikatach](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Wydać nowe certyfikaty klienta z podpisem własnym
1. [Tworzenie urzędu certyfikacji z podpisem własnym](#create-a-self-signed-certification-authority)
2. [Przekaż certyfikat urzędu certyfikacji tooCloud usługi](#upload-ca-certificate-to-cloud-service)
3. [Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi](#update-ca-certificate-in-service-configuration-file)
4. [Certyfikaty](#issue-client-certificates)
5. [Tworzenie plików PFX certyfikatów klienta](#create-pfx-files-for-client-certificates)
6. [Importowanie certyfikatu klienta](#Import-Client-Certificate)
7. [Skopiuj odciski palców certyfikatu klienta](#copy-client-certificate-thumbprints)
8. [Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Użyj istniejących certyfikatów klienta
1. [Znajdowanie klucza publicznego urzędu certyfikacji](#find-ca-public-key)
2. [Przekaż certyfikat urzędu certyfikacji tooCloud usługi](#Upload-CA-certificate-to-cloud-service)
3. [Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Skopiuj odciski palców certyfikatu klienta](#Copy-Client-Certificate-Thumbprints)
5. [Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello](#configure-allowed-clients-in-the-service-configuration-file)
6. [Skonfiguruj sprawdzanie odwołania certyfikatu klienta](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Dozwolonych adresów IP
Punkty końcowe usługi toohello dostępu może być ograniczony toospecific zakresów adresów IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>szyfrowanie tooconfigure hello magazynu
Certyfikat jest wymagany tooencrypt hello poświadczenia, które są przechowywane w magazynie metadanych hello. Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:

### <a name="use-a-new-self-signed-certificate"></a>Użyj nowego certyfikatu z podpisem własnym
1. [Utwórz certyfikat z podpisem własnym](#create-a-self-signed-certificate)
2. [Tworzenie pliku PFX certyfikatu szyfrowania z podpisem własnym](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Przekaż certyfikat szyfrowania tooCloud usługi](#upload-encryption-certificate-to-cloud-service)
4. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Użyj istniejącego certyfikatu z magazynu certyfikatów hello
1. [Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów](#export-encryption-certificate-from-certificate-store)
2. [Przekaż certyfikat szyfrowania tooCloud usługi](#upload-encryption-certificate-to-cloud-service)
3. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Użyj istniejącego certyfikatu w pliku PFX
1. [Przekaż certyfikat szyfrowania tooCloud usługi](#upload-encryption-certificate-to-cloud-service)
2. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>Witaj domyślnej konfiguracji
Hello domyślnej konfiguracji odrzuca wszystkie punkt końcowy HTTP toohello dostępu. Jest to hello zalecane ustawienia, ponieważ punkty końcowe toothese żądań hello może posiadać poufne informacje, takie jak poświadczenia bazy danych.
Konfiguracja domyślna Hello zezwala wszystkich punkt końcowy HTTPS toohello dostępu. To ustawienie może być ograniczony dalej.

### <a name="changing-hello-configuration"></a>Zmiana hello konfiguracji
Witaj grupy regułami kontroli dostępu stosowane tooand punktu końcowego są konfigurowane w hello  **<EndpointAcls>**  części hello **pliku konfiguracji usługi**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

reguły Hello w grupie kontroli dostępu są skonfigurowane w <AccessControl name=""> sekcji pliku konfiguracji usługi hello. 

Hello format opisanej w dokumentacji list kontroli dostępu do sieci.
Na przykład tooallow tylko adresy IP w zakresie 100.100.0.0 hello too100.100.255.255 hello tooaccess HTTPS punkt końcowy, reguły hello będzie wyglądać następująco:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Odmowa usługi zapobiegania
Istnieją dwa różne mechanizmy obsługiwane toodetect i zapobieganie atakom "odmowa usługi":

* Ogranicz liczbę równoczesnych żądań na hosta zdalnego (domyślnie wyłączone)
* Ogranicz szybkość dostępu do jednego hosta zdalnego (na domyślne)

Są one oparte na funkcji hello opisano w dynamicznej zabezpieczeń IP w programie IIS. Jeśli zmiana tej konfiguracji należy wziąć pod hello następujące czynniki:

* zachowanie Hello urządzeń translatora adresów sieciowych za pośrednictwem hello informacji hosta zdalnego i serwerów proxy
* Każdy zasób tooany żądania w roli sieci web hello jest uznawany za (np. ładowanie skryptów, obrazy, itp.)

## <a name="restricting-number-of-concurrent-accesses"></a>Ograniczenie liczby równoczesnych dostępów
dostępne są następujące ustawienia Hello, które skonfigurowania tego zachowania:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Zmień DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable tę ochronę.

## <a name="restricting-rate-of-access"></a>Ograniczanie szybkość dostępu
dostępne są następujące ustawienia Hello, które skonfigurowania tego zachowania:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Konfigurowanie tooa odpowiedzi hello odrzucił żądanie
Witaj następujące ustawienie konfiguruje tooa odpowiedzi hello odrzucił żądanie:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Zapoznaj się z toohello dokumentacją dla dynamicznych zabezpieczeń protokołu IP w usługach IIS dla innych obsługiwanych wartości.

## <a name="operations-for-configuring-service-certificates"></a>Operacje dotyczące konfigurowania certyfikatów usługi
Ten temat dotyczy tylko w celach informacyjnych. Wykonaj kroki konfiguracji hello opisane w temacie:

* Konfigurowanie certyfikatu SSL hello
* Skonfiguruj certyfikaty klienta

## <a name="create-a-self-signed-certificate"></a>Utwórz certyfikat z podpisem własnym
Wykonaj:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n z hello adres URL usługi. Symbole wieloznaczne ("CN = * .cloudapp .net") i alternatywnych nazw ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") są obsługiwane.
* -e z datą wygaśnięcia certyfikatu hello Utwórz silne hasło i określ go po wyświetleniu monitu.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Utwórz plik PFX dla certyfikatu SSL z podpisem własnym
Wykonaj:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny hello
* Eksportuj wszystkie właściwości rozszerzone

## <a name="export-ssl-certificate-from-certificate-store"></a>Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów
* Znajdowanie certyfikatów
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami:
  * Tak, Eksportuj klucz prywatny hello
  * Jeśli to możliwe, Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello * Wyeksportuj wszystkie rozszerzone właściwości

## <a name="upload-ssl-certificate-toocloud-service"></a>Przekaż usługi toocloud certyfikatu SSL
Przekaż certyfikat z hello istniejące lub wygenerować. Plik PFX o hello pary kluczy SSL:

* Wprowadź hasło hello ochrona powitalnych informacji o kluczu prywatnym

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Aktualizuj certyfikat SSL w pliku konfiguracji usługi
Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Urząd certyfikacji SSL importu
Wykonaj następujące kroki w wszystkie konta/maszyny, które będą komunikować się z usługą hello:

* Kliknij dwukrotnie hello. Plik CER w Eksploratorze Windows
* W oknie dialogowym certyfikat hello kliknij przycisk Zainstaluj certyfikat...
* Zaimportuj certyfikat w magazynie zaufanych głównych urzędów certyfikacji powitalne

## <a name="turn-off-client-certificate-based-authentication"></a>Wyłącz uwierzytelnianie oparte na certyfikatach
Obsługiwane jest tylko uwierzytelnianie oparte na certyfikatach klienta i wyłączenie go spowoduje umożliwiają punktów końcowych usługi toohello dostępu publicznego, innych mechanizmów znajdują się w miejscu (np. Microsoft Azure Virtual Network).

Zmienić te ustawienia toofalse w funkcji hello tooturn plików w konfiguracji usługi hello:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Następnie skopiuj hello certyfikatu w tym samym odciskiem palca jako hello SSL w ustawieniu certyfikatu hello urzędu certyfikacji:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Tworzenie urzędu certyfikacji z podpisem własnym
Wykonaj hello następujące kroki toocreate tooact certyfikatu z podpisem własnym, jako urząd certyfikacji:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize go

* -e z datą wygaśnięcia certyfikacji hello

## <a name="find-ca-public-key"></a>Znajdowanie klucza publicznego urzędu certyfikacji
Wszystkie certyfikaty klienta musi został wystawiony przez urząd certyfikacji zaufany przez usługę hello. Znajdź hello toohello klucza publicznego urzędu certyfikacji, który wystawił certyfikaty klienta hello, które mają toobe używany do uwierzytelniania w kolejności tooupload on toohello usługi w chmurze.

Jeśli plik hello kluczem publicznym hello jest niedostępny, eksportować go z magazynu certyfikatów hello:

* Znajdowanie certyfikatów
  * Wyszukaj certyfikat klienta wystawiony przez hello tego samego urzędu certyfikacji
* Kliknij dwukrotnie certyfikat hello.
* Wybierz kartę ścieżki certyfikacji hello w oknie dialogowym certyfikat hello.
* Kliknij dwukrotnie wpis urzędu certyfikacji hello w ścieżce hello.
* Zanotować hello właściwości certyfikatu.
* Zamknij hello **certyfikatu** okna dialogowego.
* Znajdowanie certyfikatów
  * Wyszukiwanie hello opisanymi powyżej urzędu certyfikacji.
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. CER z następującymi opcjami:
  * **Nie eksportuj klucza prywatnego hello**
  * Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello Jeśli to możliwe.
  * Eksportuj wszystkie właściwości rozszerzone.

## <a name="upload-ca-certificate-toocloud-service"></a>Przekaż usługi toocloud certyfikatu urzędu certyfikacji
Przekaż certyfikat z hello istniejące lub wygenerować. Plik CER kluczem publicznym hello urzędu certyfikacji.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Certyfikat urzędu certyfikacji aktualizacji w pliku konfiguracji usługi
Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Zaktualizuj wartość hello hello następujące ustawienie hello sam odcisk palca:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Certyfikaty
Każda usługa hello poszczególnych tooaccess autoryzowanych powinien mieć klienta certyfikat wystawiony dla his/hers wyłącznego użycia i należy wybrać, czy his/hers właścicielem tooprotect silne hasło jego klucz prywatny. 

Witaj, wykonaj czynności należy wykonać w hello na tym samym komputerze, na którym hello certyfikat z podpisem własnym urzędu certyfikacji został wygenerowany i przechowywane:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Dostosowywanie:

* n - o identyfikatorze klienta toohello będą uwierzytelniane z tym certyfikatem
* -e z datą wygaśnięcia certyfikatu hello
* MyID.pvk i MyID.cer z unikatowych nazw plików dla tego certyfikatu klienta.

To polecenie wyświetli monit o podanie toobe hasło utworzone, a następnie użyty raz. Należy używać silnych haseł.

## <a name="create-pfx-files-for-client-certificates"></a>Tworzenie plików PFX dla klienta certyfikatów
Dla każdego certyfikatu wygenerowanego klienta należy wykonać:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Dostosowywanie:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny hello
* Eksportuj wszystkie właściwości rozszerzone
* toowhom poszczególnych Hello, które ten certyfikat jest wystawiane należy wybrać hello hasło eksportu

## <a name="import-client-certificate"></a>Importowanie certyfikatu klienta
Każda osoba, dla którego został wystawiony certyfikat klienta należy importować pary kluczy hello na maszynach hello on użyje toocommunicate z usługą hello:

* Kliknij dwukrotnie hello. Plik PFX w Eksploratorze Windows
* Zaimportuj certyfikat do hello Magazyn osobisty z co najmniej tej opcji:
  * Dołącz wszystkie właściwości rozszerzone zaznaczone

## <a name="copy-client-certificate-thumbprints"></a>Skopiuj odciski palców certyfikatu klienta
Każda osoba, dla którego został wystawiony certyfikat klienta, należy wykonać następujące kroki w kolejności tooobtain hello odcisk palca his/hers certyfikatu, który zostanie dodany plik konfiguracji usługi toohello:

* Uruchom certmgr.exe
* Wybierz kartę osobistych powitalne
* Kliknij dwukrotnie certyfikat klienta hello toobe używany do uwierzytelniania
* Hello certyfikat zostanie otwarte okno dialogowe Wybierz kartę szczegółów hello
* Upewnij się, że Pokaż są wyświetlane wszystkie
* Wybierz hello pola o nazwie odcisk palca liście hello
* Kopiuj wartość hello odcisk palca hello ** usunąć niewidoczne znaków Unicode, przed pierwszą cyfrą hello ** usunięcia wszystkich spacji

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello
Zaktualizuj wartość hello hello następujące ustawienia w pliku konfiguracji usługi hello rozdzielaną przecinkami listę hello odciski palców certyfikatów klienta hello dozwolone usługi toohello dostęp:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Skonfiguruj sprawdzanie odwołania certyfikatu klienta
ustawienie domyślne Hello nie skontaktuj się z hello urzędu certyfikacji dla stanu odwołania certyfikatu klienta. tooturn na powitania sprawdza, czy hello urzędu certyfikacji, który wystawił certyfikaty klienta hello obsługuje kontrole, Zmień następujące ustawienia z jedną z wartości hello zdefiniowanych w hello wyliczenie X509RevocationMode hello:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Utwórz plik PFX certyfikatów z podpisem szyfrowania
Aby uzyskać certyfikat szyfrowania należy wykonać:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Dostosowywanie:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny hello
* Eksportuj wszystkie właściwości rozszerzone
* Konieczne będzie hello hasła podczas przekazywania hello usługi w chmurze toohello certyfikatu.

## <a name="export-encryption-certificate-from-certificate-store"></a>Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów
* Znajdowanie certyfikatów
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami: 
  * Tak, Eksportuj klucz prywatny hello
  * Jeśli to możliwe, Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello 
* Eksportuj wszystkie właściwości rozszerzone

## <a name="upload-encryption-certificate-toocloud-service"></a>Przekaż usługi toocloud certyfikatu szyfrowania
Przekaż certyfikat z hello istniejące lub wygenerować. Plik PFX o pary kluczy szyfrowania hello:

* Wprowadź hasło hello ochrona powitalnych informacji o kluczu prywatnym

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi
Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Typowe operacje certyfikatu
* Konfigurowanie certyfikatu SSL hello
* Skonfiguruj certyfikaty klienta

## <a name="find-certificate"></a>Znajdowanie certyfikatów
Wykonaj następujące kroki:

1. Uruchom mmc.exe.
2. Plik -> Dodaj/Usuń przystawkę...
3. Wybierz **certyfikaty**.
4. Kliknij pozycję **Dodaj**.
5. Wybierz lokalizację magazynu certyfikatu hello.
6. Kliknij przycisk **Zakończ**.
7. Kliknij przycisk **OK**.
8. Rozwiń węzeł **certyfikaty**.
9. Rozwiń węzeł magazynu certyfikatów hello.
10. Rozwiń węzeł podrzędny hello certyfikatu.
11. Wybierz certyfikat hello listy.

## <a name="export-certificate"></a>Eksportowanie certyfikatu
W hello **Kreatora eksportu certyfikatów**:

1. Kliknij przycisk **Dalej**.
2. Wybierz **tak**, następnie **klucza prywatnego hello eksportu**.
3. Kliknij przycisk **Dalej**.
4. Wybierz format pliku żądanego wyniku hello.
5. Witaj wyboru żądane opcje.
6. Sprawdź **hasło**.
7. Wpisz silne hasło i potwierdź je.
8. Kliknij przycisk **Dalej**.
9. Wpisz lub wyszukaj nazwę pliku, gdzie toostore hello certyfikatu (Użyj. Rozszerzenie PFX).
10. Kliknij przycisk **Dalej**.
11. Kliknij przycisk **Zakończ**.
12. Kliknij przycisk **OK**.

## <a name="import-certificate"></a>Importowanie certyfikatu
W Kreatorze importu certyfikatów hello:

1. Wybierz lokalizację magazynu hello.
   
   * Wybierz **bieżącego użytkownika** jeśli tylko procesów uruchomionych w obszarze bieżący użytkownik będą uzyskiwać dostęp do usługi hello
   * Wybierz **komputera lokalnego** Jeśli inne procesy w tym komputerze będą uzyskiwać dostęp do usługi hello
2. Kliknij przycisk **Dalej**.
3. W przypadku importowania z pliku Potwierdź hello ścieżkę pliku.
4. Jeśli import. Plik PFX:
   1. Wprowadź hasło hello ochrona powitalnych klucza prywatnego
   2. Wybierz opcje importowania
5. Wybierz certyfikaty "W miejscu" hello po magazynu
6. Kliknij pozycję **Browse (Przeglądaj)**.
7. Wybierz żądaną magazyn hello.
8. Kliknij przycisk **Zakończ**.
   
   * Jeśli wybrano hello magazynu zaufanego głównego urzędu certyfikacji, kliknij przycisk **tak**.
9. Kliknij przycisk **OK** na wszystkie okna dialogowe.

## <a name="upload-certificate"></a>Przekazywanie certyfikatu
W hello [portalu Azure](https://portal.azure.com/)

1. Wybierz **usługi w chmurze**.
2. Wybierz usługę w chmurze hello.
3. W menu u góry hello, kliknij polecenie **certyfikaty**.
4. Na pasku dolnej powitania kliknij **przekazać**.
5. Wybierz plik certyfikatu hello.
6. Jeśli istnieje. PFX, wprowadź hasło hello hello klucza prywatnego.
7. Po zakończeniu skopiuj odcisk palca certyfikatu hello z hello nowy wpis na liście hello.

## <a name="other-security-considerations"></a>Inne zagadnienia dotyczące zabezpieczeń
w tym dokumencie opisano ustawienia protokołu SSL Hello szyfrowania komunikacji między hello service i jej klientów, gdy punkt końcowy HTTPS hello jest używany. Jest to ważne, ponieważ poświadczenia dostępu do bazy danych i inne poufne informacje znajdują się w komunikacie hello. Należy jednak pamiętać, że usługa hello będzie się powtarzał wewnętrzny stan, w tym poświadczenia, w jego wewnętrznego tabele w bazie danych Microsoft Azure SQL hello dostarczoną do przechowywania metadanych w subskrypcji platformy Microsoft Azure. Tej bazy danych został zdefiniowany jako część hello następujące ustawienia w pliku konfiguracji usługi (. Plik CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Poświadczenia przechowywane w tej bazie danych są szyfrowane. Jednak najlepszym rozwiązaniem, sprawdź, czy role sieć web i proces roboczy wdrożeń usługi są przechowywane w górę toodate i bezpieczne, ponieważ mają dostęp toohello metadanych bazy danych i hello certyfikat używany do szyfrowania i odszyfrowywania przechowywanych poświadczeń. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

