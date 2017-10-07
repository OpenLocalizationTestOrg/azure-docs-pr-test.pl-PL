---
title: "aaaAdd Azure automatyzacji elementów runbook toorecovery planów w portalu klasycznym hello | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak usługi Azure Site Recovery obecnie umożliwia tooextend planów odzyskiwania podczas odzyskiwania tooAzure przy użyciu złożone zadania toocomplete usługi Automatyzacja Azure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Dodaj w portalu klasycznym hello planów toorecovery elementów runbook usługi Automatyzacja Azure
W tym samouczku opisano, jak usługi Azure Site Recovery integruje się z planami toorecovery rozszerzalności tooprovide automatyzacji Azure. Plany odzyskiwania można organizować odzyskiwania maszyn wirtualnych chronionych za pomocą usługi Azure Site Recovery dla chmury toosecondary replikacji i scenariusze tooAzure replikacji. Ułatwiają również w podejmowaniu odzyskiwania hello **spójnie dokładne**, **powtarzalne**, i **automatyczne**. Jeśli Twoje tooAzure maszyny wirtualne są awaryjne, integracja z usługi Automatyzacja Azure rozszerza planów odzyskiwania i daje możliwość tooexecute elementów runbook, dzięki czemu zaawansowanych automatyzacji zadań.

