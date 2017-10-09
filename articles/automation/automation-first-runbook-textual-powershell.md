---
title: aaaMy pierwszy PowerShell elementu runbook automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Samouczek, który przeprowadzi Cię przez kolejne hello tworzenia, testowania i publikowania z prostego elementu runbook programu PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: azure powershell, samouczek skryptu programu powershell, automatyzacja programu powershell
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Mój pierwszy element Runbook programu PowerShell

> [!div class="op_single_selector"]
> * [Element graficzny](automation-first-runbook-graphical.md)
> * [Program PowerShell](automation-first-runbook-textual-powershell.md)
> * [Przepływ pracy programu PowerShell](automation-first-runbook-textual.md)
> 
> 

Ten samouczek przedstawia tworzenie hello [runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) automatyzacji Azure. Możemy zaczynać prosty element runbook, który możemy testowanie i publikowanie podczas możemy wyjaśniają, jak tootrack hello stanu zadania elementu runbook hello. Firma Microsoft zmodyfikowanie hello runbook tooactually zarządzania zasobami Azure, w tym przypadku uruchamiania maszyny wirtualnej platformy Azure. Ponadto wykonujemy hello runbook bardziej niezawodne, dodając parametry elementu runbook.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).
* [Konto automatyzacji](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.  To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.
* Maszyna wirtualna platformy Azure. Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.

## <a name="step-1---create-new-runbook"></a>Krok 1. Tworzenie nowego elementu Runbook
Zaczniemy przez utworzenie prostego elementu runbook, która wyświetla tekst hello *Hello World*.

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.  
   Strona kont automatyzacji Hello zapewnia szybki przegląd hello zasobów na tym koncie. Konto powinno mieć już pewne elementy zawartości. Większość tych to hello modułów, które są automatycznie umieszczane w koncie automatyzacji. Należy również zaznaczyć zasób poświadczeń hello, który jest wymieniony w hello [wymagania wstępne](#prerequisites).
2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Utwórz nowy element runbook, klikając hello **Dodaj element runbook** przycisk, a następnie **Utwórz nowy element runbook**.
4. Nadaj nazwę hello runbook hello *MyFirstRunbook PowerShell*.
5. W takim przypadku zamierzamy toocreate [runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) tak wybierz **Powershell** dla **typ elementu Runbook**.<br><br> ![Typ elementu Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Kliknij przycisk **Utwórz** toocreate hello elementu runbook i hello Otwórz edytor tekstowy.

## <a name="step-2---add-code-toohello-runbook"></a>Krok 2 — Dodaj kod toohello runbook
Można albo kod typu bezpośrednio do elementu runbook hello, lub można wybrać polecenia cmdlet, elementy runbook i zasoby z hello formant biblioteki i ich dodano toohello runbook za pomocą parametrów powiązanych. W ramach tego przewodnika, możemy wpisz bezpośrednio w elemencie runbook hello.

1. Nasz element Runbook jest obecnie pusty. Wpisz *Write-Output „Witaj, świecie”*.<br><br> ![Witaj, świecie](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Zapisz element runbook hello, klikając **zapisać**.<br><br> ![Przycisk Zapisz](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Krok 3 - Test hello runbook
Zanim firma Microsoft publikować hello runbook toomake go dostępne w środowisku produkcyjnym, chcemy tootest on toomake się upewnić, że działa on prawidłowo. Testowanie elementu Runbook polega na uruchomieniu jego **wersji roboczej** i interaktywnym przejrzeniu danych wyjściowych.

1. Kliknij przycisk **okienku testu** tooopen hello testu okienka.<br><br> ![Okienko testowania](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Kliknij przycisk **Start** toostart hello testu. Powinno to być hello włączyć tylko opcję.
3. Zostanie utworzone [zadanie elementu Runbook](automation-runbook-execution.md) i pojawi się jego stan.  
   Stan zadania Hello rozpoczyna się jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toocome chmury hello dostępne. Będzie on przenoszony za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.  
4. Po zakończeniu zadania elementu runbook hello jego dane wyjściowe są wyświetlane. W naszym przypadku powinien być widoczny ciąg *Witaj, świecie*.<br><br> ![Dane wyjściowe w okienku testowania](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Zamknij hello testu okienku tooreturn toohello kanwy.

## <a name="step-4---publish-and-start-hello-runbook"></a>Krok 4 — publikowanie i uruchomić hello elementu runbook
utworzyliśmy runbook Hello jest nadal w trybie wersji roboczej. Potrzebujemy toopublish go przed możemy można uruchomić w środowisku produkcyjnym.  Podczas publikowania elementu runbook, należy zastąpić hello istniejącej opublikowanej wersji hello wersję roboczą.  W tym przypadku nie mamy wersję opublikowaną jeszcze ponieważ właśnie utworzyliśmy hello elementu runbook.

1. Kliknij przycisk **publikowania** toopublish hello runbook, a następnie **tak** po wyświetleniu monitu.<br><br> ![Przycisk Opublikuj](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Podczas przewijania tooview po lewej stronie powitania runbook w programie hello **elementów Runbook** okienko teraz, zostanie wyświetlona **stan pisania przyp** z **opublikowano**.
3. Przewijania wstecz toohello prawo tooview hello okienka **MyFirstRunbook PowerShell**.  
   Hello opcje górze hello zezwolić nam toostart hello runbook, wyświetlanie hello runbook, zaplanowane toostart w czasie w przyszłości hello lub utworzyć [webhook](automation-webhooks.md) , można go uruchomić za pomocą wywołania HTTP.
4. Firma Microsoft ma toostart hello runbook, więc klikamy **Start** , a następnie kliknij przycisk **Ok** po otwarciu hello Start bloku elementu Runbook.<br><br> ![Przycisk Uruchom](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Okienko zadania jest otwarty dla zadania elementu runbook hello utworzyliśmy. Możemy zamknąć w tym okienku, ale w takim przypadku możemy zostawić otwarty, możemy obserwować postęp hello zadania.
6. Stan zadania Hello jest wyświetlany w **Podsumowanie zadania** i dopasowań hello stany widzieliśmy po przetestowaliśmy hello elementu runbook.<br><br> ![Podsumowanie zadania](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Raz hello pokazuje stan elementu runbook *Ukończono*, kliknij przycisk **dane wyjściowe**. w okienku z wyjściem Hello jest otwarty i możemy stwierdzić, naszych *Hello World*.<br><br> ![Dane wyjściowe zadania](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. W okienku z wyjściem hello Zamknij.
9. Kliknij przycisk **wszystkie dzienniki** tooopen hello strumieni okienka hello zadanie elementu runbook. Firma Microsoft powinien zobaczyć tylko *Hello World* w danych wyjściowych hello strumienia, ale mogą być prezentowane z innych strumieni dla zadania elementu runbook, takie jak Verbose i błąd hello runbook toothem zapisywać dane.<br><br> ![Wszystkie dzienniki](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Zamknij hello strumieni okienka i hello zadanie w okienku tooreturn toohello MyFirstRunbook PowerShell.
11. Kliknij przycisk **zadania** okienka zadań hello tooopen dla tego elementu runbook. Ta lista zawiera wszystkie hello zadań utworzonych przez ten element runbook. Widzimy powinien tylko jedno zadanie na liście, ponieważ tylko wystąpił hello zadania raz.<br><br> ![Lista zadań](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Po kliknięciu tego zadania tooopen hello tego samego okienka zadania, które możemy wyświetlić rozpoczęcie firma Microsoft hello elementu runbook. Dzięki temu można toogo Wstecz w czasie i wyświetlenia jej szczegółów hello wszystkie zadania, które zostało utworzone dla określonego elementu runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Krok 5 — Dodawanie uwierzytelniania toomanage zasobów platformy Azure
Nasz element Runbook został przetestowany i opublikowany, ale jak do tej pory nie wykonuje on żadnych użytecznych czynności. Chcemy toohave go zarządzania zasobami Azure. Nie będzie stanie toodo, że chociaż chyba, że mamy uwierzytelniania przy użyciu poświadczeń hello określonym tooin hello [wymagania wstępne](#prerequisites). Przejdziemy z hello **Add-AzureRmAccount** polecenia cmdlet.

1. Hello Otwórz edytor tekstowy, klikając **Edytuj** w okienku hello MyFirstRunbook PowerShell.<br><br> ![Edytowanie elementu Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Firma Microsoft nie ma potrzeby hello **Write-Output** wiersz już, więc Przejdź dalej i usuń go.
3. Wpisz lub skopiuj i Wklej powitania po kod obsługujący hello uwierzytelniania przy użyciu konta Uruchom jako automatyzacji:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Kliknij przycisk **okienku testu** tak, aby można było przetestować hello elementu runbook.
5. Kliknij przycisk **Start** toostart hello testu. Po zakończeniu działania, powinien zostać wyświetlony toohello podobne dane wyjściowe po, wyświetlania podstawowych informacji z Twojego konta. Potwierdza to, że to poświadczenie hello jest prawidłowy.<br><br> ![Uwierzytelnianie](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Krok 6 — Dodaj kod toostart maszyny wirtualnej
Teraz, gdy naszych runbook uwierzytelnia tooour subskrypcji platformy Azure, firma Microsoft mogą zarządzać zasobami. Dodamy toostart polecenia maszyny wirtualnej. Można wybrać żadnej maszyny wirtualnej w ramach subskrypcji platformy Azure, a obecnie firma Microsoft będzie kodowania takiej nazwie w elemencie runbook hello.

1. Po *Add-AzureRmAccount*, typ *Start AzureRmVM-Name "VMName" - ResourceGroupName "NameofResourceGroup"* podanie nazwy hello i nazwę grupy zasobów hello toostart maszyny wirtualnej.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Zapisz hello elementu runbook, a następnie kliknij przycisk **okienku testu** tak, aby można było przetestować go.
3. Kliknij przycisk **Start** toostart hello testu. Po zakończeniu instalacji sprawdź, czy hello maszyny wirtualnej została uruchomiona.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Krok 7 — Dodaj element runbook toohello parametru wejściowego
Nasze runbook aktualnie uruchamia hello wirtualnej maszyny, że firma Microsoft zapisane na stałe w elemencie runbook hello, ale byłoby bardziej użyteczna, jeśli określono hello maszyny wirtualnej po uruchomieniu elementu runbook hello. Teraz dodamy parametrów wejściowych toohello runbook tooprovide te funkcje.

1. Dodaj parametry *VMName* i *ResourceGroupName* toohello runbook i użyć tych zmiennych hello **Start AzureRmVM** polecenia cmdlet, jak w poniższym przykładzie hello.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Zapisz hello runbook i otwórz okienko testu hello. Możesz teraz podać wartości dla Witaj dwie zmienne wejściowe, które są używane w teście hello.
3. Zamknij hello okienku testu.
4. Kliknij przycisk **publikowania** toopublish hello nowej wersji elementu hello runbook.
5. Zatrzymaj hello maszyny wirtualnej, który został uruchomiony w poprzednim kroku hello.
6. Kliknij przycisk **Start** toostart hello runbook. Typ w hello **VMName** i **ResourceGroupName** dla maszyny wirtualnej hello zacząć toostart.<br><br> ![Przekazywanie parametru](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Po zakończeniu działania elementu runbook hello, sprawdź, czy hello maszyny wirtualnej została uruchomiona.

## <a name="differences-from-powershell-workflow"></a>Różnice w stosunku do przepływu pracy programu PowerShell
Elementy runbook programu PowerShell mają hello sam cykl życia, możliwości i zarządzanie jako elementy runbook przepływu pracy programu PowerShell, ale istnieją pewne różnice i ograniczenia:

1. Uruchom szybkie tooPowerShell porównaniu elementach runbook przepływu pracy kroku kompilacji nie ma elementów runbook programu PowerShell.
2. Elementy runbook przepływu pracy programu PowerShell obsługi punkty kontrolne, za pomocą punktów kontrolnych, elementów runbook przepływu pracy programu PowerShell można wznowić z dowolnego punktu w elemencie runbook hello, natomiast elementy runbook programu PowerShell tylko można wznowić od początku hello.
3. Elementy Runbook przepływu pracy programu PowerShell obsługują wykonywanie równoległe i szeregowe, natomiast elementy Runbook programu PowerShell mogą wykonywać polecenia tylko szeregowo.
4. W elemencie Runbook przepływu pracy programu PowerShell działanie, polecenie lub blok skryptu może mieć własny obszar działania, a w elemencie Runbook programu PowerShell wszystkie elementy skryptu są uruchamiane w jednym obszarze działania. Istnieją również pewne [różnice składniowe](https://technet.microsoft.com/magazine/dn151046.aspx) między natywnym elementem Runbook programu PowerShell i elementem Runbook przepływu pracy programu PowerShell.

## <a name="next-steps"></a>Następne kroki
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
* Zobacz tooknow więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)
* Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz artykuł [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).

