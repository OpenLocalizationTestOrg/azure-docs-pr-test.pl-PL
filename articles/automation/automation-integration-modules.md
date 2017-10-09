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
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="7ee72-103">Moduły integracji usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7ee72-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="7ee72-104">PowerShell jest podstawową technologią hello za automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="7ee72-105">Ponieważ usługi Automatyzacja Azure jest oparty na programie PowerShell, moduły programu PowerShell są rozszerzalności klucza toohello automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="7ee72-106">W tym artykule firma Microsoft przeprowadzi Cię charakterystykę hello stosowania automatyzacji Azure moduły programu PowerShell, określonego tooas "Moduły integracji" i najlepszych praktyk do tworzenia własnych modułów programu PowerShell toomake się, że działają jako moduły integracji w Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="7ee72-107">Co to jest moduł programu PowerShell?</span><span class="sxs-lookup"><span data-stu-id="7ee72-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="7ee72-108">Moduł programu PowerShell to grupa poleceń cmdlet programu PowerShell, takie jak **Get-Date** lub **Copy-Item**, które mogą być używane z konsoli programu PowerShell hello, skrypty, przepływy pracy, elementy runbook i zasoby DSC środowiska PowerShell, takich jak WindowsFeature lub plik, który może służyć z konfiguracji DSC środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="7ee72-109">Wszystkie funkcje hello programu PowerShell jest uwidaczniany za pomocą poleceń cmdlet i zasoby DSC i każdego polecenia cmdlet/DSC zasobu nie jest obsługiwana przez moduł programu PowerShell, duża liczba którego dostarczanych z programem PowerShell sam.</span><span class="sxs-lookup"><span data-stu-id="7ee72-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="7ee72-110">Na przykład Witaj **Get-Date** polecenia cmdlet jest częścią hello modułu programu Microsoft.PowerShell.Utility PowerShell i **Copy-Item** polecenia cmdlet jest częścią hello modułu Microsoft.PowerShell.Management PowerShell i Witaj DSC pakietu zasobów jest częścią hello modułu PSDesiredStateConfiguration PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="7ee72-111">Oba te moduły są dostarczane z programem PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="7ee72-112">Jednak wiele modułów programu PowerShell nie są dostarczane jako część programu PowerShell i zamiast tego są dystrybuowane z produktami pierwszy lub innych firm, takich jak System Center 2012 Configuration Manager lub przez społeczność przeważająca PowerShell hello na miejsc, jak galerii programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="7ee72-113">Moduły Hello są przydatne, ponieważ ich wykonywanie złożonych zadań za pomocą funkcji hermetyzowany prostsze.</span><span class="sxs-lookup"><span data-stu-id="7ee72-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="7ee72-114">Aby uzyskać więcej informacji, zobacz artykuł o [modułach programu PowerShell w witrynie MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee72-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="7ee72-115">Co to jest moduł integracji usługi Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="7ee72-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="7ee72-116">Moduł integracji nie różni się znacząco od modułu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="7ee72-117">Jego po prostu moduł programu PowerShell, który opcjonalnie zawiera jeden plik dodatkowe — plik metadanych, określając toobe typu połączenia usługi Automatyzacja Azure używane za pomocą poleceń cmdlet modułu hello w elementach runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee72-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="7ee72-118">Opcjonalnie pliku lub nie, te PowerShell moduły można zaimportować do usługi Automatyzacja Azure toomake ich polecenia cmdlet dostępne do użycia w elementy runbook i ich dostępne zasoby DSC do użytku w konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="7ee72-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="7ee72-119">Tle hello usługi Automatyzacja Azure przechowuje te moduły, a zadanie elementu runbook i czasu wykonywania zadania kompilacji DSC ładuje je do hello piaskownic usługi Automatyzacja Azure, której elementy runbook są wykonywane i konfiguracji DSC są kompilowane.</span><span class="sxs-lookup"><span data-stu-id="7ee72-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="7ee72-120">Wszystkie zasoby DSC w modułach również automatycznie umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji, dzięki czemu mogą być pobierane przez próby tooapply konfiguracji DSC maszyny.</span><span class="sxs-lookup"><span data-stu-id="7ee72-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="7ee72-121">Było liczba modułów programu Azure PowerShell poza pole hello automatyzacji Azure można toouse, możesz rozpocząć pracę od razu automatyzacji zarządzania Azure, ale można zaimportować moduły programu PowerShell, niezależnie od systemu, usługi lub ma toointegrate z narzędzia.</span><span class="sxs-lookup"><span data-stu-id="7ee72-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="7ee72-122">Niektóre moduły są dostarczane jako "moduły globalne" w usłudze Automatyzacja hello.</span><span class="sxs-lookup"><span data-stu-id="7ee72-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="7ee72-123">Te moduły globalnych są tooyou dostępne podczas tworzenia konta automatyzacji i modyfikacjom ich czasami, który automatycznie umieszcza je tooyour konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="7ee72-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="7ee72-124">Jeśli nie chcesz ich hello toobe automatycznie aktualizowany, zawsze można importować tego samego modułu samodzielnie i który będzie miało pierwszeństwo przed hello globalnej wersji modułu tego modułu było hello usługi.</span><span class="sxs-lookup"><span data-stu-id="7ee72-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="7ee72-125">format Hello zaimportować pakiet modułu integracji to skompresowany plik mający hello sama nazwa jak hello moduł oraz rozszerzenie zip.</span><span class="sxs-lookup"><span data-stu-id="7ee72-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="7ee72-126">Zawiera ona hello moduł programu Windows PowerShell oraz wszelkie pliki pomocnicze, w tym pliku manifestu (psd1), jeśli moduł hello ma.</span><span class="sxs-lookup"><span data-stu-id="7ee72-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="7ee72-127">Jeśli moduł hello powinien zawierać typ połączenia usługi Automatyzacja Azure, musi zawierać plik o nazwie hello `<ModuleName>-Automation.json` , który określa właściwości typu połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="7ee72-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="7ee72-128">To jest umieszczony w folderze modułu hello pliku zip skompresowany plik json i zawiera pola hello "połączenia", który jest wymagany tooconnect toohello systemu lub reprezentuje moduł hello usługi.</span><span class="sxs-lookup"><span data-stu-id="7ee72-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="7ee72-129">W wyniku zostaje utworzony typ połączenia w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="7ee72-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="7ee72-130">Przy użyciu tego pliku można ustawić nazwy pól hello, typy i określa, czy pola hello powinny być szyfrowane i / lub opcjonalne dla typu połączenia hello hello modułu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="7ee72-131">Oto Hello szablonu w formacie json hello:</span><span class="sxs-lookup"><span data-stu-id="7ee72-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="7ee72-132">Jeśli wdrożono Service Management Automation i tworzenia pakietów moduły integracji dla elementy runbook automatyzacji to powinien wyglądać bardzo znanych tooyou.</span><span class="sxs-lookup"><span data-stu-id="7ee72-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="7ee72-133">Najlepsze rozwiązania w zakresie tworzenia</span><span class="sxs-lookup"><span data-stu-id="7ee72-133">Authoring Best Practices</span></span>
<span data-ttu-id="7ee72-134">Mimo że moduły integracji są zasadniczo moduły programu PowerShell, nadal jest kilka rzeczy, firma Microsoft zaleca, należy wziąć pod uwagę podczas tworzenia modułu programu PowerShell, toomake go najbardziej użyteczne w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="7ee72-135">Niektóre z nich są określone usługi Automatyzacja Azure, a niektóre z nich są przydatne toomake tylko moduły działają poprawnie w przepływie pracy programu PowerShell, niezależnie od tego, czy używasz automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="7ee72-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="7ee72-136">Uwzględnij streszczenie, opis, a identyfikator URI pomocy dla każdego polecenia cmdlet w hello module.</span><span class="sxs-lookup"><span data-stu-id="7ee72-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="7ee72-137">W programie PowerShell, można zdefiniować pewne informacje pomocy dla poleceń cmdlet tooallow hello tooreceive pomocy na użyciu hello **Get-Help** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7ee72-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="7ee72-138">Oto jak możesz na przykład zdefiniować streszczenie i identyfikator URI pomocy dla modułu programu PowerShell zapisanego w pliku psm1.</span><span class="sxs-lookup"><span data-stu-id="7ee72-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="7ee72-139">Udostępnia te informacje nie będą tylko widoczne tej pomocy przy użyciu hello **Get-Help** polecenia cmdlet w hello konsoli programu PowerShell, również uwidoczni tej funkcji pomocy w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="7ee72-140">Może to mieć na przykład miejsce podczas wstawiania działań w procesie tworzenia elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee72-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="7ee72-141">Klikając polecenie "Wyświetl szczegółową pomoc", zostanie otwarty hello identyfikator URI pomocy na innej karcie hello przeglądarki sieci web używasz tooaccess usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="7ee72-142">![Pomoc modułu integracji](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="7ee72-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="7ee72-143">Jeśli moduł hello jest uruchamiana dla systemu zdalnego</span><span class="sxs-lookup"><span data-stu-id="7ee72-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="7ee72-144">a.</span><span class="sxs-lookup"><span data-stu-id="7ee72-144">a.</span></span> <span data-ttu-id="7ee72-145">Musi on zawierać plik metadanych modułu integracji, który definiuje hello informacje potrzebne tooconnect toothat systemu zdalnego, co oznacza hello typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="7ee72-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="7ee72-146">b.</span><span class="sxs-lookup"><span data-stu-id="7ee72-146">b.</span></span> <span data-ttu-id="7ee72-147">Każde polecenie cmdlet w hello module powinny być możliwe tootake w obiekcie połączenia (wystąpienia tego typu połączenia) jako parametr.</span><span class="sxs-lookup"><span data-stu-id="7ee72-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="7ee72-148">Jeśli zezwolisz na przekazywanie obiektu z polami hello hello połączenia typu jako parametr polecenia cmdlet toohello polecenia cmdlet w hello module stają się łatwiejsze toouse automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="7ee72-149">Ten sposób użytkownicy nie mają parametry toomap hello połączenia trwałego toohello polecenia cmdlet odpowiednie parametry zawsze wywołują polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7ee72-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="7ee72-150">Na podstawie powyższego przykładu runbook hello, używa zasób połączenia usługi Twilio, nazywany tooaccess CorpTwilio usługi Twilio i zwróć wszystkie numery telefonów hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="7ee72-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="7ee72-151">Zwróć uwagę, jak jest mapowanie pól hello hello połączenia toohello parametrów polecenia cmdlet hello?</span><span class="sxs-lookup"><span data-stu-id="7ee72-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="7ee72-152">Łatwiejsze i lepsze sposób tooapproach to jest bezpośrednio przekazanie hello połączenia toohello polecenia cmdlet object-</span><span class="sxs-lookup"><span data-stu-id="7ee72-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="7ee72-153">Zachowanie takie dla Twojego polecenia cmdlet można włączyć dzięki tooaccept obiektu połączenia bezpośrednio jako parametru, a nie tylko pola połączenia dla parametrów.</span><span class="sxs-lookup"><span data-stu-id="7ee72-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="7ee72-154">Zazwyczaj należy zestawu parametrów dla poszczególnych usług, dzięki czemu użytkownik nie używa usługi Automatyzacja Azure można wywołać z polecenia cmdlet bez tworzenia tooact hashtable jako hello obiektu połączenia.</span><span class="sxs-lookup"><span data-stu-id="7ee72-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="7ee72-155">Zestaw parametrów **SpecifyConnectionFields** poniżej jest używane toopass właściwości pola połączenia hello jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="7ee72-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="7ee72-156">**UseConnectionObject** umożliwia przekazujesz hello bezpośrednio za pomocą połączenia.</span><span class="sxs-lookup"><span data-stu-id="7ee72-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="7ee72-157">Jak widać, hello TwilioSMS Wyślij polecenie cmdlet w hello [modułu programu PowerShell dla usługi Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) umożliwia przekazywanie w obu przypadkach:</span><span class="sxs-lookup"><span data-stu-id="7ee72-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="7ee72-158">Zdefiniuj typ danych wyjściowych dla wszystkich poleceń cmdlet w hello module.</span><span class="sxs-lookup"><span data-stu-id="7ee72-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="7ee72-159">Określenie typu danych wyjściowych dla polecenia cmdlet umożliwia IntelliSense czasu projektowania toohelp określić hello output właściwości hello polecenia cmdlet do użycia podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="7ee72-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="7ee72-160">Jest szczególnie przydatne podczas automatyzacji elementu runbook graficznego tworzenia, gdzie wiedzy czasu projektowania to środowisko użytkownika łatwe tooan klucza z modułu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="7ee72-161">![Typ danych wyjściowych graficznego elementu Runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="7ee72-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="7ee72-162">Jest to podobne funkcje "typ wyprzedzeniem" toohello apletu polecenia danych wyjściowych w środowisku PowerShell ISE bez konieczności toorun go.</span><span class="sxs-lookup"><span data-stu-id="7ee72-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="7ee72-163">![Funkcja IntelliSense programu POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="7ee72-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="7ee72-164">Polecenia cmdlet w hello module nie powinna przyjmować obiekt złożony typy parametrów.</span><span class="sxs-lookup"><span data-stu-id="7ee72-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="7ee72-165">Przepływ pracy programu PowerShell różni się od programu PowerShell tym, że przechowuje typy złożone w formie zdeserializowanej.</span><span class="sxs-lookup"><span data-stu-id="7ee72-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="7ee72-166">Typy pierwotne, pozostanie jako typów podstawowych, ale typy złożone są przekonwertowanego tootheir rozszeregować wersje, które są zasadniczo zbiory właściwości.</span><span class="sxs-lookup"><span data-stu-id="7ee72-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="7ee72-167">Na przykład jeśli użyto hello **Get-Process** polecenia cmdlet w elemencie runbook (lub przepływ pracy programu PowerShell dla tej sprawy), czy zwracać obiekt typu [Deserialized.System.Diagnostic.Process], nie hello [[[oczekiwany Typ System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="7ee72-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="7ee72-168">Ten typ ma wszystkie hello takie same właściwości, jak hello-deserializować typu, ale żadna z metod hello.</span><span class="sxs-lookup"><span data-stu-id="7ee72-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="7ee72-169">I Jeśli spróbujesz toopass tej wartości jako polecenia cmdlet tooa parametru, gdy polecenie cmdlet hello oczekuje wartości [System.Diagnostic.Process] dla tego parametru, otrzymasz hello następujący błąd: *nie może przetworzyć przekształcania argumentu dla parametru "proces" . Błąd: "nie można przekonwertować wartości"System.Diagnostics.Process (CcmExec)"hello typu"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process".*</span><span class="sxs-lookup"><span data-stu-id="7ee72-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="7ee72-170">To z faktu, iż niezgodność typów między hello oczekiwano typu [System.Diagnostic.Process] i hello danego typu [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="7ee72-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="7ee72-171">Witaj nawigację tego problemu jest niepodjęcia złożonych typów parametrów polecenia cmdlet hello tooensure modułu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="7ee72-172">Oto hello niewłaściwy sposób toodo go.</span><span class="sxs-lookup"><span data-stu-id="7ee72-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="7ee72-173">A tutaj jest hello prawo, biorąc w pierwotnych, która jest używana wewnętrznie przez polecenie cmdlet hello toograb hello obiekt złożony i przy jego użyciu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="7ee72-174">Ponieważ polecenia cmdlet jest wykonywany w kontekście hello programu PowerShell, nie przepływu pracy programu PowerShell, wewnątrz polecenia cmdlet hello $process staje się hello poprawnego typu [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="7ee72-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="7ee72-175">Zasoby połączenia w elementach runbook są obiektach HashTable, który jest typem złożonym, a jeszcze tych obiektach HashTable prawdopodobnie toobe toobe stanie przekazywane do polecenia cmdlet dla ich — parametr połączenia doskonale, z wyjątkiem nie rzutowania.</span><span class="sxs-lookup"><span data-stu-id="7ee72-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="7ee72-176">Z technicznego punktu widzenia niektóre typy programu PowerShell są toocast może prawidłowo z ich formularza tootheir rozszeregować serializacji formularza i dlatego mogą być przekazywane do polecenia cmdlet dla parametrów akceptowanie hello-deserializować typu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="7ee72-177">Przykładem jest tablica skrótów.</span><span class="sxs-lookup"><span data-stu-id="7ee72-177">Hashtable is one of these.</span></span> <span data-ttu-id="7ee72-178">Istnieje możliwość zaimplementowane w taki sposób, który może prawidłowo deserializować również toobe zdefiniowanych typów autora modułu, ale istnieją pewne tooconsider kompromis.</span><span class="sxs-lookup"><span data-stu-id="7ee72-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="7ee72-179">Witaj toohave potrzeb typu konstruktora domyślnego, wszystkie jego właściwości publicznych oraz mieć PSTypeConverter.</span><span class="sxs-lookup"><span data-stu-id="7ee72-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="7ee72-180">Jednak dla typów zdefiniowanych już tego autora modułu hello nie właścicielem jest zbyt nie "Napraw" je, dlatego hello zalecenie tooavoid złożonych typów parametrów wszystko w jednym.</span><span class="sxs-lookup"><span data-stu-id="7ee72-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="7ee72-181">Porada tworzenia elementu Runbook: niektóre przyczyny z poleceń cmdlet należy tootake złożony parametr typu, czy używasz innej osoby moduł, który wymaga parametru typu złożonego, obejście hello w elementach runbook przepływu pracy programu PowerShell i przepływów pracy programu PowerShell do lokalnej PowerShell, to polecenie cmdlet hello toowrap generujący hello typu złożonego i hello polecenia cmdlet, który wykorzystuje hello typu złożonego w hello tego samego działania InlineScript.</span><span class="sxs-lookup"><span data-stu-id="7ee72-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="7ee72-182">Ponieważ InlineScript wykonuje jego zawartość jako programu PowerShell, zamiast przepływu pracy programu PowerShell, polecenia cmdlet hello Generowanie typu złożonego hello dałby w efekcie tego poprawny typ, nie hello deserializować typu złożonego.</span><span class="sxs-lookup"><span data-stu-id="7ee72-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="7ee72-183">Należy wszystkie polecenia cmdlet w hello module bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="7ee72-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="7ee72-184">Przepływ pracy programu PowerShell jest uruchamiany co polecenia cmdlet, o nazwie w przepływie pracy hello w innej sesji.</span><span class="sxs-lookup"><span data-stu-id="7ee72-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="7ee72-185">Oznacza to żadnych poleceń cmdlet, które są zależne od stanu sesji utworzone / zmodyfikowane przez inne polecenia cmdlet w hello, w tym samym module nie będzie działać w elementach runbook przepływu pracy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee72-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="7ee72-186">Oto przykład tego, jaki nie toodo.</span><span class="sxs-lookup"><span data-stu-id="7ee72-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="7ee72-187">Moduł Hello powinny być całkowicie zawarte w stanie Xcopy pakietu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="7ee72-188">Ponieważ moduły usługi Automatyzacja Azure są toohello rozproszonej automatyzacji piaskownic, gdy elementy runbook muszą tooexecute, muszą one toowork niezależnie od hosta hello, w którym jest uruchomiona na.</span><span class="sxs-lookup"><span data-stu-id="7ee72-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="7ee72-189">Co to oznacza to, powinien być tooZip stanie się pakiet modułu hello, przenieś go tooany innych hostów z hello taką samą lub nowszą wersję programu PowerShell, a jego funkcji normalne importowane do środowiska PowerShell tego hosta.</span><span class="sxs-lookup"><span data-stu-id="7ee72-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="7ee72-190">Aby tego toohappen modułu hello powinien nie są zależne od żadnych plików znajduje się poza folderem modułu hello (hello folderu, który pobiera zip się podczas importowania do automatyzacji Azure) lub na wszelkie ustawienia rejestru unikatowe na hoście, takich jak określone przez hello instalacji produktu.</span><span class="sxs-lookup"><span data-stu-id="7ee72-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="7ee72-191">Jeśli z tym najlepszym rozwiązaniem nie jest zakończony, moduł hello nie będzie można korzystać w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee72-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7ee72-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ee72-192">Next steps</span></span>

* <span data-ttu-id="7ee72-193">tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="7ee72-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="7ee72-194">toolearn więcej informacji na temat tworzenia modułów programu PowerShell, zobacz [pisanie modułu programu Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="7ee72-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

