---
title: aaaSet zapasowej maszyny wirtualnej na serwerze notesu IPython | Dokumentacja firmy Microsoft
description: "Ustaw zapasowej maszyny wirtualnej platformy Azure do użycia w środowisku nauki danych z serwerem IPython zaawansowana analityka."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Konfigurowanie maszyny wirtualnej Azure jako serwera IPython Notebook na potrzeby zaawansowanej analizy
W tym temacie przedstawiono sposób tooprovision i konfigurowanie maszyny wirtualnej platformy Azure, zaawansowana analityka, który może służyć jako część środowiska analizy danych. maszyny wirtualnej systemu Windows Hello jest skonfigurowany z obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure, AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów zaawansowana analityka. Azure Eksploratora usługi Storage i AzCopy, na przykład oferują wygodny sposób magazynu obiektów blob tooAzure tooupload danych z komputera lokalnego lub toodownload go tooyour komputera lokalnego z magazynu obiektów blob.

## <a name="create-vm"></a>Krok 1: Tworzenie maszyny wirtualnej platformy Azure ogólnego przeznaczenia
Jeśli już maszyny wirtualnej platformy Azure i po prostu chcesz tooset serwera notesu IPython na nim, można pominąć ten krok i przejść za[krok 2: Dodawanie punktu końcowego dla istniejącej maszyny wirtualnej notesów IPython tooan](#add-endpoint).

Przed rozpoczęciem powitalne proces tworzenia maszyny wirtualnej na platformie Azure, należy toodetermine rozmiar hello hello komputer, który jest wymagane tooprocess hello danych ich projektu. Mniejsze maszyny mają mniej pamięci i mniejszą liczbę rdzeni Procesora niż większych maszyn, ale również są mniej kosztowne. Listę typów maszyny i cenach, zobacz hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">cennik maszyn wirtualnych </a> strony

1. Zaloguj się za<a href="https://manage.windowsazure.com" target="_blank">klasycznego portalu Azure</a>i kliknij przycisk **nowy** hello dole po lewej stronie ekranu. Okno zostanie wyskakujące. Wybierz **OBLICZENIOWE** -> **maszyny WIRTUALNEJ** -> **GALERII FROM**.
   
    ![Tworzenie obszaru roboczego][24]
2. Wybierz jedną z hello następujące obrazy:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials Experience (Windows Server 2012 R2)
     
     Następnie kliknij przycisk hello Strzałka w prawo w hello niższe prawo toogo hello dalej strona konfiguracji.
     
     ![Tworzenie obszaru roboczego][25]
3. Wprowadź nazwę dla maszyny wirtualnej hello ma toocreate, hello wybierz rozmiar maszyny hello (domyślne: A3) na podstawie rozmiaru hello maszyny hello danych hello jest tooprocess będzie i jak zaawansowane ma hello toobe maszyny (pamięci rozmiaru i hello liczba rdzeni obliczeniowe) , wprowadź nazwę użytkownika i hasło dla hello maszyny. Następnie kliknij przycisk hello Strzałka prawo toogo toohello następnej strony konfiguracji.
   
    ![Tworzenie obszaru roboczego][26]
4. Wybierz hello **REGION/KOLIGACJI grupy/WIRTUALNEJ sieci** zawierający hello **konta MAGAZYNU** planowania toouse dla tej maszyny wirtualnej, a następnie wybierz konto magazynu. Dodawanie punktu końcowego u dołu hello w hello **punkty końcowe** pola, wprowadzając nazwę hello hello punktu końcowego ("IPython" poniżej). Można wybrać dowolny ciąg jako hello **nazwa** hello punktu końcowego i dowolną liczbą całkowitą od 0 do 65536, który jest **dostępne** jako hello **PORT PUBLICZNY**. Witaj **PORT prywatny** ma toobe **9999**. Należy **uniknąć** przy użyciu publicznego portów, które już zostały przypisane do usług internetowych. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Porty dla usług Internet</a> zawiera listę portów, które zostały przypisane i należy unikać.
   
    ![Tworzenie obszaru roboczego][27]
5. Kliknij maszynę wirtualną rozszerzeń hello znacznik wyboru toostart hello procesu udostępniania.
   
    ![Tworzenie obszaru roboczego][28]

Może upłynąć 15 25 minut toocomplete hello maszyny wirtualnej procesu udostępniania. Po utworzeniu maszyny wirtualnej hello hello stan tej maszyny powinny być widoczne jako **systemem**.

![Tworzenie obszaru roboczego][29]

## <a name="add-endpoint"></a>Krok 2: Dodawanie punktu końcowego dla notebooków IPython tooan istniejącej maszyny wirtualnej
Jeśli utworzono hello maszyny wirtualnej, wykonując instrukcje hello w kroku 1, punkt końcowy hello notesu IPython został już dodany, a ten krok można pominąć.

Jeśli hello maszyny wirtualnej już istnieje, i potrzebne tooadd punktu końcowego dla notesu IPython, który zostanie zainstalowany w kroku 3 poniżej, pierwszego logowania tooAzure klasyczny portal wybierz maszynę wirtualną hello i Dodaj punkt końcowy powitania serwera IPython notesu. Hello następujący rysunek zawiera zrzut ekranu portalu powitania po dodano punkt końcowy hello notesu IPython maszyny wirtualnej systemu Windows tooa.

![Tworzenie obszaru roboczego][17]

## <a name="run-commands"></a>Krok 3: Instalowanie notesu IPython i inne narzędzia do obsługi
Po utworzeniu maszyny wirtualnej hello, użyj toolog protokołu RDP (Remote Desktop) na maszynie wirtualnej toohello systemu Windows. Aby uzyskać instrukcje, zobacz [jak tooLog na tooa maszyny wirtualnej z systemu Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Otwórz hello **wiersza polecenia** (**nie hello okno polecenia programu Powershell**) jako **administratora** i hello uruchom następujące polecenie.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Po zakończeniu instalacji hello, hello hello uruchamiany jest automatycznie serwer notesu IPython *C:\\użytkowników\\\<nazwy użytkownika\>\\dokumenty\\IPython Notesów* katalogu.

Po wyświetleniu monitu wprowadź hasło dla hello notesu IPython i hello hasło administratora maszyny hello. Dzięki temu hello toorun notesu IPython jako usługa na komputerze hello.

## <a name="access"></a>Krok 4: Dostępu IPython notesów z przeglądarki sieci web
tooaccess hello notesu IPython serwera, otwórz sieć web przeglądarki i dane wejściowe *nazwa DNS komputera https://&#60;virtual >: &#60; numeru portu publicznego >* w polu tekstowym adres URL hello. W tym miejscu hello *&#60; numeru portu publicznego >* powinna być określona hello punktu końcowego notesu IPython dodania numeru portu hello.

Witaj *&#60; nazwę DNS maszyny wirtualnej >* znajduje się w temacie hello klasycznego portalu Azure. Po zalogowaniu toohello klasycznego portalu kliknij **maszyn wirtualnych**, wybierz pozycję hello maszyny utworzone, a następnie wybierz **pulpitu NAWIGACYJNEGO**, nazwa DNS hello będą wyświetlane w następujący sposób:

![Tworzenie obszaru roboczego][19]

Wystąpi ostrzeżenie o treści *występuje problem z certyfikatem zabezpieczeń tej witryny sieci Web* (Internet Explorer) lub *połączenie nie jest prywatny* (Chrome), jak pokazano poniżej hello dane. Kliknij przycisk **Kontynuuj toothis witryny internetowej (niezalecane)** (Internet Explorer) lub **zaawansowane** , a następnie  **kontynuować za &#60;* Nazwa DNS*> (unsafe) ** toocontinue (Chrome). Następnie wprowadź hasło hello zostanie określony wcześniej tooaccess hello notesów IPython.

**Internet Explorer:**
![Tworzenie obszaru roboczego][20]

**Chrome:**
![Tworzenie obszaru roboczego][21]

Po zalogowaniu toohello IPython notesu, katalog *DataScienceSamples* będą wyświetlane w przeglądarce hello. Ten katalog zawiera przykładowe IPython notesów, które są udostępniane przez Microsoft toohelp użytkowników postępowania danych nauki zadania. Te przykładowe notesy IPython są wyewidencjonowane z [ **repozytorium GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello maszyn wirtualnych podczas hello procesu instalacji serwera IPython notesu. Firma Microsoft obsługuje i często aktualizuje to repozytorium. Użytkownicy mogą odwiedzać hello GitHub repozytorium tooget hello niedawno zaktualizowanego próbki IPython notesów.
![Tworzenie obszaru roboczego][18]

## <a name="upload"></a>Krok 5: Przekaż istniejącego notesu IPython z komputera lokalnego toohello notesu IPython serwera
Notesów IPython umożliwiają łatwe dla użytkowników tooupload istniejącego notesu IPython na ich komputerach toohello notesu IPython server na maszynach wirtualnych hello. Po zalogowaniu toohello notesu IPython w przeglądarce sieci web, kliknij na powitania **katalogu** tego hello notesu IPython zostanie przekazany do. Wybierz tooupload notesu IPython .ipynb plików z komputera lokalnego hello w hello **Eksploratora plików**i przeciągnij i upuść toohello notesu IPython katalogu na powitania przeglądarki sieci web. Kliknij przycisk hello **przekazać** przycisk tooupload hello .ipynb pliku toohello notesu IPython serwera. Inni użytkownicy następnie rozpocząć korzystanie z niej w z przeglądarek sieci web.

![Tworzenie obszaru roboczego][22]

![Tworzenie obszaru roboczego][23]

## <a name="shutdown"></a>Zamknij i usunąć przydział maszyny wirtualnej nieużywane
Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. tooensure, które nie są rozliczane, gdy nie używać sieci maszyny wirtualnej, ma toobe w hello **zatrzymane (Deallocated)** stanu nieużywane.

> [!NOTE]
> Zamknij maszynę wirtualną hello z wewnątrz maszyny Wirtualnej (przy użyciu apletu Opcje zasilania systemu Windows), hello hello maszyny Wirtualnej jest zatrzymana, ale pozostaje przydzielone. tooensure toobe rozliczane, nie należy kontynuować zawsze wstrzymują maszyn wirtualnych z hello [klasycznego portalu Azure](http://manage.windowsazure.com/). Mogą również wstrzymać hello maszyny Wirtualnej za pomocą programu Powershell, wywołując **ShutdownRoleOperation** z "PostShutdownAction" zbyt równa "StoppedDeallocated".
> 
> 

tooshut w dół i cofnięcia przydzielenia hello maszyny wirtualnej:

1. Zaloguj się za toohello [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.  
2. Wybierz **maszyn wirtualnych** z hello na pasku nawigacyjnym po lewej stronie.
3. Na liście hello maszyn wirtualnych, kliknij na powitania nazwę sieci maszyny wirtualnej, a następnie przejdź toohello **pulpitu NAWIGACYJNEGO** strony.
4. U dołu hello hello strony, kliknij przycisk **zamknięcia**.

![Zamknięcie maszyny Wirtualnej][15]

maszyny wirtualnej Hello zostaną alokację, ale nie został usunięty. Możesz uruchomić ponownie maszynę wirtualną w dowolnym momencie z hello klasycznego portalu Azure.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Maszyna wirtualna Azure jest gotowy toouse: co to jest dalej?
Maszyna wirtualna jest teraz gotowy toouse w Twojej ćwiczeniach analizy danych. Maszyna wirtualna Hello również jest gotowa do użycia jako serwer notesu IPython hello eksploracji i przetwarzania danych i innych zadań w połączeniu z uczenie maszynowe Azure i hello proces nauki danych zespołu.

Witaj następne kroki w hello zespołu w procesie nauki danych są mapowane w hello [ścieżki szkoleniowe dotyczące](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, procesów i przykładowe istnieje on w ramach przygotowania do uczenia z danych hello Azure maszyny Learning.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
