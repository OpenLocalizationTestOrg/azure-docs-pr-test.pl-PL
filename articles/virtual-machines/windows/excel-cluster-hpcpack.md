---
title: "aaaHPC pakiet klastra dla programów Excel i SOA | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do uruchamiania dużych obciążeń programu Excel i SOA w klastrze HPC Pack na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Wprowadzenie do uruchamiania obciążeń programu Excel i SOA w klastrze HPC Pack na platformie Azure
W tym artykule opisano, jak toodeploy Microsoft HPC Pack 2012 R2 klastra na maszynach wirtualnych platformy Azure przy użyciu szablonu Azure Szybki Start lub opcjonalnie skrypt wdrażania środowiska Azure PowerShell. klaster Hello używa toorun zaprojektowane obrazów maszyny Wirtualnej Azure Marketplace programu Microsoft Excel lub obciążeń zorientowane na usługę architektura (SOA) pakietem HPC. Można użyć hello toorun klastra HPC dla programu Excel i usługi SOA z lokalnych komputera klienckiego. usługi HPC dla programu Excel Hello obejmują odciążenia skoroszytu programu Excel i funkcje zdefiniowane przez użytkownika programu Excel lub funkcji UDF.

> [!IMPORTANT] 
> W tym artykule opiera się na funkcje, szablony i skryptów HPC Pack 2012 R2. W tym scenariuszu nie jest obecnie obsługiwane w HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Na wysokim poziomie hello Poniższy diagram przedstawia klastra HPC Pack hello utworzony.

![Klaster HPC z węzłami uruchamiania obciążeń programu Excel][scenario]

