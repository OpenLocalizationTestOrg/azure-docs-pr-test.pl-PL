---
title: "aaaMy pierwszy przepływu pracy programu PowerShell elementu runbook automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Samouczek, który przeprowadzi Cię przez kolejne hello tworzenia, testowania i publikowania elementu runbook prosty tekst za pomocą przepływu pracy programu PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "przepływ pracy programu powershell, przykłady przepływu pracy programu powershell, program powershell przepływu pracy"
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Mój pierwszy element Runbook przepływu pracy programu PowerShell

> [!div class="op_single_selector"]
> * [Element graficzny](automation-first-runbook-graphical.md)
> * [Program PowerShell](automation-first-runbook-textual-powershell.md)
> * [Przepływ pracy programu PowerShell](automation-first-runbook-textual.md)
> 
> 

Ten samouczek przedstawia tworzenie hello [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) automatyzacji Azure. Możemy zaczynać prosty element runbook, który możemy testowanie i publikowanie podczas wyjaśniający, jak tootrack hello stanu zadania elementu runbook hello. Firma Microsoft zmodyfikowanie hello runbook tooactually zarządzania zasobami Azure, w tym przypadku uruchamiania maszyny wirtualnej platformy Azure. Na koniec wykonujemy hello runbook bardziej niezawodne, dodając parametry elementu runbook.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).
* [Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.  To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.
* Maszyna wirtualna platformy Azure. Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.

## <a name="step-1---create-new-runbook"></a>Krok 1. Tworzenie nowego elementu Runbook
Zaczniemy przez utworzenie prostego elementu runbook, która wyświetla tekst hello *Hello World*.

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.  
   Strona kont automatyzacji Hello zapewnia szybki przegląd hello zasobów na tym koncie. Konto powinno mieć już pewne elementy zawartości. Większość tych to hello modułów, które są automatycznie umieszczane w koncie automatyzacji. Należy również zaznaczyć zasób poświadczeń hello, który jest wymieniony w hello [wymagania wstępne](#prerequisites).
2. Polecenie hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.<br><br> ![Kontrolka Elementy Runbook](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Utwórz nowy element runbook, klikając hello **Dodaj element runbook** przycisk, a następnie **Utwórz nowy element runbook**.
4. Nadaj nazwę hello runbook hello *przepływu pracy MyFirstRunbook*.
5. W takim przypadku zamierzamy toocreate [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) tak wybierz **przepływu pracy programu Powershell** dla **typ elementu Runbook**.<br><br> ![Nowy element Runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Kliknij przycisk **Utwórz** toocreate hello elementu runbook i hello Otwórz edytor tekstowy.

## <a name="step-2---add-code-toohello-runbook"></a>Krok 2 — Dodaj kod toohello runbook
Można albo kod typu bezpośrednio do elementu runbook hello, lub można wybrać polecenia cmdlet, elementy runbook i zasoby z hello formant biblioteki i ich dodano toohello runbook za pomocą parametrów powiązanych. W ramach tego przewodnika firma Microsoft będzie wpisać bezpośrednio w hello elementu runbook.

1. Nasze elementu runbook jest obecnie pusta z tylko hello wymagane *przepływu pracy* — słowo kluczowe, nazwę hello naszych runbook i nawiasów klamrowych hello, które będą encase hello całego przepływu pracy.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Wpisz ciąg *Write-Output „Witaj, świecie”* nawiasach hello.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Zapisz element runbook hello, klikając **zapisać**.<br><br> ![Zapisywanie elementu Runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>Krok 3 - Test hello runbook
Zanim firma Microsoft publikować hello runbook toomake go dostępne w środowisku produkcyjnym, chcemy tootest on toomake się upewnić, że działa on prawidłowo. Testowanie elementu Runbook polega na uruchomieniu jego **wersji roboczej** i interaktywnym przejrzeniu danych wyjściowych.

1. Kliknij przycisk **okienku testu** tooopen hello testu okienka.<br><br> ![Okienko testowania](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Kliknij przycisk **Start** toostart hello testu. Powinno to być hello włączyć tylko opcję.
3. Zostanie utworzone [zadanie elementu Runbook](automation-runbook-execution.md) i pojawi się jego stan.  
   Stan zadania Hello zostanie uruchomiona jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toocome chmury hello dostępne. Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.  
4. Po zakończeniu zadania elementu runbook hello jego dane wyjściowe są wyświetlane. W naszym przypadku powinien być widoczny ciąg *Witaj, świecie*.<br><br> ![Witaj, świecie](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Zamknij hello testu okienku tooreturn toohello kanwy.

## <a name="step-4---publish-and-start-hello-runbook"></a>Krok 4 — publikowanie i uruchomić hello elementu runbook
Witaj elementu runbook, który właśnie utworzony jest nadal w trybie wersji roboczej. Potrzebujemy toopublish go przed możemy można uruchomić w środowisku produkcyjnym. Podczas publikowania elementu runbook, należy zastąpić hello istniejącej opublikowanej wersji hello wersję roboczą. W tym przypadku nie mamy wersję opublikowaną jeszcze ponieważ właśnie utworzyliśmy hello elementu runbook.

1. Kliknij przycisk **publikowania** toopublish hello runbook, a następnie **tak** po wyświetleniu monitu.<br><br> ![Publikowanie](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Podczas przewijania tooview po lewej stronie powitania runbook w programie hello **elementów Runbook** okienko teraz, zostanie wyświetlona **stan pisania przyp** z **opublikowano**.
3. Przewijania wstecz toohello prawo tooview hello okienka **przepływu pracy MyFirstRunbook**.  
   Witaj opcje górze hello zezwolić nam toostart hello runbook, zaplanowane toostart w czasie w przyszłości hello lub tworzenia [elementu webhook](automation-webhooks.md) , może być uruchamiany za pośrednictwem połączenia HTTP.
4. Chcemy tylko toostart hello runbook więc klikamy **Start** , a następnie **tak** po wyświetleniu monitu.<br><br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Okienko zadania został otwarty do hello zadanie elementu runbook, który właśnie utworzony. Możemy zamknąć w tym okienku, ale w takim przypadku pozostanie on otwarte aby firma Microsoft obserwować postęp zadania hello.
6. Stan zadania Hello jest wyświetlany w **Podsumowanie zadania** i dopasowań hello stany widzieliśmy po przetestowaliśmy hello elementu runbook.<br><br> ![Podsumowanie zadania](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Raz hello pokazuje stan elementu runbook *Ukończono*, kliknij przycisk **dane wyjściowe**. w okienku z wyjściem Hello jest otwarty i możemy stwierdzić, naszych *Hello World*.<br><br> ![Podsumowanie zadania](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. W okienku z wyjściem hello Zamknij.
9. Kliknij przycisk **wszystkie dzienniki** tooopen hello strumieni okienka hello zadanie elementu runbook. Firma Microsoft powinien zobaczyć tylko *Hello World* w danych wyjściowych hello strumienia, ale mogą być prezentowane z innych strumieni dla zadania elementu runbook, takie jak Verbose i błąd hello runbook toothem zapisywać dane.<br><br> ![Podsumowanie zadania](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Zamknij okienko strumieni hello i hello zadania tooreturn toohello MyFirstRunbook okienko.
11. Kliknij przycisk **zadania** okienka zadań hello tooopen dla tego elementu runbook. Ta lista zawiera wszystkie hello zadań utworzonych przez ten element runbook. Widzimy powinien tylko jedno zadanie na liście, ponieważ tylko wystąpił hello zadania raz.<br><br> ![Zadania](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. Możesz kliknąć ten hello tooopen zadania sam okienka zadania, które możemy wyświetlić przy uruchamianiu firma Microsoft hello runbook. Dzięki temu można toogo Wstecz w czasie i wyświetlenia jej szczegółów hello wszystkie zadania, które zostało utworzone dla określonego elementu runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Krok 5 — Dodawanie uwierzytelniania toomanage zasobów platformy Azure
Nasz element Runbook został przetestowany i opublikowany, ale jak do tej pory nie wykonuje on żadnych użytecznych czynności. Chcemy toohave go zarządzania zasobami Azure. Nie będzie stanie toodo, że chociaż chyba, że mamy uwierzytelniania przy użyciu poświadczeń hello określonym tooin hello [wymagania wstępne](#prerequisites). Przejdziemy z hello **Add-AzureRMAccount** polecenia cmdlet.

1. Hello Otwórz edytor tekstowy, klikając **Edytuj** w okienku hello MyFirstRunbook — przepływ pracy.<br><br> ![Edytowanie elementu Runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Firma Microsoft nie ma potrzeby hello **Write-Output** wiersz już, więc Przejdź dalej i usuń go.
3. Umieść kursor hello w nawiasach klamrowych hello pustym wierszu.
4. Wpisz lub skopiuj i Wklej hello następującego kodu, który będzie obsługiwał hello uwierzytelniania przy użyciu konta Uruchom jako automatyzacji:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Kliknij przycisk **okienku testu** tak, aby można było przetestować hello elementu runbook.
6. Kliknij przycisk **Start** toostart hello testu. Po zakończeniu działania, powinien zostać wyświetlony toohello podobne dane wyjściowe po, wyświetlania podstawowych informacji z Twojego konta. Potwierdza to, że to poświadczenie hello jest prawidłowy.<br><br> ![Uwierzytelnianie](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Krok 6 — Dodaj kod toostart maszyny wirtualnej
Teraz, gdy naszych runbook uwierzytelnia tooour subskrypcji platformy Azure, firma Microsoft mogą zarządzać zasobami. Dodamy toostart polecenia maszyny wirtualnej. Można wybrać żadnej maszyny wirtualnej w ramach subskrypcji platformy Azure, a teraz będziemy hardcoding o nazwie w elemencie runbook hello.

1. Po *Add-AzureRmAccount*, typ *Start AzureRmVM-Name "VMName" - ResourceGroupName "NameofResourceGroup"* podanie nazwy hello i nazwę grupy zasobów hello toostart maszyny wirtualnej.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Zapisz hello elementu runbook, a następnie kliknij przycisk **okienku testu** tak, aby można było przetestować go.
3. Kliknij przycisk **Start** toostart hello testu. Po zakończeniu instalacji sprawdź, czy hello maszyny wirtualnej została uruchomiona.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Krok 7 — Dodaj element runbook toohello parametru wejściowego
Nasze runbook aktualnie uruchamia hello wirtualnej maszyny, że firma Microsoft zapisane na stałe w elemencie runbook hello, ale byłoby bardziej użyteczna, jeśli firma Microsoft może określać hello maszyny wirtualnej po uruchomieniu elementu runbook hello. Teraz dodamy parametrów wejściowych toohello runbook tooprovide te funkcje.

1. Dodaj parametry *VMName* i *ResourceGroupName* toohello runbook i użyć tych zmiennych hello **Start AzureRmVM** polecenia cmdlet, jak w poniższym przykładzie hello.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Zapisz hello runbook i otwórz okienko testu hello. Należy pamiętać, że użytkownik może teraz wartości dla hello dwie zmienne wejściowe, które zostaną użyte w badaniu hello.
3. Zamknij hello okienku testu.
4. Kliknij przycisk **publikowania** toopublish hello nowej wersji elementu hello runbook.
5. Zatrzymaj hello maszyny wirtualnej, który został uruchomiony w poprzednim kroku hello.
6. Kliknij przycisk **Start** toostart hello runbook. Typ w hello **VMName** i **ResourceGroupName** dla maszyny wirtualnej hello zacząć toostart.<br><br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Po zakończeniu działania elementu runbook hello, sprawdź, czy hello maszyny wirtualnej została uruchomiona.  

## <a name="next-steps"></a>Następne kroki
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* tooget pracę z elementów runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md)
* Zobacz toolearn więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)
* Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz artykuł [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).
