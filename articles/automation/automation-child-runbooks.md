---
title: elementy runbook automatyzacji Azure aaaChild | Dokumentacja firmy Microsoft
description: "W tym artykule opisano różne metody powitania od elementu runbook z innego elementu runbook usługi Automatyzacja Azure oraz udostępniania tych informacji między nimi."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Podrzędne elementy runbook automatyzacji Azure
Jest najlepszym rozwiązaniem w automatyzacji Azure toowrite wielokrotnego użytku, moduły elementów runbook zawierających osobne funkcje, które mogą być używane przez inne elementy runbook. Nadrzędny element runbook często wywołuje jeden lub więcej podrzędnych elementów runbook tooperform wymaganych funkcji. Istnieją dwa sposoby toocall podrzędnego elementu runbook, a każdy odznacza się istotnymi różnicami, które należy zrozumieć, dzięki czemu można określić, który będzie najlepiej w różnych sytuacjach.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Wywoływanie podrzędnego elementu runbook przy użyciu wykonywania śródwierszowego
tooinvoke wbudowanego elementu runbook z innego elementu runbook, należy użyć nazwy hello hello runbook i podaj wartości jego parametrów, dokładnie tak, należy użyć działania lub polecenia cmdlet.  Wszystkie elementy runbook w hello tego samego konta automatyzacji są dostępne tooall innym toobe używane w ten sposób. Hello nadrzędny element runbook będzie oczekiwał na powitania podrzędnego elementu runbook toocomplete przed przejściem do następnego wiersza toohello, a wszelkie dane wyjściowe zwracany jest bezpośrednio nadrzędnej toohello.

Po wywołaniu wbudowanego elementu runbook jest uruchamiany w hello same zadania jako hello nadrzędny element runbook. Nie będzie żadnego wskazania w historii zadań hello podrzędnego elementu runbook hello, który działał. Wszelkie wyjątki i strumienie wyjściowe z hello podrzędnego elementu runbook zostaną skojarzone z elementem nadrzędnym hello. To zmniejszyć liczbę zadań i umożliwiają łatwiejsze tootrack i tootroubleshoot ponieważ wszelkie wyjątki zgłaszane przez hello podrzędnego elementu runbook i dowolną z jego strumieni wyjściowych są skojarzone z zadaniem nadrzędnym hello.

Po opublikowaniu elementu runbook należy opublikować już wszelkimi podrzędnymi elementami runbook, który wywołuje. Jest to spowodowane usługi Automatyzacja Azure tworzy skojarzenie z wszelkimi podrzędnymi elementami runbook podczas kompilowania elementu runbook. Jeśli nie są hello nadrzędny element runbook będzie wyświetlany toopublish właściwie, ale wygeneruje wyjątek po uruchomieniu. W takim przypadku można ponownie opublikować nadrzędny element runbook hello w kolejności tooproperly odwołanie hello podrzędnych elementów runbook. Nie trzeba toorepublish hello nadrzędny element runbook w przypadku zmiany dowolnego hello podrzędnych elementów runbook ponieważ skojarzenie hello będzie zostały już utworzone.

