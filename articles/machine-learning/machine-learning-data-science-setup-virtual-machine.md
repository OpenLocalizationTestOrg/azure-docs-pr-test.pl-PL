---
title: "Skonfiguruj maszynę wirtualną jako serwer notesu IPython | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 66fd9e5573390ac6faeb82ad5b0f7ddb18d50a77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Konfigurowanie maszyny wirtualnej Azure jako serwera IPython Notebook na potrzeby zaawansowanej analizy
W tym temacie pokazano, jak udostępnić i skonfigurować maszyny wirtualnej platformy Azure, zaawansowana analityka, który może służyć jako część środowiska analizy danych. Maszyny wirtualnej systemu Windows jest konfigurowana obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure, AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów zaawansowana analityka. Eksplorator usługi Storage platformy Azure i AzCopy, na przykład można podać wygodny sposób przekazywania danych do magazynu obiektów blob platformy Azure z komputera lokalnego lub pobrać go na komputerze lokalnym, z magazynu obiektów blob.

## <a name="create-vm"></a>Krok 1: Tworzenie maszyny wirtualnej platformy Azure ogólnego przeznaczenia
Jeśli masz już maszyny wirtualnej platformy Azure i po prostu chcesz skonfigurować serwer notesu IPython na nim, można pominąć ten krok i przejdź do [krok 2: Dodawanie punktu końcowego dla komputerów przenośnych IPython do istniejącej maszyny wirtualnej](#add-endpoint).

Przed rozpoczęciem procesu tworzenia maszyny wirtualnej na platformie Azure, musisz określić rozmiaru maszyny, która jest potrzebne do przetwarzania danych dla swojego projektu. Mniejsze maszyny mają mniej pamięci i mniejszą liczbę rdzeni Procesora niż większych maszyn, ale również są mniej kosztowne. Listę typów maszyny i cenach, zobacz <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">cennik maszyn wirtualnych </a> strony

1. Zaloguj się do <a href="https://manage.windowsazure.com" target="_blank">klasycznego portalu Azure</a>i kliknij przycisk **nowy** w lewym dolnym rogu. Okno zostanie wyskakujące. Wybierz **OBLICZENIOWE** -> **maszyny WIRTUALNEJ** -> **GALERII FROM**.
   
    ![Tworzenie obszaru roboczego][24]
2. Wybierz jedną z następujących obrazów:
   
   * Windows Server 2012 R2 Datacenter
   * Windows Server Essentials Experience (Windows Server 2012 R2)
     
     Następnie kliknij przycisk strzałki w prawo w prawej dolnej, aby przejść do następnej strony konfiguracji.
     
     ![Tworzenie obszaru roboczego][25]
3. Wprowadź nazwę maszyny wirtualnej, który chcesz utworzyć, wybierz rozmiar maszyny (domyślne: A3) na podstawie rozmiaru danych komputera ma procesu i wydajny sposób mają maszyny (rozmiar pamięci i liczby rdzeni obliczeń), wprowadź nazwę użytkownika i hasło dla komputera. Następnie kliknij przycisk strzałki w prawo, aby przejść do następnej strony konfiguracji.
   
    ![Tworzenie obszaru roboczego][26]
4. Wybierz **REGION/KOLIGACJI grupy/WIRTUALNEJ sieci** zawierający **konta MAGAZYNU** czy planowane jest używany dla tej maszyny wirtualnej, a następnie wybierz konto magazynu. Dodawanie punktu końcowego na dole w **punkty końcowe** pola, wprowadzając nazwę punktu końcowego ("IPython" poniżej). Można wybrać dowolny ciąg jako **nazwa** punktu końcowego i dowolną liczbą całkowitą od 0 do 65536, który jest **dostępne** jako **PORT PUBLICZNY**. **PORT prywatny** musi być **9999**. Należy **uniknąć** przy użyciu publicznego portów, które już zostały przypisane do usług internetowych. <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Porty dla usług Internet</a> zawiera listę portów, które zostały przypisane i należy unikać.
   
    ![Tworzenie obszaru roboczego][27]
5. Kliknij znacznik wyboru, aby rozpocząć proces tworzenia maszyny wirtualnej.
   
    ![Tworzenie obszaru roboczego][28]

Może potrwać 15 25 minut, aby ukończyć proces tworzenia maszyny wirtualnej. Po utworzeniu maszyny wirtualnej, stan tej maszyny powinny być widoczne jako **systemem**.

![Tworzenie obszaru roboczego][29]

## <a name="add-endpoint"></a>Krok 2: Dodawanie punktu końcowego dla komputerów przenośnych IPython do istniejącej maszyny wirtualnej
Jeśli maszyna wirtualna została utworzona zgodnie z instrukcjami w kroku 1, punkt końcowy dla notesu IPython został już dodany, a ten krok można pominąć.

Jeśli już istnieje maszyna wirtualna, a następnie należy dodać punkt końcowy dla przenośnych IPython, który zostanie zainstalowany w kroku 3 poniżej pierwsze Zaloguj się do klasycznego portalu Azure, wybierz maszynę wirtualną, a następnie Dodaj punkt końcowy dla serwera IPython notesu. Poniższa ilustracja zawiera zrzut ekranu portalu po punktu końcowego IPython Notes został dodany do maszyny wirtualnej systemu Windows.

![Tworzenie obszaru roboczego][17]

## <a name="run-commands"></a>Krok 3: Instalowanie notesu IPython i inne narzędzia do obsługi
Po utworzeniu maszyny wirtualnej, należy użyć protokołu RDP (Remote Desktop) do logowania się do maszyny wirtualnej systemu Windows. Aby uzyskać instrukcje, zobacz [jak Zaloguj się do maszyny wirtualnej systemem Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Otwórz **wiersza polecenia** (**nie okno poleceń programu Powershell**) jako **administratora** i uruchom następujące polecenie.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Po zakończeniu instalacji serwer notesu IPython jest uruchamiana automatycznie w *C:\\użytkowników\\\<nazwy użytkownika\>\\dokumenty\\notesów IPython* katalogu.

Po wyświetleniu monitu wprowadź hasło dla notebooków IPython i hasło administratora komputera. Dzięki temu notesu IPython do uruchamiania jako usługa na komputerze.

## <a name="access"></a>Krok 4: Dostępu IPython notesów z przeglądarki sieci web
Dostęp do notesu IPython serwera, otwórz sieć web przeglądarki i dane wejściowe *nazwa DNS komputera https://&#60;virtual >: &#60; numeru portu publicznego >* w polu tekstowym adres URL. W tym miejscu *&#60; numeru portu publicznego >* powinien być określony, dodania punktu końcowego notesu IPython numer portu.

*&#60; nazwę DNS maszyny wirtualnej >* można znaleźć w klasycznym portalu Azure. Po zalogowaniu się do klasycznego portalu, kliknij przycisk **maszyn wirtualnych**, wybierz komputer, a następnie wybierz utworzony **pulpitu NAWIGACYJNEGO**, nazwa DNS będą wyświetlane w następujący sposób:

![Tworzenie obszaru roboczego][19]

Wystąpi ostrzeżenie o treści *występuje problem z certyfikatem zabezpieczeń tej witryny sieci Web* (Internet Explorer) lub *połączenie nie jest prywatny* rysunki (Chrome), jak pokazano poniżej. Kliknij przycisk **Kontynuuj przeglądanie tej witryny sieci Web (niezalecane)** (Internet Explorer) lub **zaawansowane** , a następnie  **przejdź do &#60;* Nazwa DNS*> (unsafe) ** (Chrome), aby kontynuować. Następnie wprowadź hasło określone wcześniej do notesów IPython.

**Internet Explorer:**
![Tworzenie obszaru roboczego][20]

**Chrome:**
![Tworzenie obszaru roboczego][21]

Po zalogowaniu się notesu IPython, katalog *DataScienceSamples* będzie wyświetlana w przeglądarce. Ten katalog zawiera przykładowe IPython notesów, które są współużytkowane przez firmę Microsoft, aby ułatwić użytkownikom przeprowadzanie zadania analizy danych. Te przykładowe notesy IPython są wyewidencjonowane z [ **repozytorium GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) do maszyn wirtualnych podczas instalacji serwera IPython notesu. Firma Microsoft obsługuje i często aktualizuje to repozytorium. Repozytorium GitHub, aby uzyskać najnowsze notesów IPython próbki mogą odwiedzać użytkownicy.
![Tworzenie obszaru roboczego][18]

## <a name="upload"></a>Krok 5: Przekaż istniejącego notesu IPython z komputera lokalnego na serwerze IPython notesu
Notesów IPython umożliwiają łatwe użytkownikom na przekazywanie istniejącego notesu IPython na urządzeniach lokalnych na serwerze notesu IPython na maszynach wirtualnych. Po zalogowaniu się do notesu IPython w przeglądarce sieci web, kliknij w **katalogu** który notesu IPython zostanie przekazany do. Następnie wybierz plik .ipynb notesu IPython do przekazania z komputera lokalnego w **Eksploratora plików**i przeciągnij i upuść go do katalogu IPython notesu przeglądarki sieci web. Kliknij przycisk **przekazać** przycisk można przekazać pliku .ipynb serwerowi IPython notesu. Inni użytkownicy następnie rozpocząć korzystanie z niej w z przeglądarek sieci web.

![Tworzenie obszaru roboczego][22]

![Tworzenie obszaru roboczego][23]

## <a name="shutdown"></a>Zamknij i usunąć przydział maszyny wirtualnej nieużywane
Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. Aby upewnić się, że nie rozliczanych, gdy nie używać sieci maszyny wirtualnej, musi ona być w **zatrzymane (Deallocated)** stanu nieużywane.

> [!NOTE]
> Wyłączenie maszyny wirtualnej z wewnątrz maszyny Wirtualnej (przy użyciu apletu Opcje zasilania systemu Windows), maszyna wirtualna zostanie zatrzymana ale pozostaje przydzielone. Aby upewnić się, należy kontynuować, będą naliczane opłaty, zawsze wstrzymują maszyn wirtualnych z [klasycznego portalu Azure](http://manage.windowsazure.com/). Można również Zatrzymaj maszynę Wirtualną za pomocą programu Powershell przez wywołanie metody **ShutdownRoleOperation** z "PostShutdownAction" równa się "StoppedDeallocated".
> 
> 

Aby zamknąć i Cofnij Przydział maszyny wirtualnej:

1. Zaloguj się do [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu swojego konta.  
2. Wybierz **maszyn wirtualnych** na pasku nawigacyjnym po lewej stronie.
3. Na liście maszyny wirtualnej, kliknij nazwę maszyny wirtualnej, a następnie przejdź do **pulpitu NAWIGACYJNEGO** strony.
4. W dolnej części strony kliknij **zamknięcia**.

![Zamknięcie maszyny Wirtualnej][15]

Maszyna wirtualna zostanie alokację, ale nie został usunięty. Możesz uruchomić ponownie maszynę wirtualną w dowolnym momencie z klasycznego portalu Azure.

## <a name="your-azure-vm-is-ready-to-use-whats-next"></a>Maszyna wirtualna Azure jest gotowa do użycia: co to jest dalej?
Maszyna wirtualna jest teraz gotowy do użycia w Twojej ćwiczeń analizy danych. Maszyna wirtualna jest również gotowe do użycia jako serwer notesu IPython do eksploracji i przetwarzania danych i innych zadań w połączeniu z uczenie maszynowe Azure i procesu nauki danych zespołu.

Następne kroki w procesie nauki zespołu danych są mapowane w [ścieżki szkoleniowe dotyczące](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, proces i przykładowe istnieje on w ramach przygotowania do uczenia z danych z usługi Azure Machine Learning.

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
