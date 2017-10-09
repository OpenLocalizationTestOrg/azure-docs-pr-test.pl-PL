---
title: "połączenie SSL aaaConfigure w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "Instrukcje i informacje tooconfigure bazy danych Azure, PostgreSQL i tooproperly skojarzonych aplikacji korzystają z połączeń SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Konfiguracja połączenia SSL w bazie danych Azure dla PostgreSQL
Bazy danych platformy Azure dla PostgreSQL preferowany, połączenie z klienta aplikacji toohello PostgreSQL usługi przy użyciu protokołu Secure Sockets Layer (SSL). Wymuszanie połączenia SSL między serwerem bazy danych i aplikacji klienckich pomaga chronić przed atakami "man w środku powitania" hello strumienia danych między serwerem hello i aplikacji są szyfrowane.

Domyślnie hello PostgreSQL usługa bazy danych jest skonfigurowany toorequire połączenia SSL. Opcjonalnie możesz wyłączyć wymaganie protokołu SSL dla połączenia tooyour usługi bazy danych, jeśli aplikacja kliencka nie obsługuje łączności SSL. 

## <a name="enforcing-ssl-connections"></a>Wymuszanie połączeń SSL
Wszystkie bazy danych dla serwerów PostgreSQL za pośrednictwem hello portalu Azure i interfejsu wiersza polecenia Azure wymuszanie połączeń SSL jest domyślnie włączona. 

Podobnie parametry połączenia, które są wstępnie zdefiniowanego w ustawieniach "Parametry połączenia" hello, w obszarze serwera w portalu Azure hello uwzględnia hello wymagane parametry dla typowych języków tooconnect tooyour serwera bazy danych przy użyciu protokołu SSL. Witaj parametru SSL w zależności od hello łącznika, na przykład "ssl = true" lub "sslmode = wymagają" lub "sslmode = wymagane" i innych zmian.

## <a name="configure-enforcement-of-ssl"></a>Konfigurowanie wymuszania protokołu SSL
Opcjonalnie można wyłączyć wymuszenie łączności SSL. Microsoft Azure zaleca włączyć tooalways **połączenia SSL wymusić** ustawienie w celu zwiększenia bezpieczeństwa.

### <a name="using-hello-azure-portal"></a>Przy użyciu hello portalu Azure
Odwiedź bazy danych Azure, PostgreSQL serwera, a następnie kliknij przycisk **zabezpieczenia połączeń**. Użyj tooenable przycisk przełączania hello lub wyłącz hello **połączenia SSL wymusić** ustawienie. Następnie kliknij przycisk **Save** (Zapisz). 

