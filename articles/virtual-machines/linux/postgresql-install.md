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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="ae60c-103">Instalowanie i konfigurowanie rozwiązania PostgreSQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ae60c-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="ae60c-104">PostgreSQL to podobne tooOracle zaawansowane open source bazy danych i bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="ae60c-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="ae60c-105">Zawiera on funkcje gotowe enterprise, takie jak ACID pełnej zgodności, niezawodne przetwarzania transakcyjnego i sterowania współbieżnością wielu wersji.</span><span class="sxs-lookup"><span data-stu-id="ae60c-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="ae60c-106">Obsługuje ona również standardy, takie jak ANSI SQL i SQL/MED (w tym otoki obcego danych Oracle, MySQL, MongoDB i wielu innych).</span><span class="sxs-lookup"><span data-stu-id="ae60c-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="ae60c-107">Jest to rozszerzalna o obsługę ponad 12 procedurach języków, indeksy GIN i GiST obsługę danych przestrzennych i wiele funkcji NoSQL dla formatu JSON lub aplikacji opartych na protokole klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="ae60c-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="ae60c-108">W tym artykule przedstawiono sposób tooinstall i skonfigurować PostgreSQL na maszynie wirtualnej platformy Azure systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="ae60c-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="ae60c-109">Zainstaluj PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ae60c-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="ae60c-110">Musi już mieć Azure maszyny wirtualnej z systemem Linux w kolejności toocomplete w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ae60c-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="ae60c-111">toocreate i konfigurowanie maszyny Wirtualnej systemu Linux, aby kontynuować, zobacz [samouczek maszyny Wirtualnej systemu Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae60c-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="ae60c-112">W takim przypadku należy użyć portu 1999 jako hello PostgreSQL portu.</span><span class="sxs-lookup"><span data-stu-id="ae60c-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="ae60c-113">Połącz toohello maszyny Wirtualnej systemu Linux utworzone przy użyciu programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ae60c-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="ae60c-114">Jeśli jest to powitania po raz pierwszy używasz maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [jak tooUse SSH z systemem Linux na platformie Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn jak programu PuTTY toouse tooa tooconnect maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ae60c-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="ae60c-115">Witaj uruchom następujące polecenie tooswitch toohello głównego (Administrator):</span><span class="sxs-lookup"><span data-stu-id="ae60c-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="ae60c-116">Niektórych dystrybucji zależnościami, które należy zainstalować przed zainstalowaniem PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ae60c-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="ae60c-117">Sprawdź, czy Twoje distro na tej liście, a następnie uruchom polecenie odpowiednie hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="ae60c-118">Red Hat podstawowego systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="ae60c-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="ae60c-119">Debian podstawowego systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="ae60c-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="ae60c-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="ae60c-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="ae60c-121">Pobierz PostgreSQL w katalogu głównym hello, a następnie Rozpakuj pakiet hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="ae60c-122">Przykładem jest Hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="ae60c-122">hello above is an example.</span></span> <span data-ttu-id="ae60c-123">Można znaleźć hello bardziej szczegółowe Pobierz adres w hello [indeks/pub/źródło/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="ae60c-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="ae60c-124">toostart hello kompilacji, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="ae60c-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="ae60c-125">Toobuild wszystkie czynności, które mogą być tworzone, w tym dokumentację hello (strony HTML i man) oraz dodatkowych modułów (contrib), należy uruchomić hello zamiast tego następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ae60c-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="ae60c-126">Powinien zostać wyświetlony powitania po komunikat potwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="ae60c-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="ae60c-127">Skonfiguruj PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ae60c-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="ae60c-128">(Opcjonalnie) Tworzenie łącza symbolicznego hello tooshorten PostgreSQL odwołania toonot obejmują hello numer wersji:</span><span class="sxs-lookup"><span data-stu-id="ae60c-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="ae60c-129">Utwórz katalog hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="ae60c-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="ae60c-130">Tworzenie użytkowników nie głównego i modyfikowanie profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae60c-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="ae60c-131">Następnie przełącz nowy użytkownik toothis (nazywane *postgres* w naszym przykładzie):</span><span class="sxs-lookup"><span data-stu-id="ae60c-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="ae60c-132">Ze względów bezpieczeństwa PostgreSQL używa tooinitialize użytkownika głównego z systemem innym niż, uruchomić lub zamknąć hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ae60c-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="ae60c-133">Edytuj hello *bash_profile* pliku przez wprowadzenie polecenia hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="ae60c-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="ae60c-134">Te wiersze zostaną dodane toohello koniec hello *bash_profile* pliku:</span><span class="sxs-lookup"><span data-stu-id="ae60c-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="ae60c-135">Wykonanie hello *bash_profile* pliku:</span><span class="sxs-lookup"><span data-stu-id="ae60c-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="ae60c-136">Sprawdzanie poprawności instalacji za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ae60c-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="ae60c-137">Jeśli instalacja zakończy się pomyślnie, zostanie wyświetlony powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="ae60c-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="ae60c-138">Możesz również sprawdzić wersji PostgreSQL hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="ae60c-139">Zainicjuj bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="ae60c-140">Powinien zostać wyświetlony hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ae60c-140">You should receive hello following output:</span></span>

![Obraz](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="ae60c-142">Konfigurowanie PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ae60c-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="ae60c-143">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="ae60c-144">Zmodyfikuj dwie zmienne hello /etc/init.d/postgresql pliku.</span><span class="sxs-lookup"><span data-stu-id="ae60c-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="ae60c-145">Prefiks Hello jest ustawiona na ścieżkę instalacji toohello PostgreSQL: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="ae60c-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="ae60c-146">PGDATA ustawiono toohello ścieżki do magazynu danych programu PostgreSQL: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="ae60c-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![Obraz](./media/postgresql-install/no2.png)

<span data-ttu-id="ae60c-148">Zmień hello toomake pliku wykonywalnego go:</span><span class="sxs-lookup"><span data-stu-id="ae60c-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="ae60c-149">Uruchom PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="ae60c-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="ae60c-150">Sprawdź, czy punkt końcowy hello PostgreSQL na:</span><span class="sxs-lookup"><span data-stu-id="ae60c-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="ae60c-151">Powinny być widoczne następujące dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-151">You should see hello following output:</span></span>

![Obraz](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="ae60c-153">Połączenia bazy danych Postgres toohello</span><span class="sxs-lookup"><span data-stu-id="ae60c-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="ae60c-154">Ponownie przełączyć toohello postgres użytkownika:</span><span class="sxs-lookup"><span data-stu-id="ae60c-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="ae60c-155">Utwórz bazę danych Postgres:</span><span class="sxs-lookup"><span data-stu-id="ae60c-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="ae60c-156">Połączenie bazy danych zdarzeń toohello nowo utworzony:</span><span class="sxs-lookup"><span data-stu-id="ae60c-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="ae60c-157">Tworzenie i usuwanie tabeli Postgres</span><span class="sxs-lookup"><span data-stu-id="ae60c-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="ae60c-158">Teraz, gdy nawiązano połączenie toohello bazy danych, można utworzyć tabele w nim.</span><span class="sxs-lookup"><span data-stu-id="ae60c-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="ae60c-159">Na przykład utwórz nową tabelę Postgres przykład za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ae60c-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="ae60c-160">Teraz skonfigurować cztery kolumny tabeli z hello następujące nazwy kolumn i ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="ae60c-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="ae60c-161">Witaj, które kolumny "name" ma ograniczone przez toobe polecenia VARCHAR hello w obszarze 20 znaków długości.</span><span class="sxs-lookup"><span data-stu-id="ae60c-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="ae60c-162">Kolumna "żywności" Hello wskazuje elementu żywności hello, pozwalających każda osoba.</span><span class="sxs-lookup"><span data-stu-id="ae60c-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="ae60c-163">VARCHAR ogranicza to toobe tekstu w obszarze 30 znaków.</span><span class="sxs-lookup"><span data-stu-id="ae60c-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="ae60c-164">Witaj "potwierdzone" rekordy kolumny czy hello osoba potwierdziła przyjęcie składkowe toohello.</span><span class="sxs-lookup"><span data-stu-id="ae60c-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="ae60c-165">Witaj dopuszczalne wartości to "Y" i "N".</span><span class="sxs-lookup"><span data-stu-id="ae60c-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="ae60c-166">Przedstawia kolumnę Hello "date" zarejestrowała się w usłudze hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ae60c-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="ae60c-167">Postgres wymaga zapisać daty w postaci rrrr mm-dd.</span><span class="sxs-lookup"><span data-stu-id="ae60c-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="ae60c-168">Po pomyślnym utworzeniu tabeli powinny być widoczne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-168">You should see hello following if your table has been successfully created:</span></span>

![Obraz](./media/postgresql-install/no4.png)

<span data-ttu-id="ae60c-170">Struktura tabeli hello można również wykonać za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ae60c-170">You can also check hello table structure by using hello following command:</span></span>

![Obraz](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="ae60c-172">Dodaj tabelę tooa danych</span><span class="sxs-lookup"><span data-stu-id="ae60c-172">Add data tooa table</span></span>
<span data-ttu-id="ae60c-173">Najpierw należy wstawić informacji do wiersza:</span><span class="sxs-lookup"><span data-stu-id="ae60c-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="ae60c-174">Te dane wyjściowe powinny być widoczne:</span><span class="sxs-lookup"><span data-stu-id="ae60c-174">You should see this output:</span></span>

![Obraz](./media/postgresql-install/no6.png)

<span data-ttu-id="ae60c-176">Tabelę można dodać kilka więcej osób toohello również.</span><span class="sxs-lookup"><span data-stu-id="ae60c-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="ae60c-177">Poniżej przedstawiono niektóre opcje, lub utworzyć własny:</span><span class="sxs-lookup"><span data-stu-id="ae60c-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="ae60c-178">Pokaż tabele</span><span class="sxs-lookup"><span data-stu-id="ae60c-178">Show tables</span></span>
<span data-ttu-id="ae60c-179">Użyj hello następujące polecenia tooshow tabeli:</span><span class="sxs-lookup"><span data-stu-id="ae60c-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="ae60c-180">dane wyjściowe Hello to:</span><span class="sxs-lookup"><span data-stu-id="ae60c-180">hello output is:</span></span>

![Obraz](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="ae60c-182">Usuń dane w tabeli</span><span class="sxs-lookup"><span data-stu-id="ae60c-182">Delete data in a table</span></span>
<span data-ttu-id="ae60c-183">Witaj Użyj następującego polecenia toodelete dane w tabeli:</span><span class="sxs-lookup"><span data-stu-id="ae60c-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="ae60c-184">Spowoduje to usunięcie wszystkich informacji hello hello wiersza "Jan".</span><span class="sxs-lookup"><span data-stu-id="ae60c-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="ae60c-185">dane wyjściowe Hello to:</span><span class="sxs-lookup"><span data-stu-id="ae60c-185">hello output is:</span></span>

![Obraz](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="ae60c-187">Aktualizuj dane w tabeli</span><span class="sxs-lookup"><span data-stu-id="ae60c-187">Update data in a table</span></span>
<span data-ttu-id="ae60c-188">Witaj Użyj następującego polecenia tooupdate dane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="ae60c-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="ae60c-189">Dla, Sandy potwierdzi, że jest ona uczestnictwa, więc zostanie zmieniona jej RSVP z "N" za "Y":</span><span class="sxs-lookup"><span data-stu-id="ae60c-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="ae60c-190">Uzyskaj więcej informacji o PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ae60c-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="ae60c-191">Teraz, gdy została ukończona instalacja hello PostgreSQL w maszynie Wirtualnej systemu Linux platformy Azure, można oglądać przy użyciu go na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ae60c-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="ae60c-192">toolearn więcej informacji na temat PostgreSQL, odwiedź stronę hello [PostgreSQL witryny sieci Web](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="ae60c-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

