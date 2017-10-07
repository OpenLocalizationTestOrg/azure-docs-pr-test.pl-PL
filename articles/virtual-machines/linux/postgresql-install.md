---
title: "aaaSet się PostgreSQL na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i skonfigurować PostgreSQL na maszynie wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Instalowanie i konfigurowanie rozwiązania PostgreSQL na platformie Azure
PostgreSQL to podobne tooOracle zaawansowane open source bazy danych i bazy danych DB2. Zawiera on funkcje gotowe enterprise, takie jak ACID pełnej zgodności, niezawodne przetwarzania transakcyjnego i sterowania współbieżnością wielu wersji. Obsługuje ona również standardy, takie jak ANSI SQL i SQL/MED (w tym otoki obcego danych Oracle, MySQL, MongoDB i wielu innych). Jest to rozszerzalna o obsługę ponad 12 procedurach języków, indeksy GIN i GiST obsługę danych przestrzennych i wiele funkcji NoSQL dla formatu JSON lub aplikacji opartych na protokole klucz wartość.

W tym artykule przedstawiono sposób tooinstall i skonfigurować PostgreSQL na maszynie wirtualnej platformy Azure systemem Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Zainstaluj PostgreSQL
> [!NOTE]
> Musi już mieć Azure maszyny wirtualnej z systemem Linux w kolejności toocomplete w tym samouczku. toocreate i konfigurowanie maszyny Wirtualnej systemu Linux, aby kontynuować, zobacz [samouczek maszyny Wirtualnej systemu Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

W takim przypadku należy użyć portu 1999 jako hello PostgreSQL portu.  

Połącz toohello maszyny Wirtualnej systemu Linux utworzone przy użyciu programu PuTTY. Jeśli jest to powitania po raz pierwszy używasz maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [jak tooUse SSH z systemem Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn jak programu PuTTY toouse tooa tooconnect maszyny Wirtualnej systemu Linux.

1. Witaj uruchom następujące polecenie tooswitch toohello głównego (Administrator):
   
        # sudo su -
2. Niektórych dystrybucji zależnościami, które należy zainstalować przed zainstalowaniem PostgreSQL. Sprawdź, czy Twoje distro na tej liście, a następnie uruchom polecenie odpowiednie hello:
   
   * Red Hat podstawowego systemu Linux:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian podstawowego systemu Linux:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Pobierz PostgreSQL w katalogu głównym hello, a następnie Rozpakuj pakiet hello:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Przykładem jest Hello powyżej. Można znaleźć hello bardziej szczegółowe Pobierz adres w hello [indeks/pub/źródło/](https://ftp.postgresql.org/pub/source/).
4. toostart hello kompilacji, uruchom następujące polecenia:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Toobuild wszystkie czynności, które mogą być tworzone, w tym dokumentację hello (strony HTML i man) oraz dodatkowych modułów (contrib), należy uruchomić hello zamiast tego następujące polecenie:
   
        # gmake install-world
   
    Powinien zostać wyświetlony powitania po komunikat potwierdzenia:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Skonfiguruj PostgreSQL
1. (Opcjonalnie) Tworzenie łącza symbolicznego hello tooshorten PostgreSQL odwołania toonot obejmują hello numer wersji:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Utwórz katalog hello bazy danych:
   
        # mkdir -p /opt/pgsql_data
3. Tworzenie użytkowników nie głównego i modyfikowanie profilu użytkownika. Następnie przełącz nowy użytkownik toothis (nazywane *postgres* w naszym przykładzie):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Ze względów bezpieczeństwa PostgreSQL używa tooinitialize użytkownika głównego z systemem innym niż, uruchomić lub zamknąć hello bazy danych.
   > 
   > 
4. Edytuj hello *bash_profile* pliku przez wprowadzenie polecenia hello poniżej. Te wiersze zostaną dodane toohello koniec hello *bash_profile* pliku:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Wykonanie hello *bash_profile* pliku:
   
        $ source .bash_profile
6. Sprawdzanie poprawności instalacji za pomocą hello następujące polecenie:
   
        $ which psql
   
    Jeśli instalacja zakończy się pomyślnie, zostanie wyświetlony powitania po odpowiedzi:
   
        /opt/pgsql/bin/psql
7. Możesz również sprawdzić wersji PostgreSQL hello:
   
        $ psql -V
8. Zainicjuj bazę danych hello:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Powinien zostać wyświetlony hello następujące dane wyjściowe:

![Obraz](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Konfigurowanie PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Uruchom następujące polecenia hello:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Zmodyfikuj dwie zmienne hello /etc/init.d/postgresql pliku. Prefiks Hello jest ustawiona na ścieżkę instalacji toohello PostgreSQL: **/opt/pgsql**. PGDATA ustawiono toohello ścieżki do magazynu danych programu PostgreSQL: **/opt/pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Obraz](./media/postgresql-install/no2.png)

Zmień hello toomake pliku wykonywalnego go:

    # chmod +x /etc/init.d/postgresql

Uruchom PostgreSQL:

    # /etc/init.d/postgresql start

Sprawdź, czy punkt końcowy hello PostgreSQL na:

    # netstat -tunlp|grep 1999

Powinny być widoczne następujące dane wyjściowe hello:

![Obraz](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Połączenia bazy danych Postgres toohello
Ponownie przełączyć toohello postgres użytkownika:

    # su - postgres

Utwórz bazę danych Postgres:

    $ createdb events

Połączenie bazy danych zdarzeń toohello nowo utworzony:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Tworzenie i usuwanie tabeli Postgres
Teraz, gdy nawiązano połączenie toohello bazy danych, można utworzyć tabele w nim.

Na przykład utwórz nową tabelę Postgres przykład za pomocą hello następujące polecenie:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Teraz skonfigurować cztery kolumny tabeli z hello następujące nazwy kolumn i ograniczenia:

1. Witaj, które kolumny "name" ma ograniczone przez toobe polecenia VARCHAR hello w obszarze 20 znaków długości.
2. Kolumna "żywności" Hello wskazuje elementu żywności hello, pozwalających każda osoba. VARCHAR ogranicza to toobe tekstu w obszarze 30 znaków.
3. Witaj "potwierdzone" rekordy kolumny czy hello osoba potwierdziła przyjęcie składkowe toohello. Witaj dopuszczalne wartości to "Y" i "N".
4. Przedstawia kolumnę Hello "date" zarejestrowała się w usłudze hello zdarzeń. Postgres wymaga zapisać daty w postaci rrrr mm-dd.

Po pomyślnym utworzeniu tabeli powinny być widoczne następujące hello:

![Obraz](./media/postgresql-install/no4.png)

Struktura tabeli hello można również wykonać za pomocą następującego polecenia hello:

![Obraz](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Dodaj tabelę tooa danych
Najpierw należy wstawić informacji do wiersza:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Te dane wyjściowe powinny być widoczne:

![Obraz](./media/postgresql-install/no6.png)

Tabelę można dodać kilka więcej osób toohello również. Poniżej przedstawiono niektóre opcje, lub utworzyć własny:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Pokaż tabele
Użyj hello następujące polecenia tooshow tabeli:

    select * from potluck;

dane wyjściowe Hello to:

![Obraz](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Usuń dane w tabeli
Witaj Użyj następującego polecenia toodelete dane w tabeli:

    delete from potluck where name=’John’;

Spowoduje to usunięcie wszystkich informacji hello hello wiersza "Jan". dane wyjściowe Hello to:

![Obraz](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Aktualizuj dane w tabeli
Witaj Użyj następującego polecenia tooupdate dane w tabeli. Dla, Sandy potwierdzi, że jest ona uczestnictwa, więc zostanie zmieniona jej RSVP z "N" za "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Uzyskaj więcej informacji o PostgreSQL
Teraz, gdy została ukończona instalacja hello PostgreSQL w maszynie Wirtualnej systemu Linux platformy Azure, można oglądać przy użyciu go na platformie Azure. toolearn więcej informacji na temat PostgreSQL, odwiedź stronę hello [PostgreSQL witryny sieci Web](http://www.postgresql.org/).