## <a name="prerequisites"></a>Wymagania wstępne
* **Komputer kliencki** — możesz potrzebować klienta z systemem Windows komputera toosubmit próbki programu Excel i SOA zadania toohello klastra. Należy również Windows hello toorun komputera skrypt wdrożenia klastra programu Azure PowerShell (w przypadku wybrania tej metody wdrażania).
* **Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.
* **Limit przydziału rdzeni** — może być konieczne tooincrease hello przydziału rdzeni, zwłaszcza, jeśli wdrożono kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych. Jeśli przy użyciu szablonu Azure szybkiego startu przydziału rdzeni hello w Menedżerze zasobów jest na region platformy Azure. W takim przypadku należy tooincrease hello przydziału w określonym regionie. Zobacz [limity subskrypcji platformy Azure, przydziały i ograniczenia](../../azure-subscription-service-limits.md). limit przydziału, tooincrease [otwarcia żądania pomocy technicznej online klienta](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) bez dodatkowych opłat.
* **Microsoft Office licencji** — Jeśli wdrażanie węzłów za pomocą obrazu maszyny Wirtualnej Marketplace HPC Pack 2012 R2 z programem Microsoft Excel, 30-dniowej wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013 zainstalowano obliczeń. Po zakończeniu okresu próbnego hello wymagane tooprovide prawidłowy Microsoft Office licencji tooactivate Excel toocontinue toorun obciążeń. Zobacz [aktywacji w programie Excel](#excel-activation) dalszej części tego artykułu. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Krok 1. Konfigurowanie klastra HPC Pack na platformie Azure
Zostanie przedstawiony dwie opcje tooset zapasowej hello klastra HPC Pack 2012 R2: najpierw przy użyciu szablonu Azure Szybki Start i hello portal Azure. i sekundę, za pomocą skryptu wdrażania programu Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Opcja 1. Szablon szybkiego startu
Użyj tooquickly szablonów Szybki Start Azure wdrożenie klastra HPC Pack w hello portalu Azure. Po otwarciu szablonu hello w portalu hello, możesz uzyskać Interfejsu prostego, gdzie możesz wprowadzić ustawienia powitania dla klastra. Poniżej przedstawiono kroki hello. 

> [!TIP]
> Należy użyć [szablonu portalu Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) tworzącą podobne klastra specjalnie dla obciążeń programu Excel. kroki Hello różnić się nieznacznie od następującego hello.
> 
> 

1. Odwiedź hello [strony szablonu tworzenia klastrów HPC w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Jeśli chcesz, przejrzyj informacje dotyczące szablonu hello i hello kodu źródłowego.
2. Kliknij przycisk **wdrażanie tooAzure** toostart wdrożenia z szablonem hello w hello portalu Azure.
   
   ![Wdrażanie szablonu tooAzure][github]
3. W portalu hello wykonaj te kroki tooenter hello parametry szablonu klastra HPC hello.
   
   a. Na powitania **parametry** strony, wprowadź lub zmień wartości parametrów szablonu hello. (Kliknij hello ikona dalej tooeach ustawienie informacji pomocy.) W powitania po ekranie przedstawiono przykładowe wartości. W tym przykładzie jest tworzony klaster o nazwie *hpc01* w hello *hpc.local* węzły obliczeniowe domeny składające się z węzła głównego i 2. węzły obliczeniowe Hello są tworzone na podstawie obrazu HPC Pack VM, który zawiera program Microsoft Excel.
   
   ![Wprowadź parametry][parameters-new-portal]
   
   > [!NOTE]
   > Witaj węzła głównego maszyny Wirtualnej jest tworzona automatycznie na podstawie hello [najnowsze obrazu z witryny Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC Pack 2012 R2 w systemie Windows Server 2012 R2. Obecnie hello obraz jest oparty na HPC Pack 2012 R2 Update 3.
   > 
   > Maszyny wirtualne z węzła obliczeń są tworzone na podstawie obrazu najnowsze hello rodziny węzła obliczeń hello wybrane. Wybierz hello **ComputeNodeWithExcel** opcję hello najnowsze HPC Pack obliczeń węzła obrazu zawierającego wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013. toodeploy klastra dla sesji SOA ogólne lub włączenie odciążania UDF programu Excel, wybierz hello **ComputeNode** opcji (bez programu Excel zainstalowane).
   > 
   > 
   
   b. Wybierz subskrypcję hello.
   
   c. Tworzenie grupy zasobów klastra hello, takich jak *hpc01RG*.
   
   d. Wybierz lokalizację dla grupy zasobów hello, takich jak środkowe stany USA.
   
   e. Na powitania **postanowienia prawne** Przejrzyj postanowienia hello. Jeśli akceptujesz, kliknij przycisk **zakupu**. Następnie kliknij przycisk po zakończeniu ustawienie hello wartości dla szablonu hello **Utwórz**.
4. Po zakończeniu wdrażania hello (zwykle trwa około 30 minut), wyeksportować plik certyfikatu hello klastra z węzła głównego klastra hello. W kolejnym kroku należy zaimportować ten publiczny certyfikat na powitania uwierzytelnianie komputera klienckiego tooprovide powitania po stronie serwera dla bezpiecznego powiązania protokołu HTTP.
   
   a. W hello portalu Azure, przejdź do pozycji toohello pulpitu nawigacyjnego, wybierz hello węzła głównego i kliknij przycisk **Connect** u góry hello hello tooconnect strony przy użyciu pulpitu zdalnego.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Użyj standardowych procedur w certyfikacie węzła głównego hello tooexport Menedżer certyfikatów (znajdujący się w obszarze Cert: \LocalMachine\My) bez klucza prywatnego hello. W tym przykładzie należy wyeksportować *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Wyeksportuj certyfikat hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Opcja 2. Użyj skryptu HPC Pack IaaS wdrożenia hello
Hello skrypt wdrożenia HPC Pack IaaS zawiera inny sposób elastyczne toodeploy klastra HPC Pack. Tworzy klaster w hello klasycznego modelu wdrażania, podczas gdy szablon hello używa modelu wdrażania usługi Azure Resource Manager hello. Ponadto hello skryptu jest zgodny z subskrypcji w hello Azure globalnych lub usługi chińskiej wersji platformy Azure.

**Dodatkowe wymagania wstępne**

* **Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.
* **Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Sprawdź wersję hello skryptu hello uruchamiając `New-HPCIaaSCluster.ps1 –Version`. Ten artykuł jest oparty na wersji 4.5.0 lub nowszej hello skryptu.

**Utwórz plik konfiguracji hello**

 Witaj skrypt wdrożenia HPC Pack IaaS używa pliku konfiguracji XML jako dane wejściowe, który opisuje hello infrastruktura klastra HPC hello. toodeploy klaster składa się z węzłem głównym i 18 obliczeniowe węzłów tworzonych z obrazu węzła obliczeń hello, zawierający program Microsoft Excel, Zastąp wartości dla danego środowiska na powitania następującego przykładowego pliku konfiguracji. Aby uzyskać więcej informacji na temat hello pliku konfiguracji, zobacz hello Manual.rtf plik w folderze skryptów hello i [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Uwagi dotyczące hello pliku konfiguracji**

* Witaj **VMName** węzła głównego hello **musi** można hello takie same jak hello **ServiceName**, lub toorun niepowodzeniem zadań SOA.
* Upewnij się, że możesz określić **EnableWebPortal** tak, aby hello węzła głównego certyfikatu jest generowane i eksportować.
* Plik Hello określa skryptu środowiska PowerShell po konfiguracji PostConfig.ps1 uruchamianego na powitania węzła głównego. Hello następującego przykładowego skryptu konfiguruje parametry połączenia magazynu Azure hello usuwa rolę węzła obliczeń hello z węzłem głównym hello i oferuje wszystkie węzły w tryb online, gdy są one wdrażane. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Uruchom skrypt hello**

1. Otwórz konsolę programu PowerShell hello na komputerze klienckim hello jako administrator.
2. Zmień folder skryptu toohello katalogu (E:\IaaSClusterScript w tym przykładzie).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. toodeploy hello HPC Pack klastra, uruchom następujące polecenie hello. W tym przykładzie przyjęto założenie, że ten plik konfiguracji hello znajduje się w E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Uruchamia Hello skrypt wdrożenia HPC Pack przez pewien czas. Jeden element hello skrypt wykonuje jest tooexport i Pobierz certyfikat klastra hello i zapisz go w folderze dokumenty hello bieżącego użytkownika na komputerze klienckim hello. Witaj skrypt generuje następujące toohello podobne wiadomości. W poniższym kroku należy zaimportować certyfikat hello w magazynie certyfikatów odpowiednich hello.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Krok 2. Odciążanie skoroszytów programu Excel i uruchamiania funkcji UDF z klienta lokalnego
### <a name="excel-activation"></a>Aktywacja programu Excel
W przypadku używania hello obrazu maszyny Wirtualnej ComputeNodeWithExcel dla obciążeń produkcyjnych, należy tooprovide prawidłowy Microsoft Office licencji klucza tooactivate programu Excel na powitania węzłów obliczeniowych. W przeciwnym razie hello wersję ewaluacyjną programu Excel wygasa po 30 dniach, a systemem skoroszytów programu Excel zakończy się niepowodzeniem z hello COMException (0x800AC472). 

Można licencjonowania programu Excel o 30 dni oceny czasu: Zaloguj się na toohello węzła głównego i clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` na Excel wszystkie węzły za pomocą Menedżera klastra HPC obliczeniowe. Można rearm maksymalnie dwa razy. Po tym należy podać prawidłowy klucz licencji pakietu Office.

Witaj, Office Professional Plus 2013 zainstalować w obrazie maszyny Wirtualnej hello to wersja woluminu z ogólnym woluminu licencji klucza (GVLK). Możesz to zrobić za pomocą usługi zarządzania kluczami (KMS) / aktywację opartą na usłudze (AD BA) lub klucza aktywacji wielokrotnej (MAK). 

    * toouse usługi KMS/AD-BA, użyj istniejącego serwera usługi KMS lub skonfiguruj nową przy użyciu hello pakietu Microsoft Office 2013 woluminu licencji. (Jeśli chcesz, skonfigurowanie powitania serwera na powitania węzła głównego.) Następnie Aktywuj klucz hosta usługi KMS hello za pośrednictwem hello Internetu lub telefonicznie. Następnie clusrun `ospp.vbs` tooset hello serwera usługi KMS oraz port i aktywowanie pakietu Office na wszystkie węzły obliczeniowe programu Excel hello. 

    * toouse klucza MAK, pierwszy clusrun `ospp.vbs` tooinput hello klucza, a następnie uaktywnić wszystkie węzły obliczeniowe programu Excel hello za pośrednictwem hello Internetu lub telefonicznie. 

> [!NOTE]
> Nie można używać Retail kluczami produktów Office Professional Plus 2013 z tego obrazu maszyny Wirtualnej. Jeśli masz prawidłowe klucze i nośnik instalacyjny dla wersji pakietu Office lub programu Excel innych niż ta wersja woluminu Office Professional Plus 2013 możesz ich użyć. Najpierw Odinstaluj tę wersję woluminu i zainstalować hello wersji. Witaj ponownie zainstalowana jako dostosowane toouse obrazu maszyny Wirtualnej w ramach wdrożenia na dużą skalę, można przechwycić węźle obliczeń programu Excel.
> 
> 

### <a name="offload-excel-workbooks"></a>Odciążanie skoroszytów programu Excel
Wykonaj te kroki toooffload skoroszytu programu Excel, aby został uruchomiony w klastrze HPC Pack hello na platformie Azure. toodo, musi mieć programu Excel 2010 lub 2013 już zainstalowana na komputerze klienckim hello.

1. Użyj jednej z opcji hello w kroku 1 toodeploy klastra HPC Pack z hello Excel obliczeniowe obrazu węzła. Uzyskaj hello klastra-plik certyfikatu (.cer) i klaster nazwy użytkownika i hasła.
2. Na komputerze klienckim hello zaimportuj certyfikat klastra hello w obszarze Cert: \CurrentUser\Root.
3. Upewnij się, że zainstalowano programu Excel. Utwórz plik Excel.exe.config z hello zawartości w powitania po tym samym folderze co Excel.exe na komputerze klienckim hello. Ten krok zapewnia, że załadowaniu tego hello — w modelu COM HPC Pack 2012 R2 programu Excel.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Konfigurowanie powitania klienta toosubmit zadania toohello HPC Pack klastra. Jedną z opcji jest pełna hello toodownload [instalacji HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) i zainstalować powitania klienta HPC Pack. Można również pobrać i zainstalować hello [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) i hello odpowiednie Visual C++ 2010 redistributable dla tego komputera ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. W tym przykładzie używamy próbki skoroszytu programu Excel o nazwie ConvertiblePricing_Complete.xlsb. Można go pobrać [tutaj](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Skopiuj folder roboczy tooa skoroszytu programu Excel hello takich jak D:\Excel\Run.
7. Otwórz skoroszyt programu Excel hello. Na powitania **opracowanie** wstążki, kliknij przycisk **dodatki COM** i upewnij się, że hello dodatek HPC Pack Excel COM została pomyślnie załadowana.
   
   ![Dodatek dla pakietu HPC programu Excel][addin]
8. Edycji hello VBA makro HPCControlMacros w programie Excel, zmieniając hello oznaczone jako wierszy, jak pokazano w hello następującego skryptu. Zastąp wartości odpowiednich dla danego środowiska.
   
   ![Makra programu Excel dla pakietu HPC][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Skopiuj katalog skoroszytu programu Excel hello przekazywania tooan takich jak D:\Excel\Upload. Ten katalog jest określony w stałej HPC_DependsFiles hello w makrze VBA hello.
10. toorun hello skoroszytu w klastrze hello na platformie Azure, kliknij przycisk hello **klastra** przycisk hello arkusza.

### <a name="run-excel-udfs"></a>Uruchom funkcje UDF programu Excel
toorun plikami UDF programu Excel, wykonaj hello w poprzednich krokach 1 – 3 tooset powitania klienta komputera. Dla funkcji UDF programu Excel nie potrzebujesz aplikacji Excel hello toohave zainstalowanej na węzłów obliczeniowych. Tak, gdy węzły obliczeniowe tworzenia klastra, można wybrać obrazu węzła obliczeń normalne, zamiast hello obliczeniowe obrazu węzła przy użyciu programu Excel.

> [!NOTE]
> Istnieje limit 34 znak w hello programu Excel 2010 i 2013 — okno dialogowe łącznik klastra. Możesz użyć tego okna dialogowego pole toospecify hello klastra, który uruchamia hello funkcji UDF. Jeśli nazwa klastra pełne hello jest dłuższy (na przykład hpcexcelhn01.southeastasia.cloudapp.azure.com), nie mieści się w oknie dialogowym hello. Witaj obejściem jest tooset zmiennej dla komputera, takich jak *CCP_IAASHN* z wartością hello hello klastra długie nazwy. Następnie wprowadź *CCP_IAASHN %* w oknie dialogowym hello jako nazwa węzła głównego klastra hello. 
> 
> 

Po pomyślnym wdrożeniu klastra hello kontynuować hello następujące kroki toorun wbudowaną próbki UDF programu Excel. Dostosowane plikami UDF programu Excel, zobacz te [zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL i wdrożyć je w klastrze IaaS hello.

1. Otwórz nowy skoroszyt programu Excel. Na powitania **opracowanie** wstążki, kliknij przycisk **Add-Ins**. Następnie w oknie hello, kliknij przycisk **Przeglądaj**, przejdź do folderu %CCP_HOME%Bin\XLL32 toohello i wybierz próbki hello ClusterUDF32.xll. Jeśli hello ClusterUDF32 nie istnieje na komputerze klienckim hello, skopiuj go w folderze %CCP_HOME%Bin\XLL32 hello na powitania węzła głównego.
   
   ![Wybierz hello funkcji zdefiniowanej przez użytkownika][udf]
2. Kliknij przycisk **pliku** > **opcje** > **zaawansowane**. W obszarze **formuły**, sprawdź **Zezwalaj użytkownika toorun funkcje XLL klastra obliczeniowego**. Następnie kliknij przycisk **opcje** , a następnie wprowadź nazwę klastra pełne hello w **nazwy węzła głównego klastra**. (Jakie zostały zanotowane wcześniej to pole wejściowe to ograniczona too34 znaków, tak długo nazwa_klastra może nie mieści się. Można użyć zmiennej dla komputera, w tym miejscu dla nazwy klastra długie.)
   
   ![Skonfiguruj hello funkcji zdefiniowanej przez użytkownika][options]
3. toorun hello obliczania funkcji zdefiniowanej przez użytkownika w klastrze powitania kliknij komórkę hello z =XllGetComputerNameC() wartość i naciśnij klawisz Enter. Funkcja powitania po prostu pobiera nazwę hello hello węźle obliczeń, w których hello uruchamia funkcji zdefiniowanej przez użytkownika. Dla pierwszego uruchomienia hello okno dialogowe poświadczeń wyświetli monit o hello nazwy użytkownika i hasła tooconnect toohello IaaS klastra.
   
   ![Uruchamianie funkcji zdefiniowanej przez użytkownika][run]
   
   W przypadku wielu komórek toocalculate klawisz Ctrl-Alt-Shift + F9 toorun hello obliczeń na wszystkie komórki.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Krok 3. Uruchom obciążenia SOA z klienta lokalnego
toorun ogólne SOA aplikacji w klastrze HPC Pack IaaS hello, należy najpierw użyć jednej z metod hello w kroku 1 toodeploy hello klastra. W takim przypadku Określ obrazu węzła obliczeń ogólnego, ponieważ nie ma potrzeby Excel na powitania węzłów obliczeniowych. Następnie wykonaj następujące kroki.

1. Po pobraniu hello klastra certyfikatu, należy zaimportować go na komputerze klienckim hello w obszarze Cert: \CurrentUser\Root.
2. Zainstaluj hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) i [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Te narzędzia umożliwiają toodevelop i uruchamianie aplikacji klienckich SOA.
3. Pobierz hello HelloWorldR2 [przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633). Otwórz hello HelloWorldR2.sln w Visual Studio 2010 lub 2012. (Ten przykład nie jest obecnie zgodny z nowszej wersji programu Visual Studio).
4. Tworzenie pierwszej kompilacji projektu EchoService hello. Następnie Wdróż hello usługi toohello IaaS klastra w hello taki sam sposób wdrażania tooan lokalnego klastra. Aby uzyskać szczegółowe instrukcje Zobacz hello Readme.doc w HelloWordR2. Modyfikowanie i tworzenie hello HellWorldR2 i inne projekty, zgodnie z opisem w powitania po sekcji toogenerate hello SOA aplikacji klienckich działających w klastrze IaaS platformy Azure.

### <a name="use-http-binding-with-azure-storage-queue"></a>Używaj wiązania Http z kolejką usługi Azure storage
Wiązanie Http toouse z kolejką usługi Azure storage zmiany kilka toohello przykładowy kod.

* Nazwa klastra hello aktualizacji.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Opcjonalnie użyj domyślnej hello TransportScheme w SessionStartInfo lub jawnie ustaw tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Użyj domyślnego powiązania dla hello BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Ani nie ustawiaj jawnie użycie klasy basicHttpBinding hello.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Opcjonalnie można ustawić hello UseAzureQueue flagi tootrue w SessionStartInfo. Jeśli nie jest zestawem, zostanie ustawiona tootrue domyślnie gdy nazwa klastra hello sufiksy domen platformy Azure i hello TransportScheme jest protokół Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Używaj wiązania Http bez kolejki magazynu Azure
Wiązanie Http toouse bez kolejki magazynu Azure, jawnie ustaw hello UseAzureQueue flagi toofalse w hello SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Użyj NetTcp powiązania
toouse NetTcp powiązanie, konfiguracja hello jest podobne tooconnecting tooan lokalnego klastra. Należy tooopen kilka punktów końcowych na powitania węzła głównego maszyny Wirtualnej. Jeśli używasz hello HPC Pack IaaS wdrożenia skryptu toocreate hello klastra, na przykład punkty końcowe hello zestawu w hello portalu Azure w następujący sposób.

1. Zatrzymaj hello maszyny Wirtualnej.
2. Dodaj porty TCP hello 9090, 9087, 9091, Broker 9094 dla hello sesji, odpowiednio Broker pracownik i usługi danych
   
    ![Konfigurowanie punktów końcowych][endpoint-new-portal]
3. Uruchom hello maszyny Wirtualnej.

Witaj aplikacji klienckiej SOA nie wymagają żadnych zmian, z wyjątkiem zmiany hello head toohello IaaS klastra Pełna nazwa.

## <a name="next-steps"></a>Następne kroki
* Zobacz [tych zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) uzyskać więcej informacji dotyczących uruchamiania obciążeń programu Excel z HPC Pack.
* Zobacz [Zarządzanie SOA usług Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) szczegółowe informacje na temat wdrażania i zarządzania usługami SOA pakietem HPC.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
