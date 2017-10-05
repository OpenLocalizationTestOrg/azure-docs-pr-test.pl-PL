---
title: "Skonfiguruj maszynę wirtualną programu SQL Server jako serwer notesu IPython | Dokumentacja firmy Microsoft"
description: "Ustaw zapasową danych nauki maszynę wirtualną z programu SQL Server i serwer IPython."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 8a151a6a15d4d000a774e3ec4e38bfa0e58ca33b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Konfigurowanie maszyny wirtualnej serwera Azure SQL jako serwera IPython Notebook na potrzeby zaawansowanej analizy
W tym temacie pokazano, jak udostępnić i skonfigurować maszyny wirtualnej programu SQL Server do użycia jako część środowiska nauki danych opartych na chmurze. Maszyny wirtualnej systemu Windows jest konfigurowana obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure i AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów analizy danych. Eksplorator usługi Storage platformy Azure i AzCopy, na przykład można podać wygodny sposób przekazywania danych do magazynu obiektów blob platformy Azure z komputera lokalnego lub pobrać go na komputerze lokalnym, z magazynu obiektów blob.

Galeria maszyny wirtualnej platformy Azure zawiera kilka obrazów, które zawierają programu Microsoft SQL Server. Wybierz obraz maszyny Wirtualnej programu SQL Server, który jest odpowiedni dla potrzeb danych. Obrazy zalecane są:

* SQL Server 2012 SP2 Enterprise dla małych rozmiarów średnia danych
* SQL Server 2012 SP2 Enterprise zoptymalizowane pod kątem obciążeń strumienia rozmiarów dużej bardzo dużych ilości danych
  
  > [!NOTE]
  > Obraz programu SQL Server 2012 SP2 Enterprise **nie ma dysk z danymi**. Musisz dodać lub dołączyć co najmniej jeden wirtualne dyski twarde do przechowywania danych. Podczas tworzenia maszyny wirtualnej platformy Azure ma dysku systemu operacyjnego mapowane na dysku C i dysku tymczasowym mapowane na dysku D. Nie należy używać do przechowywania danych na dysku D. Jak wskazuje nazwę, zawiera tylko magazyn tymczasowy. Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.
  > 
  > 

## <a name="Provision"></a>Podłączyć się do klasycznego portalu Azure i aprowizowanie maszyny wirtualnej programu SQL Server
1. Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.
   Jeśli nie masz konta platformy Azure, odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
2. W klasycznym portalu Azure, w lewym dolnym rogu strony sieci web, kliknij polecenie **+ nowy**, kliknij przycisk **OBLICZENIOWE**, kliknij przycisk **maszyny WIRTUALNEJ**, a następnie kliknij przycisk **FROM GALERII** .
3. Na **Utwórz maszynę wirtualną** , wybierz obraz maszyny wirtualnej zawierający na podstawie Twoich potrzeb danych programu SQL Server, a następnie kliknij przycisk Dalej strzałkę w prawym dolnym rogu strony. Aby uzyskać najbardziej aktualne informacje dotyczące obsługiwanych obrazów programu SQL Server na platformie Azure, zobacz [wprowadzenie do programu SQL Server w maszynach wirtualnych platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=294720) tematu w [programu SQL Server w maszynach wirtualnych platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=294719) zestaw dokumentacji.
   
   ![Wybierz serwer SQL maszyny Wirtualnej][1]
