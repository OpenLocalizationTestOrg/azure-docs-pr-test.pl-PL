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
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Nauka podstawowych pojęć przepływu pracy środowiska Windows PowerShell dla elementów runbook automatyzacji 
Elementy Runbook automatyzacji Azure są zaimplementowane jako przepływy pracy Windows PowerShell.  Przepływu pracy środowiska Windows PowerShell jest skrypt programu Windows PowerShell tooa podobne, lecz ma niektóre istotne różnice, które mogą być mylące tooa nowego użytkownika.  W tym artykule jest zamierzone toohelp zapisu elementów runbook za pomocą przepływu pracy programu PowerShell, zaleca się zapisu elementów runbook za pomocą programu PowerShell, chyba że potrzebne punkty kontrolne.  Istnieje kilka różnic składni podczas tworzenia elementów runbook przepływu pracy programu PowerShell i różnice te wymaga nieco więcej pracy toowrite skuteczne przepływów pracy.  

Przepływ pracy to sekwencja zaprogramowanych, połączonych kroków służących do wykonywania długotrwałych zadań lub wymagają hello koordynacji wielu kroków na wielu urządzeniach lub zarządzanych węzłach. Hello zalety przepływu pracy zamiast zwykłego skryptu obejmują możliwość hello toosimultaneously wykonywania akcji na różnych urządzeniach i tooautomatically możliwości hello skutków błędów. Przepływu pracy środowiska Windows PowerShell to skrypt programu Windows PowerShell, który używa programu Windows Workflow Foundation. Witaj przepływu pracy jest napisany za pomocą składni programu Windows PowerShell i uruchamiana przez środowisko Windows PowerShell, są przetwarzane przez program Windows Workflow Foundation.

