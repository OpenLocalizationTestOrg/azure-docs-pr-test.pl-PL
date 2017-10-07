---
title: "wprowadzenie do usługi Konfiguracja DSC automatyzacji Azure aaaGetting | Dokumentacja firmy Microsoft"
description: "Objaśnienie i przykłady typowych zadań hello w żądany stan konfiguracji (Konfiguracja DSC automatyzacji Azure)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure
W tym temacie wyjaśniono, jak toodo hello najbardziej typowych zadań z żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), takie jak tworzenie, importowanie i kompilowanie konfiguracje, dołączania za zarządzanie nimi maszyn i wyświetlania raportów. Omówienie jakie Konfiguracja DSC automatyzacji Azure jest, zobacz [Przegląd usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md). Dokumentacja usługi Konfiguracja DSC w temacie [żądany stan konfiguracji Omówienie środowiska Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).

Ten temat zawiera przewodnik krok po kroku toousing Konfiguracja DSC automatyzacji Azure. Chcąc środowiska próbki, który został już skonfigurowany bez hello wykonaj czynności opisane w tym temacie, można użyć [hello następujący szablon ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Ten szablon ustawia ukończone środowiska Konfiguracja DSC automatyzacji Azure, łącznie z maszyny Wirtualnej platformy Azure, który jest zarządzany przez Konfiguracja DSC automatyzacji Azure.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete hello przykłady w tym temacie, wymagane są następujące hello:

* Konto usługi Azure Automation. Aby uzyskać instrukcje dotyczące tworzenia konta Uruchom jako usługi Azure Automation, zobacz [Konto Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).
* Maszyna wirtualna Azure Resource Manager (nie klasycznego) systemem Windows Server 2008 R2 lub nowszym. Aby uzyskać instrukcje dotyczące tworzenia maszyny Wirtualnej, zobacz [tworzenie pierwszej maszyny wirtualnej systemu Windows w hello portalu Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Tworzenie konfiguracji DSC
Utworzymy prostą [konfiguracji DSC](https://msdn.microsoft.com/powershell/dsc/configurations) dzięki temu hello obecności lub braku hello **serwera sieci Web** Windows funkcji (IIS), w zależności od tego, jak przypisać węzłów.

1. Uruchom hello programu Windows PowerShell ISE (lub dowolnym edytorze tekstów).
2. Wpisz hello następującego tekstu:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Zapisz plik hello jako `TestConfig.ps1`.

Ta konfiguracja wymaga jednego zasobu w każdym węźle bloku, hello [zasobów WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), dzięki temu hello obecności lub braku hello **serwera sieci Web** funkcji.

## <a name="importing-a-configuration-into-azure-automation"></a>Importowanie konfiguracji usługi Automatyzacja Azure
Następnie konfiguracji hello firma Microsoft będzie zaimportować hello konta automatyzacji.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.
4. Na powitania **konfiguracji DSC** bloku, kliknij przycisk **dodać konfigurację**.
5. Na powitania **konfigurację importu** bloku, przeglądania toohello `TestConfig.ps1` plik na komputerze.
   
    ![Zrzut ekranu przedstawiający hello ** importowania konfiguracji ** bloku](./media/automation-dsc-getting-started/AddConfig.png)
6. Kliknij przycisk **OK**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Wyświetlanie konfiguracji w usłudze Automatyzacja Azure
Po zaimportowaniu konfiguracji, można go wyświetlić w hello portalu Azure.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**
4. Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (jest to nazwa hello konfiguracji hello zaimportowane w poprzedniej procedurze hello).
5. Na powitania **konfiguracji TestConfig** bloku, kliknij przycisk **źródło konfiguracji widoku**.
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **źródło konfiguracji TestConfig** zostanie otwarty blok, wyświetlanie kod programu PowerShell hello hello konfiguracji.

## <a name="compiling-a-configuration-in-azure-automation"></a>Kompilowanie konfiguracji w usłudze Automatyzacja Azure
Przed zastosowaniem węzła tooa pożądanego stanu, konfiguracji DSC definiowanie tego stanu muszą można skompilowany w co najmniej jednej konfiguracji węzła (MOF dokumentu), a umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji. Aby uzyskać bardziej szczegółowy opis kompilowania konfiguracji DSC automatyzacji Azure, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md). Aby uzyskać więcej informacji o kompilacji konfiguracji, zobacz [konfiguracji DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**
4. Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa hello hello wcześniej zaimportowane konfiguracji).
5. Na powitania **konfiguracji TestConfig** bloku, kliknij przycisk **skompilować**, a następnie kliknij przycisk **tak**. Spowoduje to uruchomienie zadania kompilacji.
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig hello wyróżnianie przycisk kompilacji](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Podczas kompilowania konfiguracji w automatyzacji Azure automatycznie wdraża dowolnego serwera ściągania toohello za utworzony węzła konfiguracji.
> 
> 

## <a name="viewing-a-compilation-job"></a>Wyświetlanie zadania kompilacji
Po rozpoczęciu kompilacji mógł być wyświetlany w hello **zadań kompilacji** kafelka w hello **konfiguracji** bloku. Witaj **zadań kompilacji** zawiera obecnie uruchomiona, zakończone oraz zadania zakończone niepowodzeniem. Po otwarciu bloku zadania kompilacji zawiera informacje dotyczące tego zadania, w tym wszelkie błędy lub ostrzeżenia napotkał, parametry wejściowe używane w konfiguracji hello i kompilacja dzienników.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.
4. Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa hello hello wcześniej zaimportowane konfiguracji).
5. Na powitania **zadań kompilacji** kafelka hello **konfiguracji TestConfig** bloku, kliknij na dowolnym hello zadań. A **zadania kompilacji** zostanie otwarty blok, oznaczenie daty hello hello zadania kompilacji został uruchomiony.
   
    ![Zrzut ekranu przedstawiający blok zadania kompilacji hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. Kliknij Kafelek w hello **zadania kompilacji** toosee bloku więcej szczegółowych informacji o hello zadania.

## <a name="viewing-node-configurations"></a>Wyświetlanie konfiguracji węzłów
Pomyślne zakończenie zadania kompilacji tworzy nowy co najmniej jednej konfiguracji węzła. Konfiguracja węzła jest dokumentem MOF, który jest serwerem ściągania toohello wdrożone i gotowe toobe ściągnąć i stosowane przez co najmniej jeden węzeł. Konfiguracje węzłów hello można wyświetlić w Twoje konto usługi Automatyzacja w hello **konfiguracji węzłów DSC** bloku. Konfiguracja węzła ma nazwę w postaci hello *ConfigurationName*. *NodeName*.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji węzłów DSC**.
   
    ![Zrzut ekranu przedstawiający blok konfiguracji węzłów DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Dołączanie maszyny Wirtualnej platformy Azure do zarządzania z usługi Konfiguracja DSC automatyzacji Azure
Można użyć Konfiguracja DSC automatyzacji Azure toomanage Azure VMs (Classic i Resource Manager), lokalnych maszyn wirtualnych systemu Linux maszyny, usług AWS maszyn wirtualnych i fizycznych komputerach lokalnych. W tym temacie firma Microsoft opisano sposób tooonboard tylko Menedżera zasobów maszyn wirtualnych platformy Azure. Uzyskać informacji na temat dołączania innych typów urządzeń, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard maszyny Wirtualnej platformy Azure Resource Manager do zarządzania przez Konfiguracja DSC automatyzacji Azure
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.
4. W hello **węzłów DSC** bloku, kliknij przycisk **dodać maszyny Wirtualnej Azure**.
   
    ![Zrzut ekranu przedstawiający blok węzłów DSC hello wyróżnianie hello przycisku Dodaj maszyny Wirtualnej Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **wybierz maszyny wirtualne tooonboard**.
6. W hello **wybierz maszyny wirtualne** bloku, wybierz hello wirtualna tooonboard i kliknij **OK**.
   
   > [!IMPORTANT]
   > Musi to być maszyny Wirtualnej platformy Azure Resource Manager systemem Windows Server 2008 R2 lub nowszym.
   > 
   > 
7. W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Konfigurowanie danych rejestracji**.
8. W hello **rejestracji** bloku, wprowadź nazwę hello konfiguracji węzła hello ma tooapply toohello maszyny Wirtualnej w hello **Nazwa konfiguracji węzła** pole. To musi dokładnie odpowiadać nazwie hello konfiguracji węzła w hello konta automatyzacji. W tym momencie podanie nazwy jest opcjonalne. Można zmienić konfiguracji węzła hello przypisane po węźle hello dołączania.
   Sprawdź **ponowny rozruch węzła, w razie potrzeby**, a następnie kliknij przycisk **OK**.
   
    ![Zrzut ekranu przedstawiający blok rejestracji hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    Określona konfiguracja węzła Hello będzie zastosowane toohello maszyny Wirtualnej w odstępach czasu określonych przez hello **częstotliwość trybu konfiguracji**, i hello maszyny Wirtualnej będzie sprawdzać dostępność aktualizacji konfiguracji węzła toohello w odstępach czasu określonych przez hello  **Częstotliwość odświeżania**. Aby uzyskać więcej informacji na temat korzystania z tych wartości, zobacz [hello Konfigurowanie lokalny program Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Utwórz**.

Azure rozpocznie się proces hello hello dołączania maszyny Wirtualnej. Po zakończeniu hello maszyny Wirtualnej pojawi się na powitania **węzłów DSC** bloku w hello konta automatyzacji.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Wyświetlanie listy hello węzłów DSC
Można wyświetlić listy hello wszystkie komputery, które zostały został załadowany do zarządzania na Twoim koncie automatyzacji w hello **węzłów DSC** bloku.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.

## <a name="viewing-reports-for-dsc-nodes"></a>Wyświetlanie raportów węzłów DSC
Zawsze Konfiguracja DSC automatyzacji Azure przeprowadza sprawdzanie spójności na węzeł zarządzany, węzeł hello wysyła stanu serwera ściągania wstecz toohello raportów. Można wyświetlać te raporty na powitania bloku dla tego węzła.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.
4. Na powitania **raporty** kafelka, kliknij dowolną raportów hello hello na liście.
   
    ![Zrzut ekranu przedstawiający blok raportu hello](./media/automation-dsc-getting-started/NodeReport.png)

W bloku hello pojedynczy raport można wyświetlić hello następujące informacje o stanie spójności odpowiednich hello Sprawdź:

* Witaj raportowanie stanu — węzeł hello jest "Zgodnych" hello konfiguracji "Niepowodzenie", czy węzeł hello jest "Nie są zgodne" (gdy węzeł hello jest w **applyandmonitor** trybu i hello komputer nie jest w stanie hello potrzeby).
* Godzina rozpoczęcia Hello hello Sprawdzanie spójności.
* Sprawdź Hello łącznego czasu wykonywania hello spójności.
* Sprawdź typ Hello spójności.
* Wszelkie błędy, w tym hello błąd kodu i komunikatu o błędzie. 
* Zasoby usługi Konfiguracja DSC używane w konfiguracji hello i hello stanu każdego zasobu (czy hello węzeł jest w stanie hello potrzebne dla tego zasobu) — możesz kliknąć na każdym tooget zasobów bardziej szczegółowe informacje dla tego zasobu.
* Witaj nazwa, adres IP i tryb konfiguracji węzła hello.

Możesz również kliknąć **wyświetlić raport raw** toosee hello rzeczywiste dane, które hello węzła wysyła toohello serwera. Aby uzyskać więcej informacji o korzystaniu z tych danych zobacz [przy użyciu serwera raportu DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).

Może upłynąć trochę czasu, po węzeł został załadowany przed hello pierwszy raport jest dostępny. Konieczne może toowait się minut too30 hello pierwszego raportu po dołączeniu węzła.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Ponowne przypisywanie konfiguracji inny węzeł tooa węzła
Można przypisać toouse węzła konfiguracji inny węzeł niż hello jedną, która początkowo przypisana.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.
4. Na powitania **węzłów DSC** bloku, kliknij na nazwie hello hello węzła ma tooreassign.
5. W bloku powitania dla tego węzła, kliknij **węzła Przypisz**.
   
    ![Zrzut ekranu przedstawiający blok węzła hello wyróżnianie hello przypisać węzła przycisku](./media/automation-dsc-getting-started/AssignNode.png)
6. Na powitania **przypisać konfiguracji węzła** bloku, wybierz hello węzła konfiguracji toowhich mają tooassign hello węzeł, a następnie kliknij przycisk **OK**.
   
    ![Zrzut ekranu przedstawiający blok przypisać konfiguracji węzła hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Wyrejestrowywania węzła
Jeśli nie chcesz już toobe węzła, zarządza Konfiguracja DSC automatyzacji Azure, możesz go wyrejestrować.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.
3. Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.
4. Na powitania **węzłów DSC** bloku, kliknij na nazwie hello hello węzła ma toounregister.
5. W bloku powitania dla tego węzła, kliknij **Unregister**.
   
    ![Zrzut ekranu przedstawiający blok węzła hello wyróżnianie hello Unregister przycisku](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Pokrewne artykuły
* [Omówienie usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md)
* [Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)
* [Omówienie stanu konfiguracji żądanego programu Windows PowerShell](https://msdn.microsoft.com/powershell/dsc/overview)
* [Polecenia cmdlet systemu Azure Automation DSC](/powershell/module/azurerm.automation/#automation)
* [Cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)

