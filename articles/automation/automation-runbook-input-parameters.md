---
title: "Parametry wejściowe aaaRunbook | Dokumentacja firmy Microsoft"
description: "Parametry wejściowe elementu Runbook zwiększyć elastyczność hello elementów runbook, zezwalając toopass danych tooa runbook po jego uruchomieniu. W tym artykule opisano różne scenariusze, w których są używane parametry wejściowe w elementach runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Parametry wejściowe elementu Runbook
Parametry wejściowe elementu Runbook zwiększyć elastyczność hello elementów runbook, zezwalając toopass tooit danych podczas jej uruchamiania. Parametry Hello mogą zostać toobe działania elementu runbook hello przeznaczone dla określonych scenariuszach i środowiskach. W tym artykule firma Microsoft pomoże różnych scenariuszy gdzie parametry wejściowe są używane w elementach runbook.

## <a name="configure-input-parameters"></a>Skonfiguruj parametry wejściowe
Parametry wejściowe można skonfigurować w programie PowerShell, przepływu pracy programu PowerShell i graficznych elementów runbook. Element runbook może mieć wiele parametrów o różnych typach danych lub Brak parametrów w ogóle. Parametry wejściowe mogą być wymagane lub opcjonalne i można przypisać wartości domyślnej dla parametrów opcjonalnych. Można przypisać wartości na toohello parametry wejściowe elementu runbook podczas uruchamiania za pomocą jednego z dostępnych metod hello. Te metody obejmują uruchamianie elementu runbook z portalu hello lub usługi sieci web. Można również uruchomić jako podrzędnego elementu runbook, wywoływaną wbudowanego innego elementu runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Skonfiguruj parametry wejściowe w elementach runbook programu PowerShell i przepływ pracy programu PowerShell
Środowiska PowerShell i [elementach runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md) automatyzacji Azure obsługuje parametry wejściowe zdefiniowane za pomocą hello następujące atrybuty.  

| **Właściwość** | **Opis** |
|:--- |:--- |
| Typ |Wymagany. Oczekiwano wartości parametru hello typu danych Hello. Dowolny typ .NET jest prawidłowy. |
| Nazwa |Wymagany. Nazwa Hello hello parametru. To musi być unikatowe w obrębie hello elementu runbook i może zawierać tylko litery, cyfry lub znaki podkreślenia. Musi ona rozpoczynać się od litery. |
| Obowiązkowy |Opcjonalny. Określa, czy należy podać wartość parametru hello. Jeśli ustawisz to zbyt**$true**, a następnie po uruchomieniu elementu runbook hello, należy podać wartość. Jeśli ustawisz to zbyt**$false**, a następnie wartość jest opcjonalna. |
| Wartość domyślna |Opcjonalny.  Określa wartość, która będzie służyć hello parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook hello. Wartość domyślna można ustawić dla każdego parametru i automatycznie wprowadzi hello parametr opcjonalny niezależnie od hello obowiązkowego ustawienia. |

Program Windows PowerShell obsługuje więcej atrybutów parametrów wejściowych niż wymienione w tym miejscu, takich jak sprawdzanie poprawności, aliasy i zestawy parametrów. Automatyzacja Azure obsługuje obecnie tylko hello parametrów wejściowych wymienionych powyżej.

Definicję parametrów w elementach runbook przepływu pracy programu PowerShell ma hello następujące ogólne formularza, gdzie wiele parametrów są oddzielone przecinkami.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Podczas definiowania parametrów, jeśli nie określisz hello **obowiązkowe** atrybutu, a następnie domyślnie parametr hello są traktowane jako opcjonalne. Ponadto jeśli ustawisz wartość domyślną dla parametru w elementach runbook przepływu pracy programu PowerShell, będzie traktowane przez programu PowerShell jako opcjonalny parametr, niezależnie od hello **obowiązkowe** wartość atrybutu.
> 
> 

Na przykład Skonfigurujmy hello parametry wejściowe elementu runbook przepływu pracy programu PowerShell, która wyświetla szczegółowe informacje o maszynach wirtualnych, jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów. Ten element runbook zawiera dwa parametry, jak pokazano w powitania po zrzut ekranu: hello nazwy maszyny wirtualnej oraz nazwy hello hello grupy zasobów.

