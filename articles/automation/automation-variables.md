---
title: zasoby aaaVariable automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Zmienna zasoby są wartości, które są dostępne tooall elementów runbook i konfiguracji DSC automatyzacji Azure.  W tym artykule opisano szczegóły hello zmiennych i w jaki sposób toowork z nimi w tworzeniu zarówno tekstową i graficznego."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Zasoby zmiennej usługi Automatyzacja Azure

Zmienna zasoby są wartości, które są dostępne tooall elementów runbook i konfiguracji DSC na Twoim koncie automatyzacji. Można je utworzyć, zmodyfikować i pobierane z hello portalu Azure, programu Windows PowerShell, a za pomocą elementu runbook lub konfiguracji DSC. Zmienne automatyzacji to przydatne w przypadku hello następujące scenariusze:

- Udostępnienie wartości dla wielu elementów runbook lub konfiguracji DSC.

- Udostępnienie wartości dla wielu zadań z hello konfiguracji DSC lub tego samego elementu runbook.

- Zarządzanie wartością z portalu hello lub hello wiersz polecenia programu Windows PowerShell, który jest używany przez elementy runbook lub konfiguracji DSC, takiego jak zestaw wspólne elementy konfiguracji, takie jak określonej listy nazw maszyn wirtualnych określonej grupy zasobów, nazwa domeny usługi AD, itp.  

Zmienne automatyzacji są trwałe, dlatego nadal toobe dostępne nawet wtedy, gdy element runbook hello lub konfiguracji DSC nie powiedzie się.  Umożliwia to także toobe wartości, ustawione przez jeden element runbook, który następnie jest używany przez inny lub jest używany przez hello tego samego elementu runbook lub hello konfiguracji DSC następnym uruchomieniu.

Po utworzeniu zmiennej możesz określić on być przechowywany zaszyfrowany.  Gdy zmienna jest zaszyfrowana, jest bezpiecznie przechowywana w automatyzacji Azure i jego wartość nie można pobrać z hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) polecenia cmdlet, które wchodzi w skład hello modułu Azure PowerShell.  Witaj jedynym sposobem można pobrać zaszyfrowaną wartość pochodzi z hello **Get-AutomationVariable** działania elementu runbook lub konfiguracji DSC.

> [!NOTE]
> Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne. Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji. Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure. Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.

## <a name="variable-types"></a>Typy zmiennych