4. W pierwszym **konfiguracji maszyny wirtualnej** Podaj następujące informacje:
   
   * Podaj **nazwę maszyny WIRTUALNEJ**.
   * W **nową nazwę użytkownika** okno, wpisz unikatową nazwę użytkownika dla konta administratora lokalnego maszyny Wirtualnej.
   * W **nowe hasło** wpisz silne hasło. Aby uzyskać więcej informacji, zobacz artykuł [Silne hasła](http://msdn.microsoft.com/library/ms161962.aspx).
   * W **POTWIERDŹ hasło** pola, wpisz ponownie hasło.
   * Wybierz odpowiednie **rozmiar** z listy rozwijanej.
     
     > [!NOTE]
     > Rozmiar maszyny wirtualnej zostanie określony podczas inicjowania obsługi administracyjnej: A2 jest najmniejszy rozmiar zalecane w przypadku obciążeń produkcyjnych. Minimalny rozmiar zalecany dla maszyny wirtualnej jest A3, korzystając z programu SQL Server Enterprise Edition. Wybierz A3 lub nowszej, korzystając z programu SQL Server Enterprise Edition. Wybierz A4, korzystając z programu SQL Server 2012 lub 2014 Enterprise zoptymalizowanych pod kątem obciążeń transakcyjnych obrazów.
     > Wybierz A7, korzystając z programu SQL Server 2012 lub 2014 Enterprise zoptymalizowanych pod kątem obciążeń magazynowania danych obrazów. Wybrany rozmiar ogranicza liczbę dysków z danymi, które można skonfigurować. Aby uzyskać najbardziej aktualne informacje dostępne rozmiary maszyny wirtualnej i liczba dysków z danymi, które można załączyć do maszyny wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Aby uzyskać informacje o cenach, zobacz [wirtualnego cennik Macines](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Kliknij strzałkę dalej w prawym dolnym rogu, aby kontynuować.
   
   ![Konfiguracja maszyny Wirtualnej][2]
5. Na drugiej stronie **konfiguracji maszyny wirtualnej** Skonfiguruj zasoby dotyczące sieci, magazynu i dostępności:
   
   * W **usługi w chmurze** wybierz **Utwórz nową usługę w chmurze**.
   * W **nazwa DNS usługi w chmurze** Podaj pierwszą część nazwy DNS w wybranych przez użytkownika, dzięki czemu ukończy nazwę w formacie **TESTNAME.cloudapp.net**
   * W **REGION/KOLIGACJI grupy/WIRTUALNEJ sieci** wybierz region, w którym będzie hostowana ten obraz wirtualnej.
   * W **konta magazynu**, wybrać istniejące konto magazynu lub wybierz automatycznie wygenerowaną.
   * W **zestawu dostępności** wybierz opcję **(Brak)**.
   * Przeczytaj i zaakceptuj informacje cenach.
6. W **punkty końcowe** kliknij na liście rozwijanej pusta w obszarze **nazwa**i wybierz **MSSQL** następnie wpisz numer portu wystąpienia aparatu bazy danych (**1433** dla domyślnego wystąpienia).
7. Maszyna wirtualna programu SQL Server mogą również służyć jako serwer notesu IPython, który zostanie skonfigurowany w kolejnym kroku.
   Dodaj nowy punkt końcowy, aby określić port używany dla serwera IPython notesu. Wprowadź nazwę w **nazwa** 9999 dla port prywatny, wybierz numer portu wybranego port publiczny i kolumn.
   
   Kliknij strzałkę dalej w prawym dolnym rogu, aby kontynuować.
   
   ![Wybierz porty MSSQL i IPython][3]
8. Zaakceptuj wartość domyślną **agent zainstalować maszyny Wirtualnej** zaznaczoną opcją i kliknij znacznik wyboru w prawym dolnym rogu kreatora, aby ukończyć proces tworzenia maszyny Wirtualnej.
   
   `![Opcje końcowego maszyny Wirtualnej][4]
9. Zaczekaj, aż Azure przygotowuje maszynę wirtualną. Oczekiwany stan maszyny wirtualnej, aby kontynuować za pomocą:
   
   * Rozpoczynanie (inicjowania obsługi administracyjnej)
   * Zatrzymane
   * Rozpoczynanie (inicjowania obsługi administracyjnej)
   * Uruchomiona (Inicjowanie obsługi administracyjnej)
   * Działanie

## <a name="RemoteDesktop"></a>Otwórz za pomocą pulpitu zdalnego i zakończyć konfigurację maszyny wirtualnej
1. Po ukończeniu inicjowania obsługi kliknij nazwę maszyny wirtualnej, aby przejść do strony pulpitu NAWIGACYJNEGO. W dolnej części strony kliknij **Connect**.
2. Wybierz opcję otwarcia pliku rpd przy użyciu programu Windows pulpitu zdalnego (`%windir%\system32\mstsc.exe`).
3. W **zabezpieczenia systemu Windows** okna dialogowego podaj hasło dla konta administratora lokalnego, który określono w poprzednim kroku.
   (Użytkownik może zostać poproszony do zweryfikowania poświadczeń maszyny wirtualnej.)
4. Podczas pierwszego logowania się do tej maszyny wirtualnej kilka procesów może być konieczne przeprowadzenie, w tym ustawienia pulpitu, aktualizacji systemu Windows i kończenia zadań konfiguracji początkowej systemu Windows (sysprep). Po zakończeniu działania programu sysprep systemu Windows, zadania konfiguracji zakończeniu instalacji programu SQL Server. Te zadania może spowodować opóźnienia za kilka minut, aż do ich zakończenia. `SELECT @@SERVERNAME`nie może zwracać prawidłową nazwę, dopiero po zakończeniu instalacji programu SQL Server i SQL Server Management Studio nie może być visable na stronie początkowej.

Po nawiązaniu połączenia z maszyną wirtualną przy użyciu pulpitu zdalnego systemu Windows maszyny wirtualnej działa podobne jak w przypadku dowolnego innego komputera. Nawiązać domyślnego wystąpienia programu SQL Server z programu SQL Server Management Studio (uruchomiony na maszynie wirtualnej) w zwykły sposób.

## <a name="InstallIPython"></a>Zainstaluj notesu IPython i inne narzędzia do obsługi
Aby skonfigurować nową maszynę Wirtualną serwera SQL, służyć jako serwer notesu IPython i zainstalować dodatkowe narzędzia obsługi takich AzCopy, Eksploratora usługi Storage Azure przydatne pakietów języka Python nauki danych i inne osoby, skrypt specjalnego dostosowania są dostępne. Aby zainstalować:

1. Kliknij prawym przyciskiem myszy **Start systemu Windows** ikony, jak i kliknij przycisk **wiersza polecenia (Administrator)**
2. Skopiuj następujące polecenia i Wklej w wierszu polecenia.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Po wyświetleniu monitu wprowadź hasło dowolnego serwera IPython notesu.
4. Skrypt dostosowywania automatyzuje kilka procedur po instalacji, które obejmują:
    * Instalacja i konfiguracja serwera IPython notesu
    * Otwieranie portów TCP w Zaporze systemu Windows dla punktów końcowych utworzony wcześniej:
    * Dla połączenia zdalnego programu SQL Server
    * Dla połączenia zdalnego serwera IPython notesu
    * Pobieranie próbki IPython notesów i skrypty SQL
    * Trwa pobieranie i instalowanie przydatne pakietów języka Python nauki danych
    * Trwa pobieranie i instalowanie narzędzi platformy Azure, takich jak AzCopy i Eksploratora usługi Storage platformy Azure  
    <br>
5. Może uzyskać dostęp i uruchom notesu IPython z dowolnej przeglądarki lokalnym lub zdalnym przy użyciu adresu URL w postaci `https://<virtual_machine_DNS_name>:<port>`, gdzie jest to port publiczny IPython wybrany podczas inicjowania obsługi administracyjnej maszyny wirtualnej.
6. Notesu IPython serwer działa jako usługa w tle i zostanie automatycznie uruchomiony ponownie po ponownym uruchomieniu maszyny wirtualnej.

## <a name="Optional"></a>Dołączenie dysku danych, w razie potrzeby
Obraz maszyny Wirtualnej nie ma dysków z danymi, np. dysków niż dysk C (dysk systemu operacyjnego) i dysku D (dysku tymczasowym), należy dodać co najmniej jeden dysk danych do przechowywania danych. Obraz maszyny Wirtualnej dla programu SQL Server 2012 SP2 Enterprise zoptymalizowane pod kątem obciążeń strumienia ma wstępnie skonfigurowane dodatkowe dysków dla plików danych i dziennika programu SQL Server.

> [!NOTE]
> Nie należy używać do przechowywania danych na dysku D. Jak wskazuje nazwę, zawiera tylko magazyn tymczasowy. Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.
> 
> 

Aby dołączyć dodatkowego dysku z danymi, wykonaj czynności opisane w [jak dołączyć dysku danych do maszyny wirtualnej systemu Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), który przeprowadzi użytkownika przez proces:

1. Dołączenia pustych dysków do maszyny wirtualnej, udostępnione we wcześniejszych krokach
2. Inicjowanie nowe dyski na maszynie wirtualnej

## <a name="SSMS"></a>Nawiązywanie połączenia SQL Server Management Studio i włączyć uwierzytelnianie w trybie mieszanym
Aparat bazy danych programu SQL Server nie może korzystać z uwierzytelniania systemu Windows bez środowiska domenowego. Aby nawiązać połączenie z aparatem bazy danych z innego komputera, skonfiguruj program SQL Server do uwierzytelniania w trybie mieszanym. Uwierzytelnianie w trybie mieszanym umożliwia korzystanie z zarówno uwierzytelniania programu SQL Server, jak i uwierzytelniania systemu Windows. Tryb uwierzytelniania SQL jest wymagany w celu pozyskiwania danych bezpośrednio z bazy danych programu SQL Server z maszyny Wirtualnej w [Azure Machine Learning Studio](https://studio.azureml.net) za pomocą modułu importu danych.

1. Podczas połączenia z maszyną wirtualną przy użyciu pulpitu zdalnego, należy użyć systemu Windows **wyszukiwania** okienko i typ **programu SQL Server Management Studio** (SMSS). Kliknij, aby uruchomić program SQL Server Management Studio (SSMS). Możesz dodać skrót do narzędzia SSMS na pulpicie do użytku w przyszłości.
   
   ![Uruchomić program SSMS][5]
   
   Podczas pierwszego uruchomienia program Management Studio musi utworzyć środowisko użytkowników programu Management Studio. Może to potrwać kilka chwil.
2. Podczas otwierania, Management Studio przedstawia **Połącz z serwerem** okno dialogowe. W **nazwy serwera** wpisz nazwę maszyny wirtualnej, aby nawiązać połączenie z aparatem bazy danych z Eksplorator obiektów.
   (Zamiast nazwy maszyny wirtualnej można również użyć **(local)** lub jednego okresu jako **nazwy serwera**. Wybierz **uwierzytelniania systemu Windows**i pozostawić  ***Twojego\_maszyny Wirtualnej\_nazwa*\\z\_lokalnego\_administratora**  w **nazwy użytkownika** pole. Kliknij przycisk **Połącz**.
   
   ![Łączenie z serwerem][6]
   
   <br>
   
   > [!TIP]
   > Możesz zmienić tryb uwierzytelniania programu SQL Server przy użyciu zmiany klucza rejestru systemu Windows lub programu SQL Server Management Studio. Aby zmienić tryb uwierzytelniania przy użyciu zmiany klucza rejestru, uruchom **nowe zapytanie** i uruchom następujący skrypt:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    Aby zmienić tryb uwierzytelniania przy użyciu programu SQL Server management Studio:

1. W **Eksplorator obiektów SQL Server Management Studio**, kliknij prawym przyciskiem myszy nazwę wystąpienia programu SQL Server (nazwę maszyny wirtualnej), a następnie kliknij przycisk **właściwości**.
   
   ![Właściwości serwera][7]
2. Na stronie **Zabezpieczenia** w obszarze **Uwierzytelnianie serwera** wybierz pozycję **Tryb uwierzytelniania programu SQL Server i systemu Windows**, a następnie kliknij przycisk **OK**.
   
   ![Wybieranie trybu uwierzytelniania][8]
3. W **programu SQL Server Management Studio** okno dialogowe, kliknij przycisk **OK** potwierdzić wymagane ponowne uruchomienie serwera SQL.
4. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy serwer, a następnie kliknij przycisk **ponownego uruchomienia**. (Jeśli program SQL Server Agent jest uruchomiony, również należy go ponownie uruchomić).
   
   ![Ponowne uruchamianie][9]
5. W **programu SQL Server Management Studio** okno dialogowe, kliknij przycisk **tak** będą musieli się zgodzić chcesz uruchomić ponownie program SQL Server.

## <a name="Logins"></a>Tworzenie identyfikatorów logowania uwierzytelniania programu SQL Server
Aby nawiązać połączenie z aparatem bazy danych z innego komputera, należy utworzyć przynajmniej jeden identyfikator logowania do uwierzytelniania w programie SQL Server.  

Można utworzyć nowego logowania programu SQL Server programowo lub przy użyciu programu SQL Server Management Studio. Aby utworzyć nowego użytkownika sysadmin z uwierzytelnianiem SQL programowo, uruchom **nowe zapytanie** i uruchom następujący skrypt. Zastąp < nową nazwę użytkownika\> i < nowe hasło\> przy użyciu wybranych *nazwy użytkownika* i *hasło*. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Dostosuj zasady haseł, zgodnie z potrzebami (przykładowy kod wyłącza zasady wygasania sprawdzanie i hasło). Aby uzyskać więcej informacji na temat identyfikatorów logowania programu SQL Server, zobacz [Tworzenie identyfikatora logowania](http://msdn.microsoft.com/library/aa337562.aspx).  

Aby utworzyć nowy logowania programu SQL Server przy użyciu programu SQL Server Management Studio:

1. W **Eksplorator obiektów SQL Server Management Studio**, rozwiń folder wystąpienia serwera, w którym chcesz utworzyć nowe dane logowania.
2. Kliknij prawym przyciskiem myszy **zabezpieczeń** folderu, wskaż **nowy**i wybierz **logowania...** .
   
   ![Nowy identyfikator logowania][10]
3. W oknie dialogowym **Identyfikator logowania — Nowy** na stronie **Ogólne** wprowadź nazwę nowego użytkownika w polu **Nazwa logowania**.
4. Wybierz pozycję **Uwierzytelnianie programu SQL Server**.
5. W polu **Hasło** wprowadź hasło dla nowego użytkownika. Wprowadź to hasło ponownie w polu **Potwierdź hasło**.
6. Aby wymusić opcji zasad hasła, złożoność i wymuszania, wybierz **wymusić zasady haseł** (zalecane). To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
7. Aby wymusić opcje zasad haseł do wygaśnięcia, wybierz **wymusić wygaśnięcie hasła** (zalecane). Wymuszanie zasad haseł należy wybrać, aby włączyć to pole wyboru. To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
8. Aby wymusić użytkownikowi utworzenie nowego hasła po logowania jest używany po raz pierwszy, wybierz **użytkownik musi zmienić hasło przy następnym logowaniu** (zalecane, jeśli ta nazwa logowania jest innym osobom do użycia. Jeśli logowanie do własnych potrzeb, nie wybieraj tej opcji.) Wymuszanie wygaśnięcie hasła należy wybrać, aby włączyć to pole wyboru. To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
9. Z listy **Domyślna baza danych** wybierz domyślną bazę danych dla identyfikatora logowania. Domyślne ustawienie tej opcji to **master**. Jeśli jeszcze nie utworzono bazy danych użytkownika, pozostaw dla tego ustawienia wartość **master**.
10. W **domyślny język** pozostaw opcję **domyślne** jako wartość.
    
    ![Właściwości identyfikatora logowania][11]
11. Jeśli jest to pierwszy identyfikator logowania, jaki tworzysz, warto go wyznaczyć jako administratora programu SQL Server. Jeśli tak, na stronie **Role serwera** zaznacz opcję **sysadmin**.
    
    > [!IMPORTANT]
    > Członkowie stałej roli serwera sysadmin mają pełną kontrolę nad aparatem bazy danych. Ze względów bezpieczeństwa należy odpowiednio ograniczyć członkostwo w tej roli.
    > 
    > 
    
    ![sysadmin][12]
12. Kliknij przycisk OK.

## <a name="DNS"></a>Określanie nazwy DNS maszyny wirtualnej
Aby połączyć się z aparatem bazy danych programu SQL Server z innego komputera, musisz znać nazwy systemu nazw domen (DNS, Domain Name System) maszyny wirtualnej.

(Jest to nazwa, używanych przez internet na identyfikację maszyny wirtualnej. Możesz użyć adresu IP, ale adres IP mogą ulec zmianie, gdy Azure przenosi zasoby nadmiarowość lub konserwacji. Nazwa DNS będzie stabilny, ponieważ mogą zostać przekierowane do nowego adresu IP).

1. W klasycznym portalu Azure (lub w poprzednim kroku), wybierz **maszyn wirtualnych**.
2. Na **WYSTĄPIEŃ maszyn wirtualnych** strony w **nazwy DNS** kolumny, Znajdź i kopiowania poprzedzone nazwy DNS dla maszyny wirtualnej, która jest wyświetlana **http://**. (Interfejsu użytkownika może nie wyświetlać całą nazwę, ale kliknij prawym przyciskiem myszy na nim i wybierz polecenie Kopiuj).

## <a name="cde"></a>Nawiąż połączenie z aparatem bazy danych z innego komputera
1. Na komputerze podłączonym do Internetu Otwórz program SQL Server Management Studio.
2. W **Połącz z serwerem** lub **nawiązywanie połączenia z aparatem bazy danych** okna dialogowego, **nazwy serwera** wprowadź nazwę DNS maszyny wirtualnej (określoną w poprzednim zadaniu) i numeru portu publicznego punktu końcowego w formacie *DNSName, numer_portu* takich jak **tutorialtestVM.cloudapp.net,57500**.
3. W polu **Authentication** (Uwierzytelnianie) wybierz opcję **SQL Server Authentication** (Uwierzytelnianie programu SQL Server).
4. W **logowania** wpisz nazwę logowania, utworzony w starszej zadań.
5. W **hasło** wpisz hasło logowania, utworzone w wcześniejszych zadań.
6. Kliknij przycisk **Połącz**.

## <a name="amlconnect"></a>Nawiąż połączenie z aparatem bazy danych z usługi Azure Machine Learning
W późniejszych etapach procesu nauki danych Team użyjesz [Azure Machine Learning Studio](https://studio.azureml.net) do tworzenia i wdrażania modeli uczenia maszyny. Aby pozyskiwania danych z baz danych programu SQL Server z maszyny Wirtualnej bezpośrednio do usługi Azure Machine Learning szkolenia lub oceniania, użyj **i zaimportuj dane** modułu w ramach nowego [Azure Machine Learning Studio](https://studio.azureml.net) eksperymentu. W tym temacie omówiono więcej szczegółowych informacji za pośrednictwem łączy Przewodnik po procesie nauki danych zespołu. Aby obejrzeć wprowadzenie, zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).

1. W **właściwości** okienku [modułu importu danych](https://msdn.microsoft.com/library/azure/dn905997.aspx), wybierz pozycję **bazy danych SQL Azure** z **źródła danych** listy rozwijanej.
2. W **nazwę serwera bazy danych** tekst Wprowadź`tcp:<DNS name of your virtual machine>,1433`
3. Wprowadź nazwę użytkownika SQL w **nazwę konta użytkownika serwera** pola tekstowego.
4. Wprowadź hasło użytkownika sql w **hasło konta użytkownika serwera** pola tekstowego.
   
   ![Uczenie maszynowe Azure i zaimportuj dane][13]

## <a name="shutdown"></a>Zamknięcie i Cofnij Przydział maszyny wirtualnej nieużywane
Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. Aby upewnić się, że nie rozliczanych, gdy nie używać sieci maszyny wirtualnej, musi ona być w **zatrzymane (Deallocated)** stanu.

> [!NOTE]
> Zamykanie maszyny wirtualnej z wewnątrz (przy użyciu apletu Opcje zasilania systemu Windows), maszyna wirtualna zostanie zatrzymana, ale pozostaje przydzielone. Aby upewnić się, opłaty nie są naliczane, zawsze wstrzymują maszyn wirtualnych z [klasycznego portalu Azure](http://manage.windowsazure.com/). Można je również zatrzymać za pomocą środowiska Powershell, wywołując polecenie ShutdownRoleOperation z parametrem „PostShutdownAction” mającym wartość „StoppedDeallocated”.
> 
> 

Zamknięcie i cofnięcia przydzielenia maszynie wirtualnej:

1. Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.  
2. Wybierz **maszyn wirtualnych** na pasku nawigacyjnym po lewej stronie.
3. Na liście maszyny wirtualnej, kliknij nazwę maszyny wirtualnej, a następnie przejdź do **pulpitu NAWIGACYJNEGO** strony.
4. W dolnej części strony kliknij **zamknięcia**.

![Zamknięcie maszyny Wirtualnej][15]

Maszyna wirtualna zostanie alokację, ale nie został usunięty. Możesz uruchomić ponownie maszynę wirtualną w dowolnym momencie z klasycznego portalu Azure.

## <a name="your-azure-sql-server-vm-is-ready-to-use-whats-next"></a>Maszyna wirtualna Azure SQL Server jest gotowe do użycia: co to jest dalej?
Maszyna wirtualna jest teraz gotowy do użycia w Twojej ćwiczeń analizy danych. Maszyna wirtualna również jest gotowa do użycia jako serwer notesu IPython do eksploracji i przetwarzania danych i innych zadań w połączeniu z uczenie maszynowe Azure i procesu nauki danych zespołu (TDSP).

Następne kroki w procesie nauki danych są mapowane w [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, proces i przykładowe istnieje on w ramach przygotowania do uczenia z danych z usługi Azure Machine Learning .

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

