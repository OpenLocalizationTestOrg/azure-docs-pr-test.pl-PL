
1. tooescalate uprawnień, wpisz:
   
        sudo -s
   
    Wprowadź hasło.
2. tooinstall serwer MySQL Community edition, wpisz:
   
        zypper install mysql-community-server
   
    Zaczekaj, aż MySQL pobiera i instaluje.
3. tooset MySQL toostart podczas rozruchu systemu hello, wpisz:
   
        insserv mysql
4. Ręcznie uruchom hello MySQL demon (mysqld) za pomocą tego polecenia:
   
        rcmysql start
   
    Stan hello toocheck hello demona MySQL, wpisz:
   
        rcmysql status
   
    Witaj toostop demona MySQL, wpisz:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Po zainstalowaniu hasła głównego MySQL hello jest domyślnie pusta. Zaleca się, że uruchamiasz **mysql\_bezpiecznego\_instalacji**, skrypt, który pomaga bezpiecznego MySQL. Hello skrypt wyświetli monit o hasła głównego MySQL hello toochange, usunąć konta użytkownika anonimowego wyłączyć głównego zdalnego logowania, usunąć bazy danych testu i ponownie załaduj hello uprawnienia tabeli. Zaleca się odpowiedzieć tooall tak z tych opcji, a następnie zmiany hasła głównego hello.
   > 
   > 
5. Wpisz ten skrypt hello toorun MySQL skrypt instalacji:
   
        mysql_secure_installation
6. Zaloguj się tooMySQL:
   
        mysql -u root -p
   
    Wprowadź hasła głównego MySQL hello (które można zmienić w poprzednim kroku hello) i zostanie wyświetlony wraz z monitem o których możesz wykonywać toointeract instrukcje SQL z bazą danych hello.
7. toocreate nowego użytkownika MySQL, uruchom następujące hello na powitania **mysql >** wiersza:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Uwaga: hello średnikami (;) na końcu hello hello wiersze są kluczowe znaczenie dla końcowy hello poleceń.
8. toocreate hello bazy danych i przyznać `mysqluser` uprawnienia użytkownika na nim hello problem następującego polecenia:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Należy pamiętać, że bazy danych, nazwy użytkownika i hasła są używane tylko przez skrypty łączenie toohello bazy danych.  Nazwy kont użytkowników bazy danych nie przedstawiają niekoniecznie konta użytkowników w systemie hello.
9. toolog w innym komputerze, wpisz:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    gdzie `ip-address` jest adresem IP hello hello komputera, z którego ma zostać nawiązane połączenie tooMySQL.
10. Witaj tooexit narzędzie administracyjne bazy danych MySQL, wpisz:
    
        quit

## <a name="add-an-endpoint"></a>Dodawanie punktu końcowego
1. Po zainstalowaniu MySQL, konieczne będzie tooconfigure tooaccess punktu końcowego MySQL zdalnie. Zaloguj się za toohello [klasycznego portalu Azure][AzurePortal]. Kliknij przycisk **maszyn wirtualnych**, kliknij nazwę hello nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.
2. Kliknij przycisk **Dodaj** u dołu hello hello strony.
3. Dodawanie punktu końcowego o nazwie "MySQL" z protokołem **TCP**, i **publicznego** i **prywatnej** porty zestaw zbyt "3306".
4. tooremotely połączenie toohello maszynę wirtualną z komputera, wpisz:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Na przykład za pomocą wykorzystanie hello wirtualnej maszyny utworzone z tego samouczka, wpisz następujące polecenie:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
