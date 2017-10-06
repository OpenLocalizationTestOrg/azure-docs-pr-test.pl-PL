---
title: Element runbook automatyzacji Azure aaaTesting | Dokumentacja firmy Microsoft
description: "Przed opublikowaniem elementu runbook automatyzacji Azure można przetestować tooensure, że działa zgodnie z oczekiwaniami.  W tym artykule opisano sposób tootest elementu runbook oraz wyświetlić dane wyjściowe."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Testowanie elementu runbook automatyzacji Azure
Podczas testowania elementu runbook hello [wersję roboczą](automation-creating-importing-runbook.md#publishing-a-runbook) jest wykonywany i wykonywane są wszystkie akcje, które wykonuje. Historia zadań nie zostało utworzone, ale hello [dane wyjściowe](automation-runbook-output-and-messages.md#output-stream) i [ostrzeżeń i błędów](automation-runbook-output-and-messages.md#message-streams) strumienie są wyświetlane w hello okienko w danych wyjściowych testu. Komunikaty toohello [strumień pełny](automation-runbook-output-and-messages.md#message-streams) są wyświetlane w okienku danych wyjściowych hello tylko wtedy, gdy hello [zmiennej $VerbosePreference](automation-runbook-output-and-messages.md#preference-variables) ustawiono tooContinue.

Nawet jeśli jest uruchamiana wersja robocza hello, hello runbook nadal hello przepływu pracy jest wykonywany normalnie i wykonuje wszystkie akcje dotyczące zasobów w środowisku hello. Z tego powodu należy przetestować tylko elementy runbook w zasobach nieprodukcyjnych.

Witaj procedury tootest [typu element runbook](automation-runbook-types.md) hello takie same, a nie ma żadnej różnicy w testowaniu między edytor tekstowy hello i hello edytora graficznego w hello portalu Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>Element runbook w portalu Azure hello tootest
Można pracować ze wszystkimi [typ elementu runbook](automation-runbook-types.md) w hello portalu Azure.

1. Witaj Otwórz wersję roboczą elementu runbook hello w obu hello [edytor tekstowy](automation-edit-textual-runbook.md) lub [edytora graficznego usługi](automation-graphical-authoring-intro.md).
2. Kliknij przycisk hello **testu** przycisk tooopen hello testu bloku.
3. Jeśli hello runbook ma parametry, wyświetlane w okienku po lewej stronie powitania, którym można podać wartości toobe używane dla testu hello.
4. Jeśli chcesz toorun hello testu na [hybrydowy proces roboczy elementu Runbook](automation-hybrid-runbook-worker.md), następnie zmienić **parametrów uruchomieniowych** za**hybrydowy proces roboczy** i hello wybierz nazwę grupy docelowej hello.  W przeciwnym razie Zachowaj domyślną hello **Azure** toorun hello testu w chmurze hello.
5. Kliknij przycisk hello **Start** przycisk toostart hello testu.
6. Jeśli element runbook hello jest [przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) lub [graficzny](automation-runbook-types.md#graphical-runbooks), a następnie można zatrzymać lub wstrzymać go podczas jest poddawana testom przyciskami hello poniżej hello okienku danych wyjściowych. Po wstrzymaniu elementu runbook hello kończy hello bieżące działanie przed jego wstrzymaniem. Po wstrzymaniu elementu runbook hello, można zatrzymać lub uruchomić go ponownie.
7. Sprawdź, czy dane wyjściowe hello runbook hello w okienku danych wyjściowych hello.

## <a name="next-steps"></a>Następne kroki
* jak toocreate lub importowanie elementu runbook, zobacz toolearn [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)
* Zobacz toolearn więcej informacji na temat tworzenia graficznego [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
* Zobacz toolearn więcej informacji o konfigurowaniu komunikaty o stanie tooreturn runboks i błędy, łącznie zalecane praktyki [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)

