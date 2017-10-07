---
title: Typy elementu Runbook automatyzacji aaaAzure | Dokumentacja firmy Microsoft
description: "Zawiera opis różnych typów elementów runbook, które można używać w automatyzacji Azure i zagadnienia, które należy wziąć pod uwagę podczas określania, które toouse typu hello. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Typy elementu runbook automatyzacji Azure
Automatyzacja Azure obsługuje cztery typy elementów runbook, które są opisane w skrócie w hello w poniższej tabeli.  Witaj poniższe sekcje zawierają dodatkowe informacje na temat poszczególnych typów, uwzględniając o tym, kiedy toouse każdego.

| Typ | Opis |
|:--- |:--- |
| [Element graficzny](#graphical-runbooks) |Na podstawie środowiska Windows PowerShell i utworzony i edytowany całkowicie edytora graficznego usługi w portalu Azure. |
| [Graficzny przepływ pracy programu PowerShell](#graphical-runbooks) |Na podstawie przepływu pracy środowiska Windows PowerShell i hello utworzony i edytowany całkowicie edytora graficznego w portalu Azure. |
| [PowerShell](#powershell-runbooks) |Tekst elementu runbook oparte na skrypt programu Windows PowerShell. |
| [Przepływ pracy programu PowerShell](#powershell-workflow-runbooks) |Tekst elementu runbook oparte na przepływ pracy programu Windows PowerShell. |

## <a name="graphical-runbooks"></a>Graficznych elementów runbook
[Graficzny](automation-runbook-types.md#graphical-runbooks) i elementów runbook graficzny przepływ pracy programu PowerShell są tworzone i edytować za pomocą edytora graficznego hello w hello portalu Azure.  Można je wyeksportować plik tooa i zaimportowanie ich do innego konta automatyzacji, ale nie można utworzyć lub edytować je z innego narzędzia.  Graficznych elementów runbook generowania kodu programu PowerShell, ale nie można bezpośrednio wyświetlić lub zmodyfikować hello kodu. Graficznych elementów runbook nie może być przekonwertowany tooone z hello [formatach tekstowych](automation-runbook-types.md), ani runbook tekst może być w formacie przekonwertowanego toographical. Graficznych elementów runbook może być przekonwertowany tooGraphical elementach runbook przepływu pracy programu PowerShell podczas importowania i na odwrót.

### <a name="advantages"></a>Zalety
* Visual skonfigurować łącze insert tworzenia modelu  
* Skupić się na jak dane przepływają przez proces hello  
* Wizualnego reprezentowania procesów zarządzania  
* Zawierać inne elementy runbook jako podrzędne elementy runbook toocreate wysokiego poziomu przepływy pracy  
* Zachęca moduły programowania  


### <a name="limitations"></a>Ograniczenia
* Nie można edytować elementu runbook poza portalu Azure.
* Może wymagać działania kodu, które zawiera złożonej logiki tooperform kodu programu PowerShell.
* Nie można wyświetlić ani bezpośrednio edytować hello PowerShell kod, który jest tworzony przez hello graficzny przepływ pracy. Należy zwrócić uwagę na to, czy można wyświetlić kod hello, utworzone w żadnych działań kodu.

## <a name="powershell-runbooks"></a>Elementy runbook programu PowerShell
Elementy runbook programu PowerShell są oparte na programie Windows PowerShell.  Bezpośredniego edytowania kodu hello hello elementu runbook za pomocą edytora tekstu hello w hello portalu Azure.  Można również użyć dowolnego edytora tekstu w trybie offline i [zaimportować hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) w automatyzacji Azure.

### <a name="advantages"></a>Zalety
* Implementuje całą logikę złożonych z kodem PowerShell bez dodatkowej złożoności hello przepływu pracy programu PowerShell. 
* Element Runbook uruchamia szybciej niż w elementach runbook przepływu pracy programu PowerShell, ponieważ nie wymaga toobe skompilowany przed uruchomieniem.

### <a name="limitations"></a>Ograniczenia
* Należy zapoznać się z skryptów środowiska PowerShell.
* Nie można użyć [przetwarzanie równoległe](automation-powershell-workflow.md#parallel-processing) tooperform wielu akcji równolegle.
* Nie można użyć [punktów kontrolnych](automation-powershell-workflow.md#checkpoints) tooresume runbook w przypadku błędu.
* Elementy runbook przepływu pracy programu PowerShell i graficznych elementów runbook można tylko dołączone jako podrzędne elementy runbook za pomocą polecenia cmdlet hello Start AzureAutomationRunbook, która tworzy nowe zadanie.

### <a name="known-issues"></a>Znane problemy
Oto obecnie znane problemy z elementów runbook programu PowerShell.

* Elementy runbook programu PowerShell nie nie można pobrać niezaszyfrowane [zasób zmiennej](automation-variables.md) o wartości null.
* Nie można pobrać elementów runbook programu PowerShell [zasób zmiennej](automation-variables.md) z  *~*  w nazwie hello.
* Get-Process w pętli w programie PowerShell elementu runbook może ulec awarii po około 80 iteracji. 
* Element runbook programu PowerShell może zakończyć się niepowodzeniem, jeśli prób toowrite bardzo dużą ilość strumienia wyjściowego toohello danych na raz.   Ten problem można zwykle obejść przez generowanie właśnie hello potrzebne informacje podczas pracy z dużych obiektów.  Na przykład zamiast Generowanie przypominać *Get-Process*, można output tylko hello wymagane pola z *Get-Process | Wybierz parametr i procesora CPU*.

## <a name="powershell-workflow-runbooks"></a>Elementy runbook przepływu pracy programu PowerShell
Element runbook przepływu pracy programu PowerShell jest tekst elementów runbook na podstawie [przepływu pracy środowiska Windows PowerShell](automation-powershell-workflow.md).  Bezpośredniego edytowania kodu hello hello elementu runbook za pomocą edytora tekstu hello w hello portalu Azure.  Można również użyć dowolnego edytora tekstu w trybie offline i [zaimportować hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) w automatyzacji Azure.

### <a name="advantages"></a>Zalety
* Implementuje całą logikę złożonych z kodem przepływu pracy programu PowerShell.
* Użyj [punktów kontrolnych](automation-powershell-workflow.md#checkpoints) tooresume runbook w przypadku błędu.
* Użyj [przetwarzanie równoległe](automation-powershell-workflow.md#parallel-processing) tooperform wielu akcji równolegle.
* Mogą być inne graficznych elementów runbook i elementy runbook przepływu pracy programu PowerShell jako podrzędne elementy runbook toocreate wysokiego poziomu przepływów pracy.

### <a name="limitations"></a>Ograniczenia
* Autor należy zapoznać się z przepływu pracy programu PowerShell.
* Element Runbook musi uwzględniać hello stopnia złożoności przepływu pracy programu PowerShell takich jak [deserializacji obiektów](automation-powershell-workflow.md#code-changes).
* Element Runbook ma toostart dłużej niż elementów runbook programu PowerShell, ponieważ musi on skompilowany przed uruchomieniem toobe.
* Elementy runbook programu PowerShell można dołączyć jako podrzędne elementy runbook tylko za pomocą polecenia cmdlet hello Start AzureAutomationRunbook, która tworzy nowe zadanie.

## <a name="considerations"></a>Zagadnienia do rozważenia
Należy uwzględnić następujące dodatkowe zagadnienia podczas określania, które toouse typu dla określonego elementu runbook hello konta.

* Elementy runbook nie mogą konwertować z typu graficzny tootextual lub na odwrót.
* Istnieją ograniczenia dotyczące używania elementów runbook o różnych typach jako podrzędnego elementu runbook.  Zobacz [podrzędnych elementów runbook automatyzacji Azure](automation-child-runbooks.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat tworzenia graficznego elementu runbook, zobacz [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md)
* Witaj toounderstand różnice między środowiska PowerShell i programu PowerShell przepływy pracy dla elementów runbook, zobacz [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)
* Aby uzyskać więcej informacji na temat sposobu toocreate lub importowanie elementu Runbook, zobacz [Tworzenie lub importowanie elementu Runbook](automation-creating-importing-runbook.md)

