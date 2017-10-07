---
title: "przepływ pracy programu PowerShell dla usługi Automatyzacja Azure aaaLearning | Dokumentacja firmy Microsoft"
description: "Ten artykuł dotyczy jako szybki lekcji dla autorów doświadczenia w obsłudze programu PowerShell toounderstand hello określonych różnice między środowiska PowerShell i przepływu pracy programu PowerShell i elementów runbook tooAutomation zastosowanie koncepcji."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="4e30e-103">Nauka podstawowych pojęć przepływu pracy środowiska Windows PowerShell dla elementów runbook automatyzacji</span><span class="sxs-lookup"><span data-stu-id="4e30e-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="4e30e-104">Elementy Runbook automatyzacji Azure są zaimplementowane jako przepływy pracy Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e30e-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="4e30e-105">Przepływu pracy środowiska Windows PowerShell jest skrypt programu Windows PowerShell tooa podobne, lecz ma niektóre istotne różnice, które mogą być mylące tooa nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e30e-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="4e30e-106">W tym artykule jest zamierzone toohelp zapisu elementów runbook za pomocą przepływu pracy programu PowerShell, zaleca się zapisu elementów runbook za pomocą programu PowerShell, chyba że potrzebne punkty kontrolne.</span><span class="sxs-lookup"><span data-stu-id="4e30e-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="4e30e-107">Istnieje kilka różnic składni podczas tworzenia elementów runbook przepływu pracy programu PowerShell i różnice te wymaga nieco więcej pracy toowrite skuteczne przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="4e30e-108">Przepływ pracy to sekwencja zaprogramowanych, połączonych kroków służących do wykonywania długotrwałych zadań lub wymagają hello koordynacji wielu kroków na wielu urządzeniach lub zarządzanych węzłach.</span><span class="sxs-lookup"><span data-stu-id="4e30e-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="4e30e-109">Hello zalety przepływu pracy zamiast zwykłego skryptu obejmują możliwość hello toosimultaneously wykonywania akcji na różnych urządzeniach i tooautomatically możliwości hello skutków błędów.</span><span class="sxs-lookup"><span data-stu-id="4e30e-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="4e30e-110">Przepływu pracy środowiska Windows PowerShell to skrypt programu Windows PowerShell, który używa programu Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="4e30e-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="4e30e-111">Witaj przepływu pracy jest napisany za pomocą składni programu Windows PowerShell i uruchamiana przez środowisko Windows PowerShell, są przetwarzane przez program Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="4e30e-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="4e30e-112">Aby uzyskać szczegółowe informacje dotyczące kwestii hello w tym artykule, zobacz [wprowadzenie do przepływu pracy środowiska Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e30e-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="4e30e-113">Podstawowa struktura przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="4e30e-113">Basic structure of a workflow</span></span>
<span data-ttu-id="4e30e-114">Witaj pierwszy krok tooconverting przepływu pracy programu PowerShell tooa skryptu programu PowerShell jest otaczającej go z hello **przepływu pracy** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="4e30e-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="4e30e-115">Przepływ pracy, który rozpoczyna się od hello **przepływu pracy** — słowo kluczowe następuje hello treść skryptu hello ujęta w nawiasy klamrowe.</span><span class="sxs-lookup"><span data-stu-id="4e30e-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="4e30e-116">następuje nazwa Hello przepływu pracy hello hello **przepływu pracy** — słowo kluczowe, jak pokazano w hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="4e30e-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="4e30e-117">Nazwa Hello hello przepływu pracy musi odpowiadać nazwie hello elementu runbook automatyzacji hello.</span><span class="sxs-lookup"><span data-stu-id="4e30e-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="4e30e-118">Jeśli hello runbook jest importowany, a następnie nazwę hello musi odpowiadać nazwie przepływu pracy hello i musi kończyć się *ps1*.</span><span class="sxs-lookup"><span data-stu-id="4e30e-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="4e30e-119">tooadd parametry toohello przepływu pracy Użyj hello **Param** tak jak skrypt tooa — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="4e30e-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="4e30e-120">Zmiany kodu</span><span class="sxs-lookup"><span data-stu-id="4e30e-120">Code changes</span></span>
<span data-ttu-id="4e30e-121">Kod przepływu pracy programu PowerShell wygląda niemal identyczny tooPowerShell kod skryptu, z wyjątkiem kilku znaczących zmian.</span><span class="sxs-lookup"><span data-stu-id="4e30e-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="4e30e-122">Witaj następujące sekcje opisują zmiany należy skrypt programu PowerShell tooa toomake dla niego toorun w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="4e30e-123">Działania</span><span class="sxs-lookup"><span data-stu-id="4e30e-123">Activities</span></span>
<span data-ttu-id="4e30e-124">Działanie jest konkretnym zadaniem w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="4e30e-125">Tak jak skrypt składa się z co najmniej jedno polecenie, przepływ pracy składa się z jednego lub kilku działań wykonywanych w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4e30e-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="4e30e-126">Windows PowerShell Workflow automatycznie konwertuje wiele spośród hello tooactivities poleceń cmdlet programu Windows PowerShell po uruchomieniu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="4e30e-127">Po określeniu jednej z tych poleceń cmdlet w elemencie runbook odpowiadające mu działanie hello jest uruchamiane przez program Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="4e30e-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="4e30e-128">W przypadku poleceń cmdlet bez odpowiadającego im działania przepływu pracy środowiska Windows PowerShell automatycznie uruchamia polecenie cmdlet hello w ramach [InlineScript](#inlinescript) działania.</span><span class="sxs-lookup"><span data-stu-id="4e30e-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="4e30e-129">Istnieje zestaw poleceń cmdlet, które są wyłączone i nie można go używać w przepływie pracy, chyba że zostaną jawnie umieszczone w bloku InlineScript.</span><span class="sxs-lookup"><span data-stu-id="4e30e-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="4e30e-130">Aby uzyskać więcej szczegółowych informacji dotyczących tych pojęć, zobacz [używanie działań w skryptowych przepływach pracy](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e30e-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="4e30e-131">Działania przepływów pracy dzielą zestaw wspólnych parametrów tooconfigure ich działanie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="4e30e-132">Aby uzyskać więcej informacji o typowych parametrach przepływu pracy hello, zobacz [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e30e-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="4e30e-133">Parametry pozycyjne</span><span class="sxs-lookup"><span data-stu-id="4e30e-133">Positional parameters</span></span>
<span data-ttu-id="4e30e-134">Nie można używać parametrów pozycyjnych działań i poleceń cmdlet w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="4e30e-135">Oznacza to jest, że muszą używać nazwy parametrów.</span><span class="sxs-lookup"><span data-stu-id="4e30e-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="4e30e-136">Rozważmy na przykład hello następującego kodu, który pobiera wszystkie uruchomione usługi.</span><span class="sxs-lookup"><span data-stu-id="4e30e-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="4e30e-137">Jeśli spróbujesz toorun ten sam kod w przepływie pracy, takich jak "Nie można rozpoznać ustawionego przy użyciu hello określony parametr nazwanych parametrów". komunikat o błędzie</span><span class="sxs-lookup"><span data-stu-id="4e30e-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="4e30e-138">toocorrect, podaj nazwę parametru hello jak hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="4e30e-139">Zdeserializowana obiektów</span><span class="sxs-lookup"><span data-stu-id="4e30e-139">Deserialized objects</span></span>
<span data-ttu-id="4e30e-140">Obiekty w przepływach pracy są deserializacji.</span><span class="sxs-lookup"><span data-stu-id="4e30e-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="4e30e-141">Oznacza to, że ich właściwości są nadal dostępne, ale nie ich metod.</span><span class="sxs-lookup"><span data-stu-id="4e30e-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="4e30e-142">Rozważmy na przykład hello następującego kodu programu PowerShell, który zatrzymuje usługę przy użyciu metody Stop hello hello obiektu usługi.</span><span class="sxs-lookup"><span data-stu-id="4e30e-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="4e30e-143">Jeśli spróbujesz toorun to w przepływie pracy, komunikat o błędzie informujący o tym "wywołanie metody nie jest obsługiwane w przepływie pracy Windows PowerShell."</span><span class="sxs-lookup"><span data-stu-id="4e30e-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="4e30e-144">Jedną z opcji jest toowrap tych dwóch wierszy kodu w [InlineScript](#inlinescript) blok w takim przypadku $Service będzie obiektem usługi hello bloku.</span><span class="sxs-lookup"><span data-stu-id="4e30e-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="4e30e-145">Innym rozwiązaniem jest toouse inne polecenie cmdlet, które wykonuje hello same funkcje co metoda hello, jeśli jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="4e30e-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="4e30e-146">W naszym przykładzie polecenie cmdlet Stop-Service hello udostępnia hello same funkcje co Metoda Stop hello, a można użyć następujących hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="4e30e-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="4e30e-147">InlineScript</span></span>
<span data-ttu-id="4e30e-148">Witaj **InlineScript** działanie jest przydatne, gdy należy co najmniej jedno polecenie toorun jako tradycyjnych skrypt programu PowerShell zamiast przepływu pracy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e30e-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="4e30e-149">Podczas przetwarzania polecenia w przepływie pracy są wysyłane tooWindows Workflow Foundation, polecenia w bloku InlineScript są przetwarzane przez środowisko Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e30e-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="4e30e-150">Blok InlineScript wykorzystuje hello składni pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="4e30e-151">Może zwracać danych wyjściowych z InlineScript, przypisując hello dane wyjściowe tooa zmiennej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="4e30e-152">Witaj poniższy przykład zatrzymuje usługę i danych wyjściowych hello nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="4e30e-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="4e30e-153">Można jednak przekazać wartości w bloku InlineScript, ale muszą używać **$Using** modyfikator zakresu.</span><span class="sxs-lookup"><span data-stu-id="4e30e-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="4e30e-154">Witaj poniższy przykład jest identyczne toohello poprzedniego przykładu z tą różnicą, że hello nazwa usługi jest zapewniana przez zmienną.</span><span class="sxs-lookup"><span data-stu-id="4e30e-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="4e30e-155">Podczas działania InlineScript mogą okazać się niezbędne w niektórych przepływach pracy, nie obsługują konstrukcje przepływu pracy i należy używać tylko w razie konieczności dla hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="4e30e-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="4e30e-156">Nie można użyć [punktów kontrolnych](#checkpoints) wewnątrz bloku InlineScript.</span><span class="sxs-lookup"><span data-stu-id="4e30e-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="4e30e-157">Jeśli wystąpi błąd w bloku hello, musi zostać wznowiony od początku hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="4e30e-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="4e30e-158">Nie można użyć [równoległe wykonywanie](#parallel-processing) wewnątrz InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="4e30e-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="4e30e-159">InlineScript ma wpływ na skalowalność hello przepływu pracy, ponieważ utrzymuje hello sesji środowiska Windows PowerShell dla hello całej długości tego bloku InlineScript hello.</span><span class="sxs-lookup"><span data-stu-id="4e30e-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="4e30e-160">Aby uzyskać więcej informacji na temat używania InlineScript, zobacz [uruchamianie poleceń programu Windows PowerShell w przepływie pracy](http://technet.microsoft.com/library/jj574197.aspx) i [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e30e-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="4e30e-161">Przetwarzanie równoległe</span><span class="sxs-lookup"><span data-stu-id="4e30e-161">Parallel processing</span></span>
<span data-ttu-id="4e30e-162">Jedną z zalet przepływów pracy programu Windows PowerShell jest tooperform możliwości hello zestaw poleceń równolegle, a nie po kolei zgodnie z typowym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="4e30e-163">Można użyć hello **równoległych** toocreate — słowo kluczowe blok skryptu z wieloma poleceniami, które są uruchamiane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="4e30e-164">Ta metoda korzysta hello składni pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="4e30e-165">W tym przypadku działania Activity1 i Activity2 rozpoczyna się od hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="4e30e-166">Activity3 rozpoczyna się dopiero po zakończeniu zarówno działania Activity1 i Activity2.</span><span class="sxs-lookup"><span data-stu-id="4e30e-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="4e30e-167">Rozważmy na przykład hello następującego polecenia programu PowerShell, które skopiować wielu plików tooa sieci docelowej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="4e30e-168">Te polecenia są uruchamiane po kolei, że jeden plik musi zakończyć się kopiowanie przed rozpoczęciem powitalne obok jest.</span><span class="sxs-lookup"><span data-stu-id="4e30e-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="4e30e-169">Witaj poniższy przepływ pracy jest uruchamiany te same polecenia równolegle tak, aby uruchomić wszystkie kopiowania na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="4e30e-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="4e30e-170">Tylko wtedy, gdy są kopiowane jest hello ukończenia wyświetlony komunikat.</span><span class="sxs-lookup"><span data-stu-id="4e30e-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="4e30e-171">Służy hello **ForEach-Parallel** utworzyć jednocześnie tooprocess poleceń dla każdego elementu w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="4e30e-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="4e30e-172">Hello elementów w kolekcji hello są przetwarzane równolegle, podczas gdy hello polecenia w bloku skryptu hello są wykonywane sekwencyjnie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="4e30e-173">Ta metoda korzysta hello składni pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="4e30e-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="4e30e-174">W tym przypadku działania Activity1 uruchamia na powitania sam czasu dla wszystkich elementów w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="4e30e-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="4e30e-175">Dla każdego elementu Activity2 zostanie uruchomiony po zakończeniu działania Activity1.</span><span class="sxs-lookup"><span data-stu-id="4e30e-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="4e30e-176">Activity3 rozpoczyna się dopiero po zakończeniu zarówno działania Activity1 i Activity2 dla wszystkich elementów.</span><span class="sxs-lookup"><span data-stu-id="4e30e-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="4e30e-177">Poniższy przykład Hello jest podobne toohello poprzedni przykład kopiowanie plików równolegle.</span><span class="sxs-lookup"><span data-stu-id="4e30e-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="4e30e-178">W takim przypadku dla każdego pliku zostanie wyświetlony komunikat, po skopiowaniu.</span><span class="sxs-lookup"><span data-stu-id="4e30e-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="4e30e-179">Tylko wtedy, gdy wszystkie zostaną całkowicie skopiowane jest hello zakończenia wyświetlony komunikat.</span><span class="sxs-lookup"><span data-stu-id="4e30e-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="4e30e-180">Nie zaleca się działania podrzędne elementy runbook równolegle, ponieważ ma ona wyświetlana toogive niewiarygodne wyniki.</span><span class="sxs-lookup"><span data-stu-id="4e30e-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="4e30e-181">Witaj dane wyjściowe hello podrzędnego elementu czasami runbook nie jest wyświetlany, a ustawienia w jeden element podrzędny element runbook może mieć wpływ na hello innych równoległych podrzędnych elementów runbook</span><span class="sxs-lookup"><span data-stu-id="4e30e-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="4e30e-182">Punkty kontrolne</span><span class="sxs-lookup"><span data-stu-id="4e30e-182">Checkpoints</span></span>
<span data-ttu-id="4e30e-183">A *punktu kontrolnego* jest migawką bieżącego stanu przepływu pracy hello, która zawiera bieżące wartości zmiennych hello hello, a wszystkie dane wyjściowe wygenerowane toothat punktu.</span><span class="sxs-lookup"><span data-stu-id="4e30e-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="4e30e-184">Jeśli przepływ pracy kończy się na błąd lub jest wstrzymana, następnie hello następnym uruchomieniu go uruchomi z ostatniego punktu kontrolnego zamiast hello początku hello worfklow.</span><span class="sxs-lookup"><span data-stu-id="4e30e-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="4e30e-185">Punkt kontrolny można ustawić w przepływie pracy z hello **Checkpoint-Workflow** działania.</span><span class="sxs-lookup"><span data-stu-id="4e30e-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="4e30e-186">W hello następującego przykładowego kodu wystąpi wyjątek po Activity2 powoduje hello tooend przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="4e30e-187">Po ponownym uruchomieniu przepływu pracy hello rozpoczyna się od działania Activity2, ponieważ przypadało ono zaraz po hello ostatnim ustawionym punkcie kontrolnym.</span><span class="sxs-lookup"><span data-stu-id="4e30e-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="4e30e-188">Należy ustawić punkty kontrolne w przepływie pracy po działań, które mogą być podatne tooexception i nie powinien być powtarzany, jeśli hello przepływ pracy zostanie wznowione.</span><span class="sxs-lookup"><span data-stu-id="4e30e-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="4e30e-189">Przepływ pracy może na przykład utworzyć maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="4e30e-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="4e30e-190">Punkt kontrolny można ustawić przed i po maszyny wirtualnej hello hello polecenia toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e30e-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="4e30e-191">W przypadku niepowodzenia tworzenia hello hello poleceń będzie powtarzany Jeśli hello przepływu pracy została uruchomiona ponownie.</span><span class="sxs-lookup"><span data-stu-id="4e30e-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="4e30e-192">W przypadku niepowodzenia worfklow powitania po pomyślnym zainicjowaniu tworzenia hello następnie hello zostanie nie można utworzyć maszyny wirtualnej ponownie po wznowieniu hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4e30e-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="4e30e-193">Poniższy przykład Hello kopiuje wiele lokalizacji sieciowej tooa plików i ustawia punkt kontrolny po każdym pliku.</span><span class="sxs-lookup"><span data-stu-id="4e30e-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="4e30e-194">W przypadku utraty lokalizacji sieciowej hello hello przepływu pracy kończy się za błąd.</span><span class="sxs-lookup"><span data-stu-id="4e30e-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="4e30e-195">Gdy jest ona uruchamiana ponownie, zostanie wznowiona w ostatniego punktu kontrolnego hello co oznacza, że hello tylko te pliki, które zostały już skopiowane są pomijane.</span><span class="sxs-lookup"><span data-stu-id="4e30e-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="4e30e-196">Ponieważ nazwa użytkownika poświadczeń nie są zachowywane po wywołaniu metody hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) działania lub po hello ostatniego punktu kontrolnego, należy tooset hello poświadczenia toonull go i następnie pobrać je ponownie z magazynu trwałego powitania po  **Suspend-Workflow** lub nosi nazwę punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="4e30e-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="4e30e-197">W przeciwnym razie może zostać wyświetlony następujący komunikat o błędzie hello: *nie można wznowić zadanie przepływu pracy hello, albo ponieważ trwałości danych nie można zapisać całkowicie, lub zapisać trwałości danych została uszkodzona. Należy ponownie uruchomić przepływ pracy hello.*</span><span class="sxs-lookup"><span data-stu-id="4e30e-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="4e30e-198">powitania od tego samego kodu pokazuje sposób toohandle to w elementach runbook przepływu pracy programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e30e-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="4e30e-199">Nie jest to wymagane, jeśli są uwierzytelniani za pomocą konta Uruchom jako skonfigurowaną nazwę główną usługi.</span><span class="sxs-lookup"><span data-stu-id="4e30e-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="4e30e-200">Aby uzyskać więcej informacji na temat punktów kontrolnych, zobacz [tooa Dodawanie punktów kontrolnych przepływu pracy skryptu](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e30e-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e30e-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e30e-201">Next steps</span></span>
* <span data-ttu-id="4e30e-202">tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="4e30e-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
