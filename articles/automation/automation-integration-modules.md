---
title: "<span data-ttu-id=\"ceb9e-101\">Tworzenie modułu integracji usługi Azure Automation | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"ceb9e-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"ceb9e-102\">Samouczek, który przeprowadzi Cię przez proces tworzenia, testowania i przykładowego użycia modułów integracji w usłudze Azure Automation.</span><span class=\"sxs-lookup\"><span data-stu-id=\"ceb9e-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
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
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="ceb9e-103">Moduły integracji usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ceb9e-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="ceb9e-104">Program PowerShell to podstawowa technologia używana w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="ceb9e-105">Ponieważ usługa Azure Automation jest zbudowana w oparciu o program PowerShell, moduły tego programu stanowią podstawę możliwości rozszerzania usługi Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="ceb9e-106">W tym artykule przedstawimy szczegółowe informacje na temat używania w usłudze Azure Automation modułów programu PowerShell określanych jako „moduły integracji” oraz najlepsze rozwiązania w zakresie takiego tworzenia modułów programu PowerShell, aby mogły one działać jako moduły integracji w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="ceb9e-107">Co to jest moduł programu PowerShell?</span><span class="sxs-lookup"><span data-stu-id="ceb9e-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="ceb9e-108">Moduł to grupa poleceń cmdlet programu PowerShell, takich jak **Get-Date** lub **Copy-Item**, które mogą być używane w konsoli programu PowerShell, skryptów, przepływów pracy, elementów Runbook i zasobów konfiguracji DSC programu PowerShell, takich jak plik lub funkcja systemu Windows, których można używać z poziomu konfiguracji DSC programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="ceb9e-109">Wszystkie funkcje programu PowerShell są dostępne za pośrednictwem poleceń cmdlet i zasobów DSC. Wszystkie polecenia cmdlet i zasoby DSC są wspierane przez moduł programu PowerShell (wiele takich modułów jest dołączanych do programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ceb9e-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="ceb9e-110">Na przykład polecenie cmdlet **Get-Date** jest częścią modułu Microsoft.PowerShell.Utility programu PowerShell, polecenie cmdlet **Copy-Item** jest częścią modułu Microsoft.PowerShell.Management, a zasób DSC pakietu jest częścią modułu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="ceb9e-111">Oba te moduły są dostarczane z programem PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="ceb9e-112">Wiele modułów programu PowerShell nie jest dołączanych do tego programu. Są one rozpowszechniane razem z produktami firmy Microsoft lub firm zewnętrznych, takimi jak System Center 2012 Configuration Manager, albo przez dużą społeczność programu PowerShell w miejscach takich jak Galeria programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="ceb9e-113">Moduły są przydatne, ponieważ w prostszy sposób wykonują złożone zadania za pomocą zhermetyzowanych funkcji.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="ceb9e-114">Aby uzyskać więcej informacji, zobacz artykuł o [modułach programu PowerShell w witrynie MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ceb9e-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="ceb9e-115">Co to jest moduł integracji usługi Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="ceb9e-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="ceb9e-116">Moduł integracji nie różni się znacząco od modułu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="ceb9e-117">Jest to po prostu moduł programu PowerShell opcjonalnie zawierający jeden dodatkowy plik — plik metadanych określający typ połączenia usługi Azure Automation do użycia z poleceniami cmdlet modułu w elementach Runbook.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="ceb9e-118">Bez względu na to, czy plik opcjonalny jest używany, te moduły programu PowerShell mogą być importowane do usługi Azure Automation w celu udostępnienia ich poleceń cmdlet do użycia w elementach Runbook, a zasobów DSC — do użycia w konfiguracjach DSC.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="ceb9e-119">Usługa Azure Automation przechowuje te moduły w tle, a w momencie wykonywania zadania elementu Runbook i zadania kompilacji DSC ładuje je do piaskownic usługi Azure Automation, w których są wykonywane elementy Runbook i kompilowane są konfiguracje DSC.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="ceb9e-120">Wszystkie zasoby DSC w modułach są również automatycznie umieszczane na serwerze ściągania konfiguracji DSC usługi Automation, dzięki czemu mogą być ściągane przez komputery próbujące zastosować konfiguracje DSC.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="ceb9e-121">Niektóre moduły programu Azure PowerShell są dostarczane z usługą Azure Automation jako gotowe do użytku. Dzięki temu można od razu rozpocząć automatyzację zarządzania platformą Azure. Można również importować moduły programu PowerShell niezależnie od systemu, usługi lub narzędzia do zintegrowania.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="ceb9e-122">Niektóre moduły w usłudze Automation są dostarczane jako „moduły globalne”.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="ceb9e-123">Moduły globalne są dostępne podczas tworzenia konta automatyzacji i są czasami aktualizowane, co powoduje ich automatyczne wypychanie do konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="ceb9e-124">Jeśli nie chcesz, aby były one automatycznie aktualizowane, zawsze możesz zaimportować sam moduł. Będzie on miał pierwszeństwo przed wersją globalną modułu, która jest dostarczana z usługą.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="ceb9e-125">Format, w którym można zaimportować pakiet modułu integracji, to skompresowany plik o takiej samej nazwie jak moduł, z rozszerzeniem ZIP.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="ceb9e-126">Zawiera on moduł programu Windows PowerShell oraz wszelkie pliki pomocnicze, w tym plik manifestu (psd1), jeśli istnieje dla modułu.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="ceb9e-127">Jeśli moduł powinien zawierać typ połączenia usługi Azure Automation, musi również zawierać plik o nazwie `<ModuleName>-Automation.json`, który określa właściwości typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="ceb9e-128">Jest to plik JSON umieszczony w folderze modułu skompresowanego pliku ZIP i zawiera pola typu „connection” wymagane do nawiązania połączenia z systemem lub usługą reprezentowaną przez moduł.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="ceb9e-129">W wyniku zostaje utworzony typ połączenia w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="ceb9e-130">Przy użyciu tego pliku można ustawić nazwy i typy pól oraz określić, czy powinny one być szyfrowane lub opcjonalne dla danego typu połączenia modułu.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="ceb9e-131">Szablon w formacie pliku JSON wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ceb9e-131">The following is a template in the json file format:</span></span>

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

