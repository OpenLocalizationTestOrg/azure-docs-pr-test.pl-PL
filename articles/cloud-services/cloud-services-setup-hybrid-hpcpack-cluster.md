---
title: "aaaSet się hybrydowego HPC Pack klastra na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Microsoft HPC Pack i Azure tooset Konfigurowanie mały, hybrydowego wysokiej wydajności przetwarzania danych (HPC) klastra"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Skonfiguruj hybrydowych wysokiej wydajności obliczeniowej klastra (HPC) z pakietu Microsoft HPC Pack i węzłów obliczeń platformy Azure na żądanie
Za pomocą programu Microsoft HPC Pack 2012 R2 i Azure tooset wydajności małych, wysokiej hybrydowych, obliczeniowych klastra (HPC). klaster Hello wyświetlane w tym artykule składa się z węzłem głównym HPC Pack lokalnymi i niektóre wyliczenia węzłów wdrażanie na żądanie w systemie Azure usługa w chmurze. Następnie możesz uruchomić zadania obliczeń na powitania hybrydowego klastra.

![Klaster HPC hybrydowego][Overview] 

Ten samouczek pokazuje, jednym z podejść jest czasami nazywany klastra "serii toohello chmury," toouse skalowalne, na żądanie zasobów Azure toorun obliczeniowych aplikacji.

