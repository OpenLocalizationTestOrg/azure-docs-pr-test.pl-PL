---
title: "aaaProvision partii zadań Azure pul z niestandardowymi obrazami | Dokumentacja firmy Microsoft"
description: "Można utworzyć partię obliczeniowe puli z tooprovision niestandardowego obrazu węzłów, które zawierają hello oprogramowania i danych aplikacji. Niestandardowe obrazy są efektywną tooconfigure obliczeniowe toorun węzłów obciążeń partii."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Użyć niestandardowego obrazu toocreate puli maszyn wirtualnych

Podczas tworzenia puli maszyn wirtualnych w partii zadań Azure, należy określić obraz maszyny wirtualnej (VM), który udostępnia hello systemu operacyjnego w każdym węźle obliczeń w puli hello. Za pomocą portalu Azure Marketplace obrazu lub poprzez świadczenie niestandardowego obrazu wirtualnego dysku twardego, które zostały przygotowane, można utworzyć puli maszyn wirtualnych. Podając niestandardowego obrazu, masz kontrolę nad konfiguracji systemu operacyjnego hello w czasie hello, że każdy węzeł obliczeniowy zostanie zainicjowana. Obraz niestandardowy mogą również obejmować aplikacji i danych referencyjnych, które są dostępne na powitania węźle obliczeń, jak jego obsługa została zainicjowana.

Przy użyciu niestandardowego obrazu może zaoszczędzić czas podczas pobierania węzłów obliczeniowych przez pulę gotowe toorun obciążenie partii. Mimo że zawsze używać obrazu platformy Azure Marketplace i instalować oprogramowanie na każdy węzeł obliczeniowy po została przygotowana, ta metoda może być mniej wydajne niż przy użyciu niestandardowego obrazu. 

Niektóre przyczyny toouse niestandardowego obrazu, który jest skonfigurowany dla danego scenariusza obejmują konieczności:

- **Konfigurowanie systemu operacyjnego hello (systemu operacyjnego)** żadnej specjalnej konfiguracji systemu operacyjnego hello można wykonać na powitania niestandardowego obrazu. 
- **Zainstaluj dużych aplikacji.** Instalowanie aplikacji na obraz niestandardowy jest bardziej efektywne niż je zainstalować w każdym węźle obliczeń, po jego obsługa została zainicjowana.
- **Skopiuj znacznej ilości danych.** Jeśli hello dane są kopiowane toohello niestandardowego obrazu, musi tylko toobe skopiować jeden raz, zamiast tooeach węźle obliczeń, oszczędzając czas i przepustowości.
- **Podczas procesu konfiguracji hello ponowny rozruch hello maszyny Wirtualnej.** Witaj ponowny rozruch maszyny Wirtualnej może być czasochłonne, zwłaszcza, jeśli liczba węzłów obliczeniowych.

## <a name="prerequisites"></a>Wymagania wstępne