Jeśli ma nie wiesz o usługi Automatyzacja Azure jeszcze, zarejestruj się [tutaj](https://azure.microsoft.com/services/automation/) i pobierania ich przykładowe skrypty [tutaj](https://azure.microsoft.com/documentation/scripts/). Przeczytaj więcej na temat [usługi Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) i jak plany tooorchestrate tooAzure odzyskiwania przy użyciu funkcji odzyskiwania [tutaj](https://azure.microsoft.com/blog/?p=166264).

W tym samouczku krótkich przedstawiono sposób integrowania elementu runbook usługi Automatyzacja Azure do planów odzyskiwania. Firma Microsoft będzie zautomatyzować prostych zadań, które wcześniej wymagana ręczna interwencja i zobacz, jak tooconvert multi krok odzyskiwania do akcji odzyskiwania jednym kliknięciem. Firma Microsoft będzie też przyjrzeć poznać sposoby rozwiązywania prostego skryptu, jeśli jego nieprawidłowość.

## <a name="protect-hello-application-tooazure"></a>Ochrona powitalnych tooAzure aplikacji
Daj nam rozpoczynać się od prostej aplikacji składający się z dwóch maszyn wirtualnych. W tym miejscu zostały HRweb stosowania firmy Fabrikam. Firma Fabrikam-HRweb frontonu i zaplecza Hrweb-firma Fabrikam to Witaj dwie maszyny wirtualne chronione przy użyciu usługi Azure Site Recovery tooAzure. maszyn wirtualnych hello tooprotect za pomocą usługi Azure Site Recovery, wykonaj poniższe kroki hello.

1. Włącz ochronę maszyn wirtualnych.
2. Upewnij się, że hello maszyn wirtualnych zakończyły replikację początkową i jest replikowana.
3. Zaczekaj do ukończenia replikacji początkowej hello i chronione mówi hello stan replikacji.

## ![](media/site-recovery-runbook-automation/01.png)
W tym samouczku utworzymy plan odzyskiwania na powitania tooAzure hello toofailover Fabrikam HRweb aplikacji w aplikacji. Następnie firma Microsoft będzie zintegrować ją z elementu runbook, który spowoduje utworzenie punktu końcowego na powitania przejścia w tryb failover maszyny wirtualnej platformy Azure stron sieci web tooserve na porcie 80.

Najpierw utwórz plan odzyskiwania do naszej aplikacji.

## <a name="create-hello-recovery-plan"></a>Tworzenie planu odzyskiwania hello
tooAzure aplikacji hello toorecover, należy toocreate planu odzyskiwania.
Przy użyciu planu odzyskiwania, które można określić kolejność hello odzyskiwania maszyn wirtualnych. Maszyna wirtualna Hello umieszczona w grupie 1 będzie odzyskanie i uruchomić się jako pierwszy i postępuj hello maszyny wirtualnej z grupy 2.

Tworzenie planu odzyskiwania, który wygląda jak poniżej.

![](media/site-recovery-runbook-automation/12.png)

więcej informacji na temat planów odzyskiwania, przeczytaj dokumentację tooread [tutaj](https://msdn.microsoft.com/library/azure/dn788799.aspx "tutaj").

Następnie utwórz hello artefakty niezbędne w automatyzacji Azure.

## <a name="create-hello-automation-account-and-its-assets"></a>Tworzenie konta automatyzacji hello i jej zasobów
Należy runbook toocreate konto usługi Automatyzacja Azure. Jeśli nie masz już konto, przejdź wskazywane przez kartę automatyzacji tooAzure ![](media/site-recovery-runbook-automation/02.png)i Utwórz nowe konto.

1. Nadaj kontu hello tooidentify nazwy z.
2. Określ region geograficzny, w którym ma tooplace hello konta.

Zalecane jest tooplace hello konta w hello tym samym regionie co magazyn hello funkcja automatycznego odzyskiwania systemu.

![](media/site-recovery-runbook-automation/03.png)

Następnie należy utworzyć hello następujące zasoby w hello konta.

### <a name="add-a-subscription-name-as-asset"></a>Dodaj nazwę subskrypcji jako zasobów
1. Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w hello zasobów usługi Automatyzacja Azure i wybierz zbyt![](media/site-recovery-runbook-automation/05.png)
2. Wybierz typ zmiennej hello jako **ciągu**
3. Określ nazwę zmiennej jako **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Określ nazwę rzeczywiste subskrypcji platformy Azure jako hello wartość zmiennej.

   ![](media/site-recovery-runbook-automation/07_1.png)

Można ustalić nazwy hello subskrypcji ze strony ustawień hello Twojego konta na powitania portalu Azure.

### <a name="add-an-azure-login-credential-as-asset"></a>Dodaj poświadczeń logowania do systemu Azure jako zasobów
Automatyzacja Azure korzysta z programu Azure PowerShell tooconnect toothe subskrypcji i działa na powitania artefakty istnieje. W tym celu należy przeprowadzić uwierzytelniania za pomocą konta Microsoft lub konta służbowego.
Poświadczenia konta hello można przechowywać w toobe zasobów bezpiecznie używany przez element runbook hello.

1. Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w hello zasobów usługi Automatyzacja Azure i wybierz pozycję![](media/site-recovery-runbook-automation/09.png)
2. Wybierz typ poświadczenia hello jako **poświadczenie programu PowerShell systemu Windows**
3. Określ nazwę hello jako **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Określ hello nazwy użytkownika i hasła toosign za pomocą.

Teraz oba te ustawienia są dostępne w zasobów.

![](media/site-recovery-runbook-automation/11.png)

Więcej informacji na temat sposobu tooconnect tooyour subskrypcji za pomocą programu PowerShell znajduje [tutaj](/powershell/azure/overview).

Następnie spowoduje utworzenie elementu runbook w automatyzacji Azure, które można dodać punktu końcowego dla maszyny wirtualnej frontonu powitania po pracy awaryjnej.

## <a name="azure-automation-context"></a>Kontekst usługi Automatyzacja Azure
Funkcja automatycznego odzyskiwania systemu przekazuje kontekst zmiennej toohello runbook toohelp pisania skryptów deterministyczna. Jeden można argumentowało nazwy hello hello usługi w chmurze i hello maszyny wirtualnej są przewidywalne, ale się stanie, że nie jest on zawsze hello przypadku z powodu toocertain scenariuszy, takich jak hello co gdzie hello nazwy hello maszyny wirtualnej mogła ulec zmianie ukończenia znaki toounsupported na platformie Azure. Dlatego te informacje są przesyłane planu odzyskiwania toohello ASR jako część hello *kontekstu*.

Poniżej przedstawiono przykładowy wygląd hello zmiennej kontekstu.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


w poniższej tabeli Hello zawiera nazwę i opis dla każdej zmiennej w kontekście hello.

| **Nazwa zmiennej** | **Opis** |
| --- | --- |
| RecoveryPlanName |Nazwa planu uruchomione. Ułatwia wykonanie akcji ze względu na użycie nazwy hello sam skrypt |
| FailoverType |Określa, czy tryb failover hello jest przetestować, planowane lub nieplanowane. |
| Element FailoverDirection |Określ, czy odzyskiwania jest tooprimary lub pomocniczej |
| Identyfikator grupy |Zidentyfikować numer grupy hello w ramach planu odzyskiwania hello planu hello jest uruchomiona. |
| VmMap |Tablica wszystkich maszyn wirtualnych hello hello grupy |
| Klucz VMMap |Klucz unikatowy (identyfikator GUID) dla każdej maszyny Wirtualnej. Ma hello taka sama, jak hello programu VMM o identyfikatorze hello maszyny wirtualnej, jeśli to możliwe. |
| RoleName |Nazwa maszyny Wirtualnej platformy Azure, która jest przywracana hello |
| CloudServiceName |Nazwa usługi w chmurze platformy Azure pod które hello utworzeniu maszyny wirtualnej. |

Witaj tooidentify VmMap klucza w kontekście hello można również przejść toohello strony właściwości maszyny Wirtualnej w usłudze ASR i przyjrzyj się hello właściwości GUID maszyny Wirtualnej.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Tworzenie elementu runbook automatyzacji
Na maszynie wirtualnej frontonu hello tworzyć hello runbook tooopen portu 80.

1. Utwórz nowy element runbook w hello konto usługi Automatyzacja Azure o nazwie hello **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Przejdź toohello widoku autora elementu hello runbook, a następnie wprowadź hello trybie wersji roboczej.
3. Najpierw określ hello toouse zmiennej jako kontekstu planu odzyskiwania hello

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Następnym połączeniu toohello subskrypcji przy użyciu nazwy hello poświadczeń i subskrypcji

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Należy pamiętać, że używasz hello Azure zasoby — **AzureCredential** i **AzureSubscriptionName** tutaj.
5. Teraz Określ szczegóły punktu końcowego hello i hello GUID hello maszyny wirtualnej, dla której ma zostać tooexpose hello endpoint. W przypadku hello frontonu maszyny wirtualnej.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   To ustawienie określa hello protokół punktu końcowego platformy Azure, port lokalny na powitania maszyny Wirtualnej i jej zamapowanych publicznego. Te zmienne są parametry wymagane przez hello Azure poleceń, które dodać tooVMs punktów końcowych. Witaj VMGUID przechowuje hello hello maszyny wirtualnej, którą należy toooperate na identyfikator GUID.
6. skrypt Hello teraz wyodrębnić hello kontekst hello podany identyfikator GUID maszyny Wirtualnej i utworzyć punktu końcowego na maszynie wirtualnej hello odwołuje się on.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Po zakończeniu tej operacji, kliknij przycisk Publikuj ![](media/site-recovery-runbook-automation/20.png) tooallow Twojego skryptu toobe dostępna do wykonania.

Ukończ skrypt Hello jest podany poniżej użytkownikowi

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Dodaj planu odzyskiwania toohello skryptu hello
Gdy skrypt hello jest gotowy, można dodać toohello planu odzyskiwania, który został utworzony wcześniej.

1. W planie odzyskiwania hello utworzone wybierz tooadd skrypt po grupie 2. ![](media/site-recovery-runbook-automation/15.png)
2. Określ nazwę skryptu. Jest to po prostu przyjazną nazwę dla tego skryptu do projekcji w ramach planu odzyskiwania hello.
3. W skrypcie tooAzure pracy awaryjnej hello — wybierz nazwę konta usługi Automatyzacja Azure hello.
4. W hello Azure elementów Runbook wybierz element runbook hello, Twojego autorstwa.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Skrypty po stronie podstawowej
Podczas wykonywania tooAzure trybu failover, można tooexecute skrypty po stronie głównej. Skrypty te zostanie uruchomiony na serwerze VMM hello podczas pracy awaryjnej.
Skrypty po stronie podstawowej są dostępne tylko w przypadku zamknięcia wstępne tylko i post etapy zamknięcia. Jest to spowodowane oczekujemy toobe lokacji głównej hello zwykle niedostępne momencie uderzenia awarii.
Podczas nieplanowany tryb failover tylko w przypadku uczestnictwa w operacjach lokacji głównej, będzie podejmować toorun hello głównej stronie skryptów. Jeśli nie są dostępne lub limit czasu pracy awaryjnej hello będą nadal toorecover hello maszyn wirtualnych.
Skrypty po stronie głównej cofanie dostępnych dla lokacji VMware/fizyczna/funkcji Hyper-v bez tooAzure VMM chronione - podczas tooAzure trybu failover.
Jednak po awarii z platformy Azure tooon lokalnie skrypty po stronie głównej (elementów Runbook) może służyć do wszystkich miejsc docelowych oprócz VMware.

## <a name="test-hello-recovery-plan"></a>Plan odzyskiwania hello testu
Po dodaniu hello runbook toohello planu można zainicjować test trybu failover i zobaczyć ją w akcji. Zawsze zalecane toorun tootest pracy awaryjnej testu Twojej aplikacji i hello odzyskiwania planu tooensure czy nie ma żadnych błędów.

1. Wybierz plan odzyskiwania hello i zainicjuj test trybu failover.
2. Podczas wykonywania planu hello możesz wyświetlić czy hello runbook jest wykonywana za pomocą jego stan.

   ![](media/site-recovery-runbook-automation/17.png)
3. Możesz również sprawdzić hello szczegółowy stan wykonywania elementu runbook na stronie zadań usługi Automatyzacja Azure hello hello elementu runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. Po zakończeniu pracy awaryjnej hello, oprócz hello wyniku wykonania elementu runbook, widoczny czy wykonanie hello zakończy się pomyślnie lub nie odwiedzać strony maszyny wirtualnej platformy Azure hello i patrzeć hello punktów końcowych.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Przykładowe skrypty
Podczas Rezygnacja za pomocą automatyzacji jedną powszechnie używane zadania dodawania tooan punktu końcowego maszyny wirtualnej platformy Azure w tym samouczku, może wykonać szereg inne zadania automatyzacji zaawansowanych przy użyciu automatyzacji Azure. Firma Microsoft i hello społeczności usługi Automatyzacja Azure znajdują się przykładowe elementy runbook, które mogą pomóc rozpocząć tworzenie własnych rozwiązań i narzędzie elementów runbook, którego można użyć jako bloków konstrukcyjnych dla większych automatyzacji zadań. Rozpocznij korzystanie z nich z galerii hello i tworzenie planów odzyskiwania jednym kliknięciem zaawansowanych aplikacji przy użyciu usługi Azure Site Recovery.

## <a name="additional-resources"></a>Dodatkowe zasoby
[Przegląd automatyzacji Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Omówienie usługi Automatyzacja Azure")

[Przykładowe skrypty usługi Automatyzacja Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "przykładowe skrypty usługi Automatyzacja Azure")
