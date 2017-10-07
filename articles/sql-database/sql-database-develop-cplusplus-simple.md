---
title: "aaaConnect tooSQL bazy danych przy użyciu C i C++ | Dokumentacja firmy Microsoft"
description: "Użyj hello próbki kodu w tym toobuild szybki start nowoczesnych aplikacji w języku C++ i obsługiwanej przez zaawansowanych relacyjnej bazy danych w chmurze hello z bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Połącz tooSQL bazy danych przy użyciu C i C++
Ten wpis jest przeznaczony dla deweloperów C i C++ w trakcie tooAzure tooconnect bazy danych SQL. Podzielona jest sekcje dzięki czemu można przechodzić toohello sekcja, która najlepiej przechwytuje zainteresowanie. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Wymagania wstępne dotyczące samouczka C/C++ hello
Upewnij się, że masz hello następujące elementy:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu uzyskania [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Program [Visual Studio](https://www.visualstudio.com/downloads/). Należy zainstalować toobuild składników języka C++ hello i uruchomienia tego przykładu.
* [Programowanie Linux programu Visual Studio](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Jeśli tworzysz w systemie Linux, należy również zainstalować rozszerzenia programu Visual Studio Linux hello. 

## <a id="AzureSQL"></a>Azure SQL Database i programu SQL Server na maszynach wirtualnych
Azure SQL jest oparty na programie Microsoft SQL Server i jest zaprojektowana tooprovide wysokiej dostępności, wydajności i skalowalności usługi. Istnieje wiele korzyści toousing SQL Azure za pośrednictwem zastrzeżonych uruchomiony lokalnie bazy danych. Z usługami SQL Azure nie ma tooinstall, konfigurowanie, obsługa lub zarządzać bazy danych, ale tylko hello zawartości i struktury hello bazy danych. Typowe rzeczy, które możemy martwić w przypadku baz danych, takich jak odporność na uszkodzenia i nadmiarowość są wbudowane w. 

Platforma Azure ma obecnie dwie opcje do obsługi obciążeń serwera SQL: baza danych Azure SQL, bazy danych jako usługę i programu SQL server na maszynach wirtualnych (VM). Firma Microsoft nie otrzyma do szczegółów dotyczących hello różnice między tymi dwiema z tą różnicą, że baza danych Azure SQL jest najlepsze rozwiązanie dla nowej aplikacji opartych na chmurze tootake zaletą hello oszczędności, i podaj optymalizacji wydajności usługi w chmurze. Planując migracja lub rozszerzanie lokalnej aplikacji toohello chmury, programu SQL server na maszynie wirtualnej Azure może działać lepiej dla Ciebie. prosty rzeczy tookeep tego artykułu, Utwórzmy bazy danych Azure SQL. 

## <a id="ODBC"></a>Technologie dostępu do danych: ODBC i OLE DB
Nie różni się tooAzure połączenia bazy danych SQL i obecnie istnieją dwa sposoby tooconnect toodatabases: ODBC (ODBC) i OLE DB (łączenie i osadzanie obiektów bazy danych). W ostatnich latach ma wyrównane Microsoft [ODBC dla dostępu do natywnych danych relacyjnych](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC jest stosunkowo proste, a także znacznie szybsze niż OLE DB. Hello tutaj tylko zastrzeżenie: jest, że ODBC używać starego interfejsu API w stylu języka C. 

## <a id="Create"></a>Krok 1: Tworzenie bazy danych Azure SQL
Zobacz hello [wprowadzenie strony](sql-database-get-started-portal.md) toolearn jak toocreate przykładowej bazy danych.  Alternatywnie, można to wykonać [krótki film dwie minuty](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate bazy danych Azure SQL przy użyciu hello portalu Azure.

## <a id="ConnectionString"></a>Krok 2: Uzyskanie parametrów połączenia
Po zainicjowano bazy danych Azure SQL, należy toocarry limit hello następujące informacje o połączeniu toodetermine kroki i dodać IP klienta dostępu zapory. 

W [portalu Azure](https://portal.azure.com/), przejdź parametry połączenia ODBC bazy danych Azure SQL tooyour przy użyciu hello **Pokaż parametry połączenia bazy danych** wyświetlane jako część sekcji Przegląd hello bazy danych: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Kopiuj zawartość hello hello **ODBC (obejmuje Node.js) [uwierzytelnianie SQL]** ciągu. Możemy użyć tego ciągu nowsze tooconnect z naszych interpreter wiersza polecenia języka C++ ODBC. Ten ciąg zawiera szczegółowe informacje, takie jak sterownik hello, serwera i inne parametry połączenia bazy danych. 

## <a id="Firewall"></a>Krok 3: Dodawanie zapory toohello IP
Przejdź toohello sekcji zapory dla serwera bazy danych i dodać Twojego [zapory toohello IP klienta przy użyciu tych kroków](sql-database-configure-firewall-settings.md) toomake się, że firma Microsoft może nawiązać połączenia: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

W tym momencie zostały skonfigurowane w bazie danych SQL Azure i są gotowe tooconnect w kodzie C++. 

## <a id="Windows"></a>Krok 4: Łączenie się z aplikacji systemu Windows C/C++
Możesz łatwo połączyć tooyour [bazy danych SQL Azure za pośrednictwem sterownika ODBC w systemie Windows za pomocą tego przykładu](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) który kompiluje się z programem Visual Studio. przykład Witaj implementuje ODBC interpreter wiersza polecenia, które mogą być używane tooconnect tooour bazy danych SQL Azure. W tym przykładzie przyjmuje albo bazy danych źródłowy plik o nazwie pliku (DSN) jako argumentu wiersza polecenia lub parametry połączenia pełne hello, które firma Microsoft wcześniej skopiowany z hello portalu Azure. Wywołaj hello strony właściwości dla tego projektu i Wklej parametry połączenia hello jako argumentu, jak pokazano poniżej: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Upewnij się, że Podaj szczegóły uwierzytelniania prawo hello bazy danych jako część tego ciągu połączenia bazy danych. 

Uruchamianie toobuild aplikacji hello go. Powinny pojawić się hello następujące okna weryfikowania pomyślnego nawiązania połączenia. Możesz nawet uruchamiać niektórych podstawowych poleceń SQL, takich jak **Utwórz tabelę** toovalidate łączność z bazą danych:

![Polecenia SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Alternatywnie można utworzyć pliku DSN przy użyciu Kreatora hello, który jest uruchamiany, jeśli zostały podane nie argumenty polecenia. Zaleca się, spróbuj wykonać tę opcję, a także. Można użyć tego pliku DSN do automatyzacji i ochrona ustawienia uwierzytelniania: 

![Tworzenie pliku DSN](./media/sql-database-develop-cplusplus-simple/datasource.png)

Gratulacje! Pomyślnie teraz nawiązano tooAzure SQL przy użyciu języka C++ i ODBC w systemie Windows. Można kontynuować odczytu toodo hello takie same dla platformy Linux również. 

## <a id="Linux"></a>Krok 5: Łączenie z aplikacji Linux C/C++
W przypadku, gdy nie wiesz wiadomości powitania jeszcze programu Visual Studio umożliwia teraz toodevelop aplikacji C++ Linux, a także. Informacje o tym nowy scenariusz w hello [Visual C++ dla systemu Linux programowanie](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blogu. toobuild dla systemu Linux, należy komputer zdalny, którym jest uruchomiona distro Twojego systemu Linux. Jeśli nie masz dostępne, można ustawić jeden szybko przy użyciu [maszyn wirtualnych Azure Linux](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

W tym samouczku Załóżmy, że masz dystrybucji Ubuntu 16.04 Linux Konfigurowanie. kroki Hello tutaj również należy zastosować tooUbuntu 15.10, Red Hat 6 i Red Hat 7. 

Witaj następujące kroki instalacji hello bibliotek wymaganych dla programu SQL i ODBC dla Twojej distro:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Uruchom program Visual Studio. W obszarze Narzędzia -> Opcje -> Cross Platform -> Menedżera połączeń, Dodaj pole Linux tooyour połączenia: 

![Opcje narzędzia](./media/sql-database-develop-cplusplus-simple/tools.png)

Po nawiązaniu połączenia za pomocą protokołu SSH, należy utworzyć pusty (Linux) szablon projektu: 

![Nowy szablon projektu](./media/sql-database-develop-cplusplus-simple/template.png)

Następnie można dodać [C nowy plik źródłowy i zastąp go z tą zawartością](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Przy użyciu hello funkcja ODBC API SQLAllocHandle, operacja SQLSetConnectAttr i SQLDriverConnect, należy tooinitialize może być i ustanowienia tooyour połączenia bazy danych. Podobnie jak próbki Windows ODBC hello, należy tooreplace hello SQLDriverConnect wywołania ze szczegółami hello skopiowany z portalu Azure hello wcześniej parametry ciągu połączenia bazy danych. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Witaj ostatni element toodo przed kompilowanie tooadd **odbc** jako zależności biblioteki: 

![Dodawanie jako biblioteki wejściowej ODBC](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch aplikacji, wywołaj hello konsoli systemu Linux z hello **debugowania** menu: 

![Konsola systemu Linux](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Jeśli połączenie zakończyło się pomyślnie, powinien zostać wyświetlony hello nazwa bieżącej bazy danych drukowana w hello konsoli systemu Linux: 

![Dane wyjściowe z okna konsoli systemu Linux](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Gratulacje! Pomyślnie ukończono samouczek hello i teraz można podłączyć tooyour bazy danych SQL Azure z C++ na platformach systemu Windows i Linux.

## <a id="GetSolution"></a>Pobierz kompletnego rozwiązania samouczka hello C/C++
Można znaleźć rozwiązania GetStarted hello, który zawiera wszystkie przykłady hello w tym artykule w witrynie github:

* [Przykładowe Windows w języku C++ ODBC](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Pobierz tooAzure tooconnect przykład ODBC C++ Windows hello SQL
* [Przykładowe ODBC C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Pobierz hello Linux C++ ODBC próbki tooconnect tooAzure SQL

## <a name="next-steps"></a>Następne kroki
* Przejrzyj hello [omówienie tworzenia bazy danych SQL](sql-database-develop-overview.md)
* Więcej informacji na temat hello [dokumentacja interfejsu API ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Wzorce projektowe dla wielodostępnych aplikacji SaaS wykorzystujących usługę Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Eksploruj wszystkich hello [możliwości bazy danych SQL](https://azure.microsoft.com/services/sql-database/)

