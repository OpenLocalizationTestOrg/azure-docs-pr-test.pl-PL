---
title: aaaMy pierwszy graficzny element runbook automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Samouczek, który przeprowadzi Cię przez kolejne hello tworzenia, testowania i publikowania prostego graficznego elementu runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: runbook, szablon runbook, automatyzacja runbook, azure runbook
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>Mój pierwszy graficzny element Runbook

> [!div class="op_single_selector"]
> * [Element graficzny](automation-first-runbook-graphical.md)
> * [Program PowerShell](automation-first-runbook-textual-powershell.md)
> * [Przepływ pracy programu PowerShell](automation-first-runbook-textual.md)
> 
> 

Ten samouczek przedstawia tworzenie hello [graficznym elementem runbook](automation-runbook-types.md#graphical-runbooks) automatyzacji Azure.  Możemy zaczynać prosty element runbook, który testuje i publikuje podczas możemy wyjaśniają, jak tootrack hello stanu zadania elementu runbook hello.  Firma Microsoft zmodyfikowanie hello runbook tooactually zarządzania zasobami Azure, w tym przypadku uruchamiania maszyny wirtualnej platformy Azure.  Następnie możemy ukończenia samouczka hello dokonując hello runbook bardziej niezawodne, dodając parametry elementu runbook i łączy warunkowych.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy powitania po.

* Subskrypcja platformy Azure.  Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub <a href="/pricing/free-account/" target="_blank">[utworzyć bezpłatne konto](https://azure.microsoft.com/free/).
* [Konto usługi Automatyzacja Azure](automation-sec-configure-azure-runas-account.md) toohold hello elementu runbook i ich uwierzytelniać tooAzure zasobów.  To konto musi mieć uprawnienie toostart i zatrzymać hello maszyny wirtualnej.
* Maszyna wirtualna platformy Azure.  Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.

## <a name="step-1---create-runbook"></a>Krok 1. Tworzenie elementu runbook
Możemy Rozpocznij od utworzenia prosty element runbook, która wyświetla tekst hello *Hello World*.

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.  
   Strona kont automatyzacji Hello zapewnia szybki przegląd hello zasobów na tym koncie.  Konto powinno mieć już pewne elementy zawartości.  Większość tych to hello modułów, które są automatycznie umieszczane w koncie automatyzacji.  Należy również zaznaczyć zasób poświadczeń hello, który jest wymieniony w hello [wymagania wstępne](#prerequisites).
2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.<br> ![Kontrolka Elementy Runbook](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Utwórz nowy element runbook, klikając hello **Dodaj element runbook** przycisk, a następnie **Utwórz nowy element runbook**.
4. Nadaj nazwę hello runbook hello *graficznego MyFirstRunbook*.
5. W takim przypadku zamierzamy toocreate [graficznym elementem runbook](automation-graphical-authoring-intro.md) tak wybierz **graficzny** dla **typ elementu Runbook**.<br> ![Nowy element Runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Kliknij przycisk **Utwórz** toocreate hello elementu runbook i otwórz hello edytora graficznego.

## <a name="step-2---add-activities-toohello-runbook"></a>Krok 2 — Dodawanie działań toohello runbook
Hello formant biblioteki po lewej stronie powitania hello Edytor umożliwia tooselect działania tooadd tooyour runbook.  Zamierzamy tooadd **Write-Output** polecenia cmdlet toooutput tekst z hello elementu runbook.

1. W hello formant biblioteki, kliknij pole tekstowe wyszukiwania hello i wpisz **Write-Output**.  wyniki wyszukiwania Hello zostaną wyświetlone poniżej. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Przewiń w dół toohello dolnej części listy hello.  Można albo kliknij prawym przyciskiem myszy **Write-Output** i wybierz **dodać toocanvas** lub kliknij przycisk Dalej cmdlet toohello hello elipsy, a następnie wybierz **dodać toocanvas**.
3. Kliknij przycisk hello **Write-Output** działania na powitania kanwy.  Spowoduje to otwarcie bloku kontroli konfiguracji hello, co pozwala tooconfigure hello działania.
4. Witaj **etykiety** domyślne nazwy toohello hello polecenia cmdlet, ale można zmienić go toosomething bardziej przyjazna dla użytkownika. Zmień ją za*toooutput zapisu Hello World*.
5. Kliknij przycisk **parametry** tooprovide wartości parametrów hello polecenia cmdlet.  
   Niektóre polecenia cmdlet mają wiele zestawów parametrów i trzeba tooselect których możesz jeden toouse. W takim przypadku **Write-Output** ma tylko jeden zestaw parametrów, więc nie trzeba tooselect jeden. <br> ![Właściwości polecenia Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Wybierz hello **InputObject** parametru.  To parametr hello gdzie strumienia wyjściowego toohello toosend tekst hello jest określona.
7. W hello **źródła danych** listy rozwijanej wybierz **wyrażenie programu PowerShell**.  Witaj **źródła danych** lista rozwijana zawiera różne źródła służącego toopopulate wartość parametru.  
   Możesz używać danych wyjściowych ze źródeł, takich jak inne działanie, element zawartości usługi Automation lub wyrażenie programu PowerShell.  W takim przypadku chcemy tylko tekst hello toooutput *Hello World*. Możemy użyć wyrażenia programu PowerShell i wprowadzić ciąg.
8. W hello **wyrażenie** wpisz *"Hello World"* , a następnie kliknij przycisk **OK** dwukrotnie tooreturn toohello kanwy.<br> ![Wyrażenie programu PowerShell](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Zapisz element runbook hello, klikając **zapisać**.<br> ![Zapisywanie elementu Runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Krok 3 - Test hello runbook
Zanim firma Microsoft publikować hello runbook toomake go dostępne w środowisku produkcyjnym, chcemy tootest on toomake się upewnić, że działa on prawidłowo.  Testowanie elementu Runbook polega na uruchomieniu jego **wersji roboczej** i interaktywnym przejrzeniu danych wyjściowych.

1. Kliknij przycisk **okienku testu** tooopen hello testu bloku.<br> ![Okienko testowania](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Kliknij przycisk **Start** toostart hello testu.  Powinno to być hello włączyć tylko opcję.
3. A [zadanie elementu runbook](automation-runbook-execution.md) jest tworzony i jej stanie wyświetlony w okienku hello.  
   Stan zadania Hello rozpoczyna się jako *w kolejce* wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.  Następnie przesyłane za*uruchamianie* gdy pracownik oświadczeń hello zadania, a następnie *systemem* , gdy element runbook hello faktycznie zacznie działać.  
4. Po zakończeniu zadania elementu runbook hello jego dane wyjściowe są wyświetlane. W naszym przypadku powinien być widoczny ciąg *Witaj, świecie*.<br> ![Witaj, świecie](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Zamknij hello testu bloku tooreturn toohello kanwy.

## <a name="step-4---publish-and-start-hello-runbook"></a>Krok 4 — publikowanie i uruchomić hello elementu runbook
utworzyliśmy runbook Hello jest nadal w trybie wersji roboczej. Potrzebujemy toopublish go przed możemy można uruchomić w środowisku produkcyjnym.  Podczas publikowania elementu runbook, należy zastąpić hello istniejącej opublikowanej wersji hello wersję roboczą.  W tym przypadku nie mamy wersję opublikowaną jeszcze ponieważ właśnie utworzyliśmy hello elementu runbook.

1. Kliknij przycisk **publikowania** toopublish hello runbook, a następnie **tak** po wyświetleniu monitu.<br> ![Publikowanie](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Podczas przewijania tooview po lewej stronie powitania runbook w programie hello **elementów Runbook** bloku pokazuje **stan pisania przyp** z **opublikowano**.
3. Przewijania wstecz toohello prawo tooview hello bloku **MyFirstRunbook**.  
   Witaj opcje górze hello zezwolić nam toostart hello runbook, zaplanowane toostart w czasie w przyszłości hello lub tworzenia [elementu webhook](automation-webhooks.md) , może być uruchamiany za pośrednictwem połączenia HTTP.
4. Chcemy tylko toostart hello runbook więc klikamy **Start** , a następnie **tak** po wyświetleniu monitu.<br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Zadanie elementu runbook hello utworzonej został otwarty bloku zadania.  Możemy zamknąć ten blok, ale w takim przypadku możemy zostawić otwarty, możemy obserwować postęp hello zadania.
6. Stan zadania Hello jest wyświetlany w **Podsumowanie zadania** i dopasowań hello stany widzieliśmy po przetestowaliśmy hello elementu runbook.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Raz hello pokazuje stan elementu runbook *Ukończono*, kliknij przycisk **dane wyjściowe**. Hello **dane wyjściowe** bloku jest otwarty i zobaczysz naszych *Hello World* w okienku hello.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Zamknij hello bloku danych wyjściowych.
9. Kliknij przycisk **wszystkie dzienniki** tooopen hello strumieni bloku hello zadanie elementu runbook.  Firma Microsoft powinien zobaczyć tylko *Hello World* w danych wyjściowych hello strumienia, ale mogą być prezentowane z innych strumieni dla zadania elementu runbook, takie jak Verbose i błąd hello runbook toothem zapisywać dane.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Zamknij hello wszystkie dzienniki bloku i hello zadania bloku tooreturn toohello MyFirstRunbook bloku.
11. Kliknij przycisk **zadania** bloku zadania hello tooopen dla tego elementu runbook.  Ta lista zawiera wszystkie zadania hello utworzone przez ten element runbook. Widzimy powinien tylko jedno zadanie na liście, ponieważ tylko wystąpił hello zadania raz.<br> ![Zadania](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Po kliknięciu tego zadania tooopen hello tego samego okienka zadania, które możemy wyświetlić rozpoczęcie firma Microsoft hello elementu runbook.  Dzięki temu można toogo Wstecz w czasie i wyświetlenia jej szczegółów hello wszystkie zadania, które zostało utworzone dla określonego elementu runbook.

## <a name="step-5---create-variable-assets"></a>Krok 5. Tworzenie zmiennych elementów zawartości
Nasz element Runbook został przetestowany i opublikowany, ale jak do tej pory nie wykonuje on żadnych użytecznych czynności. Chcemy toohave go zarządzania zasobami Azure.  Przed skonfigurowanie hello tooauthenticate elementu runbook, możemy utworzyć identyfikator subskrypcji hello toohold zmiennej i odwołaj się po skonfigurowanie hello tooauthenticate działania w kroku 6 poniżej.  W tym kontekście subskrypcji toohello odwołanie umożliwia tooeasily pracy między wiele subskrypcji.  Przed kontynuowaniem należy skopiować identyfikator subskrypcji z hello opcji subskrypcji hello okienka nawigacji.  

1. W bloku konta automatyzacji powitania kliknij hello **zasoby** Kafelek i hello **zasoby** bloku jest otwarty.
2. W bloku zasobów powitania kliknij hello **zmienne** kafelka.
3. W bloku zmienne hello, kliknij **dodać zmienną**.<br>![Zmienna usługi Automation](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. W hello nowej zmiennej bloku, w hello **nazwa** wprowadź **AzureSubscriptionId** w hello **wartość** wprowadź identyfikator subskrypcji.  Zachowaj *ciąg* dla hello **typu** i wartość domyślną hello **szyfrowania**.  
5. Kliknij przycisk **Utwórz** toocreate hello zmiennej.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Krok 6 — Dodawanie uwierzytelniania toomanage zasobów platformy Azure
Teraz, gdy mamy zmiennej toohold naszych identyfikator subskrypcji można skonfigurować naszych tooauthenticate elementu runbook z hello Uruchom jako poświadczeniami, które są hello określonego tooin [wymagania wstępne](#prerequisites).  Przejdziemy przez dodanie hello Uruchom jako platformy Azure połączenia **zasobów** i **Add-AzureRMAccount** kanwy toohello polecenia cmdlet.  

1. Otwórz hello edytora graficznego klikając **Edytuj** na powitania MyFirstRunbook bloku.<br> ![Edytowanie elementu Runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Firma Microsoft nie ma potrzeby hello **toooutput zapisu Hello World** , więc kliknij go prawym przyciskiem myszy i wybierz **usunąć**.
3. W hello kontroli biblioteka, rozwiń węzeł **połączeń** i Dodaj **AzureRunAsConnection** toohello kanwy, wybierając **dodać toocanvas**.
4. Na kanwie hello wybierz **AzureRunAsConnection** w Panelu sterowania konfiguracji hello wpisz **uzyskać Uruchom jako połączenia** w hello **etykiety** pola tekstowego.  Jest to połączenie hello
5. W hello formant biblioteki, wpisz **Add-AzureRmAccount** w polu tekstowym wyszukiwania hello.
6. Dodaj **Add-AzureRmAccount** toohello kanwy.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Umieść kursor nad **uzyskać Uruchom jako połączenia** aż koło pojawi się na dole hello hello kształtu. Kliknięcie okręgu hello i przeciągnięcie strzałki hello zbyt**Add-AzureRmAccount**.  Strzałka Hello, które utworzono jest *łącze*.  rozpoczyna się od elementu runbook Hello **uzyskać Uruchom jako połączenia** , a następnie uruchom **Add-AzureRmAccount**.<br> ![Tworzenie połączenia między działaniami](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Na kanwie hello wybierz **Add-AzureRmAccount** i hello konfiguracji umożliwia sterowanie typu okienko **tooAzure logowania** w hello **etykiety** pola tekstowego.
9. Kliknij przycisk **parametry** i zostanie wyświetlony blok konfigurację parametru działania hello.
10. **Dodaj-AzureRmAccount** ma wiele zestawów parametrów, potrzebujemy tooselect jedną przed możemy podać wartości parametrów.  Kliknij przycisk **ustawić parametr** , a następnie wybierz hello **ServicePrincipalCertificatewithSubscriptionId** zestaw parametrów.
11. Po wybraniu zestaw parametrów hello hello parametry są wyświetlane w bloku konfigurację parametru działania hello.  Kliknij pozycję **APPLICATIONID**.<br> ![Dodawanie parametrów konta usługi Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. W bloku wartość parametru hello, wybierz **dane wyjściowe działania** dla hello **źródła danych** i wybierz **uzyskać Uruchom jako połączenia** z listy hello w hello **pola ścieżka** typu pole tekstowe **ApplicationId**, a następnie kliknij przycisk **OK**.  Firma Microsoft są określanie hello nazwy właściwości hello hello pole ścieżki, ponieważ obiekt o właściwości wielu danych wyjściowych działania hello.
13. Kliknij przycisk **CERTIFICATETHUMBPRINT**i wybierz w bloku wartość parametru hello **dane wyjściowe działania** dla hello **źródła danych**.  Wybierz **uzyskać Uruchom jako połączenia** z listy hello w hello **ścieżkę pola** typu pole tekstowe **CertificateThumbprint**, a następnie kliknij przycisk **OK**.
14. Kliknij przycisk **SERVICEPRINCIPAL**i wybierz w bloku wartość parametru hello **ConstantValue** dla hello **źródła danych**, kliknij opcję hello **True**, a następnie kliknij przycisk **OK**.
15. Kliknij przycisk **TENANTID**i wybierz w bloku wartość parametru hello **dane wyjściowe działania** dla hello **źródła danych**.  Wybierz **uzyskać Uruchom jako połączenia** z listy hello w hello **ścieżkę pola** typu pole tekstowe **identyfikatora dzierżawcy**, a następnie kliknij przycisk **OK** dwa razy.  
16. W hello formant biblioteki, wpisz **Set-AzureRmContext** w polu tekstowym wyszukiwania hello.
17. Dodaj **Set-AzureRmContext** toohello kanwy.
18. Na kanwie hello wybierz **Set-AzureRmContext** i hello konfiguracji umożliwia sterowanie typu okienko **Określ identyfikator subskrypcji** w hello **etykiety** pola tekstowego.
19. Kliknij przycisk **parametry** i zostanie wyświetlony blok konfigurację parametru działania hello.
20. **Set-AzureRmContext** ma wiele zestawów parametrów, potrzebujemy tooselect jedną przed możemy podać wartości parametrów.  Kliknij przycisk **ustawić parametr** , a następnie wybierz hello **SubscriptionId** zestaw parametrów.  
21. Po wybraniu zestaw parametrów hello hello parametry są wyświetlane w bloku konfigurację parametru działania hello.  Kliknij pozycję **SubscriptionID**.
22. W bloku wartość parametru hello, wybierz **zasób zmiennej** dla hello **źródła danych** i wybierz **AzureSubscriptionId** z listy hello, a następnie kliknij przycisk **OK**  dwa razy.   
23. Umieść kursor nad **tooAzure logowania** aż koło pojawi się na dole hello hello kształtu. Kliknięcie okręgu hello i przeciągnięcie strzałki hello zbyt**Określ identyfikator subskrypcji**.

Element runbook powinien wyglądać hello na tym etapie następujące: <br>![Konfiguracja uwierzytelniania elementu Runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Krok 7 — dodawanie toostart działania maszyny wirtualnej
W tym miejscu możemy dodać **Start AzureRmVM** toostart działania maszyny wirtualnej.  Można wybrać żadnej maszyny wirtualnej w Twojej subskrypcji platformy Azure i teraz należy umieszczaj nazwy do polecenia cmdlet hello.

1. W hello formant biblioteki, wpisz **Start-AzureRm** w polu tekstowym wyszukiwania hello.
2. Dodaj **Start AzureRmVM** toohello obszaru roboczego, a następnie kliknij i przeciągnij go pod **Określ identyfikator subskrypcji**.
3. Umieść kursor nad **Określ identyfikator subskrypcji** aż koło pojawi się na dole hello hello kształtu.  Kliknięcie okręgu hello i przeciągnięcie strzałki hello zbyt**Start AzureRmVM**.
4. Wybierz pozycję **Start-AzureRmVM**.  Kliknij przycisk **parametry** , a następnie **ustawić parametr** ustawia tooview hello **Start AzureRmVM**.  Wybierz hello **ResourceGroupNameParameterSetName** zestaw parametrów. Zwróć uwagę, że obok parametrów **ResourceGroupName** i **Name** znajdują się wykrzykniki.  Oznacza to, że te parametry są wymagane.  Oczekiwane wartości obu parametrów to ciągi.
5. Wybierz pozycję **Nazwa**.  Wybierz **wyrażenie programu PowerShell** dla hello **źródła danych** i wpisz nazwę hello maszyny wirtualnej hello ujęty w cudzysłów, uruchamianych z tego elementu runbook.  Kliknij przycisk **OK**.<br>![Wartość parametru Name pozycji Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Wybierz pozycję **ResourceGroupName**. Użyj **wyrażenie programu PowerShell** dla hello **źródła danych** i wpisz nazwę hello grupy zasobów hello ujęty w cudzysłów.  Kliknij przycisk **OK**.<br> ![Parametry polecenia Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Kliknij okienko testu, aby można było przetestować element runbook hello.
8. Kliknij przycisk **Start** toostart hello testu.  Po zakończeniu instalacji sprawdź, czy hello maszyny wirtualnej została uruchomiona.

Element runbook powinien wyglądać hello na tym etapie następujące: <br>![Konfiguracja uwierzytelniania elementu Runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Krok 8 — Dodawanie dodatkowych parametrów wejściowych toohello runbook
Obecnie naszych runbook uruchomi hello maszyny wirtualnej w grupie zasobów hello określoną w hello **Start AzureRmVM** polecenia cmdlet.  Nasze runbook będą bardziej użyteczna, jeśli firma Microsoft może określić po uruchomieniu elementu runbook hello.  Teraz dodamy parametrów wejściowych toohello runbook tooprovide te funkcje.

1. Otwórz hello edytora graficznego klikając **Edytuj** na powitania **MyFirstRunbook** okienka.
2. Kliknij przycisk **dane wejściowe i wyjściowe** , a następnie **dodać dane wejściowe** tooopen hello parametr wejściowy elementu Runbook okienka.<br> ![Wejście i wyjście elementu Runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Określ *VMName* dla hello **nazwa**.  Zachowaj *ciąg* dla hello **typu**, ale zmienić **obowiązkowe** zbyt*tak*.  Kliknij przycisk **OK**.
4. Utworzyć drugi wymaganego parametru wejściowego o nazwie *ResourceGroupName* , a następnie kliknij przycisk **OK** tooclose hello **wejściowa i wyjściowa** okienka.<br> ![Parametry wejściowe elementu Runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Wybierz hello **Start AzureRmVM** działania, a następnie kliknij przycisk **parametry**.
6. Zmień hello **źródła danych** dla **nazwa** za**dane wejściowe elementu Runbook** , a następnie wybierz **VMName**.<br>
7. Zmień hello **źródła danych** dla **ResourceGroupName** za**dane wejściowe elementu Runbook** , a następnie wybierz **ResourceGroupName**.<br> ![Parametry polecenia Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Zapisz hello runbook i otwórz okienko testu hello.  Należy pamiętać, że użytkownik może teraz wartości dla hello dwie zmienne wejściowe, używane w teście hello.
9. Zamknij hello okienku testu.
10. Kliknij przycisk **publikowania** toopublish hello nowej wersji elementu hello runbook.
11. Zatrzymaj hello maszyny wirtualnej, który został uruchomiony w poprzednim kroku hello.
12. Kliknij przycisk **Start** toostart hello runbook.  Typ w hello **VMName** i **ResourceGroupName** dla maszyny wirtualnej hello zacząć toostart.<br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Po zakończeniu działania elementu runbook hello, sprawdź, czy hello maszyny wirtualnej została uruchomiona.

## <a name="step-9---create-a-conditional-link"></a>Krok 9. Tworzenie połączenia warunkowego
Firma Microsoft teraz zmodyfikować hello elementu runbook, tak aby tylko spróbuje maszyny wirtualnej hello toostart Jeśli nie jest już uruchomiona.  Można to zrobić przez dodanie **Get-AzureRmVM** runbook toohello polecenia cmdlet, który pobiera stan poziomu wystąpienia hello hello maszyny wirtualnej. Następnie dodaj kod przepływu pracy programu PowerShell modułu o nazwie **pobierania stanu** z fragment programu PowerShell code toodetermine, jeśli stan maszyny wirtualnej hello jest uruchomiony lub zatrzymany.  Łączy warunkowych z hello **pobierania stanu** działa tylko w module **Start AzureRmVM** Jeśli hello bieżący stan działania zostanie zatrzymana.  Na koniec mamy output tooinform wiadomość hello Jeśli hello maszyna wirtualna została pomyślnie uruchomiona lub nie przy użyciu polecenia cmdlet programu PowerShell Write-Output.

1. Otwórz **MyFirstRunbook** hello edytora graficznego.
2. Usuń łącze hello między **Określ identyfikator subskrypcji** i **Start AzureRmVM** kliknij go, a następnie naciskając klawisz hello *usunąć* klucza.
3. W hello formant biblioteki, wpisz **Get-AzureRm** w polu tekstowym wyszukiwania hello.
4. Dodaj **Get-AzureRmVM** toohello kanwy.
5. Wybierz **Get-AzureRmVM** , a następnie **ustawić parametr** ustawia tooview hello **Get-AzureRmVM**.  Wybierz hello **GetVirtualMachineInResourceGroupNameParamSet** zestaw parametrów.  Zwróć uwagę, że obok parametrów **ResourceGroupName** i **Name** znajdują się wykrzykniki.  Oznacza to, że te parametry są wymagane.  Oczekiwane wartości obu parametrów to ciągi.
6. W obszarze **Źródło danych** dla pozycji **Name** wybierz pozycję **Wejście elementu Runbook**, a następnie wybierz pozycję **VMName**.  Kliknij przycisk **OK**.
7. W obszarze **Źródło danych** dla pozycji **ResourceGroupName** wybierz pozycję **Wejście elementu Runbook**, a następnie wybierz pozycję **ResourceGroupName**.  Kliknij przycisk **OK**.
8. W obszarze **Źródło danych** dla pozycji **Stan** wybierz opcję **Stała wartość**, a następnie kliknij pozycję **Prawda**.  Kliknij przycisk **OK**.  
9. Utwórz łącze między **Określ identyfikator subskrypcji** za**Get-AzureRmVM**.
10. W formancie biblioteki hello, rozwiń węzeł **sterowanie elementem Runbook** i Dodaj **kod** toohello kanwy.  
11. Utwórz łącze między **Get-AzureRmVM** za**kod**.  
12. Kliknij przycisk **kod** i w okienku konfiguracji hello zmienić etykietę zbyt**pobierania stanu**.
13. Wybierz **kod** parametr i hello **edytora kodu** zostanie wyświetlony blok.  
14. W edytorze kodu hello Wklej hello następującego fragmentu kodu:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Utwórz łącze między **pobierania stanu** za**Start AzureRmVM**.<br> ![Element Runbook z modułem kodu](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Wybierz łącze hello i w okienku konfiguracji hello, zmień **zastosować warunek** za**tak**.   Łącze hello notatki włącza wiersz tooa kreskowane wskazujący, że działania docelowego hello działa tylko wtedy, jeśli warunek hello rozpoznaje tootrue.  
17. Dla hello **warunku wyrażenia**, typ *$ActivityOutput ["Pobierz stan"] - eq "ZATRZYMANO"*.  **Początek AzureRmVM** działa teraz tylko po zatrzymaniu hello maszyny wirtualnej.
18. W hello kontroli biblioteka, rozwiń węzeł **poleceń cmdlet** , a następnie **Microsoft.PowerShell.Utility**.
19. Dodaj **Write-Output** kanwy toohello dwa razy.<br> ![Element Runbook z pozycją Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Na powitania pierwszy **Write-Output** sterowania, kliknij przycisk **parametry** i zmień hello **etykiety** wartość zbyt*powiadomić uruchomiona maszyna wirtualna*.
21. Dla **InputObject**, zmień **źródła danych** za**wyrażenie programu PowerShell** oraz typ w wyrażeniu hello *"$VMName została pomyślnie uruchomiona."* .
22. Na powitania drugi **Write-Output** sterowania, kliknij przycisk **parametry** i zmień hello **etykiety** wartość zbyt*powiadomić wirtualna uruchomić nie powiodło się*
23. Dla **InputObject**, zmień **źródła danych** za**wyrażenie programu PowerShell** oraz typ w wyrażeniu hello *"$VMName nie można uruchomić."* .
24. Utwórz łącze między **Start AzureRmVM** za**powiadomić uruchomiona maszyna wirtualna** i **powiadomić wirtualna uruchomić nie powiodło się**.
25. Wybierz łącze hello zbyt**powiadomić uruchomiona maszyna wirtualna** i zmienić **zastosować warunek** za**True**.
26. Dla hello **warunku wyrażenia**, typ *$ActivityOutput ["AzureRmVM Start"]. IsSuccessStatusCode - eq $true*.  Write-Output kontrolować działa teraz tylko, jeśli hello maszyny wirtualnej została pomyślnie uruchomiona.
27. Wybierz łącze hello zbyt**powiadomić wirtualna uruchomić nie powiodło się** i zmienić **zastosować warunek** za**True**.
28. Dla hello **warunku wyrażenia**, typ *$ActivityOutput ["AzureRmVM Start"]. IsSuccessStatusCode - ne $true*.  Write-Output teraz kontroli tylko wtedy, jeśli hello maszyny wirtualnej nie została pomyślnie uruchomiona.
29. Zapisz hello runbook i otwórz okienko testu hello.
30. Uruchom element runbook hello z maszyną wirtualną hello zatrzymana, a powinna być uruchamiana.

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat tworzenia graficznego [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md)
* tooget pracę z elementów runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)