<span data-ttu-id="ceb9e-132">Jeśli wdrożono usługę Service Management Automation i utworzono pakiety modułów integracji dla elementów Runbook automatyzacji, szablon powinien wyglądać znajomo.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="ceb9e-133">Najlepsze rozwiązania w zakresie tworzenia</span><span class="sxs-lookup"><span data-stu-id="ceb9e-133">Authoring Best Practices</span></span>
<span data-ttu-id="ceb9e-134">Mimo że moduły integracji są zasadniczo modułami programu PowerShell, istnieje kilka kwestii, które warto wziąć pod uwagę podczas tworzenia modułu programu PowerShell w celu zmaksymalizowania jego użyteczności w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="ceb9e-135">Niektóre z tych kwestii są powiązane z usługą Azure Automation, a niektóre z nich po prostu ułatwiają współpracę modułów z przepływem pracy programu PowerShell, bez względu na to, czy korzystasz z tej usługi.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="ceb9e-136">Dodaj streszczenie, opis i identyfikator URI pomocy do każdego polecenia cmdlet w module.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="ceb9e-137">W programie PowerShell możesz zdefiniować pewne informacje pomocy dotyczące poleceń cmdlet, aby umożliwić użytkownikowi uzyskanie pomocy na temat korzystania z nich dzięki poleceniu cmdlet **Get-Help**.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="ceb9e-138">Oto jak możesz na przykład zdefiniować streszczenie i identyfikator URI pomocy dla modułu programu PowerShell zapisanego w pliku psm1.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="ceb9e-139">Podanie tych informacji nie tylko umożliwi wyświetlenie pomocy przy użyciu polecenia cmdlet **Get-Help** w konsoli programu PowerShell, ale także udostępni tę funkcję pomocy w usłudze Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="ceb9e-140">Może to mieć na przykład miejsce podczas wstawiania działań w procesie tworzenia elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="ceb9e-141">Kliknięcie pozycji „Wyświetl szczegółową pomoc” spowoduje otwarcie identyfikatora URI pomocy na innej karcie przeglądarki sieci Web używanej do uzyskiwania dostępu do usługi Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="ceb9e-142">![Pomoc modułu integracji](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="ceb9e-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="ceb9e-143">Jeśli moduł działa w odniesieniu do systemu zdalnego,</span><span class="sxs-lookup"><span data-stu-id="ceb9e-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="ceb9e-144">a.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-144">a.</span></span> <span data-ttu-id="ceb9e-145">powinien zawierać plik metadanych modułu integracji, który definiuje informacje wymagane do nawiązania połączenia z systemem zdalnym, co oznacza typ połączenia;</span><span class="sxs-lookup"><span data-stu-id="ceb9e-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="ceb9e-146">b.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-146">b.</span></span> <span data-ttu-id="ceb9e-147">w każdym poleceniu cmdlet w module użytkownik powinien móc zastosować obiekt połączenia (wystąpienie tego typu połączenia) jako parametr.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="ceb9e-148">Poleceń cmdlet w module będzie można łatwiej używać w usłudze Azure Automation, jeśli zezwolisz na przekazywanie obiektu z polami typu połączenia jako parametru do polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="ceb9e-149">Dzięki temu użytkownicy nie będą musieli mapować parametrów elementu zawartości połączenia do odpowiednich parametrów polecenia cmdlet podczas każdego wywoływania polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="ceb9e-150">W powyższym przykładzie elementu Runbook element zawartości połączenia usługi Twilio o nazwie CorpTwilio jest używany do uzyskiwania dostępu do usługi Twilio i zwraca wszystkie numery telefonów w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="ceb9e-151">Zwróć uwagę na sposób mapowania pól połączenia do parametrów polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="ceb9e-152">Łatwiejsze i skuteczniejsze podejście do tej czynności to bezpośrednie przekazanie obiektu połączenia do polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ceb9e-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="ceb9e-153">Aby umożliwić takie zachowanie poleceń cmdlet, należy zezwolić im na akceptowanie obiektu połączenia bezpośrednio jako parametru, a nie tylko pól połączeń dla parametrów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="ceb9e-154">Zazwyczaj chcesz ustawić parametr dla poszczególnych elementów, dzięki czemu użytkownik nieużywający usługi Azure Automation może wywoływać polecenia cmdlet bez tworzenia tabeli skrótów działającej jako obiekt połączenia.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="ceb9e-155">Poniższy zestaw parametrów **SpecifyConnectionFields** jest używany do przekazywania kolejnych właściwości pól połączeń.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="ceb9e-156">Parametr **UseConnectionObject** umożliwia bezpośrednie przekazanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="ceb9e-157">Jak widać, polecenie cmdlet Send-TwilioSMS w [module programu PowerShell dla usługi Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) umożliwia przekazywanie w dowolny sposób:</span><span class="sxs-lookup"><span data-stu-id="ceb9e-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="ceb9e-158">Zdefiniuj typ danych wyjściowych dla wszystkich poleceń cmdlet w module.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="ceb9e-159">Zdefiniowanie typu danych wyjściowych polecenia cmdlet ułatwia określanie właściwości danych wyjściowych polecenia do użycia podczas tworzenia za pomocą funkcji IntelliSense czasu projektowania.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="ceb9e-160">Jest szczególnie przydatne podczas tworzenia graficznego elementu Runbook usługi Azure Automation, gdzie znajomość czasu projektowania jest kluczem do stworzenia prostego środowiska pracy użytkownika modułu.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="ceb9e-161">![Typ danych wyjściowych graficznego elementu Runbook](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="ceb9e-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="ceb9e-162">Jest to funkcja podobna do funkcji „wpisywania z wyprzedzeniem” danych wyjściowych polecenia cmdlet w środowisku PowerShell ISE bez konieczności jego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="ceb9e-163">![Funkcja IntelliSense programu POSH](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="ceb9e-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="ceb9e-164">Polecenia cmdlet w module nie powinny przyjmować złożonych typów obiektów jako parametrów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="ceb9e-165">Przepływ pracy programu PowerShell różni się od programu PowerShell tym, że przechowuje typy złożone w formie zdeserializowanej.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="ceb9e-166">Typy pierwotne pozostają elementami podstawowymi, ale typy złożone są konwertowane na wersje zdeserializowane, które zasadniczo są zbiorami właściwości.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="ceb9e-167">Jeśli na przykład w elemencie Runbook (lub przepływie pracy programu PowerShell) użyto polecenia cmdlet **Get-Process**, zwróci ono obiekt typu [Deserialized.System.Diagnostic.Process], a nie oczekiwany typ [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="ceb9e-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="ceb9e-168">Ten typ ma te same właściwości co typ niezdeserializowany, ale nie zawiera żadnej z metod.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="ceb9e-169">Jeśli natomiast spróbujesz przekazać tę wartość jako parametr do polecenia cmdlet, gdzie polecenie cmdlet oczekuje wartości [System.Diagnostic.Process] dla tego parametru, pojawi się następujący błąd: *Nie można przetworzyć przekształcenia argumentu dla parametru „process”. Błąd: „Nie można przekonwertować wartości „System.Diagnostics.Process (CcmExec)” typu „Deserialized.System.Diagnostics.Process” na typ „System.Diagnostics.Process”.*</span><span class="sxs-lookup"><span data-stu-id="ceb9e-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="ceb9e-170">Przyczyną tego jest niezgodność między oczekiwanym typem [System.Diagnostic.Process] i danym typem [Deserialized.System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="ceb9e-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="ceb9e-171">Aby rozwiązać ten problem, upewnij się, że polecenia cmdlet modułu nie przyjmują złożonych typów jako parametrów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="ceb9e-172">Oto nieprawidłowy sposób wykonania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="ceb9e-173">A oto odpowiednia metoda — przyjęcie elementu podstawowego, który może być wewnętrznie używany przez polecenie cmdlet do pobierania i używania obiektu złożonego.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="ceb9e-174">Ponieważ polecenia cmdlet są wykonywane w kontekście programu PowerShell, a nie przepływu pracy programu PowerShell, wewnątrz polecenia cmdlet element $process staje się poprawnym typem [System.Diagnostic.Process].</span><span class="sxs-lookup"><span data-stu-id="ceb9e-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="ceb9e-175">Elementy zawartości połączenia w elementach Runbook to tabele skrótów typu złożonego. Te tabele skrótów mogą być przekazywane do poleceń cmdlet na potrzeby parametru -Connection idealnie, bez wyjątku dotyczącego rzutowania.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="ceb9e-176">Technicznie rzecz biorąc, niektóre typy programu PowerShell można prawidłowo rzutować z postaci serializowanej do postaci zdeserializowanej i dlatego można je przekazywać do poleceń cmdlet jako parametry akceptujące typy niezdeserializowane.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="ceb9e-177">Przykładem jest tablica skrótów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-177">Hashtable is one of these.</span></span> <span data-ttu-id="ceb9e-178">Istnieje możliwość zaimplementowania typów zdefiniowanych przez autora modułu w taki sposób, aby mogły być również prawidłowo zdeserializowane, ale wymaga to pewnych kompromisów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="ceb9e-179">Typ musi zawierać konstruktor domyślny i element PSTypeConverter, a wszystkie jego właściwości muszą być publiczne.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="ceb9e-180">Jednak typów już zdefiniowanych, które nie należą do autora modułu, nie można naprawić, dlatego zaleca się unikanie typów złożonych jako parametrów.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="ceb9e-181">Porada dotycząca tworzenia elementu Runbook: jeśli z dowolnej przyczyny polecenia cmdlet muszą przyjmować parametr typu złożonego lub gdy korzystasz z modułu innej osoby wymagającego parametru typu złożonego, obejściem w elementach Runbook przepływu pracy programu PowerShell i przepływach pracy programu PowerShell w lokalnym programie PowerShell jest opakowanie polecenia cmdlet, które generuje typ złożony, i polecenia cmdlet, który wykorzystuje typ złożony, w ramach tego samego działania InlineScript.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="ceb9e-182">Ponieważ skrypt InlineScript wykonuje zawartość jako program PowerShell, a nie przepływ pracy programu PowerShell, wygenerowanie przez polecenie cmdlet typu złożonego spowoduje utworzenie prawidłowego typu, a nie zdeserializowanego typu złożonego.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="ceb9e-183">Utwórz wszystkie polecenia cmdlet w module jako bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="ceb9e-184">Przepływ pracy programu PowerShell powoduje uruchomienie każdego polecenia cmdlet wywoływanego w przepływie pracy w ramach innej sesji.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="ceb9e-185">Oznacza to, że polecenia cmdlet, które zależą od stanu sesji utworzone/zmodyfikowane przez inne polecenia cmdlet w tym samym module, nie będą działać w elementach Runbook przepływu pracy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="ceb9e-186">Oto przykład czynności, których nie należy wykonywać.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-186">Here is an example of what not to do.</span></span>
   
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
6. <span data-ttu-id="ceb9e-187">Moduł powinien być w pełni zawarty w pakiecie z obsługą opcji Xcopy.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="ceb9e-188">Ponieważ moduły usługi Azure Automation są dystrybuowane do piaskownic usługi Automation, jeśli trzeba wykonać elementy Runbook, muszą one działać niezależnie od hosta, na którym są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="ceb9e-189">Oznacza to, że użytkownik powinien mieć możliwość spakowania pakietu modułu i przeniesienia go na inny host z tą samą lub nowszą wersją programu PowerShell, a moduł powinien działać w zwykły sposób po zaimportowaniu do środowiska PowerShell tego hosta.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="ceb9e-190">Aby było to możliwe, moduł nie powinien być zależny od żadnych plików poza folderem modułu (folderem pakowanym podczas importowania do usługi Azure Automation) ani od żadnych ustawień rejestru unikatowych na hoście, na przykład określonych podczas instalowania produktu.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="ceb9e-191">Jeśli to rozwiązanie nie zostanie zastosowane, użycie modułu w usłudze Azure Automation będzie niemożliwe.</span><span class="sxs-lookup"><span data-stu-id="ceb9e-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ceb9e-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ceb9e-192">Next steps</span></span>

* <span data-ttu-id="ceb9e-193">Aby rozpocząć pracę z elementami Runbook przepływu pracy programu PowerShell, zobacz artykuł [My first PowerShell workflow runbook](automation-first-runbook-textual.md) (Mój pierwszy element Runbook przepływu pracy programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ceb9e-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="ceb9e-194">Aby dowiedzieć się więcej na temat tworzenia modułów programu PowerShell, zobacz artykuł [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx) (Pisanie modułu programu Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ceb9e-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