Po utworzeniu zmiennej z hello portalu Azure, należy określić typ danych z listy rozwijanej hello tak hello portalu można wyświetlić hello odpowiednią kontrolkę dla wartości zmiennej hello. Zmienna Hello nie jest ograniczone toothis danych typu, ale musisz ustawić zmiennej hello przy użyciu programu Windows PowerShell, jeśli chcesz, aby toospecify wartość innego typu. Jeśli określisz **nie zdefiniowano**, a następnie hello hello zmiennej zostanie ustawiona zbyt**$null**, i należy ustawić wartość hello z hello [AzureAutomationVariable zestaw](http://msdn.microsoft.com/library/dn913767.aspx) polecenia cmdlet lub **Set-AutomationVariable** działania.  Nie można utworzyć ani zmienić hello wartość dla typu zmienną złożone w portalu hello, ale można podać wartości typu przy użyciu programu Windows PowerShell. Typy złożone zostaną zwrócone jako [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Można przechowywać wiele wartości tooa pojedynczą zmienną, tworząc tablicy lub tablica skrótów i zapisać go toohello zmiennej.

Witaj poniżej przedstawiono listę typów zmiennych, które są dostępne w automatyzacji:

* Ciąg
* Liczba całkowita
* Data i godzina
* Wartość logiczna
* Wartość null

## <a name="cmdlets-and-workflow-activities"></a>Działania poleceń cmdlet i przepływu pracy

polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate zmiennych i zarządzania nimi automatyzacji przy użyciu programu Windows PowerShell. One dostarczane jako część hello [modułu Azure PowerShell](../powershell-install-configure.md) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.

|Polecenia cmdlet|Opis|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Pobiera hello wartość istniejącej zmiennej.|
|[Nowe AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Tworzy nową zmienną i ustawia jej wartość.|
|[Usuń AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Usuwa istniejącej zmiennej.|
|[Zestaw AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Ustawia hello wartość istniejącej zmiennej.|

Hello działań przepływu pracy w poniższej tabeli hello są używane tooaccess zmienne automatyzacji w elemencie runbook. Są dostępne tylko dla elementu runbook lub konfiguracji DSC i nie są dostarczane jako część hello modułu Azure PowerShell.

|Działania przepływu pracy|Opis|
|:---|:---|
|Get-AutomationVariable|Pobiera hello wartość istniejącej zmiennej.|
|Set-AutomationVariable|Ustawia hello wartość istniejącej zmiennej.|

> [!NOTE] 
> Należy unikać używania zmiennych w hello — Nazwa parametru **Get-AutomationVariable** runbook lub konfiguracji DSC, ponieważ może to skomplikować wykrywanie zależności między elementami runbook lub konfiguracji DSC automatyzacji zmienne w czasie projektowania.

## <a name="creating-a-new-automation-variable"></a>Tworzenie nowej zmiennej automatyzacji

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate nową zmienną z hello portalu Azure

1. Twoje konto usługi Automatyzacja kliknij hello **zasoby** Kafelek, a następnie na powitania **zasoby** bloku, wybierz opcję **zmienne**.
2. Na powitania **zmienne** kafelka, wybierz opcję **dodać zmienną**.
3. Uzupełnij opcje hello na powitania **nową zmienną** bloku i kliknij przycisk **Utwórz** Zapisz nową zmienną hello.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate nową zmienną za pomocą programu Windows PowerShell

Witaj [AzureRmAutomationVariable nowy](https://msdn.microsoft.com/library/mt603613.aspx) polecenie cmdlet tworzy nową zmienną i ustawia wartość początkową. Można pobrać przy użyciu wartości hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Jeśli wartość hello jest typem prostym, zwracany jest tego samego typu. Jeśli jest to typ złożony, a następnie **PSCustomObject** jest zwracany.

Hello następujące przykładowe polecenia Pokaż jak toocreate zmiennej typu string, a następnie zwracają wartość.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Hello następujące przykładowe polecenia Pokaż jak toocreate zmiennej o złożony typem, a następnie zwracają jego właściwości. W takim przypadku obiekt maszyny wirtualnej z **Get-AzureRmVm** jest używany.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Użycie zmiennej w element runbook lub konfiguracji DSC

Użyj hello **Set-AutomationVariable** działania tooset hello wartości zmiennej automatyzacji elementu runbook lub Konfiguracja DSC oraz hello **Get-AutomationVariable** tooretrieve go.  Nie można używać hello **AzureAutomationVariable zestaw** lub **Get-AzureAutomationVariable** polecenia cmdlet w element runbook lub konfiguracji DSC, ponieważ są mniej wydajne niż hello działania przepływu pracy.  Również nie można pobrać wartości hello bezpiecznego zmiennych z **Get-AzureAutomationVariable**.  Witaj tylko sposób toocreate nową zmienną z wewnątrz elementu runbook lub konfiguracji DSC jest toouse hello [AzureAutomationVariable nowy](http://msdn.microsoft.com/library/dn913771.aspx) polecenia cmdlet.


### <a name="textual-runbook-samples"></a>Przykłady tekstowy

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Ustawianie i pobieranie prostych wartości zmiennych

Hello następujące przykładowe polecenia Pokaż jak tooset i pobierania zmiennej w elemencie runbook tekstową. W tym przykładzie zakłada się, że zmienne typu całkowitoliczbowego o nazwie *NumberOfIterations* i *NumberOfRunnings* oraz zmienna typu ciąg o nazwie *SampleMessage* zostały już utworzone.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Ustawianie i pobieranie obiekt złożony w zmiennej

Hello następujące przykładowy kod przedstawia sposób tooupdate zmiennej w tekstowy złożona wartość. W tym przykładzie maszyny wirtualnej platformy Azure są pobierane z **Get-AzureVM** i zapisane tooan istniejącej zmiennej automatyzacji.  Zgodnie z objaśnieniem w [typy zmiennych](#variable-types), to jest przechowywana jako PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


W hello następującego kodu hello wartość jest pobierana z maszyny wirtualnej hello toostart zmiennej i używany hello.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Ustawiania i pobierania kolekcję w zmiennej

Hello następujące przykładowy kod przedstawia sposób toouse zmienną z kolekcją złożonych wartości tekstowej elementu runbook. W tym przykładzie wiele maszyn wirtualnych platformy Azure są pobierane z **Get-AzureVM** i zapisane tooan istniejącej zmiennej automatyzacji.  Zgodnie z objaśnieniem w [typy zmiennych](#variable-types), to jest przechowywane jako zbiór PSCustomObjects.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

W hello następującego kodu kolekcji hello są pobierane z hello zmiennej i używać toostart każdej maszyny wirtualnej.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Przykłady graficznym elementem runbook

W graficznym elementem runbook, należy dodać hello **Get-AutomationVariable** lub **Set-AutomationVariable** hello zmiennej w okienku Biblioteka hello edytora graficznego usługi hello prawym przyciskiem myszy i wybierając hello działanie, które mają.

![Dodawanie zmiennej toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Ustawianie wartości w zmiennej
Witaj poniższej ilustracji przedstawiono przykładowe działania tooupdate zmiennej z prostą wartością w graficznym elementem runbook. W tym przykładzie jednej maszyny wirtualnej platformy Azure są pobierane z **Get-AzureRmVM** i nazwa komputera hello jest zapisywany tooan istniejącej zmiennej automatyzacji z typu String.  Nie ma znaczenia, czy hello [jest link potoku lub sekwencji](automation-graphical-authoring-intro.md#links-and-workflow) ponieważ oczekuje tylko jednego obiektu w danych wyjściowych hello.

![Zestaw prostej zmiennej](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Następne kroki

* Zobacz toolearn więcej informacji na temat łączenie działań w tworzeniu graficznego [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md) 