- **Konto usługi partia zadań utworzonych za pomocą Tryb alokacji puli subskrypcji użytkownika hello.** toouse pule maszyny wirtualnej tooprovision niestandardowego obrazu, tworzenie konta partii zadań z hello subskrypcji użytkownika [Tryb alokacji puli](batch-api-basics.md#pool-allocation-mode). W tym trybie partii pule są przydzielone do subskrypcji hello, w którym znajduje się konto hello. Zobacz hello [konta](batch-api-basics.md#account) sekcji [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md) informacje na temat ustawiania trybu alokacji puli hello podczas tworzenia konta usługi partia zadań.

- **Konto usługi Azure Storage.** toocreate puli maszyn wirtualnych przy użyciu niestandardowego obrazu należy standardowe, ogólnego przeznaczenia konta magazynu Azure w hello tej samej subskrypcji i regionu. Jeśli tworzysz niestandardowy obraz z maszyny Wirtualnej platformy Azure, zostanie skopiowany hello toohello konto magazynu obrazu gdzie znajduje się dysk systemu operacyjnego hello maszyny Wirtualnej, a toocreate oddzielnego konta magazynu nie są wymagane. 
    
## <a name="prepare-a-custom-image"></a>Przygotuj obraz niestandardowy

tooprepare niestandardowego obrazu do użycia z partii musi generalize istniejącej instalacji systemu Linux lub Windows. Uogólnianie instalacji systemu operacyjnego usuwa informacje dotyczące komputera. wynik Hello jest obraz, który można zainstalować na innych komputerach lub maszynach wirtualnych.  

> [!IMPORTANT]
> Partii nie obsługuje obecnie korzysta z platformy Azure zarządzanych obrazów tooprovision puli. niestandardowy obraz powitania Użyj tooprovision puli musi być przechowywany w usłudze Azure Storage. 
>
> Podczas przygotowywania obraz niestandardowy, należy pamiętać hello następujące punkty:
> - Upewnij się, obraz systemu operacyjnego podstawowej tego hello Użyj tooprovision Twojego pule partii jest nie ma wstępnie zainstalowanych rozszerzeń Azure, takich jak hello rozszerzenia niestandardowego skryptu. Jeśli obraz powitania zawiera wstępnie zainstalowane rozszerzenia, Azure mogą wystąpić problemy, wdrażanie hello maszyny Wirtualnej.
> - Upewnij się, tego hello podstawowy obraz systemu operacyjnego zapewniają się, że używa hello domyślnym tymczasowego dysku, jak hello agenta węzła partii aktualnie oczekuje hello domyślnym tymczasowego dysku.
>
>

Można użyć dowolnego istniejącego przygotowane obrazu systemu Windows lub Linux jako obraz niestandardowy. Na przykład, jeśli chcesz toouse obraz lokalnych, Przekaż konta Azure Storage tooan obrazu hello, który znajduje się w hello tej samej subskrypcji i regionu co użycie konta usługi partia zadań [AzCopy](../storage/storage-use-azcopy.md) lub innego narzędzia przekazywania.

Można również przygotować obraz niestandardowy z nowej lub istniejącej maszyny Wirtualnej Azure. W przypadku tworzenia nowej maszyny Wirtualnej, można użyć obrazu portalu Azure Marketplace jako obrazu podstawowego hello niestandardowego obrazu, a następnie dostosować go. podstawowy obraz powitania toocustomize utworzyć maszyny Wirtualnej platformy Azure i dodać aplikacje lub tooit danych. Następnie generalize hello tooserve maszyny Wirtualnej jako obraz niestandardowy i zapisać go tooAzure magazynu. 

tooprepare niestandardowego obrazu z maszyny Wirtualnej platformy Azure, wykonaj następujące kroki:

1. Utwórz **niezarządzane** maszyny Wirtualnej platformy Azure z obrazu w portalu Azure Marketplace. Azure Marketplace zawiera obrazy dla obu [Windows](../virtual-machines/windows/quick-create-portal.md) i [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    W kroku 3 hello proces tworzenia maszyny Wirtualnej, upewnij się, że wybrano **nr** dla **magazynu: Użyj zarządzanych dysków** opcji. Również Zanotuj hello nazwy konta magazynu dla dysku systemu operacyjnego hello maszyny Wirtualnej, ponieważ to konto magazynu jest również, gdzie Azure zapisze niestandardowego obrazu:

    ![Tworzenie maszyny Wirtualnej niezarządzanej i nazwy konta magazynu hello Uwaga](media/batch-custom-images/vm-create-storage.png)
 
2. Ukończyć powitalnych proces tworzenia maszyny Wirtualnej, a następnie zaczekaj na jej toobe przydzielone przez platformę Azure. Oto obrazu, który zawiera Maszynę wirtualną w hello portalu Azure w hello uruchomiona:

    ![Utwórz maszynę Wirtualną z obrazu witryny marketplace](media/batch-custom-images/vm-status-running.png)

3. Po uruchomieniu hello maszyny Wirtualnej, Połącz tooit za pośrednictwem protokołu RDP (dla systemu Windows) lub protokołu SSH (dla systemu Linux). Zainstaluj oprogramowanie niezbędne skopiować żądanych danych, a następnie Uogólnij hello maszyny Wirtualnej. Wykonaj kroki hello opisanego w [Generalize hello wirtualna](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Wykonaj kroki hello zbyt[Zaloguj tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). tooinstall programu Azure PowerShell, zobacz [Omówienie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Następnie wykonaj kroki hello zbyt[hello Deallocate maszyny Wirtualnej i zestaw hello stanu toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    W portalu Azure hello Zwróć uwagę, że powitalne cofnięciu przydziału maszyny Wirtualnej:

    ![Upewnij się, że powitalne cofnięciu przydziału maszyny Wirtualnej](media/batch-custom-images/vm-status-deallocated.png)

6.  Tworzenie i zapisywanie tooAzure obrazu maszyny Wirtualnej hello magazynu przy użyciu hello [AzureRmVMImage Zapisz](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) polecenia cmdlet programu PowerShell. Postępuj zgodnie z instrukcjami hello opisane w [Utwórz obraz powitania](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    Witaj maszyny Wirtualnej jest zapisywany obraz konta usługi Magazyn Azure toohello utworzone podczas tworzenia hello maszyny Wirtualnej, jak pokazano w kroku 1 tej procedury. polecenie cmdlet Hello AzureRmVMImage Zapisz zapisuje toohello obraz powitania **systemu** kontenera na tym koncie magazynu. Witaj `-DestinationContainername` katalogu wirtualnego w ramach hello nazwy parametrów **systemu** kontenera. Witaj `-VHDNamePrefix` parametr określa prefiks nazwy obiektu blob hello. Ten prefiks jest dołączany początku toohello nazwa obiektu blob z łącznikiem. 

    Na przykład załóżmy, że wywołanie AzureRmVMImage Zapisz z hello następujące parametry:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    Obraz wynikowy Hello jest zapisywany toohello lokalizację i nazwę obiektu blob, pokazano poniżej:

    ![Lokalizacja zapisanego wirtualnego dysku twardego w kontenerze systemu](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Maszyna wirtualna platformy Azure niezarządzane tworzy kilka kont magazynu do różnych celów. Jeśli nie Zanotuj hello nazwę kontenera magazynu hello dysku hello systemu operacyjnego, gdy hello maszyna wirtualna została utworzona, a następnie znajdź magazynu hello skojarzonego konta, które zawiera hello **systemu** kontenera. Nawigowanie hello **systemu** kontenera toofind hello niestandardowego obrazu przy użyciu określonej wartości hello na powitania **AzureRmVMImage Zapisz** polecenia.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Utwórz pulę z niestandardowego obrazu w portalu hello

Po zapisaniu niestandardowego obrazu i znasz lokalizacji, można utworzyć puli partii z tego obrazu. Wykonaj te kroki toocreate pulę z hello portalu Azure:

1. Przejdź tooyour konta usługi partia zadań w hello portalu Azure. To konto musi być w hello tej samej subskrypcji i regionu co hello magazynu zawierającego niestandardowy obraz powitania konta. 
2. W hello **ustawienia** okno na powitania po lewej, wybierz hello **pule** elementu menu.
3. W hello **pule** okna, wybierz hello **Dodaj** polecenia.
4. Na powitania **Dodaj pulę,** wybierz **niestandardowego obrazu (Linux/system Windows)** z hello **typ obrazu** listy rozwijanej. Hello portal Wyświetla hello **obraz niestandardowy** selektora. Przejdź toohello konta magazynu, gdzie znajduje się obraz niestandardowy, a następnie wybierz hello żądaną wirtualnego dysku twardego z kontenera hello. 
5. Wybierz prawidłowe hello **wydawcy lub oferta/jednostki Sku** dla Twojego niestandardowego pliku VHD.
6. Określ pozostałych hello wymagane ustawienia, w tym hello **rozmiaru węzła**, **Target dedykowanych węzłów**, i **niski priorytet węzłów**, a także wszelkie potrzebne ustawienia opcjonalne.

    Na przykład dla programu Microsoft Windows Server Datacenter 2016 niestandardowego obrazu, hello **Dodaj pulę,** zostanie wyświetlone okno, jak pokazano poniżej:

    ![Dodaj pulę z niestandardowego obrazu systemu Windows](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck czy istniejącej puli jest oparta na niestandardowego obrazu, zobacz hello **systemu operacyjnego** właściwości hello zasobów podsumowania część hello **puli** okna. Jeśli pula hello został utworzony z obrazu niestandardowego, ustawiono zbyt**niestandardowego obrazu maszyny Wirtualnej**.

Wszystkie dyski VHD niestandardowe skojarzone z pulą są wyświetlane w puli hello **właściwości** okna.
 
## <a name="next-steps"></a>Następne kroki

- Aby uzyskać szczegółowe informacje o partii, zobacz [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md).
- Aby uzyskać informacje dotyczące tworzenia konta usługi partia zadań, zobacz [Tworzenie konta usługi partia zadań z portalu Azure hello](batch-account-create-portal.md).
