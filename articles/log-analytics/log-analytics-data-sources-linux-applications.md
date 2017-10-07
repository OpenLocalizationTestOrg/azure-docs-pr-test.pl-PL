---
title: "aaaCollect wydajność aplikacji systemu Linux w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera szczegółowe informacje dotyczące konfigurowania hello Agent pakietu OMS liczników wydajności systemu Linux toocollect MySQL i Apache HTTP Server."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Zbieraj liczniki wydajności dla aplikacji systemu Linux w analizy dzienników 
Ten artykuł zawiera szczegółowe informacje dotyczące konfigurowania hello [Agent pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect liczniki wydajności dla określonych aplikacji.  aplikacji Hello zawarte w tym artykule przedstawiono:  

- [MySQL](#MySQL)
- [Apache HTTP Server](#apache-http-server)

## <a name="mysql"></a>MySQL
Jeśli serwer MySQL lub MariaDB serwer zostanie wykryte na powitania komputera po zainstalowaniu agenta pakietu OMS hello, zostanie automatycznie zainstalowana dostawcy dla serwera MySQL monitorowania wydajności. Ten dostawca łączy toohello lokalnego MySQL/MariaDB tooexpose Statystyka wydajności serwera. Poświadczenia użytkownika MySQL musi być skonfigurowany tak, aby hello dostawcy mogą uzyskiwać dostęp do powitania serwera MySQL.

### <a name="configure-mysql-credentials"></a>Skonfiguruj poświadczenia MySQL
Hello MySQL OMI dostawcy wymaga wstępnie skonfigurowane użytkownika MySQL i zainstalowane w kolejności tooquery hello wydajności i informacje o kondycji z wystąpienia MySQL hello bibliotek klienta MySQL.  Te poświadczenia są przechowywane w pliku uwierzytelniania, który jest przechowywany na powitania agenta systemu Linux.  Plik authentication Hello określa jakiego adresu wiązania i nasłuchuje portu hello MySQL wystąpienia co poświadczenia toouse toogather metryki.  

Podczas instalacji hello Agent pakietu OMS dla systemu Linux hello MySQL OMI dostawcy rozpocznie skanowanie plików konfiguracyjnych my.cnf MySQL (lokalizacje domyślne) bind adres i port i częściowo hello zestaw plików uwierzytelniania MySQL OMI.

Plik authentication MySQL Hello jest przechowywany w `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Format pliku uwierzytelniania
Poniżej przedstawiono hello format hello plik authentication MySQL OMI

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

Witaj wpisy w pliku uwierzytelniania hello są opisane w hello w poniższej tabeli.

| Właściwość | Opis |
|:--|:--|
| Port | Reprezentuje hello bieżącego portu hello MySQL nasłuchuje wystąpienie. Port 0 określa, czy następujące właściwości hello są używane dla domyślnego wystąpienia. |
| Adres BIND| Bieżący bind MySQL — adres. |
| nazwa użytkownika| Wystąpienie serwera MySQL hello toomonitor toouse używać użytkownika MySQL. |
| Hasło kodowane w formacie Base64| Hasło użytkownika monitorowania MySQL hello zakodowane w formacie Base64. |
| Aktualizacje automatyczne| Określa czy toorescan dla zmian w pliku my.cnf hello i zastąpić plik MySQL OMI Authentication hello, gdy hello MySQL OMI dostawcy jest uaktualniany. |

### <a name="default-instance"></a>Domyślne wystąpienie
Hello MySQL OMI uwierzytelniania pliku można określić domyślnego wystąpienia i toomake numer portu wielu wystąpień MySQL na jednym hoście Linux łatwiejsze zarządzanie.  wystąpienie domyślne Hello jest oznaczona przez wystąpienie o portu 0. Wszystkie dodatkowe wystąpienia będzie dziedziczyć właściwości ustawione z hello domyślnego wystąpienia, chyba że określają różne wartości. Na przykład jeśli wystąpienie MySQL nasłuchiwanie na porcie "3308" zostanie dodany, powiązanego adresu hello domyślnego wystąpienia, username i password kodowany w standardzie Base64 będzie można tootry używane i monitorowanie wystąpienia hello nasłuchiwanie 3308. Jeśli wystąpienie hello na 3308 jest adresem tooanother powiązane i używa hello nazwa_użytkownika MySQL tego samego hasła pary tylko hello bind — adres jest niezbędny i hello inne właściwości dziedziczone.

Witaj w poniższej tabeli ma przykład wystąpienia ustawienia 

| Opis | Plik |
|:--|:--|
| Domyślne wystąpienie i wystąpienia z portem 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Domyślne wystąpienie i wystąpienia z portu 3308 i innej nazwy użytkownika i hasła. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Uwierzytelnianie programu MySQL OMI
Dołączone do instalacji hello hello MySQL OMI dostawca jest program pliku uwierzytelniania MySQL OMI, które mogą być używane tooedit hello MySQL OMI uwierzytelniania pliku. Hello uwierzytelniania programu można znaleźć w następującej lokalizacji hello.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> Plik poświadczeń Hello musi być do odczytu przez konto omsagent hello. Zalecane jest uruchomienie polecenia mycimprovauth hello jako omsgent.

Witaj Poniższa tabela zawiera szczegółowe informacje na powitania składni poświęcone mycimprovauth.

| Operacja | Przykład | Opis
|:--|:--|:--|
| AutoUpdate * false\|wartość true * | mycimprovauth autoupdate false | Ustawia, czy plik authentication hello zostanie automatycznie zaktualizowana na ponowne uruchomienie lub zaktualizować. |
| domyślne *powiązanego adresu nazwa_użytkownika hasło* | pwd głównych domyślnego 127.0.0.1 mycimprovauth | Ustawia hello domyślnego wystąpienia w hello plik authentication MySQL OMI.<br>pole hasła Hello powinny być wprowadzane w formacie zwykłego tekstu — hasło hello w hello MySQL OMI uwierzytelniania pliku będzie zakodowanych w Base 64. |
| Usuń * default\|numer_portu * | mycimprovauth 3308 | Usuwa określone wystąpienie hello albo domyślnie lub numer portu. |
| Pomoc | mycimprov pomocy | Drukuje listę poleceń toouse. |
| Drukuj | mycimprov drukowania | Drukuje łatwe tooread plik authentication MySQL OMI. |
| Zaktualizuj numer_portu *powiązanego adresu nazwa_użytkownika hasło* | mycimprov aktualizacji 3307 127.0.0.1 głównego pwd | Aktualizuje określone wystąpienie hello lub dodaje hello wystąpienia, jeśli nie istnieje. |

Witaj przedstawiono przykładowe polecenia zdefiniować domyślne konto użytkownika serwera MySQL hello localhost.  pole hasła Hello powinny być wprowadzane w formacie zwykłego tekstu — hasło hello w hello MySQL OMI uwierzytelniania pliku będzie zakodowanych w Base 64

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Uprawnienia bazy danych wymagane dla liczników wydajności MySQL
Witaj MySQL użytkownika wymaga następującego zapytania toocollect dane dotyczące wydajności serwera MySQL toohello dostępu. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


Witaj MySQL użytkownika wymaga również toohello dostępu wybierz następujące domyślne tabele.

- INFORMATION_SCHEMA
- MySQL. 

Te uprawnienia można otrzymać, uruchamiając następujące polecenia grant hello.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> tooa uprawnienia toogrant MySQL monitorowania hello użytkowników, udzielanie użytkownika musi mieć uprawnienie "GRANT option" hello, jak również udzielenia uprawnienia hello.

### <a name="define-performance-counters"></a>Zdefiniuj liczniki wydajności

Po skonfigurowaniu hello Agent pakietu OMS dla systemu Linux toosend danych tooLog Analytics, należy skonfigurować toocollect liczniki wydajności hello.  Użyj procedury hello [systemu Windows i Linux źródła danych wydajności w analizy dzienników](log-analytics-data-sources-windows-events.md) z licznikami hello w hello w poniższej tabeli.

| Nazwa obiektu | Nazwa licznika |
|:--|:--|
| Baza danych MySQL | Miejsce na dysku w bajtach |
| Baza danych MySQL | Tabele |
| Serwer MySQL | Przerwane połączenie protokołu Pct |
| Serwer MySQL | Procent użycia połączenia |
| Serwer MySQL | Użycie miejsca na dysku w bajtach |
| Serwer MySQL | Tabela pełne skanowanie Pct |
| Serwer MySQL | Pula buforów InnoDB trafień Pct |
| Serwer MySQL | Procent użycia pula buforu InnoDB |
| Serwer MySQL | Procent użycia pula buforu InnoDB |
| Serwer MySQL | Protokół Pct trafień pamięci podręcznej klucza |
| Serwer MySQL | Procent użycia klucza pamięci podręcznej |
| Serwer MySQL | Protokół Pct zapisu klucza pamięci podręcznej |
| Serwer MySQL | Procent trafień pamięci podręcznej zapytania |
| Serwer MySQL | Protokół Pct śliwek pamięci podręcznej zapytania |
| Serwer MySQL | Procent użycia pamięci podręcznej zapytania |
| Serwer MySQL | Procent trafień w pamięci podręcznej tabeli |
| Serwer MySQL | Procent użycia pamięci podręcznej tabeli |
| Serwer MySQL | Protokół Pct rywalizacji blokady tabeli |

## <a name="apache-http-server"></a>Apache HTTP Server 
W przypadku wykrycia Apache HTTP Server na komputerze powitania po zainstalowaniu pakietu omsagent hello, zostanie automatycznie zainstalowana dostawcy dla Apache HTTP Server monitorowania wydajności. Ten dostawca zależy od modułu Apache, które muszą zostać załadowane do hello Apache HTTP Server w kolejności tooaccess danych dotyczących wydajności. Moduł Hello mogą być ładowane z hello następujące polecenie:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache modułu monitorowania, uruchom następujące polecenie hello:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Zdefiniuj liczniki wydajności

Po skonfigurowaniu hello Agent pakietu OMS dla systemu Linux toosend danych tooLog Analytics, należy skonfigurować toocollect liczniki wydajności hello.  Użyj procedury hello [systemu Windows i Linux źródła danych wydajności w analizy dzienników](log-analytics-data-sources-windows-events.md) z licznikami hello w hello w poniższej tabeli.

| Nazwa obiektu | Nazwa licznika |
|:--|:--|
| Apache HTTP Server | Zajętych pracowników |
| Apache HTTP Server | Bezczynnych pracowników |
| Apache HTTP Server | Protokół PCT zajętych pracowników. |
| Apache HTTP Server | Łączna liczba Pct Procesora |
| Apache Host wirtualny | Błędów na minutę - klienta |
| Apache Host wirtualny | Błędów na minutę - serwer |
| Apache Host wirtualny | KB na żądanie |
| Apache Host wirtualny | Żądania KB na sekundę |
| Apache Host wirtualny | Liczba żądań na sekundę |



## <a name="next-steps"></a>Następne kroki
* [Zebrać liczników wydajności](log-analytics-data-sources-performance-counters.md) z agentów systemu Linux.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań. 