Ten samouczek zakłada nie doświadczenie z lub klastry obliczeniowe HPC Pack. Jest zamierzone toohelp tylko w przypadku wdrażania klastra obliczeniowego hybrydowego szybko w celach demonstracyjnych. Zagadnienia i czynności toodeploy hybrydowego HPC Pack klastra na większą skalę w środowisku produkcyjnym lub toouse HPC Pack 2016, można znaleźć hello [szczegółowe wskazówki](http://go.microsoft.com/fwlink/p/?LinkID=200493). W innych sytuacjach pakietem HPC łącznie z automatycznego wdrażania klastra na maszynach wirtualnych Azure, zobacz [opcje klastra HPC z pakietem Microsoft HPC w systemie Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.
* **Na komputerze lokalnym systemem Windows Server 2012 R2 lub Windows Server 2012** -używa tego komputera jako hello węzła głównego klastra HPC hello. Jeśli nie są już systemem Windows Server, musisz pobrać i zainstalować [wersji ewaluacyjnej](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * Witaj, komputer musi być tooan przyłączone do domeny usługi Active Directory. Do celów testowych można skonfigurować hello węzła głównego komputer jako kontroler domeny. tooadd hello roli serwera usług domenowych w usłudze Active Directory i promować hello węzła głównego komputer jako kontroler domeny, zobacz dokumentację hello systemu Windows Server.
  * toosupport HPC Pack hello systemu operacyjnego musi być zainstalowany w jednej z tych językach: angielski, japoński lub angielski, chiński (uproszczony).
  * Sprawdź, czy krytycznych i ważne aktualizacje są instalowane.
* **HPC Pack 2012 R2** - [Pobierz](http://go.microsoft.com/fwlink/p/?linkid=328024) hello pakiet instalacyjny dla hello najnowszej wersji bez opłat i skopiuj hello pliki toohello węzła głównego komputera. Wybierz pliki instalacyjne w hello sam język jako instalacji systemu Windows Server.

    >[!NOTE]
    > Jeśli chcesz toouse HPC Pack 2016 zamiast HPC Pack 2012 R2, są wymagane dodatkowe czynności konfiguracyjne. Zobacz hello [szczegółowe wskazówki](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Konto domeny** — to konto musi mieć prawa administratora lokalnego na powitania tooinstall węzłem głównym HPC Pack.
* **Połączenie TCP na porcie 443** z hello tooAzure węzła głównego.

## <a name="install-hpc-pack-on-hello-head-node"></a>Zainstaluj pakiet HPC na powitania węzła głównego
Microsoft HPC Pack należy najpierw zainstalować na komputerze lokalnym systemem Windows Server. Ten komputer staje się hello węzła głównego klastra hello.

1. Zaloguj się na węzła głównego toohello przy użyciu konta domeny, które ma uprawnienia administratora lokalnego.

2. Uruchom Kreatora instalacji pakietu HPC hello uruchamiania programu Setup.exe z plików instalacyjnych hello HPC Pack.

3. Na powitania **Instalator HPC Pack 2012 R2** kliknij **nowej instalacji lub Dodaj nowe funkcje tooan istniejącej instalacji**.

    ![HPC Pack 2012 Instalatora][install_hpc1]

4. Na powitania **strony Umowy użytkownika oprogramowania Microsoft**, kliknij przycisk **dalej**.

5. Na powitania **Wybieranie typu instalacji** kliknij przycisk **utworzenie nowego klastra HPC, tworząc węzła głównego**, a następnie kliknij przycisk **dalej**.

6. Kreator Hello działa wiele testów przed instalacją. Kliknij przycisk **dalej** na powitania **reguły instalacji** strony, jeśli wszystkie testy zostały zaliczone pomyślnie. W przeciwnym razie Przejrzyj podane informacje hello i wprowadź niezbędne zmiany w danym środowisku. Następnie uruchom ponownie testów hello lub jeśli niezbędne start Witaj ponownie Kreatora instalacji.
7. Na powitania **konfiguracji bazy danych HPC** upewnij się, że **Head, węzła** jest zaznaczone dla wszystkich baz danych HPC, a następnie kliknij przycisk **dalej**. 

    ![Konfiguracja bazy danych][install_hpc4]

8. Zaakceptuj domyślne na pozostałych stronach kreatora hello hello. Na powitania **zainstalować wymagane składniki** kliknij przycisk **zainstalować**.
   
    ![Instalowanie][install_hpc6]

9. Po zakończeniu instalacji hello, usuń zaznaczenie pola wyboru **Uruchom Menedżera klastra HPC** , a następnie kliknij przycisk **Zakończ**. (Można uruchomić Menedżera klastra HPC w kolejnym kroku.)
   
    ![Zakończ][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Przygotowanie hello subskrypcji platformy Azure
Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com) z subskrypcją platformy Azure. Po wykonaniu tych czynności można wdrożyć węzły platformy Azure z węzłem głównym lokalne powitania. 
  
  > [!NOTE]
  > Również Zanotuj identyfikator subskrypcji platformy Azure, która jest potrzebna później. Identyfikator hello w **subskrypcje** w portalu hello.
  > 

### <a name="upload-hello-default-management-certificate"></a>Przekaż hello domyślnego certyfikatu zarządzania
HPC Pack instaluje certyfikat z podpisem własnym na powitania węzła głównego, nazywany hello domyślne Microsoft HPC Azure Management certyfikatu, który można przekazać jako certyfikat zarządzania platformy Azure. Ten certyfikat jest dostępne w celu testowania i weryfikacja koncepcji wdrożenia toosecure hello połączenie między hello węzła głównego i Azure.

1. Z komputera z węzłem głównym hello, zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Kliknij przycisk **subskrypcje** > *your_subscription_name*.

3. Kliknij przycisk **certyfikaty zarządzania** > **przekazać**.4. Przejdź na powitania węzła głównego hello pliku C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer. Następnie kliknij przycisk **przekazać**.

   
Witaj **domyślne HPC Azure Management** certyfikatu jest widoczna na liście hello certyfikaty zarządzania.

### <a name="create-an-azure-cloud-service"></a>Tworzenie usługi w chmurze platformy Azure
> [!NOTE]
> Aby uzyskać najlepszą wydajność, należy utworzyć w hello hello usługa w chmurze i hello konta magazynu (w kolejnym kroku) tym samym regionie geograficznym.
> 
> 

1. W portalu powitania kliknij **usługi (klasyczne) w chmurze** > **+ Dodaj**.

2.  Wpisz nazwę DNS usługi hello, wybierz grupę zasobów i lokalizację, a następnie kliknij **Utwórz**.


### <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage
1. W portalu powitania kliknij **kont magazynu (klasyczne)** > **+ Dodaj**.

2. Wpisz nazwę konta hello i wybierz hello **klasycznego** modelu wdrażania.

3. Wybierz grupę zasobów i lokalizację i pozostaw innych ustawień na wartości domyślne. Następnie kliknij pozycję **Utwórz**.

## <a name="configure-hello-head-node"></a>Skonfiguruj hello węzła głównego
Menedżer klastrów HPC toodeploy toouse węzły platformy Azure i zadania toosubmit najpierw wykonać pewne czynności konfiguracyjne wymagane klastra.

1. Na powitania węzła głównego Uruchom Menedżera klastra HPC. Jeśli hello **wybierz węzeł Head** zostanie wyświetlone okno dialogowe, kliknij przycisk **komputera lokalnego**. Witaj **listy zadań do wykonania wdrożenia** pojawi się.

2. W obszarze **wymagane zadania wdrażania**, kliknij przycisk **konfiguracji sieci**.
   
    ![Konfigurowanie sieci][config_hpc2]

3. Witaj Kreatora konfiguracji sieci wybierz **wszystkie węzły tylko w sieci przedsiębiorstwa** (topologia 5). Ta konfiguracja sieci jest najprostsza w celach demonstracyjnych hello.
   
    ![Topologia 5][config_hpc3]
   
4. Kliknij przycisk **dalej** tooaccept domyślne wartości na pozostałych stronach kreatora hello hello. Następnie na powitania **przeglądu** , kliknij pozycję **Konfiguruj** konfiguracji sieci hello toocomplete.

5. W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **poświadczenia instalacji**.

6. W hello **poświadczeń instalacji** okno dialogowe, wpisz hello poświadczenia konta domeny hello użytą tooinstall HPC Pack. Następnie kliknij przycisk **OK**. 
   
    ![Poświadczenia instalacji][config_hpc6]
   
7. W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **skonfigurować hello nazewnictwo nowe węzły**.

8. W hello **Określ węzeł nazwy serii** okna dialogowego Zaakceptuj domyślne hello nazwy serii i kliknij przycisk **OK**. Mimo że hello Azure węzły, które można dodać w tym samouczku są nazywane automatycznie, należy wykonać ten krok.
   
    ![Węzeł nazewnictwa][config_hpc8]
   
9. W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **Tworzenie szablonu węzła**. Później w samouczku hello używasz hello węzła szablonu tooadd węzłów Azure toohello klastra.

10. W hello Kreator tworzenia szablonu węzła, wykonaj następujące hello:
    
    a. Na powitania **wybierz typ szablonu węzła** kliknij przycisk **szablonu węzła w systemie Windows Azure**, a następnie kliknij przycisk **dalej**.
    
    ![Szablon węzła][config_hpc10]
    
    b. Kliknij przycisk **dalej** tooaccept hello domyślna nazwa szablonu.
    
    c. Na powitania **Podaj informacje o subskrypcji** wprowadź identyfikator subskrypcji platformy Azure (dostępne w danych konta platformy Azure). Następnie w **certyfikat zarządzania**, wyszukaj **domyślne Microsoft HPC Azure Management.** Następnie kliknij przycisk **Next** (Dalej).
    
    ![Szablon węzła][config_hpc12]
    
    d. Na powitania **Podaj informacje o usłudze** strony, usługa w chmurze wybierz hello i hello konta magazynu, który został utworzony w poprzednim kroku. Następnie kliknij przycisk **Next** (Dalej).
    
    ![Szablon węzła][config_hpc13]
    
    e. Kliknij przycisk **dalej** tooaccept domyślne wartości na pozostałych stronach kreatora hello hello. Następnie na powitania **przeglądu** , kliknij pozycję **Utwórz** toocreate hello węzła szablonu.
    
    > [!NOTE]
    > Domyślnie hello Azure węzła szablon zawiera ustawienia toostart (udostępniania) i Zatrzymaj hello węzłów ręcznie, za pomocą Menedżera klastra HPC. Opcjonalnie można skonfigurować toostart harmonogram i Zatrzymaj automatycznie hello węzły platformy Azure.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Dodaj klaster toohello węzły platformy Azure
Teraz można używać hello węzła szablonu tooadd węzłów Azure toohello klastra. Dodawanie hello węzłów toohello klastra są przechowywane informacje o ich konfiguracji, tak, aby uruchomić (zainicjować obsługi administracyjnej) je w dowolnym momencie hello w usłudze w chmurze. Subskrypcja tylko pobiera obciążony węzły platformy Azure po uruchomionych wystąpień hello hello w usłudze w chmurze.

Wykonaj te kroki tooadd dwóch małych węzłów.

1. W Menedżerze klastra HPC, kliknij przycisk **węzła zarządzania** (nazywane **zarządzanie zasobami** w bieżącej wersji pakietu HPC) > **Dodaj węzeł**.
   
    ![Dodaj węzeł][add_node1]

2. W hello Kreatora dodawania węzłów na powitania **wybierz metodę wdrożenia** kliknij przycisk **węzłów dodać systemu Windows Azure**, a następnie kliknij przycisk **dalej**.
   
    ![Dodaj węzeł Azure][add_node1_1]

3. Na powitania **określ nowe węzły** strony, szablon Azure węzła hello wybierz wcześniej utworzony (o nazwie domyślnie **domyślny szablon AzureNode**). Następnie określ **2** węzłów rozmiar **małych**, a następnie kliknij przycisk **dalej**.
   
    ![Określ węzły][add_node2]
   
4. Na powitania **wykonywanie hello Kreatora dodawania węzłów** kliknij przycisk **Zakończ**.
    
     Dwa węzły platformy Azure o nazwie **AzureCN 0001** i **AzureCN 0002**, zostaną wyświetlone w Menedżerze klastra HPC. Są w hello **wdrożone nie** stanu.
   
    ![Dodanych węzłach][add_node3]

## <a name="start-hello-azure-nodes"></a>Uruchom hello węzły platformy Azure
Jeśli chcesz toouse hello klastra zasobów platformy Azure, użyj Menedżera klastra HPC toostart (zainicjować obsługi administracyjnej) hello Azure węzły i umieść je online.

1. W Menedżerze klastra HPC, kliknij przycisk **węzła zarządzania** (nazywane **zarządzanie zasobami** w bieżącej wersji pakietu HPC), i wybierz hello węzły platformy Azure.

2. Kliknij przycisk **Start**, a następnie kliknij przycisk **OK**.
   
   ![Uruchom węzłów][add_node4]
   
    węzły Hello przejście toohello **inicjowania obsługi administracyjnej** stanu. Inicjowanie obsługi administracyjnej hello tootrack dziennika postęp obsługi administracyjnej hello widoku.
   
    ![Zainicjuj obsługę węzłów][add_node6]

3. Po kilku minutach hello Azure węzły zakończyć inicjowanie obsługi i znajdują się w hello **Offline** stanu. W tym stanie wystąpień roli hello są uruchomione, ale jeszcze nie może zaakceptować zadań klastra.

4. tooconfirm, który hello wystąpień roli są uruchomione w hello portalu Azure, kliknij przycisk **usługi w chmurze (klasyczne)** > *your_cloud_service_name*.
   
   Powinny pojawić się dwa **HpcWorkerRole** uruchomionych w usłudze hello wystąpień (węzłów). HPC Pack automatycznie wdraża dwa **HpcProxy** wystąpienia (rozmiar średnia liczba godzin) toohandle komunikacji między węzłem głównym hello i platformą Azure.

   ![Uruchomione wystąpienia][view_instances1]

5. toorun online toobring hello Azure węzłów klastra, zadań, wybierz hello węzłów, kliknij prawym przyciskiem myszy, a następnie kliknij **przejdź do trybu Online**.
   
    ![Węzły w trybie offline][add_node7]
   
    Menedżer klastrów HPC wskazuje, że węzły hello są w hello **Online** stanu.

## <a name="run-a-command-across-hello-cluster"></a>Uruchom polecenie w klastrze hello
toocheck hello instalacji, użyj hello HPC Pack **clusrun** toorun polecenia polecenie lub aplikacji na co najmniej jednym węźle klastra. Prosty przykład użyć **clusrun** konfiguracji IP hello tooget hello węzły platformy Azure.

1. W węźle głównym hello Otwórz wiersz polecenia jako administrator.

2. Wpisz następujące polecenie hello:
   
    `clusrun /nodes:azurecn* ipconfig`

3. Jeśli zostanie wyświetlony monit, wprowadź hasło administratora klastra. Powinny pojawić się, że podobne toohello następujących danych wyjściowych polecenia.
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a>Uruchom zadanie testowe
Teraz przesłać zadanie testu, które działa w klastrze hybrydowego hello. W tym przykładzie jest zadaniem proste parametrycznych (typ obliczenia leżą równoległe). W tym przykładzie jest uruchamiany podzadania, które dodać tooitself całkowitą przy użyciu hello **ustawić /a** polecenia. Wszystkie węzły hello w klastrze hello współtworzenia podzadania hello toofinishing liczb całkowitych od 1 too100.

1. W Menedżerze klastra HPC, kliknij przycisk **zadania zarządzania** > **nowe zadanie parametrycznych odchylenia**.
   
    ![Nowe zadanie][test_job1]

2. W hello **nowe zadanie parametrycznych odchylenia** okna dialogowego, **wiersza polecenia**, typ `set /a *+*` (zastępowanie hello domyślnego wiersza polecenia wyświetlany). Pozostaw wartości domyślne dla pozostałych ustawień hello, a następnie kliknij przycisk **przesyłania** toosubmit hello zadania.
   
    ![Parametrycznych][param_sweep1]

3. Po zakończeniu zadania hello, kliknij dwukrotnie hello **Moje zadania odchylenia** zadania.

4. Kliknij przycisk **zadania widoku**, a następnie kliknij przycisk podzadanie tooview hello obliczane dane wyjściowe z tym samym poziomie.
   
    ![Wyniki zadań][view_job361]

5. Kliknij toosee, który węzeł wykonać obliczenie hello na tym samym poziomie **przydzielone węzłów**. (Klastra mogą być wyświetlane nazwy innego węzła).
   
    ![Wyniki zadań][view_job362]

## <a name="stop-hello-azure-nodes"></a>Zatrzymaj hello węzły platformy Azure
Po wypróbowanie hello klastra, należy zatrzymać hello Azure węzłów tooavoid niepotrzebnych opłat tooyour konta. Ten krok zatrzymuje usługę w chmurze hello i usuwa hello wystąpień roli platformy Azure.

1. W Menedżerze klastra HPC w **węzła zarządzania** (nazywane **zarządzanie zasobami** w poprzednich wersjach programu HPC Pack), wybierz oba węzły platformy Azure. Następnie kliknij przycisk **zatrzymać**.
   
    ![Zatrzymaj węzłów][stop_node1]

2. W hello **zatrzymania systemu Windows Azure węzłów** okno dialogowe, kliknij przycisk **zatrzymać**. 
   
3. węzły Hello przejście toohello **zatrzymywanie** stanu. Po upływie kilku minut, Menedżer klastra HPC pokazuje, czy węzły hello są **wdrożone nie**.
   
    ![Węzły Niewdrożone][stop_node4]

4. tooconfirm, który hello wystąpień roli nie jest już uruchomiony na platformie Azure w hello Azure portalu, kliknij przycisk **usługi (klasyczne) w chmurze** > *your_cloud_service_name*. Brak wystąpień są wdrażane w środowisku produkcyjnym hello. 
   
    Na tym kończy się hello samouczka.

## <a name="next-steps"></a>Następne kroki
* Eksploruj dokumentacji hello [HPC Pack](https://technet.microsoft.com/library/cc514029).
* Zobacz tooset się hybrydowe wdrożenie klastra HPC Pack na większą skalę [serii tooAzure wystąpień roli procesu roboczego z pakietem Microsoft HPC](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Inne sposoby toocreate klastra HPC Pack na platformie Azure, w tym za pomocą szablonów usługi Azure Resource Manager dla [opcje klastra HPC z pakietem Microsoft HPC w systemie Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
