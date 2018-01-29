---
title: "Konfiguracja zabezpieczeń scalania podziału | Dokumentacja firmy Microsoft"
description: "Konfigurowanie x409 certyfikaty szyfrowania w usłudze podziału/merge elastycznego skalowania."
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 98f046a943c1fe33b421b3ab6830d78e6c4304a0
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="split-merge-security-configuration"></a>Konfiguracja zabezpieczeń scalania podziału
Do korzystania z usługi podziału/Merge, należy poprawnie skonfigurować zabezpieczeń. Usługa jest część funkcji elastycznego skalowania bazy danych SQL Azure firmy Microsoft. Aby uzyskać więcej informacji, zobacz [elastycznej podziału skali i scal samouczek usługi](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Konfigurowanie certyfikatów
Certyfikaty są skonfigurowane na dwa sposoby. 

1. [Aby skonfigurować certyfikat SSL](#to-configure-the-ssl-certificate)
2. [Aby skonfigurować certyfikaty klienta](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a>Uzyskiwanie certyfikatów
Certyfikaty można uzyskać z publicznych urzędów certyfikacji (CA) lub [usługi certyfikatów systemu Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Są to preferowanymi metodami uzyskiwanie certyfikatów.

Jeśli te opcje nie są dostępne, można wygenerować **certyfikaty z podpisem własnym**.

## <a name="tools-to-generate-certificates"></a>Narzędzia do generowania certyfikatów
* [MakeCert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a>Aby uruchomić narzędzia
* Z wiersz polecenia dla deweloperów programu Visual Studio, zobacz [wiersz polecenia programu Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Jeśli zainstalowany, przejdź do:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Pobierz WDK z [Windows 8.1: Pobieranie zestawów i narzędzi](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="to-configure-the-ssl-certificate"></a>Aby skonfigurować certyfikat SSL
Certyfikat SSL jest wymagany do zaszyfrowania komunikacji i uwierzytelniania serwera. Wybierz najbardziej odpowiednią z trzech poniższych scenariuszy i wykonaj wszystkie jej kroki:

### <a name="create-a-new-self-signed-certificate"></a>Utwórz nowy certyfikat z podpisem własnym
1. [Utwórz certyfikat z podpisem własnym](#create-a-self-signed-certificate)
2. [Utwórz plik PFX dla certyfikatu SSL z podpisem własnym](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Przekaż certyfikat SSL do usługi w chmurze](#upload-ssl-certificate-to-cloud-service)
4. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)
5. [Urząd certyfikacji SSL importu](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a>Aby użyć istniejącego certyfikatu z magazynu certyfikatów
1. [Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów](#export-ssl-certificate-from-certificate-store)
2. [Przekaż certyfikat SSL do usługi w chmurze](#upload-ssl-certificate-to-cloud-service)
3. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a>Aby użyć istniejącego certyfikatu w pliku PFX
1. [Przekaż certyfikat SSL do usługi w chmurze](#upload-ssl-certificate-to-cloud-service)
2. [Aktualizuj certyfikat SSL w pliku konfiguracji usługi](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a>Aby skonfigurować certyfikaty klienta
Certyfikaty klienta są wymagane do uwierzytelniania żądań do usługi. Wybierz najbardziej odpowiednią z trzech poniższych scenariuszy i wykonaj wszystkie jej kroki:

### <a name="turn-off-client-certificates"></a>Wyłącz certyfikaty klienta
1. [Wyłącz uwierzytelnianie oparte na certyfikatach](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Wydać nowe certyfikaty klienta z podpisem własnym
1. [Tworzenie urzędu certyfikacji z podpisem własnym](#create-a-self-signed-certification-authority)
2. [Przekaż certyfikat urzędu certyfikacji do usługi w chmurze](#upload-ca-certificate-to-cloud-service)
3. [Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi](#update-ca-certificate-in-service-configuration-file)
4. [Certyfikaty](#issue-client-certificates)
5. [Tworzenie plików PFX certyfikatów klienta](#create-pfx-files-for-client-certificates)
6. [Importowanie certyfikatu klienta](#Import-Client-Certificate)
7. [Skopiuj odciski palców certyfikatu klienta](#copy-client-certificate-thumbprints)
8. [Konfigurowanie klientów dozwolonych w pliku konfiguracji usługi](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Użyj istniejących certyfikatów klienta
1. [Znajdowanie klucza publicznego urzędu certyfikacji](#find-ca-public-key)
2. [Przekaż certyfikat urzędu certyfikacji do usługi w chmurze](#Upload-CA-certificate-to-cloud-service)
3. [Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Skopiuj odciski palców certyfikatu klienta](#Copy-Client-Certificate-Thumbprints)
5. [Konfigurowanie klientów dozwolonych w pliku konfiguracji usługi](#configure-allowed-clients-in-the-service-configuration-file)
6. [Skonfiguruj sprawdzanie odwołania certyfikatu klienta](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Dozwolonych adresów IP
Dostęp do punktów końcowych usługi można ograniczyć do określonych zakresów adresów IP.

## <a name="to-configure-encryption-for-the-store"></a>Aby skonfigurować szyfrowanie magazynu
Certyfikat jest wymagany do szyfrowania poświadczeń, które są przechowywane w magazynie metadanych. Wybierz najbardziej odpowiednią z trzech poniższych scenariuszy i wykonaj wszystkie jej kroki:

### <a name="use-a-new-self-signed-certificate"></a>Użyj nowego certyfikatu z podpisem własnym
1. [Utwórz certyfikat z podpisem własnym](#create-a-self-signed-certificate)
2. [Tworzenie pliku PFX certyfikatu szyfrowania z podpisem własnym](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Przekaż certyfikat szyfrowania, aby usługa w chmurze](#upload-encryption-certificate-to-cloud-service)
4. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a>Użyj istniejącego certyfikatu z magazynu certyfikatów
1. [Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów](#export-encryption-certificate-from-certificate-store)
2. [Przekaż certyfikat szyfrowania, aby usługa w chmurze](#upload-encryption-certificate-to-cloud-service)
3. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Użyj istniejącego certyfikatu w pliku PFX
1. [Przekaż certyfikat szyfrowania, aby usługa w chmurze](#upload-encryption-certificate-to-cloud-service)
2. [Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a>Domyślna konfiguracja
Domyślna konfiguracja nie zezwala na dostęp do punktu końcowego HTTP. To jest zalecane ustawienie, ponieważ żądania z tymi punktami końcowymi może posiadać poufne informacje, takie jak poświadczenia bazy danych.
Domyślna konfiguracja umożliwia dostęp do punktu końcowego protokołu HTTPS. To ustawienie może być ograniczony dalej.

### <a name="changing-the-configuration"></a>Zmiana konfiguracji
Grupy z regułami kontroli dostępu, które dotyczą i punktu końcowego są konfigurowane w  **<EndpointAcls>**  sekcji **pliku konfiguracji usługi**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

Zasady grupy kontroli dostępu są konfigurowane w <AccessControl name=""> sekcji pliku konfiguracji usługi. 

Format opisanej w dokumentacji list kontroli dostępu do sieci.
Na przykład aby zezwolić tylko adresy IP w zakresie 100.100.0.0 do 100.100.255.255 można uzyskać dostępu do punktu końcowego protokołu HTTPS, reguły będzie wyglądać następująco:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Odmowa usługi zapobiegania
Istnieją dwa różne mechanizmy obsługiwane wykrywanie i zapobieganie atakom "odmowa usługi":

* Ogranicz liczbę równoczesnych żądań na hosta zdalnego (domyślnie wyłączone)
* Ogranicz szybkość dostępu do jednego hosta zdalnego (na domyślne)

Są one oparte na funkcji opisano w dynamicznej zabezpieczeń IP w programie IIS. Jeśli zmiana ta konfiguracja ostrożnie następujące czynniki:

* Zachowanie urządzeń translatora adresów sieciowych za pośrednictwem informacji hosta zdalnego i serwerów proxy
* Każde żądanie do dowolnego zasobu w roli sieci web jest uznawany za (np. ładowanie skryptów, obrazy, itp.)

## <a name="restricting-number-of-concurrent-accesses"></a>Ograniczenie liczby równoczesnych dostępów
Dostępne są następujące ustawienia, które skonfigurowania tego zachowania:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Zmień DynamicIpRestrictionDenyByConcurrentRequests na wartość true, aby włączyć tę ochronę.

## <a name="restricting-rate-of-access"></a>Ograniczanie szybkość dostępu
Dostępne są następujące ustawienia, które skonfigurowania tego zachowania:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a>Konfigurowanie odpowiedzi na żądanie odmowy
Następujące ustawienie umożliwia skonfigurowanie odpowiedzi na żądanie odmowy:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Zajrzyj do dokumentacji dla dynamicznych zabezpieczeń protokołu IP w usługach IIS dla innych obsługiwanych wartości.

## <a name="operations-for-configuring-service-certificates"></a>Operacje dotyczące konfigurowania certyfikatów usługi
Ten temat dotyczy tylko w celach informacyjnych. Wykonaj kroki konfiguracji opisane w temacie:

* Konfigurowanie certyfikatu protokołu SSL
* Skonfiguruj certyfikaty klienta

## <a name="create-a-self-signed-certificate"></a>Utwórz certyfikat z podpisem własnym
Wykonaj:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

Aby dostosować:

* -n z adresem URL usługi. Symbole wieloznaczne ("CN = * .cloudapp .net") i alternatywnych nazw ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") są obsługiwane.
* -e z datą wygaśnięcia certyfikatu Utwórz silne hasło i określ go po wyświetleniu monitu.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Utwórz plik PFX dla certyfikatu SSL z podpisem własnym
Wykonaj:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny
* Eksportuj wszystkie właściwości rozszerzone

## <a name="export-ssl-certificate-from-certificate-store"></a>Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów
* Znajdowanie certyfikatów
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami:
  * Tak, Eksportuj klucz prywatny
  * Jeśli to możliwe, Dołącz wszystkie certyfikaty do ścieżki certyfikacji * Wyeksportuj wszystkie rozszerzone właściwości

## <a name="upload-ssl-certificate-to-cloud-service"></a>Przekaż certyfikat SSL do usługi w chmurze
Przekazywanie certyfikatu z istniejącym lub wygenerowany. Plik PFX o pary kluczy SSL:

* Wprowadź hasło chroniące informacje o kluczu prywatnym

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Aktualizuj certyfikat SSL w pliku konfiguracji usługi
Zaktualizuj wartość odcisku palca poniższe ustawienia w pliku konfiguracji usługi z odciskiem palca certyfikatu przekazane do usługi w chmurze:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Urząd certyfikacji SSL importu
Wykonaj następujące kroki w wszystkie konta/maszyny, które będą komunikować się z usługą:

* Kliknij dwukrotnie. Plik CER w Eksploratorze Windows
* W oknie dialogowym certyfikat kliknij przycisk Zainstaluj certyfikat...
* Zaimportuj certyfikat do magazynu zaufanych głównych urzędów certyfikacji

## <a name="turn-off-client-certificate-based-authentication"></a>Wyłącz uwierzytelnianie oparte na certyfikatach
Obsługiwane jest tylko uwierzytelnianie oparte na certyfikatach klienta i wyłączenie go spowoduje umożliwiają publiczny dostęp do punktów końcowych usługi, innych mechanizmów znajdują się w miejscu (np. Microsoft Azure Virtual Network).

Zmiana tych ustawień na wartość false w pliku konfiguracji usługi, aby wyłączyć funkcję:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Następnie skopiuj tym samym odciskiem palca jako certyfikatu SSL w ustawieniu certyfikatu urzędu certyfikacji:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Tworzenie urzędu certyfikacji z podpisem własnym
Wykonaj poniższe kroki, aby utworzyć certyfikat z podpisem własnym do działania jako urząd certyfikacji:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

Aby dostosować go

* -e z datą wygaśnięcia certyfikacji

## <a name="find-ca-public-key"></a>Znajdowanie klucza publicznego urzędu certyfikacji
Wszystkie certyfikaty klienta musi został wystawiony przez urząd certyfikacji zaufany przez usługę. Znajdź klucz publiczny dla urzędu certyfikacji, który wystawił certyfikaty, które mają być używane do uwierzytelniania w celu przekazania go do usługi w chmurze klienta.

Jeśli plik zawierający klucz publiczny nie jest dostępna, należy wyeksportować go z magazynu certyfikatów:

* Znajdowanie certyfikatów
  * Wyszukaj wystawiony przez urząd certyfikacji tego samego certyfikatu klienta
* Kliknij dwukrotnie certyfikat.
* Wybierz kartę Ścieżka certyfikacji w oknie dialogowym certyfikat.
* Kliknij dwukrotnie wpis urzędu certyfikacji w ścieżce.
* Zanotować właściwości certyfikatu.
* Zamknij **certyfikatu** okna dialogowego.
* Znajdowanie certyfikatów
  * Wyszukiwanie certyfikacji opisanymi powyżej.
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. CER z następującymi opcjami:
  * **Nie eksportuj klucza prywatnego**
  * Dołącz wszystkie certyfikaty do ścieżki certyfikacji, jeśli to możliwe.
  * Eksportuj wszystkie właściwości rozszerzone.

## <a name="upload-ca-certificate-to-cloud-service"></a>Przekaż certyfikat urzędu certyfikacji do usługi w chmurze
Przekazywanie certyfikatu z istniejącym lub wygenerowany. Plik CER przy użyciu klucza publicznego urzędu certyfikacji.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Certyfikat urzędu certyfikacji aktualizacji w pliku konfiguracji usługi
Zaktualizuj wartość odcisku palca poniższe ustawienia w pliku konfiguracji usługi z odciskiem palca certyfikatu przekazane do usługi w chmurze:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Zaktualizuj wartość następujące ustawienia z tym samym odciskiem palca:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Certyfikaty
Każda osoba uprawnień do uzyskania dostępu do usługi powinien mieć klienta certyfikat wystawiony dla his/hers wyłącznego użycia i powinna wybrać własne his/hers silne hasło, aby chronić jego klucz prywatny. 

W tym samym komputerze, na którym generowane i przechowywane certyfikat urzędu certyfikacji z podpisem własnym należy wykonać następujące czynności:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Dostosowywanie:

* n - o identyfikatorze dla klientowi, który będą uwierzytelniane z tym certyfikatem
* -e z datą wygaśnięcia certyfikatu
* MyID.pvk i MyID.cer z unikatowych nazw plików dla tego certyfikatu klienta.

To polecenie wyświetli monit o podanie hasła w celu utworzone, a następnie użyć raz. Należy używać silnych haseł.

## <a name="create-pfx-files-for-client-certificates"></a>Tworzenie plików PFX dla klienta certyfikatów
Dla każdego certyfikatu wygenerowanego klienta należy wykonać:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Dostosowywanie:

    MyID.pvk and MyID.cer with the filename for the client certificate

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny
* Eksportuj wszystkie właściwości rozszerzone
* Osoby, dla którego ten certyfikat został wystawiony, należy wybrać hasło eksportu

## <a name="import-client-certificate"></a>Importowanie certyfikatu klienta
Każda osoba, dla którego został wystawiony certyfikat klienta należy importować pary kluczy na maszynach, które będzie on używany do komunikacji z usługą:

* Kliknij dwukrotnie. Plik PFX w Eksploratorze Windows
* Importowanie certyfikatu do osobistego magazynu z co najmniej tej opcji:
  * Dołącz wszystkie właściwości rozszerzone zaznaczone

## <a name="copy-client-certificate-thumbprints"></a>Skopiuj odciski palców certyfikatu klienta
Poszczególnych osób, dla którego został wystawiony certyfikat klienta, wykonaj następujące kroki w celu uzyskania his/hers odcisk palca certyfikatu, który zostanie dodany do pliku konfiguracji usługi:

* Uruchom certmgr.exe
* Wybierz kartę osobiste.
* Kliknij dwukrotnie certyfikat klienta, które mają być używane do uwierzytelniania
* W oknie dialogowym certyfikat, który zostanie otwarty wybierz kartę szczegółów
* Upewnij się, że Pokaż są wyświetlane wszystkie
* Wybierz pole o nazwie odcisk palca na liście
* Skopiuj wartość odcisku palca ** usunąć niewidoczne znaków Unicode, przed pierwszą ** usunięcia wszystkich spacji

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a>Konfigurowanie klientów dozwolone w pliku konfiguracji usługi
Zaktualizuj wartość poniższe ustawienia w pliku konfiguracji usługi rozdzielaną przecinkami listę odcisków palców certyfikatów klientów, zezwolenie na dostęp do usługi:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Skonfiguruj sprawdzanie odwołania certyfikatu klienta
Ustawienie domyślne nie sprawdza się z urzędem certyfikacji dla stanu odwołania certyfikatu klienta. Aby włączyć kontroli, jeśli urząd certyfikacji, który wystawił certyfikaty klienta obsługuje kontrole, należy zmienić następujące ustawienie z jedną z wartości zdefiniowanych w wyliczeniu X509RevocationMode:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Utwórz plik PFX certyfikatów z podpisem szyfrowania
Aby uzyskać certyfikat szyfrowania należy wykonać:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Dostosowywanie:

    MyID.pvk and MyID.cer with the filename for the encryption certificate

Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:

* Tak, Eksportuj klucz prywatny
* Eksportuj wszystkie właściwości rozszerzone
* Konieczne będzie hasło podczas przekazywania certyfikatu do usługi w chmurze.

## <a name="export-encryption-certificate-from-certificate-store"></a>Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów
* Znajdowanie certyfikatów
* Kliknij przycisk Akcje -> Wszystkie zadania -> Export...
* Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami: 
  * Tak, Eksportuj klucz prywatny
  * Jeśli to możliwe, Dołącz wszystkie certyfikaty do ścieżki certyfikacji 
* Eksportuj wszystkie właściwości rozszerzone

## <a name="upload-encryption-certificate-to-cloud-service"></a>Przekaż certyfikat szyfrowania do usługi w chmurze
Przekazywanie certyfikatu z istniejącym lub wygenerowany. Plik PFX o pary kluczy szyfrowania:

* Wprowadź hasło chroniące informacje o kluczu prywatnym

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi
Zaktualizuj wartość odcisku palca z następujących ustawień w pliku konfiguracji usługi z odciskiem palca certyfikatu przekazane do usługi w chmurze:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Typowe operacje certyfikatu
* Konfigurowanie certyfikatu protokołu SSL
* Skonfiguruj certyfikaty klienta

## <a name="find-certificate"></a>Znajdowanie certyfikatów
Wykonaj następujące kroki:

1. Uruchom mmc.exe.
2. Plik -> Dodaj/Usuń przystawkę...
3. Wybierz **certyfikaty**.
4. Kliknij pozycję **Dodaj**.
5. Wybierz lokalizację magazynu certyfikatów.
6. Kliknij przycisk **Zakończ**.
7. Kliknij przycisk **OK**.
8. Rozwiń węzeł **certyfikaty**.
9. Rozwiń węzeł magazynu certyfikatów.
10. Rozwiń węzeł podrzędny certyfikatu.
11. Wybierz certyfikat z listy.

## <a name="export-certificate"></a>Eksportowanie certyfikatu
W **Kreator eksportu certyfikatów**:

1. Kliknij przycisk **Dalej**.
2. Wybierz **tak**, następnie **Eksportuj klucz prywatny**.
3. Kliknij przycisk **Dalej**.
4. Wybierz format pliku żądanego wyniku.
5. Sprawdź wybrane opcje.
6. Sprawdź **hasło**.
7. Wpisz silne hasło i potwierdź je.
8. Kliknij przycisk **Dalej**.
9. Wpisz lub wyszukaj nazwę pliku miejsce przechowywania certyfikatu (Użyj. Rozszerzenie PFX).
10. Kliknij przycisk **Dalej**.
11. Kliknij przycisk **Zakończ**.
12. Kliknij przycisk **OK**.

## <a name="import-certificate"></a>Importowanie certyfikatu
W Kreatorze importu certyfikatów:

1. Wybierz lokalizację magazynu.
   
   * Wybierz **bieżącego użytkownika** jeśli tylko procesów uruchomionych w obszarze bieżący użytkownik będą uzyskiwać dostęp do usługi
   * Wybierz **komputera lokalnego** Jeśli inne procesy w tym komputerze będą uzyskiwać dostęp do usługi
2. Kliknij przycisk **Dalej**.
3. W przypadku importowania z pliku upewnij się, ścieżkę pliku.
4. Jeśli import. Plik PFX:
   1. Wprowadź hasło, ochrona klucza prywatnego
   2. Wybierz opcje importowania
5. Wybierz "W miejscu" certyfikaty w następującym magazynie
6. Kliknij pozycję **Browse (Przeglądaj)**.
7. Wybierz żądany magazyn.
8. Kliknij przycisk **Zakończ**.
   
   * Jeśli wybrano magazynie zaufany główny urząd certyfikacji, kliknij przycisk **tak**.
9. Kliknij przycisk **OK** na wszystkie okna dialogowe.

## <a name="upload-certificate"></a>Przekazywanie certyfikatu
W [portalu Azure](https://portal.azure.com/)

1. Wybierz **usługi w chmurze**.
2. Wybierz usługę w chmurze.
3. W górnym menu, kliknij przycisk **certyfikaty**.
4. Na dolnym pasku kliknij **przekazać**.
5. Wybierz plik certyfikatu.
6. Jeśli istnieje. PFX, wprowadź hasło klucza prywatnego.
7. Po zakończeniu skopiuj odcisk palca certyfikatu z nowy wpis na liście.

## <a name="other-security-considerations"></a>Inne zagadnienia dotyczące zabezpieczeń
Ustawienia protokołu SSL, w tym dokumencie opisano szyfrowania komunikacji między usługą i jej klientów, gdy punkt końcowy HTTPS jest używany. Jest to ważne, ponieważ poświadczenia dostępu do bazy danych i inne poufne informacje znajdują się w komunikacie. Należy jednak pamiętać, że usługa będzie się powtarzał wewnętrzny stan, w tym poświadczenia, w jego wewnętrznego tabele w bazie danych Microsoft Azure SQL w subskrypcji platformy Microsoft Azure zostały podane dla magazynu metadanych. Tej bazy danych został zdefiniowany jako część następujące ustawienie w pliku konfiguracji usługi (. Plik CSCFG): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Poświadczenia przechowywane w tej bazie danych są szyfrowane. Jednak najlepszym rozwiązaniem, sprawdź, czy role sieć web i proces roboczy wdrożeń usługi są zawsze aktualne i bezpieczne, ponieważ mają dostęp do bazy danych metadanych i certyfikat używany do szyfrowania i odszyfrowywania przechowywanych poświadczeń. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

