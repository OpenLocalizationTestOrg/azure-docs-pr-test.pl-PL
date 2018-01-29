---
title: Testowanie elementu runbook automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Przed opublikowaniem elementu runbook automatyzacji Azure możesz przetestować, aby upewnić się, że działa zgodnie z oczekiwaniami.  W tym artykule opisano, jak przetestować element runbook oraz wyświetlić dane wyjściowe."
services: automation
documentationcenter: 
author: georgewallace
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
ms.openlocfilehash: 49e8dfa341940386f15932ec4346c8811effbf0b
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2018
---
# <a name="testing-a-runbook-in-azure-automation"></a>Testowanie elementu runbook automatyzacji Azure
Podczas testowania elementu runbook [wersję roboczą](automation-creating-importing-runbook.md#publishing-a-runbook) jest wykonywany i wykonywane są wszystkie akcje, które wykonuje. Historia zadań nie został utworzony, ale [dane wyjściowe](automation-runbook-output-and-messages.md#output-stream) i [ostrzeżeń i błędów](automation-runbook-output-and-messages.md#message-streams) strumienie są wyświetlane w teście output okienka. Komunikaty [strumień pełny](automation-runbook-output-and-messages.md#message-streams) są wyświetlane w okienku danych wyjściowych tylko wtedy, gdy [zmiennej $VerbosePreference](automation-runbook-output-and-messages.md#preference-variables) jest ustawiona, aby kontynuować.

Nawet, jeśli jest uruchamiana wersja robocza elementu runbook nadal przepływu pracy jest wykonywany normalnie i wykonuje wszystkie akcje dotyczące zasobów w środowisku. Z tego powodu należy przetestować tylko elementy runbook w zasobach nieprodukcyjnych.

Procedury do przetestowania każdego [typu element runbook](automation-runbook-types.md) jest takie same i występują nie różni się w trakcie testów między edytor tekstowy i edytora graficznego w portalu Azure.  

## <a name="to-test-a-runbook-in-the-azure-portal"></a>Aby przetestować element runbook w portalu Azure
Można pracować ze wszystkimi [typ elementu runbook](automation-runbook-types.md) w portalu Azure.

1. Otwórz wersję roboczą elementu runbook albo [edytor tekstowy](automation-edit-textual-runbook.md) lub [edytora graficznego usługi](automation-graphical-authoring-intro.md).
2. Kliknij przycisk **testu** przycisk, aby otworzyć blok testu.
3. Jeśli element runbook ma parametry, będą one wyświetlane w okienku po lewej stronie, w którym można podać wartości do użycia dla testu.
4. Jeśli chcesz uruchomić test [hybrydowy proces roboczy elementu Runbook](automation-hybrid-runbook-worker.md), następnie zmienić **parametrów uruchomieniowych** do **hybrydowy proces roboczy** i wybierz nazwę grupy docelowej.  W przeciwnym razie Zachowaj domyślną **Azure** do uruchomienia testu w chmurze.
5. Kliknij przycisk **Start** przycisk, aby uruchomić test.
6. Jeśli element runbook ma [przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) lub [graficzny](automation-runbook-types.md#graphical-runbooks), a następnie można zatrzymać lub wstrzymać go podczas testowania za pomocą przycisków pod okienkiem danych wyjściowych. Po wstrzymaniu elementu runbook przed jego wstrzymaniem ukończy bieżącego działania. Gdy element runbook zostanie wstrzymany, można zatrzymać lub uruchom go ponownie.
7. Sprawdź dane wyjściowe z elementu runbook w okienku danych wyjściowych.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się, jak utworzyć lub zaimportować element runbook, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)
* Aby dowiedzieć się więcej na temat tworzenia elementów graficznych, zobacz [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md) (Tworzenie elementów graficznych w usłudze Azure Automation).
* Aby rozpocząć pracę z elementami Runbook przepływu pracy programu PowerShell, zobacz artykuł [My first PowerShell workflow runbook](automation-first-runbook-textual.md) (Mój pierwszy element Runbook przepływu pracy programu PowerShell).
* Aby dowiedzieć się więcej o konfigurowaniu elementów runbook, aby zwrócić komunikaty o stanie i błędy, łącznie zalecane rozwiązania, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md)

