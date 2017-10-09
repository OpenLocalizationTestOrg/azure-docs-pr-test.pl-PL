---
title: "Moduł integracji usługi Automatyzacja Azure aaaCreate | Dokumentacja firmy Microsoft"
description: "Samouczek który przeprowadzi Cię przez użycie tworzenie, testowanie i przykład hello moduły integracji automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Moduły integracji usługi Azure Automation
PowerShell jest podstawową technologią hello za automatyzacji Azure. Ponieważ usługi Automatyzacja Azure jest oparty na programie PowerShell, moduły programu PowerShell są rozszerzalności klucza toohello automatyzacji Azure. W tym artykule firma Microsoft przeprowadzi Cię charakterystykę hello stosowania automatyzacji Azure moduły programu PowerShell, określonego tooas "Moduły integracji" i najlepszych praktyk do tworzenia własnych modułów programu PowerShell toomake się, że działają jako moduły integracji w Automatyzacja Azure. 

## <a name="what-is-a-powershell-module"></a>Co to jest moduł programu PowerShell?
Moduł programu PowerShell to grupa poleceń cmdlet programu PowerShell, takie jak **Get-Date** lub **Copy-Item**, które mogą być używane z konsoli programu PowerShell hello, skrypty, przepływy pracy, elementy runbook i zasoby DSC środowiska PowerShell, takich jak WindowsFeature lub plik, który może służyć z konfiguracji DSC środowiska PowerShell. Wszystkie funkcje hello programu PowerShell jest uwidaczniany za pomocą poleceń cmdlet i zasoby DSC i każdego polecenia cmdlet/DSC zasobu nie jest obsługiwana przez moduł programu PowerShell, duża liczba którego dostarczanych z programem PowerShell sam. Na przykład Witaj **Get-Date** polecenia cmdlet jest częścią hello modułu programu Microsoft.PowerShell.Utility PowerShell i **Copy-Item** polecenia cmdlet jest częścią hello modułu Microsoft.PowerShell.Management PowerShell i Witaj DSC pakietu zasobów jest częścią hello modułu PSDesiredStateConfiguration PowerShell. Oba te moduły są dostarczane z programem PowerShell. Jednak wiele modułów programu PowerShell nie są dostarczane jako część programu PowerShell i zamiast tego są dystrybuowane z produktami pierwszy lub innych firm, takich jak System Center 2012 Configuration Manager lub przez społeczność przeważająca PowerShell hello na miejsc, jak galerii programu PowerShell.  Moduły Hello są przydatne, ponieważ ich wykonywanie złożonych zadań za pomocą funkcji hermetyzowany prostsze.  Aby uzyskać więcej informacji, zobacz artykuł o [modułach programu PowerShell w witrynie MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>Co to jest moduł integracji usługi Azure Automation?
Moduł integracji nie różni się znacząco od modułu programu PowerShell. Jego po prostu moduł programu PowerShell, który opcjonalnie zawiera jeden plik dodatkowe — plik metadanych, określając toobe typu połączenia usługi Automatyzacja Azure używane za pomocą poleceń cmdlet modułu hello w elementach runbook. Opcjonalnie pliku lub nie, te PowerShell moduły można zaimportować do usługi Automatyzacja Azure toomake ich polecenia cmdlet dostępne do użycia w elementy runbook i ich dostępne zasoby DSC do użytku w konfiguracji DSC. Tle hello usługi Automatyzacja Azure przechowuje te moduły, a zadanie elementu runbook i czasu wykonywania zadania kompilacji DSC ładuje je do hello piaskownic usługi Automatyzacja Azure, której elementy runbook są wykonywane i konfiguracji DSC są kompilowane.  Wszystkie zasoby DSC w modułach również automatycznie umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji, dzięki czemu mogą być pobierane przez próby tooapply konfiguracji DSC maszyny.  

Było liczba modułów programu Azure PowerShell poza pole hello automatyzacji Azure można toouse, możesz rozpocząć pracę od razu automatyzacji zarządzania Azure, ale można zaimportować moduły programu PowerShell, niezależnie od systemu, usługi lub ma toointegrate z narzędzia. 

> [!NOTE]
> Niektóre moduły są dostarczane jako "moduły globalne" w usłudze Automatyzacja hello. Te moduły globalnych są tooyou dostępne podczas tworzenia konta automatyzacji i modyfikacjom ich czasami, który automatycznie umieszcza je tooyour konto automatyzacji. Jeśli nie chcesz ich hello toobe automatycznie aktualizowany, zawsze można importować tego samego modułu samodzielnie i który będzie miało pierwszeństwo przed hello globalnej wersji modułu tego modułu było hello usługi. 

format Hello zaimportować pakiet modułu integracji to skompresowany plik mający hello sama nazwa jak hello moduł oraz rozszerzenie zip. Zawiera ona hello moduł programu Windows PowerShell oraz wszelkie pliki pomocnicze, w tym pliku manifestu (psd1), jeśli moduł hello ma.

Jeśli moduł hello powinien zawierać typ połączenia usługi Automatyzacja Azure, musi zawierać plik o nazwie hello `<ModuleName>-Automation.json` , który określa właściwości typu połączenia hello. To jest umieszczony w folderze modułu hello pliku zip skompresowany plik json i zawiera pola hello "połączenia", który jest wymagany tooconnect toohello systemu lub reprezentuje moduł hello usługi. W wyniku zostaje utworzony typ połączenia w usłudze Azure Automation. Przy użyciu tego pliku można ustawić nazwy pól hello, typy i określa, czy pola hello powinny być szyfrowane i / lub opcjonalne dla typu połączenia hello hello modułu. Oto Hello szablonu w formacie json hello:

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Jeśli wdrożono Service Management Automation i tworzenia pakietów moduły integracji dla elementy runbook automatyzacji to powinien wyglądać bardzo znanych tooyou. 

## <a name="authoring-best-practices"></a>Najlepsze rozwiązania w zakresie tworzenia
Mimo że moduły integracji są zasadniczo moduły programu PowerShell, nadal jest kilka rzeczy, firma Microsoft zaleca, należy wziąć pod uwagę podczas tworzenia modułu programu PowerShell, toomake go najbardziej użyteczne w automatyzacji Azure. Niektóre z nich są określone usługi Automatyzacja Azure, a niektóre z nich są przydatne toomake tylko moduły działają poprawnie w przepływie pracy programu PowerShell, niezależnie od tego, czy używasz automatyzacji. 

1. Uwzględnij streszczenie, opis, a identyfikator URI pomocy dla każdego polecenia cmdlet w hello module. W programie PowerShell, można zdefiniować pewne informacje pomocy dla poleceń cmdlet tooallow hello tooreceive pomocy na użyciu hello **Get-Help** polecenia cmdlet. Oto jak możesz na przykład zdefiniować streszczenie i identyfikator URI pomocy dla modułu programu PowerShell zapisanego w pliku psm1.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Udostępnia te informacje nie będą tylko widoczne tej pomocy przy użyciu hello **Get-Help** polecenia cmdlet w hello konsoli programu PowerShell, również uwidoczni tej funkcji pomocy w automatyzacji Azure.  Może to mieć na przykład miejsce podczas wstawiania działań w procesie tworzenia elementu Runbook. Klikając polecenie "Wyświetl szczegółową pomoc", zostanie otwarty hello identyfikator URI pomocy na innej karcie hello przeglądarki sieci web używasz tooaccess usługi Automatyzacja Azure.<br>![Pomoc modułu integracji](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Jeśli moduł hello jest uruchamiana dla systemu zdalnego

    a. Musi on zawierać plik metadanych modułu integracji, który definiuje hello informacje potrzebne tooconnect toothat systemu zdalnego, co oznacza hello typu połączenia.  
    b. Każde polecenie cmdlet w hello module powinny być możliwe tootake w obiekcie połączenia (wystąpienia tego typu połączenia) jako parametr.  

    Jeśli zezwolisz na przekazywanie obiektu z polami hello hello połączenia typu jako parametr polecenia cmdlet toohello polecenia cmdlet w hello module stają się łatwiejsze toouse automatyzacji Azure. Ten sposób użytkownicy nie mają parametry toomap hello połączenia trwałego toohello polecenia cmdlet odpowiednie parametry zawsze wywołują polecenia cmdlet. Na podstawie powyższego przykładu runbook hello, używa zasób połączenia usługi Twilio, nazywany tooaccess CorpTwilio usługi Twilio i zwróć wszystkie numery telefonów hello hello konta.  Zwróć uwagę, jak jest mapowanie pól hello hello połączenia toohello parametrów polecenia cmdlet hello?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Łatwiejsze i lepsze sposób tooapproach to jest bezpośrednio przekazanie hello połączenia toohello polecenia cmdlet object-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Zachowanie takie dla Twojego polecenia cmdlet można włączyć dzięki tooaccept obiektu połączenia bezpośrednio jako parametru, a nie tylko pola połączenia dla parametrów. Zazwyczaj należy zestawu parametrów dla poszczególnych usług, dzięki czemu użytkownik nie używa usługi Automatyzacja Azure można wywołać z polecenia cmdlet bez tworzenia tooact hashtable jako hello obiektu połączenia. Zestaw parametrów **SpecifyConnectionFields** poniżej jest używane toopass właściwości pola połączenia hello jeden po drugim. **UseConnectionObject** umożliwia przekazujesz hello bezpośrednio za pomocą połączenia. Jak widać, hello TwilioSMS Wyślij polecenie cmdlet w hello [modułu programu PowerShell dla usługi Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) umożliwia przekazywanie w obu przypadkach: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Zdefiniuj typ danych wyjściowych dla wszystkich poleceń cmdlet w hello module. Określenie typu danych wyjściowych dla polecenia cmdlet umożliwia IntelliSense czasu projektowania toohelp określić hello output właściwości hello polecenia cmdlet do użycia podczas tworzenia. Jest szczególnie przydatne podczas automatyzacji elementu runbook graficznego tworzenia, gdzie wiedzy czasu projektowania to środowisko użytkownika łatwe tooan klucza z modułu.<br><br> ![Typ danych wyjściowych graficznego elementu Runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Jest to podobne funkcje "typ wyprzedzeniem" toohello apletu polecenia danych wyjściowych w środowisku PowerShell ISE bez konieczności toorun go.<br><br> ![Funkcja IntelliSense programu POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Polecenia cmdlet w hello module nie powinna przyjmować obiekt złożony typy parametrów. Przepływ pracy programu PowerShell różni się od programu PowerShell tym, że przechowuje typy złożone w formie zdeserializowanej. Typy pierwotne, pozostanie jako typów podstawowych, ale typy złożone są przekonwertowanego tootheir rozszeregować wersje, które są zasadniczo zbiory właściwości. Na przykład jeśli użyto hello **Get-Process** polecenia cmdlet w elemencie runbook (lub przepływ pracy programu PowerShell dla tej sprawy), czy zwracać obiekt typu [Deserialized.System.Diagnostic.Process], nie hello [[[oczekiwany Typ System.Diagnostic.Process]. Ten typ ma wszystkie hello takie same właściwości, jak hello-deserializować typu, ale żadna z metod hello. I Jeśli spróbujesz toopass tej wartości jako polecenia cmdlet tooa parametru, gdy polecenie cmdlet hello oczekuje wartości [System.Diagnostic.Process] dla tego parametru, otrzymasz hello następujący błąd: *nie może przetworzyć przekształcania argumentu dla parametru "proces" . Błąd: "nie można przekonwertować wartości"System.Diagnostics.Process (CcmExec)"hello typu"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*   To z faktu, iż niezgodność typów między hello oczekiwano typu [System.Diagnostic.Process] i hello danego typu [Deserialized.System.Diagnostic.Process]. Witaj nawigację tego problemu jest niepodjęcia złożonych typów parametrów polecenia cmdlet hello tooensure modułu. Oto hello niewłaściwy sposób toodo go.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    A tutaj jest hello prawo, biorąc w pierwotnych, która jest używana wewnętrznie przez polecenie cmdlet hello toograb hello obiekt złożony i przy jego użyciu. Ponieważ polecenia cmdlet jest wykonywany w kontekście hello programu PowerShell, nie przepływu pracy programu PowerShell, wewnątrz polecenia cmdlet hello $process staje się hello poprawnego typu [System.Diagnostic.Process].  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Zasoby połączenia w elementach runbook są obiektach HashTable, który jest typem złożonym, a jeszcze tych obiektach HashTable prawdopodobnie toobe toobe stanie przekazywane do polecenia cmdlet dla ich — parametr połączenia doskonale, z wyjątkiem nie rzutowania. Z technicznego punktu widzenia niektóre typy programu PowerShell są toocast może prawidłowo z ich formularza tootheir rozszeregować serializacji formularza i dlatego mogą być przekazywane do polecenia cmdlet dla parametrów akceptowanie hello-deserializować typu. Przykładem jest tablica skrótów. Istnieje możliwość zaimplementowane w taki sposób, który może prawidłowo deserializować również toobe zdefiniowanych typów autora modułu, ale istnieją pewne tooconsider kompromis. Witaj toohave potrzeb typu konstruktora domyślnego, wszystkie jego właściwości publicznych oraz mieć PSTypeConverter. Jednak dla typów zdefiniowanych już tego autora modułu hello nie właścicielem jest zbyt nie "Napraw" je, dlatego hello zalecenie tooavoid złożonych typów parametrów wszystko w jednym. Porada tworzenia elementu Runbook: niektóre przyczyny z poleceń cmdlet należy tootake złożony parametr typu, czy używasz innej osoby moduł, który wymaga parametru typu złożonego, obejście hello w elementach runbook przepływu pracy programu PowerShell i przepływów pracy programu PowerShell do lokalnej PowerShell, to polecenie cmdlet hello toowrap generujący hello typu złożonego i hello polecenia cmdlet, który wykorzystuje hello typu złożonego w hello tego samego działania InlineScript. Ponieważ InlineScript wykonuje jego zawartość jako programu PowerShell, zamiast przepływu pracy programu PowerShell, polecenia cmdlet hello Generowanie typu złożonego hello dałby w efekcie tego poprawny typ, nie hello deserializować typu złożonego.
5. Należy wszystkie polecenia cmdlet w hello module bezstanowe. Przepływ pracy programu PowerShell jest uruchamiany co polecenia cmdlet, o nazwie w przepływie pracy hello w innej sesji. Oznacza to żadnych poleceń cmdlet, które są zależne od stanu sesji utworzone / zmodyfikowane przez inne polecenia cmdlet w hello, w tym samym module nie będzie działać w elementach runbook przepływu pracy programu PowerShell.  Oto przykład tego, jaki nie toodo.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. Moduł Hello powinny być całkowicie zawarte w stanie Xcopy pakietu. Ponieważ moduły usługi Automatyzacja Azure są toohello rozproszonej automatyzacji piaskownic, gdy elementy runbook muszą tooexecute, muszą one toowork niezależnie od hosta hello, w którym jest uruchomiona na. Co to oznacza to, powinien być tooZip stanie się pakiet modułu hello, przenieś go tooany innych hostów z hello taką samą lub nowszą wersję programu PowerShell, a jego funkcji normalne importowane do środowiska PowerShell tego hosta. Aby tego toohappen modułu hello powinien nie są zależne od żadnych plików znajduje się poza folderem modułu hello (hello folderu, który pobiera zip się podczas importowania do automatyzacji Azure) lub na wszelkie ustawienia rejestru unikatowe na hoście, takich jak określone przez hello instalacji produktu. Jeśli z tym najlepszym rozwiązaniem nie jest zakończony, moduł hello nie będzie można korzystać w automatyzacji Azure.  

## <a name="next-steps"></a>Następne kroki

* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
* toolearn więcej informacji na temat tworzenia modułów programu PowerShell, zobacz [pisanie modułu programu Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