Aby uzyskać szczegółowe informacje dotyczące kwestii hello w tym artykule, zobacz [wprowadzenie do przepływu pracy środowiska Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Podstawowa struktura przepływu pracy
Witaj pierwszy krok tooconverting przepływu pracy programu PowerShell tooa skryptu programu PowerShell jest otaczającej go z hello **przepływu pracy** — słowo kluczowe.  Przepływ pracy, który rozpoczyna się od hello **przepływu pracy** — słowo kluczowe następuje hello treść skryptu hello ujęta w nawiasy klamrowe. następuje nazwa Hello przepływu pracy hello hello **przepływu pracy** — słowo kluczowe, jak pokazano w hello następującej składni:

    Workflow Test-Workflow
    {
       <Commands>
    }

Nazwa Hello hello przepływu pracy musi odpowiadać nazwie hello elementu runbook automatyzacji hello. Jeśli hello runbook jest importowany, a następnie nazwę hello musi odpowiadać nazwie przepływu pracy hello i musi kończyć się *ps1*.

tooadd parametry toohello przepływu pracy Użyj hello **Param** tak jak skrypt tooa — słowo kluczowe.

## <a name="code-changes"></a>Zmiany kodu
Kod przepływu pracy programu PowerShell wygląda niemal identyczny tooPowerShell kod skryptu, z wyjątkiem kilku znaczących zmian.  Witaj następujące sekcje opisują zmiany należy skrypt programu PowerShell tooa toomake dla niego toorun w przepływie pracy.

### <a name="activities"></a>Działania
Działanie jest konkretnym zadaniem w przepływie pracy. Tak jak skrypt składa się z co najmniej jedno polecenie, przepływ pracy składa się z jednego lub kilku działań wykonywanych w określonej kolejności. Windows PowerShell Workflow automatycznie konwertuje wiele spośród hello tooactivities poleceń cmdlet programu Windows PowerShell po uruchomieniu przepływu pracy. Po określeniu jednej z tych poleceń cmdlet w elemencie runbook odpowiadające mu działanie hello jest uruchamiane przez program Windows Workflow Foundation. W przypadku poleceń cmdlet bez odpowiadającego im działania przepływu pracy środowiska Windows PowerShell automatycznie uruchamia polecenie cmdlet hello w ramach [InlineScript](#inlinescript) działania. Istnieje zestaw poleceń cmdlet, które są wyłączone i nie można go używać w przepływie pracy, chyba że zostaną jawnie umieszczone w bloku InlineScript. Aby uzyskać więcej szczegółowych informacji dotyczących tych pojęć, zobacz [używanie działań w skryptowych przepływach pracy](http://technet.microsoft.com/library/jj574194.aspx).

Działania przepływów pracy dzielą zestaw wspólnych parametrów tooconfigure ich działanie. Aby uzyskać więcej informacji o typowych parametrach przepływu pracy hello, zobacz [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Parametry pozycyjne
Nie można używać parametrów pozycyjnych działań i poleceń cmdlet w przepływie pracy.  Oznacza to jest, że muszą używać nazwy parametrów.

Rozważmy na przykład hello następującego kodu, który pobiera wszystkie uruchomione usługi.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Jeśli spróbujesz toorun ten sam kod w przepływie pracy, takich jak "Nie można rozpoznać ustawionego przy użyciu hello określony parametr nazwanych parametrów". komunikat o błędzie  toocorrect, podaj nazwę parametru hello jak hello poniżej.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Zdeserializowana obiektów
Obiekty w przepływach pracy są deserializacji.  Oznacza to, że ich właściwości są nadal dostępne, ale nie ich metod.  Rozważmy na przykład hello następującego kodu programu PowerShell, który zatrzymuje usługę przy użyciu metody Stop hello hello obiektu usługi.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Jeśli spróbujesz toorun to w przepływie pracy, komunikat o błędzie informujący o tym "wywołanie metody nie jest obsługiwane w przepływie pracy Windows PowerShell."  

Jedną z opcji jest toowrap tych dwóch wierszy kodu w [InlineScript](#inlinescript) blok w takim przypadku $Service będzie obiektem usługi hello bloku.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Innym rozwiązaniem jest toouse inne polecenie cmdlet, które wykonuje hello same funkcje co metoda hello, jeśli jest dostępny.  W naszym przykładzie polecenie cmdlet Stop-Service hello udostępnia hello same funkcje co Metoda Stop hello, a można użyć następujących hello przepływu pracy.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Witaj **InlineScript** działanie jest przydatne, gdy należy co najmniej jedno polecenie toorun jako tradycyjnych skrypt programu PowerShell zamiast przepływu pracy programu PowerShell.  Podczas przetwarzania polecenia w przepływie pracy są wysyłane tooWindows Workflow Foundation, polecenia w bloku InlineScript są przetwarzane przez środowisko Windows PowerShell.

Blok InlineScript wykorzystuje hello składni pokazano poniżej.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Może zwracać danych wyjściowych z InlineScript, przypisując hello dane wyjściowe tooa zmiennej. Witaj poniższy przykład zatrzymuje usługę i danych wyjściowych hello nazwy usługi.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Można jednak przekazać wartości w bloku InlineScript, ale muszą używać **$Using** modyfikator zakresu.  Witaj poniższy przykład jest identyczne toohello poprzedniego przykładu z tą różnicą, że hello nazwa usługi jest zapewniana przez zmienną.

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


Podczas działania InlineScript mogą okazać się niezbędne w niektórych przepływach pracy, nie obsługują konstrukcje przepływu pracy i należy używać tylko w razie konieczności dla hello z następujących powodów:

* Nie można użyć [punktów kontrolnych](#checkpoints) wewnątrz bloku InlineScript. Jeśli wystąpi błąd w bloku hello, musi zostać wznowiony od początku hello hello bloku.
* Nie można użyć [równoległe wykonywanie](#parallel-processing) wewnątrz InlineScriptBlock.
* InlineScript ma wpływ na skalowalność hello przepływu pracy, ponieważ utrzymuje hello sesji środowiska Windows PowerShell dla hello całej długości tego bloku InlineScript hello.

Aby uzyskać więcej informacji na temat używania InlineScript, zobacz [uruchamianie poleceń programu Windows PowerShell w przepływie pracy](http://technet.microsoft.com/library/jj574197.aspx) i [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Przetwarzanie równoległe
Jedną z zalet przepływów pracy programu Windows PowerShell jest tooperform możliwości hello zestaw poleceń równolegle, a nie po kolei zgodnie z typowym skrypcie.

Można użyć hello **równoległych** toocreate — słowo kluczowe blok skryptu z wieloma poleceniami, które są uruchamiane jednocześnie. Ta metoda korzysta hello składni pokazano poniżej. W tym przypadku działania Activity1 i Activity2 rozpoczyna się od hello tym samym czasie. Activity3 rozpoczyna się dopiero po zakończeniu zarówno działania Activity1 i Activity2.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Rozważmy na przykład hello następującego polecenia programu PowerShell, które skopiować wielu plików tooa sieci docelowej.  Te polecenia są uruchamiane po kolei, że jeden plik musi zakończyć się kopiowanie przed rozpoczęciem powitalne obok jest.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Witaj poniższy przepływ pracy jest uruchamiany te same polecenia równolegle tak, aby uruchomić wszystkie kopiowania na powitania sam czas.  Tylko wtedy, gdy są kopiowane jest hello ukończenia wyświetlony komunikat.

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


Służy hello **ForEach-Parallel** utworzyć jednocześnie tooprocess poleceń dla każdego elementu w kolekcji. Hello elementów w kolekcji hello są przetwarzane równolegle, podczas gdy hello polecenia w bloku skryptu hello są wykonywane sekwencyjnie. Ta metoda korzysta hello składni pokazano poniżej. W tym przypadku działania Activity1 uruchamia na powitania sam czasu dla wszystkich elementów w kolekcji hello. Dla każdego elementu Activity2 zostanie uruchomiony po zakończeniu działania Activity1. Activity3 rozpoczyna się dopiero po zakończeniu zarówno działania Activity1 i Activity2 dla wszystkich elementów.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Poniższy przykład Hello jest podobne toohello poprzedni przykład kopiowanie plików równolegle.  W takim przypadku dla każdego pliku zostanie wyświetlony komunikat, po skopiowaniu.  Tylko wtedy, gdy wszystkie zostaną całkowicie skopiowane jest hello zakończenia wyświetlony komunikat.

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
> Nie zaleca się działania podrzędne elementy runbook równolegle, ponieważ ma ona wyświetlana toogive niewiarygodne wyniki.  Witaj dane wyjściowe hello podrzędnego elementu czasami runbook nie jest wyświetlany, a ustawienia w jeden element podrzędny element runbook może mieć wpływ na hello innych równoległych podrzędnych elementów runbook
>

## <a name="checkpoints"></a>Punkty kontrolne
A *punktu kontrolnego* jest migawką bieżącego stanu przepływu pracy hello, która zawiera bieżące wartości zmiennych hello hello, a wszystkie dane wyjściowe wygenerowane toothat punktu. Jeśli przepływ pracy kończy się na błąd lub jest wstrzymana, następnie hello następnym uruchomieniu go uruchomi z ostatniego punktu kontrolnego zamiast hello początku hello worfklow.  Punkt kontrolny można ustawić w przepływie pracy z hello **Checkpoint-Workflow** działania.

W hello następującego przykładowego kodu wystąpi wyjątek po Activity2 powoduje hello tooend przepływu pracy. Po ponownym uruchomieniu przepływu pracy hello rozpoczyna się od działania Activity2, ponieważ przypadało ono zaraz po hello ostatnim ustawionym punkcie kontrolnym.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Należy ustawić punkty kontrolne w przepływie pracy po działań, które mogą być podatne tooexception i nie powinien być powtarzany, jeśli hello przepływ pracy zostanie wznowione. Przepływ pracy może na przykład utworzyć maszynę wirtualną. Punkt kontrolny można ustawić przed i po maszyny wirtualnej hello hello polecenia toocreate. W przypadku niepowodzenia tworzenia hello hello poleceń będzie powtarzany Jeśli hello przepływu pracy została uruchomiona ponownie. W przypadku niepowodzenia worfklow powitania po pomyślnym zainicjowaniu tworzenia hello następnie hello zostanie nie można utworzyć maszyny wirtualnej ponownie po wznowieniu hello przepływu pracy.

Poniższy przykład Hello kopiuje wiele lokalizacji sieciowej tooa plików i ustawia punkt kontrolny po każdym pliku.  W przypadku utraty lokalizacji sieciowej hello hello przepływu pracy kończy się za błąd.  Gdy jest ona uruchamiana ponownie, zostanie wznowiona w ostatniego punktu kontrolnego hello co oznacza, że hello tylko te pliki, które zostały już skopiowane są pomijane.

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

Ponieważ nazwa użytkownika poświadczeń nie są zachowywane po wywołaniu metody hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) działania lub po hello ostatniego punktu kontrolnego, należy tooset hello poświadczenia toonull go i następnie pobrać je ponownie z magazynu trwałego powitania po  **Suspend-Workflow** lub nosi nazwę punktu kontrolnego.  W przeciwnym razie może zostać wyświetlony następujący komunikat o błędzie hello: *nie można wznowić zadanie przepływu pracy hello, albo ponieważ trwałości danych nie można zapisać całkowicie, lub zapisać trwałości danych została uszkodzona. Należy ponownie uruchomić przepływ pracy hello.*

powitania od tego samego kodu pokazuje sposób toohandle to w elementach runbook przepływu pracy programu PowerShell.

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


Nie jest to wymagane, jeśli są uwierzytelniani za pomocą konta Uruchom jako skonfigurowaną nazwę główną usługi.  

Aby uzyskać więcej informacji na temat punktów kontrolnych, zobacz [tooa Dodawanie punktów kontrolnych przepływu pracy skryptu](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Następne kroki
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
