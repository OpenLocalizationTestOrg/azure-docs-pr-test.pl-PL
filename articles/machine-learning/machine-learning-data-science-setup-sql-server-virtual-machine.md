---
title: aaaSet zapasowej maszyny wirtualnej programu SQL Server jako serwer notesu IPython | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Konfigurowanie maszyny wirtualnej serwera Azure SQL jako serwera IPython Notebook na potrzeby zaawansowanej analizy
W tym temacie przedstawiono sposób tooprovision i skonfigurować toobe maszyny wirtualnej programu SQL Server używany jako część środowiska nauki danych opartych na chmurze. maszyny wirtualnej systemu Windows Hello jest skonfigurowany z obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure i AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów analizy danych. Azure Eksploratora usługi Storage i AzCopy, na przykład oferują wygodny sposób magazynu obiektów blob tooAzure tooupload danych z komputera lokalnego lub toodownload go tooyour komputera lokalnego z magazynu obiektów blob.

Witaj galerii Azure maszyny wirtualnej zawiera kilka obrazów, które zawierają programu Microsoft SQL Server. Wybierz obraz maszyny Wirtualnej programu SQL Server, który jest odpowiedni dla potrzeb danych. Obrazy zalecane są:

* SQL Server 2012 SP2 Enterprise toomedium małych rozmiarów danych
* SQL Server 2012 SP2 Enterprise zoptymalizowane pod kątem obciążeń strumienia toovery dużych rozmiarów dużej ilości danych
  
  > [!NOTE]
  > Obraz programu SQL Server 2012 SP2 Enterprise **nie ma dysk z danymi**. Będzie konieczne tooadd lub dołączanie danych co najmniej jeden toostore wirtualnych dysków twardych. Podczas tworzenia maszyny wirtualnej platformy Azure ma dysku dla dysku toohello C systemie zamapowany hello i tymczasowego mapowane toohello D dysku. Nie należy używać hello D dysku toostore danych. Jak wskazuje nazwę hello, zawiera tylko magazyn tymczasowy. Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.
  > 
  > 