Parametry Hello podrzędnego elementu runbook wywoływanego śródwierszowo mogą mieć dowolny typ danych, włącznie z obiektami złożonymi, a istnieje nie [serializacji JSON](automation-starting-a-runbook.md#runbook-parameters) się po ponownym uruchomieniu hello element runbook za pomocą portalu zarządzania Azure hello lub hello Polecenie cmdlet Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Typy elementów Runbook
Typy, które można wywołać siebie:

* A [runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) i [graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) można wywołać każdy, wbudowanego (są na podstawie programu PowerShell).
* A [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) i przepływ pracy programu PowerShell graficznego elementów runbook można wywołać każdy, wbudowanego (oba są przepływu pracy programu PowerShell)
* Witaj typów środowiska PowerShell i powitalne typów przepływu pracy programu PowerShell nie można wywołać wbudowanego siebie i musi być Start AzureRmAutomationRunbook.

Podczas publikowania sprawy kolejności:

* Witaj publikowania kolejność elementów runbook jest ważne tylko dla elementów runbook przepływu pracy programu PowerShell i graficzny przepływ pracy programu PowerShell.

Podczas wywoływania graficzny lub przepływ pracy programu PowerShell podrzędnego elementu runbook przy użyciu wykonywania śródwierszowego tylko należy użyć nazwy hello hello elementu runbook.  Podczas wywoływania podrzędnego elementu runbook programu PowerShell musi poprzedzony nazwy z *.\\*  toospecify, który hello skryptu znajduje się w katalogu lokalnego hello. 

### <a name="example"></a>Przykład
Poniższy przykład Hello wywołuje testu podrzędnego elementu runbook, który akceptuje trzy parametry, obiekt złożony, liczbę całkowitą i wartość logiczną. dane wyjściowe Hello hello podrzędnego elementu runbook jest przypisana zmienna tooa.  W takim przypadku hello podrzędnego elementu runbook jest element runbook przepływu pracy programu PowerShell

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Poniżej przedstawiono hello tym samym przykładzie, jako element podrzędny hello przy użyciu elementu runbook programu PowerShell.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Uruchamianie podrzędnego elementu runbook za pomocą polecenia cmdlet
Można użyć hello [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart polecenia cmdlet runbook zgodnie z opisem w [toostart element runbook za pomocą środowiska Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Dostępne są dwa tryby użycia tego polecenia cmdlet.  W trybie jednego hello polecenie cmdlet zwraca identyfikator zadania hello natychmiast po utworzeniu zadania podrzędne hello hello podrzędnego elementu runbook.  W hello innych tryb, w którym zostanie włączone, określając hello **— oczekiwania** parametru polecenia cmdlet hello będzie czekać podrzędnych hello zakończenie zadania i zwraca dane wyjściowe hello z hello podrzędnego elementu runbook.

jako osobne zadanie zostanie uruchomione zadanie Hello uruchomiona za pomocą polecenia cmdlet podrzędnego elementu runbook z hello nadrzędny element runbook. To powoduje większą liczbę zadań niż wywoływania hello wbudowanego elementu runbook i ich dokonuje tootrack trudniejsze. Witaj nadrzędny może jednak uruchomić wiele podrzędnych elementów runbook asynchronicznie bez oczekiwania na każdym toocomplete. Aby uzyskać takie same wykonywanie równoległe wywoływania hello podrzędnych elementów runbook wbudowany, hello nadrzędny element runbook musi toouse hello [słowa kluczowego parallel](automation-powershell-workflow.md#parallel-processing).

Parametry dla podrzędnego elementu runbook uruchomione za pomocą polecenia cmdlet są przekazywane jako tablica skrótów zgodnie z opisem w [parametrów elementu Runbook](automation-starting-a-runbook.md#runbook-parameters). Mogą być używane tylko proste typy danych. Jeśli hello runbook ma parametr o złożonym typie danych, następnie go musi być wywoływany śródwierszowo.

### <a name="example"></a>Przykład
Witaj poniższy przykład podrzędnego elementu runbook rozpoczyna się od parametrów, a następnie czeka na jego toocomplete przy użyciu hello Start AzureRmAutomationRunbook-oczekiwania parametru. Po ukończeniu dane wyjściowe są zbierane z hello podrzędnego elementu runbook.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Porównanie metod wywoływania podrzędnego elementu runbook
Witaj Poniższa tabela zawiera podsumowanie hello różnice między Witaj dwie metody wywoływania elementu runbook z innego elementu runbook.

|  | Wbudowany | Polecenie cmdlet |
|:--- |:--- |:--- |
| Zadanie |Podrzędne elementy runbook uruchomione w hello same zadania jako element nadrzędny hello. |Tworzone jest osobne zadanie hello podrzędnego elementu runbook. |
| Wykonanie |Nadrzędny element runbook czeka na powitania podrzędnego elementu runbook toocomplete przed kontynuowaniem. |Nadrzędny element runbook kontynuuje działanie od razu po uruchomieniu podrzędnego elementu runbook *lub* nadrzędny element runbook czeka toofinish zadania podrzędne hello. |
| Dane wyjściowe |Nadrzędny element runbook może bezpośrednio pobierać dane wyjściowe z podrzędnego elementu runbook. |Nadrzędny element runbook musi pobrać dane wyjściowe z zadania podrzędnego elementu runbook *lub* nadrzędny element runbook może bezpośrednio pobierać dane wyjściowe z podrzędnego elementu runbook. |
| Parametry |Wartości parametrów hello podrzędnego elementu runbook są określane oddzielnie i mogą mieć dowolny typ danych. |Wartości hello podrzędnego elementu runbook parametry muszą być połączone w jedną tablicę skrótów i może zawierać tylko proste, tablicy i obiekt typy danych tego korzystają z serializacji JSON. |
| Konto usługi Automation |Nadrzędny element runbook w hello można używać tylko podrzędnego elementu runbook tego samego konta automatyzacji. |Nadrzędny element runbook można użyć podrzędnego elementu runbook z dowolnego konta automatyzacji z hello tej samej subskrypcji platformy Azure i subskrypcji różnych nawet jeśli masz tooit połączenia. |
| Publikowanie |Podrzędnego elementu runbook należy opublikować przed opublikowaniem nadrzędnego elementu runbook. |Podrzędnego elementu runbook należy opublikować w dowolnym momencie przed uruchomieniem nadrzędnego elementu runbook. |

## <a name="next-steps"></a>Następne kroki
* [Uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)
* [Element Runbook danych wyjściowych i komunikatów w usłudze Automatyzacja Azure](automation-runbook-output-and-messages.md)