![Automatyzacja przepływu pracy programu PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

W tej definicji parametru hello parametry **$VMName** i **$resourceGroupName** proste parametrów typu ciąg. Jednak elementów runbook programu PowerShell i przepływ pracy programu PowerShell obsługuje wszystkie typy proste i typów złożonych, takie jak **obiektu** lub **PSCredential** dla parametrów wejściowych.

Jeśli element runbook ma parametru wejściowego typu obiektu, skorzystaj z tablicy skrótów programu PowerShell z (nazwa, wartość) pary toopass wartości. Na przykład, jeśli masz hello następującego parametru w elemencie runbook:

     [Parameter (Mandatory = $true)]
     [object] $FullName

Następnie można przekazać następującego parametru toohello wartości hello:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Skonfiguruj parametry wejściowe w graficznych elementów runbook
zbyt[skonfigurować graficznym elementem runbook](automation-first-runbook-graphical.md) z parametrami wejściowymi, Utwórzmy graficzny element runbook, która wyświetla szczegółowe informacje o maszynach wirtualnych, albo jednej maszyny Wirtualnej lub wszystkich maszyn wirtualnych w grupie zasobów. Konfigurowanie elementu runbook składa się z dwóch głównych działań, zgodnie z poniższym opisem.

[**Uwierzytelniania elementów Runbook za pomocą konta Uruchom jako platformy Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate z platformy Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello właściwości maszyn wirtualnych.

Można użyć hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nazwy hello toooutput działań maszyn wirtualnych. Witaj działania **Get-AzureRmVm** akceptuje dwa parametry hello **nazwę maszyny wirtualnej** i hello **Nazwa grupy zasobów**. Ponieważ te parametry może wymagać różnych wartości w każdym uruchomieniu elementu runbook hello, można dodać elementu runbook tooyour parametrów wejściowych. Poniżej przedstawiono parametry wejściowe tooadd hello kroki:

1. Wybierz hello graficzny element runbook z hello **Runbook** bloku, a następnie kliknij przycisk [ **Edytuj** ](automation-graphical-authoring-intro.md) go.
2. W edytorze elementów runbook hello, kliknij polecenie **dane wejściowe i wyjściowe** tooopen hello **dane wejściowe i wyjściowe** bloku.
   
    ![Graficzny element runbook automatyzacji](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Witaj **dane wejściowe i wyjściowe** bloku zostanie wyświetlona lista parametry wejściowe zdefiniowane dla hello elementu runbook. W tym bloku możesz dodać nowego parametru wejściowego lub Edytuj konfigurację hello istniejących parametru wejściowego. tooadd nowy parametr hello elementu runbook, kliknij przycisk **dodać dane wejściowe** tooopen hello **parametr wejściowy elementu Runbook** bloku. Istnieje można skonfigurować hello następujące parametry:
   
   | **Właściwość** | **Opis** |
   |:--- |:--- |
   | Nazwa |Wymagany.  Nazwa Hello hello parametru. To musi być unikatowe w obrębie hello elementu runbook i może zawierać tylko litery, cyfry lub znaki podkreślenia. Musi ona rozpoczynać się od litery. |
   | Opis |Opcjonalny. Opis przeznaczenia hello parametru wejściowego. |
   | Typ |Opcjonalny. Typ danych Hello są oczekiwane w przypadku hello wartość parametru. Typy parametrów obsługiwanych są **ciąg**, **Int32**, **Int64**, **dziesiętną**, **logiczna**, **DateTime**, i **obiektu**. Jeśli typem danych nie jest zaznaczone, domyślnie zbyt**ciąg**. |
   | Obowiązkowy |Opcjonalny. Określa, czy należy podać wartość parametru hello. Jeśli wybierzesz **tak**, a następnie po uruchomieniu elementu runbook hello, należy podać wartość. Jeśli wybierzesz **nie**, a następnie wartość nie jest wymagana, gdy element runbook hello jest uruchomiony i może zostać ustawiona wartość domyślna. |
   | Wartość domyślna |Opcjonalny. Określa wartość, która będzie służyć hello parametru, jeśli wartość nie zostanie przekazany, po uruchomieniu elementu runbook hello. Można ustawić wartości domyślnej dla parametru, który nie jest obowiązkowe. Wybierz wartość domyślną tooset **niestandardowy**. Ta wartość jest używana, chyba że inna wartość zostanie podana przy uruchamianiu elementu runbook hello. Wybierz **Brak** Jeśli nie chcesz tooprovide dowolną wartość domyślna. |
   
    ![Dodaj nowe dane wejściowe](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Utwórz dwa parametry o następujących właściwościach, które będą używane przez hello hello **Get AzureRmVm** działania:
   
   * **Parametr1:**
     
     * Nazwa - VMName
     * Typ — ciąg
     * Obowiązkowy - nr
   * **Parameter2:**
     
     * Nazwa - resourceGroupName
     * Typ — ciąg
     * Obowiązkowy - nr
     * Wartość domyślna — niestandardowy
     * Wartość domyślna niestandardowe — \<nazwę grupy zasobów hello, która zawiera maszyny wirtualne hello >
5. Po dodaniu parametry powitania kliknij **OK**.  Możesz teraz przeglądać w hello **danych wejściowych i wyjściowych bloku**. Kliknij przycisk **OK** ponownie, a następnie kliknij przycisk **zapisać** i **publikowania** elementu runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Przypisz wartości tooinput parametrów w elementach runbook
Można jednak przekazać wartości tooinput parametrów w elementach runbook w hello następujące scenariusze.

### <a name="start-a-runbook-and-assign-parameters"></a>Uruchom element runbook i przypisz parametrów
Element runbook może zostać uruchomiona na wiele sposobów: przez hello portalu Azure, z elementu webhook, polecenia cmdlet programu PowerShell, interfejsu API REST hello lub hello zestawu SDK. Poniżej omówiono różne metody uruchamiania elementu runbook i przypisywanie parametrów.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Uruchom opublikowanego elementu runbook za pomocą portalu Azure hello i parametry
Gdy zostanie [uruchomić elementu runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Uruchom element Runbook** zostanie otwarty blok i można skonfigurować wartości parametrów hello, które zostały utworzone.

![Rozpoczynanie korzystania z portalu hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Etykieta hello poniżej pola wejściowego hello zawiera atrybuty hello, które zostały ustawione dla parametru hello. Atrybuty obejmują obowiązkowe i opcjonalne, typ i wartość domyślną. Witaj pomocy dymek dalej toohello nazwę parametru zawiera wszystkie informacje klucza hello potrzebne toomake decyzji o wartości wejściowe parametru. Informacje te obejmują, czy parametr jest obowiązkowy lub opcjonalne. Zawiera także hello typ i wartość domyślną (jeśli istnieje) i inne przydatne informacje.

![Dymek pomocy](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Obsługa parametrów typu String **pusty** wartości ciągu.  Wprowadzanie **[ciąg EmptyString]** w parametru wejściowego hello pole zostanie przekazany parametr toohello pusty ciąg. Ponadto nie obsługują parametrów typu ciąg **Null** wartości były przekazywane. Jeśli nie zostanie przekazany żadnego parametru ciągu toohello wartość, następnie programu PowerShell zostanie zinterpretować go jako wartości null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Uruchom opublikowanego elementu runbook za pomocą poleceń cmdlet programu PowerShell i parametry
* **Polecenia cmdlet Menedżera zasobów systemu Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w grupie zasobów za pomocą [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Przykład:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Polecenia cmdlet do zarządzania usługi Azure:** można uruchomić element runbook usługi Automatyzacja, który został utworzony w domyślnej grupie zasobów za pomocą [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Przykład:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Po uruchomieniu elementu runbook za pomocą poleceń cmdlet programu PowerShell, domyślnego parametru, **MicrosoftApplicationManagementStartedBy** jest tworzony z wartością hello **PowerShell**. Ten parametr można wyświetlić w hello **szczegóły zadania** bloku.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Uruchom element runbook przy użyciu zestawu SDK i przypisz parametrów
* **Metoda Menedżera zasobów Azure:** można uruchomić elementu runbook za pomocą hello zestawu SDK języka programowania. Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji. Możesz wyświetlić cały kod hello w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Metoda zarządzania usługami platformy Azure:** można uruchomić elementu runbook za pomocą hello zestawu SDK języka programowania. Poniżej przedstawiono fragment kodu C# dla uruchamianie elementu runbook na Twoim koncie automatyzacji. Możesz wyświetlić cały kod hello w naszym [repozytorium GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart tej metody Utwórz hello toostore słownik parametrów elementu runbook **VMName** i **resourceGroupName**i ich wartości. Następnie uruchom hello elementu runbook. Poniżej znajduje się fragment hello C# kodu dla wywołania metody hello, który jest zdefiniowany powyżej.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Uruchom element runbook za pomocą hello interfejsu API REST i przypisz parametrów
Zadanie elementu runbook można tworzyć i pracy z hello interfejsu API REST usługi Automatyzacja Azure przy użyciu hello **PUT** metody za pomocą następującego hello żądanie identyfikatora URI.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

W identyfikatorze URI żądania hello Zastąp hello następujące parametry:

* **Identyfikator subskrypcji:** Twojego identyfikatora subskrypcji platformy Azure.  
* **Nazwa usługi chmury:** nazwa hello hello chmury usługi toowhich hello żądania, które mają być wysyłane.  
* **Automatyzacja account-name:** hello nazwa konta automatyzacji, który znajduje się w obrębie hello określona usługa w chmurze.  
* **Identyfikator zadania:** hello identyfikatora GUID dla hello zadania. Identyfikatory GUID w programie PowerShell można utworzyć przy użyciu hello **[GUID]::NewGuid(). ToString()** polecenia.

W kolejności toopass parametry toohello runbook zadania należy użyć hello treści żądania. Trwa hello następujące dwie właściwości podany w formacie JSON:

* **Nazwa elementu Runbook:** wymagane. Hello nazwa elementu hello runbook hello toostart zadania.  
* **Parametry elementu Runbook:** opcjonalne. Słownik hello listy parametrów w (nazwa, wartość) formatu, gdzie nazwa powinna być typu String, a wartość może być dowolną prawidłową wartość JSON.

Jeśli chcesz, aby toostart hello **Get-AzureVMTextual** elementu runbook, który został utworzony wcześniej **VMName** i **resourceGroupName** jako parametry, użyj następującego formatu JSON hello Witaj treści żądania.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Jeśli pomyślnie utworzono zadanie hello, zwracany jest kod stanu HTTP 201. Więcej informacji o nagłówki odpowiedzi i treść odpowiedzi hello, można znaleźć w artykule toohello temat zbyt[utworzyć zadanie elementu runbook za pomocą hello interfejsu API REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Testowanie elementu runbook i przypisz parametrów
Gdy możesz [testu hello wersję roboczą elementu runbook](automation-testing-runbook.md) przy użyciu opcji testu hello, hello **Test** zostanie otwarty blok i można skonfigurować wartości parametrów hello, które zostały utworzone.

![Testowanie i parametry](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Łączenie elementu runbook tooa harmonogram i parametry
Możesz [Połącz harmonogram](automation-schedules.md) runbook tooyour tak hello elementu runbook rozpoczyna się w określonym czasie. Po utworzeniu harmonogramu hello i hello runbook użyje tych wartości, gdy jest ona uruchamiana zgodnie z harmonogramem hello przypisaniu parametrów wejściowych. Nie można zapisać harmonogramu hello, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.

![Planowanie i przydzielanie parametrów](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Tworzenie elementu webhook dla elementu runbook i parametry
Można utworzyć [webhook](automation-webhooks.md) dla elementu runbook i skonfiguruj parametry wejściowe elementu runbook. Nie można zapisać elementu webhook hello, zanim nie zostaną dostarczone wszystkie wartości parametrów obowiązkowych.

![Utwórz element webhook i przypisz parametrów](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Podczas wykonywania elementu runbook przy użyciu elementu webhook, hello wstępnie zdefiniowanych parametrów wejściowych  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  jest wysyłany razem z hello parametry wejściowe zdefiniowane. Możesz kliknąć tooexpand hello **WebhookData** parametr, aby uzyskać więcej informacji.

![Parametr WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na runbook przychodzących i wychodzących, zobacz [usługi Automatyzacja Azure: element runbook danych wejściowych, wyjściowych i zagnieżdżonych elementów rrunbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).
* Aby uzyskać więcej informacji o różnych sposobów toostart elementu runbook, zobacz [uruchamianie elementu runbook](automation-starting-a-runbook.md).
* tooedit tekstowa elementu runbook, można znaleźć zbyt[edytowania elementów runbook tekstową](automation-edit-textual-runbook.md).
* tooedit graficznym elementem runbook można znaleźć zbyt[tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).