## <a name="Provision"></a>Połącz toohello klasycznego portalu Azure i aprowizowanie maszyny wirtualnej programu SQL Server
1. Zaloguj się za toohello [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.
   Jeśli nie masz konta platformy Azure, odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
2. Na powitania klasycznego portalu Azure, w lewym dolnym hello hello strony sieci web, kliknij przycisk **+ nowy**, kliknij przycisk **OBLICZENIOWE**, kliknij przycisk **maszyny WIRTUALNEJ**, a następnie kliknij przycisk **FROM GALERIA**.
3. Na powitania **Utwórz maszynę wirtualną** strony, wybierz obraz maszyny wirtualnej zawierający na podstawie Twoich potrzeb danych programu SQL Server, a następnie kliknij strzałkę dalej hello u dołu po prawej stronie powitania. Najbardziej aktualne informacje hello na powitania obrazów programu SQL Server są obsługiwane na platformie Azure, zobacz [wprowadzenie do programu SQL Server w maszynach wirtualnych platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=294720) tematu w hello [programu SQL Server w usłudze Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) zestaw dokumentacji.
   
   ![Wybierz serwer SQL maszyny Wirtualnej][1]
4. Na powitania pierwszy **konfiguracji maszyny wirtualnej** Podaj następujące informacje:
   
   * Podaj **nazwę maszyny WIRTUALNEJ**.
   * W hello **nową nazwę użytkownika** okno, wpisz unikatową nazwę użytkownika umożliwiającą hello konta lokalnego administratora maszyny Wirtualnej.
   * W hello **nowe hasło** wpisz silne hasło. Aby uzyskać więcej informacji, zobacz artykuł [Silne hasła](http://msdn.microsoft.com/library/ms161962.aspx).
   * W hello **POTWIERDŹ hasło** pozycję ponownie hello hasło.
   * Wybierz odpowiednie hello **rozmiar** hello — z listy rozwijanej.
     
     > [!NOTE]
     > rozmiar Hello hello maszyny wirtualnej zostanie określony podczas inicjowania obsługi administracyjnej: A2 jest najmniejszy rozmiar hello zalecane w przypadku obciążeń produkcyjnych. Minimalny rozmiar zalecany dla maszyny wirtualnej jest A3, korzystając z programu SQL Server Enterprise Edition. Wybierz A3 lub nowszej, korzystając z programu SQL Server Enterprise Edition. Wybierz A4, korzystając z programu SQL Server 2012 lub 2014 Enterprise zoptymalizowanych pod kątem obciążeń transakcyjnych obrazów.
     > Wybierz A7, korzystając z programu SQL Server 2012 lub 2014 Enterprise zoptymalizowanych pod kątem obciążeń magazynowania danych obrazów. wybrany rozmiar Hello ogranicza liczbę dysków z danymi, które można skonfigurować. Najbardziej aktualne informacje hello liczby dysków z danymi i dostępne rozmiary maszyny wirtualnej, dołączenie tooa maszyny wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Aby uzyskać informacje o cenach, zobacz [wirtualnego cennik Macines](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Kliknij strzałkę dalej hello na toocontinue prawy dolny hello.
   
   ![Konfiguracja maszyny Wirtualnej][2]
5. Na powitania drugi **konfiguracji maszyny wirtualnej** Skonfiguruj zasoby dotyczące sieci, magazynu i dostępności:
   
   * W hello **usługi w chmurze** wybierz **Utwórz nową usługę w chmurze**.
   * W hello **nazwa DNS usługi w chmurze** Podaj hello pierwszą część nazwy DNS w wybranych przez użytkownika, dzięki czemu ukończy nazwę w formacie **TESTNAME.cloudapp.net**
   * W hello **REGION/KOLIGACJI grupy/WIRTUALNEJ sieci** wybierz region, w którym będzie hostowana ten obraz wirtualnej.
   * W hello **konta magazynu**, wybrać istniejące konto magazynu lub wybierz automatycznie wygenerowaną.
   * W hello **zestawu dostępności** wybierz opcję **(Brak)**.
   * Przeczytaj i zaakceptuj hello uzyskać informacje o cenach.
6. W hello **punkty końcowe** sekcji, kliknij przycisk hello pusty listy rozwijanej w obszarze **nazwa**i wybierz **MSSQL** następnie wpisz numer portu hello wystąpienia aparatu bazy danych (hello**1433** hello wystąpienia domyślnego).
7. Maszyna wirtualna programu SQL Server mogą również służyć jako serwer notesu IPython, który zostanie skonfigurowany w kolejnym kroku.
   Dodaj nowy punkt końcowy toospecify hello portu toouse serwera IPython notesu. Wprowadź nazwę w hello **nazwa** 9999 dla hello port prywatny, wybierz numer portu wybranego hello port publiczny i kolumn.
   
   Kliknij strzałkę dalej hello na toocontinue prawy dolny hello.
   
   ![Wybierz porty MSSQL i IPython][3]
8. Zaakceptuj domyślną hello **agent zainstalować maszyny Wirtualnej** opcja zaznaczone i kliknij znacznik wyboru hello hello w hello prawym dolnym rogu hello kreatora toocomplete hello procesu inicjowania obsługi administracyjnej maszyny Wirtualnej.
   
   `![Opcje końcowego maszyny Wirtualnej][4]
9. Zaczekaj, aż Azure przygotowuje maszynę wirtualną. Oczekiwane tooproceed stan maszyny wirtualnej hello za pomocą:
   
   * Rozpoczynanie (inicjowania obsługi administracyjnej)
   * Zatrzymane
   * Rozpoczynanie (inicjowania obsługi administracyjnej)
   * Uruchomiona (Inicjowanie obsługi administracyjnej)
   * Działanie

## <a name="RemoteDesktop"></a>Otwórz hello maszyny wirtualnej przy użyciu pulpitu zdalnego i ukończyć instalację
1. Po ukończeniu inicjowania obsługi kliknij nazwę hello strony pulpitu NAWIGACYJNEGO toohello toogo maszyny wirtualnej. U dołu hello hello strony, kliknij przycisk **Connect**.
2. Wybierz plik rpd hello tooopen przy użyciu programu pulpitu zdalnego systemu Windows hello (`%windir%\system32\mstsc.exe`).
3. Na powitania **zabezpieczenia systemu Windows** okna dialogowego podaj hello hasło dla konta administratora lokalnego, który określono w poprzednim kroku.
   (Może wymagać poświadczeń hello tooverify hello maszyny wirtualnej.)
4. Witaj po raz pierwszy logujesz się na maszynie wirtualnej toothis, kilka procesów może być konieczne toocomplete, w tym ustawienia pulpitu, aktualizacji systemu Windows i zakończenia zadania konfiguracji początkowej Windows hello (sysprep). Po zakończeniu działania programu sysprep systemu Windows, zadania konfiguracji zakończeniu instalacji programu SQL Server. Te zadania może spowodować opóźnienia za kilka minut, aż do ich zakończenia. `SELECT @@SERVERNAME`dopiero po zakończeniu instalacji programu SQL Server i SQL Server Management Studio nie może być visable na powitania strony początkowej, nie mogą zwracać hello poprawną nazwę.

Po przejściu maszyny wirtualnej podłączonej toohello przy użyciu pulpitu zdalnego systemu Windows, hello maszyny wirtualnej działa podobnie jak dowolnego innego komputera. Połącz toohello domyślnego wystąpienia programu SQL Server z programu SQL Server Management Studio (uruchomiony na maszynie wirtualnej hello) w hello normalny sposób.

## <a name="InstallIPython"></a>Zainstaluj notesu IPython i inne narzędzia do obsługi
tooconfigure Twojego nowego tooserve maszyny Wirtualnej programu SQL Server jako serwer notesu IPython i obsługi dodatkowych instalacji narzędzi takich AzCopy, Eksploratora usługi Storage Azure przydatne pakietów języka Python nauki danych i inne osoby, skrypt specjalnego dostosowania jest dostarczany w stanie tooyou. tooinstall:

1. Kliknij prawym przyciskiem myszy hello **Start systemu Windows** ikony, jak i kliknij przycisk **wiersza polecenia (Administrator)**
2. Hello następujące polecenia Kopiuj i Wklej w wierszu polecenia hello.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Po wyświetleniu monitu wprowadź hasło wybranym na powitania serwera IPython notesu.
4. skrypt dostosowywania Hello automatyzuje kilka procedur po instalacji, które obejmują:
    * Instalacja i konfiguracja serwera IPython notesu
    * Otwieranie portów TCP w Zaporze systemu Windows hello dla punktów końcowych hello utworzony wcześniej:
    * Dla połączenia zdalnego programu SQL Server
    * Dla połączenia zdalnego serwera IPython notesu
    * Pobieranie próbki IPython notesów i skrypty SQL
    * Trwa pobieranie i instalowanie przydatne pakietów języka Python nauki danych
    * Trwa pobieranie i instalowanie narzędzi platformy Azure, takich jak AzCopy i Eksploratora usługi Storage platformy Azure  
    <br>
5. Może uzyskać dostęp i uruchom notesu IPython z dowolnej przeglądarki lokalnym lub zdalnym przy użyciu adresu URL formularza hello `https://<virtual_machine_DNS_name>:<port>`, gdzie jest hello IPython publiczny port wybrany podczas inicjowania obsługi administracyjnej hello maszyny wirtualnej.
6. Notesu IPython serwer działa jako usługa w tle i zostanie automatycznie uruchomiony ponownie po ponownym uruchomieniu hello maszyny wirtualnej.

## <a name="Optional"></a>Dołączenie dysku danych, w razie potrzeby
Jeśli obraz maszyny Wirtualnej nie ma dysków z danymi, np. dysków niż dysk C (dysk systemu operacyjnego) i dysku D (dysku tymczasowym), należy tooadd jedną lub więcej danych dyski toostore danych. Witaj obrazu maszyny Wirtualnej dla programu SQL Server 2012 SP2 Enterprise zoptymalizowane pod kątem obciążeń strumienia ma wstępnie skonfigurowane dodatkowe dysków dla plików danych i dziennika programu SQL Server.

> [!NOTE]
> Nie należy używać hello D dysku toostore danych. Jak wskazuje nazwę hello, zawiera tylko magazyn tymczasowy. Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.
> 
> 

tooattach dodatkowego dysku z danymi, wykonaj kroki hello opisanego w [jak tooAttach tooa dysku danych maszyny wirtualnej systemu Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), który przeprowadzi użytkownika przez proces:

1. Trwa dołączanie maszyny wirtualnej toohello puste dyski udostępnione we wcześniejszych krokach
2. Inicjowanie hello nowe dyski na maszynie wirtualnej hello

## <a name="SSMS"></a>Połącz tooSQL Server Management Studio i włączyć uwierzytelnianie w trybie mieszanym
Witaj aparatu bazy danych programu SQL Server nie można używać uwierzytelniania systemu Windows bez środowiska domeny. tooconnect toohello aparatu bazy danych z innego komputera, skonfigurować serwer SQL dla uwierzytelniania w trybie mieszanym. Uwierzytelnianie w trybie mieszanym umożliwia korzystanie z zarówno uwierzytelniania programu SQL Server, jak i uwierzytelniania systemu Windows. Tryb uwierzytelniania SQL jest wymagany w kolejności tooingest dane bezpośrednio z bazy danych programu SQL Server z maszyny Wirtualnej w [Azure Machine Learning Studio](https://studio.azureml.net) za pomocą hello importowanie danych modułu.

1. Podczas połączenia toohello maszyny wirtualnej przy użyciu pulpitu zdalnego, należy użyć systemu Windows hello **wyszukiwania** okienko i typ **programu SQL Server Management Studio** (SMSS). Kliknij przycisk hello toostart programu SQL Server Management Studio (SSMS). Możesz tooadd tooSSMS skrót na pulpicie do użytku w przyszłości.
   
   ![Uruchomić program SSMS][5]
   
   Witaj Otwórz Management Studio, należy utworzyć środowisko Management Studio użytkowników powitania po raz pierwszy. Może to potrwać kilka chwil.
2. Podczas otwierania, Management Studio przedstawia hello **połączyć tooServer** okno dialogowe. W hello **nazwy serwera** okno, nazwa typu hello hello maszyny wirtualnej tooconnect toohello aparatu bazy danych z hello Eksplorator obiektów.
   (Zamiast hello nazwę maszyny wirtualnej można również użyć **(local)** lub jednego okresu jako hello **nazwy serwera**. Wybierz **uwierzytelniania systemu Windows**i pozostawić  ***Twojego\_maszyny Wirtualnej\_nazwa*\\z\_lokalnego\_administratora**  w hello **nazwy użytkownika** pole. Kliknij przycisk **Połącz**.
   
   ![Połącz tooServer][6]
   
   <br>
   
   > [!TIP]
   > Możesz zmienić hello tryb uwierzytelniania programu SQL Server przy użyciu zmiany klucza rejestru systemu Windows lub hello SQL Server Management Studio. tryb uwierzytelniania toochange przy użyciu hello zmiany klucza rejestru, start **nowe zapytanie** i wykonywanie hello następującego skryptu:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    tryb uwierzytelniania hello toochange przy użyciu programu SQL Server management Studio:

1. W **Eksplorator obiektów SQL Server Management Studio**, kliknij prawym przyciskiem myszy nazwę hello wystąpienia programu SQL Server (hello nazwę maszyny wirtualnej), a następnie kliknij przycisk **właściwości**.
   
   ![Właściwości serwera][7]
2. Na powitania **zabezpieczeń** w obszarze **uwierzytelniania serwera**, wybierz pozycję **tryb programu SQL Server i uwierzytelniania systemu Windows**, a następnie kliknij przycisk **OK** .
   
   ![Wybieranie trybu uwierzytelniania][8]
3. W hello **programu SQL Server Management Studio** okno dialogowe, kliknij przycisk **OK** potwierdzić hello toorestart wymagania programu SQL Server.
4. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy serwer, a następnie kliknij przycisk **ponownego uruchomienia**. (Jeśli program SQL Server Agent jest uruchomiony, również należy go ponownie uruchomić).
   
   ![Ponowne uruchamianie][9]
5. W hello **programu SQL Server Management Studio** okno dialogowe, kliknij przycisk **tak** będą musieli się zgodzić, które mają toorestart programu SQL Server.

## <a name="Logins"></a>Tworzenie identyfikatorów logowania uwierzytelniania programu SQL Server
tooconnect toohello aparatu bazy danych z innego komputera, należy utworzyć co najmniej jeden identyfikator logowania uwierzytelniania programu SQL Server.  

Można utworzyć nowego logowania programu SQL Server programowo lub przy użyciu hello SQL Server Management Studio. toocreate nowego użytkownika sysadmin z uwierzytelnianiem SQL programowo, uruchom **nowe zapytanie** i wykonywanie hello następującego skryptu. Zastąp < nową nazwę użytkownika\> i < nowe hasło\> przy użyciu wybranych *nazwy użytkownika* i *hasło*. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Dostosuj zasady haseł hello zgodnie z potrzebami (hello przykładowy kod wyłącza zasady wygasania sprawdzanie i hasło). Aby uzyskać więcej informacji na temat identyfikatorów logowania programu SQL Server, zobacz [Tworzenie identyfikatora logowania](http://msdn.microsoft.com/library/aa337562.aspx).  

toocreate przy użyciu programu SQL Server Management Studio hello nowego logowania programu SQL Server:

1. W **Eksplorator obiektów SQL Server Management Studio**, rozwiń folder hello wystąpienia serwera hello, w której ma zostać toocreate hello nowe dane logowania.
2. Powitania kliknij prawym przyciskiem myszy **zabezpieczeń** folderu, wskaż zbyt**nowy**i wybierz **logowania...** .
   
   ![Nowy identyfikator logowania][10]
3. W hello **nowe dane logowania -** okno dialogowe na powitania **ogólne** strony, wprowadź nazwę hello hello nowego użytkownika w hello **nazwa logowania** pole.
4. Wybierz pozycję **Uwierzytelnianie programu SQL Server**.
5. W hello **hasło** wprowadź hasło dla nowego użytkownika hello. Wprowadź hasło ponownie w hello **Potwierdź hasło** pole.
6. Wybierz opcje zasad haseł tooenforce złożoność i wymuszania, **wymusić zasady haseł** (zalecane). To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
7. Wybierz opcje zasad haseł tooenforce do wygaśnięcia, **wymusić wygaśnięcie hasła** (zalecane). Wymuszanie zasad haseł musi być wybrany tooenable tego pola wyboru. To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
8. Wybierz toocreate użytkownika hello tooforce nowe hasło po hello logowania po raz pierwszy jest używany, **użytkownik musi zmienić hasło przy następnym logowaniu** (zalecane, jeśli to nazwa logowania jest osobie else toouse. W przypadku logowania hello na własny użytek, nie wybieraj tej opcji.) Wymuszanie datę wygaśnięcia hasła musi być wybrany tooenable tego pola wyboru. To jest domyślną opcją w przypadku wybrania uwierzytelniania programu SQL Server.
9. Z hello **domyślna baza danych** wybierz domyślna baza danych hello logowania. **główny** hello domyślne dla tej opcji. Jeśli jeszcze nie utworzono bazy danych użytkownika, to pole pozostanie ustawiona zbyt**wzorca**.
10. W hello **domyślny język** pozostaw opcję **domyślne** jako wartość hello.
    
    ![Właściwości identyfikatora logowania][11]
11. To hello logowania pierwszy tworzysz, możesz wyznaczyć tę nazwę logowania administratora serwera SQL. Jeśli tak, na stronie **Role serwera** zaznacz opcję **sysadmin**.
    
    > [!IMPORTANT]
    > Członkowie stałej roli serwera sysadmin hello mają pełną kontrolę nad hello aparatu bazy danych. Ze względów bezpieczeństwa należy odpowiednio ograniczyć członkostwo w tej roli.
    > 
    > 
    
    ![sysadmin][12]
12. Kliknij przycisk OK.

## <a name="DNS"></a>Określić nazwy DNS hello hello maszyny wirtualnej
tooconnect toohello aparatu bazy danych programu SQL Server z innego komputera, musisz znać hello systemu nazw domen (DNS, Domain Name System) nazwa hello maszyny wirtualnej.

(Jest to hello nazwa hello internet używa tooidentify hello wirtualnej maszyny. Możesz użyć adresu IP hello, ale hello adresu IP mogą ulec zmianie, gdy Azure przenosi zasoby nadmiarowość lub konserwacji. Nazwa DNS Hello będzie stabilny, ponieważ może być przekierowywane tooa nowego adresu IP.)

1. W hello klasycznego portalu Azure (lub hello w poprzednim kroku), wybierz **maszyn wirtualnych**.
2. Na powitania **WYSTĄPIEŃ maszyn wirtualnych** strony w hello **nazwy DNS** poprzedzone kolumny, Znajdź i kopiowania nazwy DNS hello hello maszyny wirtualnej, która jest wyświetlana **http://**. (hello interfejsu użytkownika może nie wyświetlać hello całą nazwę, ale kliknij prawym przyciskiem myszy na nim i wybierz polecenie Kopiuj).

## <a name="cde"></a>Połącz toohello aparatu bazy danych z innego komputera
1. Na komputerze połączone toohello internet, Otwórz program SQL Server Management Studio.
2. W hello **połączyć tooServer** lub **połączyć tooDatabase aparat** okno dialogowe, w hello **nazwy serwera** wprowadź nazwę DNS maszyny wirtualnej (określoną w hello hello poprzednie zadanie) i numer portu publicznego punktu końcowego w formacie hello *DNSName, numer_portu* takich jak **tutorialtestVM.cloudapp.net,57500**.
3. W hello **uwierzytelniania** wybierz opcję **uwierzytelniania programu SQL Server**.
4. W hello **logowania** okno, nazwa typu hello logowania, utworzony w starszej zadań.
5. W hello **hasło** okno, wpisz hasło hello hello logowania, utworzone w wcześniejszych zadań.
6. Kliknij przycisk **Połącz**.

## <a name="amlconnect"></a>Łączenie z toohello aparatu bazy danych z usługi Azure Machine Learning
W następnych etapów hello proces nauki danych zespołu, będzie używany hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild i wdrażanie modeli uczenia maszyny. tooingest danych z baz danych maszyny Wirtualnej programu SQL Server bezpośrednio do usługi Azure Machine Learning szkolenia lub oceniania, użyj hello **i zaimportuj dane** modułu w ramach nowego [Azure Machine Learning Studio](https://studio.azureml.net) eksperymentu. W tym temacie omówiono więcej szczegółowych informacji za pośrednictwem hello proces nauki danych zespołu przewodnik łącza. Aby obejrzeć wprowadzenie, zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).

1. W hello **właściwości** okienko hello [modułu importu danych](https://msdn.microsoft.com/library/azure/dn905997.aspx), wybierz pozycję **bazy danych SQL Azure** z hello **źródła danych** listy rozwijanej.
2. W hello **nazwę serwera bazy danych** tekst Wprowadź`tcp:<DNS name of your virtual machine>,1433`
3. Wprowadź nazwę użytkownika SQL hello w hello **nazwę konta użytkownika serwera** pola tekstowego.
4. Wprowadź hasło użytkownika sql hello w hello **hasło konta użytkownika serwera** pola tekstowego.
   
   ![Uczenie maszynowe Azure i zaimportuj dane][13]

## <a name="shutdown"></a>Zamknięcie i Cofnij Przydział maszyny wirtualnej nieużywane
Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. tooensure, które nie są rozliczane, gdy nie używać sieci maszyny wirtualnej, ma toobe w hello **zatrzymane (Deallocated)** stanu.

> [!NOTE]
> Zamykanie maszyny wirtualnej hello z wewnątrz (przy użyciu apletu Opcje zasilania systemu Windows), hello maszyny Wirtualnej jest zatrzymana, ale pozostaje przydzielone. tooensure opłaty są nie są naliczane, zawsze wstrzymują maszyn wirtualnych z hello [klasycznego portalu Azure](http://manage.windowsazure.com/). Mogą również wstrzymać hello maszyny Wirtualnej za pomocą programu Powershell przez wywołanie metody ShutdownRoleOperation z równości "PostShutdownAction" za "StoppedDeallocated".
> 
> 

tooshutdown i cofnięcia przydzielenia hello maszyny wirtualnej:

1. Zaloguj się za toohello [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.  
2. Wybierz **maszyn wirtualnych** z hello na pasku nawigacyjnym po lewej stronie.
3. Na liście hello maszyn wirtualnych, kliknij na powitania nazwę sieci maszyny wirtualnej, a następnie przejdź toohello **pulpitu NAWIGACYJNEGO** strony.
4. U dołu hello hello strony, kliknij przycisk **zamknięcia**.

![Zamknięcie maszyny Wirtualnej][15]

maszyny wirtualnej Hello zostaną alokację, ale nie został usunięty. Możesz uruchomić ponownie maszynę wirtualną w dowolnym momencie z hello klasycznego portalu Azure.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Maszyna wirtualna Azure SQL Server jest gotowe toouse: co to jest dalej?
Maszyna wirtualna jest teraz gotowy toouse w Twojej ćwiczeniach analizy danych. Maszyna wirtualna Hello również jest gotowa do użycia jako serwer notesu IPython hello eksploracji i przetwarzania danych i innych zadań w połączeniu z uczenie maszynowe Azure i hello zespołu danych nauki procesu (TDSP).

Witaj kolejne kroki w procesie nauki danych hello są mapowane w hello [proces nauki danych zespołu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, procesów i przykładowe istnieje on w ramach przygotowania do uczenia z danych hello Azure maszyny Learning.

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