![Zabezpieczenia połączeń — Wyłącz wymuszanie protokołu SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Ustawienie hello można potwierdzić, sprawdzając hello **omówienie** hello toosee strony **stan wymuszenia SSL** wskaźnika.

### <a name="using-azure-cli"></a>Korzystanie z interfejsu wiersza polecenia platformy Azure
Można włączyć lub wyłączyć hello **wymuszania ssl** przy użyciu parametru `Enabled` lub `Disabled` odpowiednio wartości wiersza polecenia platformy Azure.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Upewnij się, obsługuje Twojej aplikacji lub struktury połączeń SSL
Wiele wspólnej struktury aplikacji używających PostgreSQL dla usług bazy danych, takich jak Drupal i Django, nie należy włączać SSL domyślnie podczas instalacji. Włączenie łączności SSL muszą być konfigurowane po instalacji lub przy użyciu interfejsu wiersza polecenia polecenia toohello określonych aplikacji. Jeśli hello skojarzonych aplikacji nie jest prawidłowo skonfigurowany serwer PostgreSQL wymusza połączeń SSL, aplikacja hello może zakończyć się niepowodzeniem tooconnect tooyour bazy danych serwera. Zapoznaj się toolearn dokumentacją aplikacji, jak tooenable połączeń SSL.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Aplikacje wymagające weryfikacji certyfikatów dla połączeń SSL
W niektórych przypadkach aplikacje wymagają lokalnego pliku certyfikatu bezpiecznego wygenerowane z zaufanych tooconnect pliku (.cer) certyfikatu urzędu certyfikacji. Zobacz hello następującego pliku .cer hello tooobtain kroki, Dekoduj certyfikat hello i powiązać ją tooyour aplikacji.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Pobierz plik certyfikatu hello z hello certyfikatu urzędu certyfikacji 
Witaj potrzebnego certyfikatu toocommunicate za pośrednictwem protokołu SSL z bazą danych Azure dla znajduje się serwer PostgreSQL [tutaj](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Pobierz plik certyfikatu hello lokalnie.

### <a name="download-and-install-openssl-on-your-machine"></a>Pobierz i zainstaluj biblioteki OpenSSL na tym komputerze 
plik certyfikatu hello toodecode potrzebne do Twojej aplikacji tooconnect bezpiecznie tooyour serwera bazy danych, należy tooinstall biblioteki OpenSSL na komputerze lokalnym.

#### <a name="for-linux-os-x-or-unix"></a>Dla systemu Linux, Unix lub OS X
biblioteki OpenSSL Hello znajdują się w kodzie źródłowym bezpośrednio z hello [Foundation oprogramowania biblioteki OpenSSL](http://www.openssl.org). Witaj poniższe instrukcje pomocne przy hello kroki niezbędne tooinstall biblioteki OpenSSL na komputerze z systemem Linux. W tym artykule używa poleceń znane toowork na Ubuntu 12.04 i wyższych.

Otwórz sesję terminala i zainstaluj biblioteki OpenSSL
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Wyodrębnij pliki hello z hello pakietu
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Wprowadź katalog hello, w którym zostały wyodrębnione pliki hello. Domyślnie należy go w następujący sposób.

```bash
cd openssl-1.1.0e
```
Konfigurowanie biblioteki OpenSSL, wykonując następujące polecenia hello. Hello pliki w folderze inne niż /usr/local/openssl, należy się następujące hello toochange odpowiednio.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Biblioteki OpenSSL jest skonfigurowany prawidłowo, trzeba toocompile on tooconvert certyfikatu. toocompile, uruchom następujące polecenie hello:

```bash
make
```
Po zakończeniu kompilacji jest gotowy tooinstall biblioteki OpenSSL jako plik wykonywalny, uruchamiając następujące polecenie hello:
```bash
make install
```
tooconfirm zostały pomyślnie zainstalowane biblioteki OpenSSL w systemie, hello uruchom następujące polecenie i sprawdź, czy możesz uzyskać hello toomake samych danych wyjściowych.

```bash
/usr/local/openssl/bin/openssl version
```
W przypadku powodzenia powinny być widoczne następujące wiadomość hello.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Dla systemu Windows
Instalowanie biblioteki OpenSSL na komputerach z systemem Windows można wykonać w hello następujące sposoby:
1. **(Zalecane)**  Za pomocą wbudowanych funkcji Bash dla systemu Windows hello w Windows 10 i nowszych, biblioteki OpenSSL jest instalowany domyślnie. Instrukcje dotyczące sposobu tooenable funkcji Bash dla systemu Windows w systemie Windows 10 można znaleźć [tutaj](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Za pomocą pobierania określonej przez społeczność hello aplikacji Win32/64. Podczas hello biblioteki OpenSSL Software Foundation Podaj ani nie zatwierdza wszystkie określone składniki Instalatora Windows, zawierają listę dostępnych instalatorów [tutaj](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Dekoduj plik certyfikatu
Witaj pobrane głównego urzędu certyfikacji, plik jest w formacie zaszyfrowanym. Użyj pliku certyfikatu hello toodecode biblioteki OpenSSL. toodo tak, uruchom to polecenie biblioteki OpenSSL:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>Łączenie tooAzure bazy danych dla PostgreSQL przy użyciu uwierzytelniania certyfikatu SSL
Teraz, certyfikatu pomyślnie zostały zdekodowany, teraz można podłączyć serwer bazy danych tooyour bezpiecznie za pośrednictwem protokołu SSL. tooallow weryfikacji certyfikatu serwera, certyfikat hello muszą być umieszczone w hello ~/.postgresql/root.crt pliku w katalogu macierzystego użytkownika hello. (Microsoft Windows hello pliku jest o nazwie % APPDATA%\postgresql\root.crt.). następujące Hello zawiera instrukcje podłączania tooAzure bazy danych dla PostgreSQL.

> [!NOTE]
> Obecnie jest to znany problem, jeśli używasz "sslmode Sprawdź Full" w usłudze toohello połączenia hello połączenia zakończy się niepowodzeniem z hello następujący błąd: _certyfikatu serwera dla "&lt;region&gt;. Control.Database.Windows.NET"(i 7 innych nazw) nie odpowiada nazwie hosta"&lt;servername&gt;. postgres.database.azure.com "._
> Jeśli "sslmode Sprawdź Full" jest wymagane, użyj Konwencja nazewnictwa serwerów hello  **&lt;servername&gt;. database.windows.net** jako nazwy hosta w ciągu połączenia. Planujemy tooremove to ograniczenie w przyszłości hello. Połączenia przy użyciu innych [tryby SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) powinno być kontynuowane konwencji nazewnictwa hosta hello preferowane toouse  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Za pomocą narzędzia wiersza polecenia psql
Witaj poniższy przykład przedstawia sposób toosuccessfully łączenia z serwerem PostgreSQL tooyour przy użyciu narzędzia wiersza polecenia psql hello. Użyj hello `root.crt` plik utworzony i hello `sslmode=verify-ca` lub `sslmode=verify-full` opcji.

Przy użyciu interfejsu wiersza polecenia PostgreSQL hello, wykonaj następujące polecenie hello:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
W razie powodzenia pojawi się hello następujące dane wyjściowe:
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>Za pomocą narzędzia pgAdmin graficznego interfejsu użytkownika
Konfigurowanie tooconnect pgAdmin 4 bezpiecznie za pośrednictwem protokołu SSL wymaga tooset hello `SSL mode = Verify-CA` lub `SSL mode = Verify-Full` w następujący sposób:

![Zrzut ekranu przedstawiający pgAdmin — połączenie — tryb SSL wymagają](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Następne kroki
Przegląd różnych opcji łączności aplikacji po [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)
