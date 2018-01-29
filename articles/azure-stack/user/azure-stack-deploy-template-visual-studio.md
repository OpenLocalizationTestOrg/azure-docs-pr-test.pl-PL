---
title: "Wdrażanie szablonów z programem Visual Studio w stosie Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie wdrażania szablonów z programem Visual Studio w stosie Azure."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: helaw
ms.openlocfilehash: 8fc32dc50d96d202dfc982cbdc52d8e479c3a3eb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a>Wdrażanie szablonów w stosie Azure przy użyciu programu Visual Studio

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Wdrażanie szablonów usługi Azure Resource Manager development kit stosu Azure za pomocą programu Visual Studio.

1. [Zainstaluj i połącz](azure-stack-install-visual-studio.md) stos Azure z programem Visual Studio.
2. Otwórz program Visual Studio.
3. Kliknij przycisk **pliku**, kliknij przycisk **nowy**i w **nowy projekt** kliknij okno dialogowe **grupy zasobów platformy Azure**.
4. Wprowadź **nazwa** nowy projekt, a następnie kliknij przycisk **OK**.
5. W **wybierz szablon Azure** okno dialogowe, zmień *Pokaż szablony z tej lokalizacji* listy rozwijanej **Szybki Start Azure stosu**
6. Kliknij przycisk **101-create magazynu account**, a następnie kliknij przycisk **OK**.  
7. W nowego projektu można wyświetlić listę dostępnych szablonów rozwijając **szablony** w węźle **Eksploratora rozwiązań** okienka.
8. W **Eksploratora rozwiązań** okienku kliknij prawym przyciskiem myszy nazwę projektu, kliknij przycisk **Wdróż**, następnie kliknij przycisk **nowe wdrożenie**.
9. W **wdrażanie w grupie zasobów** okna dialogowego, **subskrypcji** listy rozwijanej, wybierz subskrypcję Microsoft Azure stosu.
10. W **grupy zasobów** listy, wybierz istniejącą grupę zasobów lub Utwórz nową.
11. W **lokalizacja grupy zasobów** listy, wybierz lokalizację, a następnie kliknij przycisk **Wdróż**.
12. W **Edytuj parametry** okna dialogowego wprowadź wartości dla parametrów (różniących się przez szablon), a następnie kliknij przycisk **zapisać**.

## <a name="next-steps"></a>Następne kroki
[Wdrażanie szablonów za pomocą wiersza polecenia](azure-stack-deploy-template-command-line.md)

[Tworzenie szablonów dla stosu Azure](azure-stack-develop-templates.md)

