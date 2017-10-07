---
title: "aaaAdd Azure automatyzacji elementów runbook toorecovery plany w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Site Recovery można rozszerzyć planów odzyskiwania przy użyciu usługi Automatyzacja Azure. Dowiedz się, jak toocomplete złożone zadania podczas tooAzure odzyskiwania."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Dodaj planów toorecovery elementów runbook usługi Automatyzacja Azure
W tym artykule opisano sposób Azure Site Recovery integruje się z usługi Automatyzacja Azure toohelp rozszerzyć planów odzyskiwania. Plany odzyskiwania można organizować odzyskiwania maszyn wirtualnych, które są chronione za pomocą usługi Site Recovery. Plany odzyskiwania działa zarówno dla chmury dodatkowej tooa replikacji i tooAzure replikacji. Plany odzyskiwania również sprawić, że odzyskiwania hello **spójnie dokładne**, **powtarzalne**, i **automatyczne**. Jeśli nie zostanie za pośrednictwem sieci tooAzure maszyn wirtualnych, integracja z usługi Automatyzacja Azure rozszerza planów odzyskiwania. Służy on tooexecute elementów runbook, które oferują zaawansowane automatyzacji zadań.

W przypadku nowych tooAzure automatyzacji może [Zarejestruj](https://azure.microsoft.com/services/automation/) i [Pobierz przykładowe skrypty](https://azure.microsoft.com/documentation/scripts/). Aby uzyskać więcej informacji i toolearn jak tooorchestrate tooAzure odzyskiwania przy użyciu [planów odzyskiwania](https://azure.microsoft.com/blog/?p=166264), zobacz [usługi Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

W tym artykule opisano sposób integrowania elementu runbook usługi Automatyzacja Azure do planów odzyskiwania. Używamy przykłady tooautomate podstawowe zadania, które wcześniej wymagały ręcznej interwencji. Opisano również sposób tooconvert tooa odzyskiwania wieloetapowych jednym kliknięciem Akcja odzyskiwania.

## <a name="customize-hello-recovery-plan"></a>Dostosowywanie hello planu odzyskiwania
1. Przejdź toohello **usługi Site Recovery** bloku zasobów planu odzyskiwania. Na przykład hello plan odzyskiwania obejmuje dwa tooit dodano maszyn wirtualnych, do odzyskania. toobegin Dodawanie elementu runbook, kliknij przycisk hello **Dostosuj** kartę.

    ![Kliknij przycisk Dostosuj hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Kliknij prawym przyciskiem myszy **Grupa 1: Uruchom**, a następnie wybierz **post dodać akcję**.

    ![Kliknij prawym przyciskiem myszy Grupa 1: Uruchom i dodać post akcji](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Kliknij przycisk **wybierz skrypt**.

4. Na powitania **Akcja aktualizacji** bloku, nazwa skryptu hello **Hello World**.

    ![Witaj aktualizacji akcji bloku](media/site-recovery-runbook-automation-new/update-rp.png)

5. Wprowadź nazwę konta automatyzacji.
    >[!NOTE]
    > Konto automatyzacji Hello można w dowolnym regionie Azure. Hello konta automatyzacji musi należeć do hello tej samej subskrypcji co magazyn usługi Azure Site Recovery hello.

6. Na Twoim koncie automatyzacji wybierz element runbook. Ten element runbook jest hello skrypt, który jest uruchamiany podczas wykonywania hello hello planu odzyskiwania, po odzyskaniu hello hello pierwszej grupy.

7. skrypt hello toosave, kliknij przycisk **OK**. skrypt Hello jest dodawany zbyt**Grupa 1: kroki po**.

    ![1:Start grupy po akcji](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Zagadnienia dotyczące Dodawanie skryptu

* Dla opcji zbyt**usunąć krok** lub **hello skrypt aktualizacji**, kliknij prawym przyciskiem myszy hello skryptu.
* Skrypt można uruchomić na platformie Azure w trybie failover z tooAzure komputera lokalnego. Ponadto można go uruchomić na platformie Azure jako skrypt lokacji podstawowej zamknięcia systemu, podczas powrotu po awarii z platformy Azure tooan na lokalnej maszynie.
* Po uruchomieniu skryptu injects kontekstu planu odzyskiwania. Witaj poniższy przykład przedstawia zmiennej kontekstu:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Witaj w poniższej tabeli wymieniono hello nazwę i opis każdej zmiennej w kontekście hello.

    | **Nazwa zmiennej** | **Opis** |
    | --- | --- |
    | RecoveryPlanName |Nazwa Hello planu hello uruchomione. Ta zmienna pomaga wykonać różne operacje, na podstawie nazwy planu odzyskiwania hello. Również można ponownie użyć skryptu hello. |
    | FailoverType |Określa, czy tryb failover hello testu, planowane lub nieplanowane. |
    | Element FailoverDirection |Określa, czy odzyskiwania tooa podstawowej lub dodatkowej lokacji. |
    | Identyfikator grupy |Identyfikuje numer grupy hello w planie odzyskiwania hello uruchomionej hello planu. |
    | VmMap |Tablica wszystkich maszyn wirtualnych w grupie hello. |
    | Klucz VMMap |Unikatowy klucz (GUID) dla każdej maszyny Wirtualnej. Witaj sam jak identyfikator Azure Virtual Machine Manager (VMM) hello hello maszyny Wirtualnej, jeśli to możliwe. |
    | SubscriptionId |Identyfikator subskrypcji platformy Azure Hello, w których hello maszyna wirtualna została utworzona. |
    | RoleName |Nazwa Hello hello maszyny Wirtualnej platformy Azure, która jest przywracana. |
    | CloudServiceName |Nazwa usługi w chmurze Azure Hello pod które hello maszyna wirtualna została utworzona. |
    | Grupy zasobów o nazwie|Nazwa grupy zasobów platformy Azure Hello pod którą hello maszyna wirtualna została utworzona. |
    | RecoveryPointId|Witaj sygnaturę czasową po odzyskaniu hello maszyny Wirtualnej. |

* Upewnij się, że tego konta automatyzacji hello ma hello następujących modułów:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Wszystkie moduły muszą być zgodne wersje. Tooensure łatwy sposób, że wszystkie moduły są zgodne jest toouse hello najnowsze wersje wszystkich modułów hello.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Dostęp do wszystkich maszyn wirtualnych z hello VMMap w pętli
Użyj następującego kodu tooloop na wszystkich maszynach wirtualnych z hello Microsoft VMMap hello:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hello grupy nazwa i rola Nazwa wartości zasobów są puste, gdy skrypt hello jest grupy rozruchu tooa akcji przed. wartości Hello są wypełniane tylko wtedy, gdy hello maszyn wirtualnych w danej grupie powiedzie się w tryb failover. skrypt Hello jest akcją po hello grupy rozruchu.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Użyj hello sam element runbook automatyzacji w wielu planów odzyskiwania

Możesz użyć jednego skryptu w wielu planów odzyskiwania za pomocą zmiennych zewnętrznych. Można użyć [zmienne automatyzacji Azure](../automation/automation-variables.md) toostore parametrów, które można przekazać do odzyskiwania planu wykonania. Dodając Nazwa planu odzyskiwania hello jako zmienną toohello prefiksu, można utworzyć pojedyncze zmienne dla każdego planu odzyskiwania. Następnie należy użyć zmiennych hello jako parametry. Bez zmieniania hello skryptu można zmienić parametru, ale nadal hello zmiany hello sposób działania skryptu.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Użyj zmiennej prostego ciągu w skrypcie elementu runbook

W tym przykładzie skrypt ma hello danych wejściowych z grupy zabezpieczeń sieci (NSG) i stosuje je toohello maszyny wirtualne w planie odzyskiwania.

Toodetect hello skryptu, jakiego planu odzyskiwania jest uruchomiona można użyć w kontekście planu odzyskiwania hello:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply istniejącej grupy NSG, musisz znać nazwę grupy NSG hello oraz nazwę grupy zasobów NSG hello. Użyj tych zmiennych jako dane wejściowe dla skryptów planu odzyskiwania. toodo, Utwórz dwie zmienne w hello zasoby konta automatyzacji. Dodaj nazwę hello hello planu odzyskiwania, który tworzysz hello parametrów jako prefiksu nazwy zmiennej toohello.

1. Utwórz nazwę zmiennej toostore hello NSG. Dodaj prefiks nazwy zmiennej toohello przy użyciu nazwy hello hello planu odzyskiwania.

    ![Utwórz zmienną Nazwa grupy NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Utwórz nazwę grupy zasobów NSG hello toostore zmiennej. Dodaj prefiks nazwy zmiennej toohello przy użyciu nazwy hello hello planu odzyskiwania.

    ![Tworzenie grupy NSG Nazwa grupy zasobów](media/site-recovery-runbook-automation-new/var2.png)


3.  W skrypcie hello Użyj hello następujące wartości zmiennych hello tooget kodu odwołania:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Użyj hello zmiennych w hello runbook tooapply hello NSG toohello interfejs sieciowy hello przełączona w tryb failover maszyny Wirtualnej:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Dla każdego planu odzyskiwania należy utworzyć zmienne niezależne, dzięki czemu można ponownie użyć skryptu hello. Dodaj prefiks przy użyciu nazwy planu odzyskiwania hello. Pełne, end-to-end skryptu dla tego scenariusza, zobacz [dodać publicznych adresów IP i NSG tooVMs podczas testowania trybu failover planu odzyskiwania usługi Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Użyj toostore zmiennej złożone więcej informacji

Rozważmy scenariusz, w którym ma zostać tooturn jednego skryptu, na publiczny adres IP na określonych maszynach wirtualnych. W innym scenariuszu może być tooapply różne grupy NSG na różnych maszynach wirtualnych (a nie na wszystkich maszynach wirtualnych). Możesz wprowadzić skrypt, który jest wielokrotnego użytku dla każdego planu odzyskiwania. Każdy plan odzyskiwania może mieć zmiennej liczbę maszyn wirtualnych. Na przykład odzyskiwania SharePoint, ma dwa końce frontonu. Aplikacja podstawowe — biznesowych (LOB) ma tylko jeden frontonu. Nie można utworzyć oddzielne zmienne dla każdego planu odzyskiwania. 

W hello poniższy przykład, firma Microsoft używa nowe techniki i utworzyć [zmiennej złożone](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) w zasobów konta usługi Automatyzacja Azure hello. W tym celu określania wielu wartości. Należy użyć programu Azure PowerShell toocomplete hello następujące kroki:

1. W programie PowerShell Zaloguj tooyour subskrypcji platformy Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. Parametry hello toostore, Utwórz zmienną złożone hello przy użyciu nazwy hello hello planu odzyskiwania:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. W tej zmiennej złożone **VMDetails** hello chronione maszyny Wirtualnej jest hello identyfikator maszyny Wirtualnej. tooget hello identyfikator maszyny Wirtualnej w hello portalu Azure, Wyświetl hello właściwości maszyny Wirtualnej. Witaj Poniższy zrzut ekranu przedstawia zmiennej, która przechowuje informacje szczegółowe hello dwóch maszyn wirtualnych:

    ![Użyj hello identyfikator maszyny Wirtualnej jako hello identyfikator GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Użyj tej zmiennej w elemencie runbook. Jeśli hello wskazał identyfikator GUID maszyny Wirtualnej znajduje się w kontekście planu odzyskiwania hello, zastosuj hello NSG na powitania maszyny Wirtualnej:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. W elemencie runbook pętli maszyn wirtualnych hello kontekstu planu odzyskiwania hello. Sprawdź, czy hello maszyna wirtualna istnieje w **$VMDetailsObj**. Jeśli istnieje, uzyskać dostęp do właściwości hello hello zmiennej tooapply hello NSG:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Hello sam skryptu służącego do planów odzyskiwania inny. Wprowadź różne parametry przechowując hello wartość, która odpowiada tooa planu odzyskiwania w różnych zmiennych.

## <a name="sample-scripts"></a>Przykładowe skrypty

toodeploy przykładowe skrypty tooyour konta automatyzacji, kliknij przycisk hello **wdrażanie tooAzure** przycisku.

[![Wdrażanie tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Innym przykładem Zobacz powitania po wideo. Jednak przedstawia sposób toorecover tooAzure aplikacji WordPress dwuwarstwowa:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Dodatkowe zasoby
* [Azure automatyzacji usługi konta Uruchom jako](../automation/automation-sec-configure-azure-runas-account.md)
* [Omówienie usługi Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "Omówienie usługi Automatyzacja Azure")
* [Azure Automation przykładowe skrypty](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "usługi Automatyzacja Azure przykładowe skrypty")
