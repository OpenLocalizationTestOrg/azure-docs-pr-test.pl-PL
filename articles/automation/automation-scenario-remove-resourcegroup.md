---
title: "Usunięcie grupy zasobów aaaAutomate | Dokumentacja firmy Microsoft"
description: "Wersja przepływu pracy programu PowerShell scenariusz automatyzacji Azure tooremove elementów runbook w tym grupy wszystkich zasobów w ramach subskrypcji."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Scenariusz użycia usługi Azure Automation — automatyczne usuwanie grup zasobów
Wielu klientów tworzy więcej niż jedną grupę zasobów. Niektóre grupy mogą służyć do zarządzania aplikacjami produkcyjnymi, a inne mogą być używane jako środowiska rozwojowe, testowe lub przejściowe. Automatyzowanie hello wdrażania tych zasobów jest jeden element, ale trwa toodecommission stanie grupy zasobów za pomocą kliknięcia przycisku hello jest inny. To typowe zadanie zarządzania można uprościć przy użyciu usługi Azure Automation. Jest to przydatne podczas pracy z subskrypcją platformy Azure o limicie wydatków za pośrednictwem oferta dla członków MSDN lub hello programu Essentials chmury sieci partnera firmy Microsoft.

W tym scenariuszu jest oparta na elemencie runbook programu PowerShell i jest zaprojektowana tooremove grup zasobów, które określają z subskrypcji. ustawienie domyślne Hello elementu hello runbook jest tootest przed kontynuowaniem. Daje to pewność, że nie przypadkowego usunięcia grupy zasobów hello przed wszystko jest gotowe toocomplete tej procedury.   

## <a name="getting-hello-scenario"></a>Pobieranie hello scenariusza
W tym scenariuszu składa się z elementu runbook programu PowerShell, który można pobrać z hello [galerii programu PowerShell](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Można również importować go bezpośrednio z hello [galerię elementów Runbook](automation-runbook-gallery.md) w hello portalu Azure.<br><br>

| Element Runbook | Opis |
| --- | --- |
| Remove-ResourceGroup |Usuwa jeden lub więcej grup zasobów platformy Azure i skojarzonych zasobów hello subskrypcji. |

<br>
Witaj następujące parametry wejściowe są zdefiniowane dla tego elementu runbook:

| Parametr | Opis |
| --- | --- |
| NameFilter (Filtr nazw) (wymagany) |Określa nazwę filtra toolimit hello grupy zasobów, które mają na usuwanie. Można przekazać wiele wartości za pomocą listy rozdzielanej przecinkami.<br>Filtr Hello nie jest rozróżniana wielkość liter i jest zgodny z dowolnym grupę zasobów, która zawiera ciąg hello. |
| PreviewMode (Tryb podglądu) (opcjonalny) |Wykonuje hello runbook toosee grupy zasobów, które zostaną usunięte, ale brak działania.<br>Domyślnie Hello **true** toohelp uniknąć przypadkowego usunięcia jednego lub więcej grup zasobów przekazany toohello elementu runbook. |

## <a name="install-and-configure-this-scenario"></a>Instalowanie i konfigurowanie tego scenariusza
### <a name="prerequisites"></a>Wymagania wstępne
Ten element runbook jest uwierzytelniany przy użyciu hello [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Instalowanie i publikować elementy runbook hello
Po pobraniu hello runbook można go zaimportować przy użyciu procedury hello w [importowanie elementu runbook procedur](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Opublikuj hello runbook po jego został pomyślnie zaimportowany na koncie automatyzacji.

## <a name="using-hello-runbook"></a>Przy użyciu hello elementu runbook
Witaj poniższe kroki objaśniają hello wykonywania tego elementu runbook i pomocy należy zapoznać się z jej działania. Tylko testowania hello elementu runbook w tym przykładzie nie faktycznie ich nie usuwać hello grupy zasobów.  

1. Z hello portalu Azure, Twoje konto usługi Automatyzacja i kliknij przycisk **elementów Runbook**.
2. Wybierz hello **ResourceGroup Usuń** runbook i kliknij przycisk **Start**.
3. Po uruchomieniu elementu runbook hello hello **Uruchom element Runbook** zostanie otwarty blok i parametry hello można skonfigurować. Wprowadź nazwy hello grup zasobów w ramach subskrypcji, można użyć do testowania, spowoduje żadnych problemów, jeśli przypadkowo usunięte.<br> ![Parametry elementu Runbook Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Upewnij się, że **Previewmode** ustawiono zbyt**true** tooavoid usuwanie hello wybrane grupy zasobów.  **Uwaga** ten element runbook nie spowoduje usunięcia hello grupę zasobów, która zawiera konto automatyzacji hello działa ten element runbook.  
   >
   >
4. Po skonfigurowaniu wszystkich wartości parametru powitania kliknij **OK**, i hello runbook zostaną umieszczone w kolejce do wykonania.  

Szczegóły hello tooview hello **ResourceGroup Usuń** zadanie elementu runbook w hello portalu Azure, wybierz opcję **zadania** w elemencie runbook hello. Parametry wejściowe Wyświetla podsumowanie hello Hello zadania i dane wyjściowe hello dodatkowo strumienia toogeneral informacje o zadaniu hello i wszelkie wyjątki, które wystąpiły.<br> ![Stan zadania elementu Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Witaj **Podsumowanie zadania** obejmuje wiadomości powitania strumienie danych wyjściowych, ostrzeżeń i błędów. Wybierz **dane wyjściowe** tooview szczegółowe wyniki z hello wykonanie elementu runbook.<br> ![Dane wyjściowe elementu Runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz tooget tworzenie własnych runbook [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md).
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md).
