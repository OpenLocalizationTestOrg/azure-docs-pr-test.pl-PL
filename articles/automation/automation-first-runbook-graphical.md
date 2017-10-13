---
title: "Mój pierwszy graficzny element Runbook w usłudze Azure Automation | Microsoft Docs"
description: "Samouczek, który przeprowadzi Cię przez procesy tworzenia, testowania i publikowania prostego graficznego elementu Runbook."
services: automation
documentationcenter: 
author: eslesar
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
ms.openlocfilehash: b8accf16c43b7a01233742161e68db6f831a2d30
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="my-first-graphical-runbook"></a>Mój pierwszy graficzny element Runbook

> [!div class="op_single_selector"]
> * [Element graficzny](automation-first-runbook-graphical.md)
> * [Program PowerShell](automation-first-runbook-textual-powershell.md)
> * [Przepływ pracy programu PowerShell](automation-first-runbook-textual.md)
> * [Python](automation-first-runbook-textual-python2.md)
> 

Ten samouczek przeprowadzi Cię przez proces tworzenia [graficznego elementu Runbook](automation-runbook-types.md#graphical-runbooks) w usłudze Azure Automation.  Rozpoczniemy pracę od użycia prostego elementu runbook służącego do testowania i publikowania, objaśniając równocześnie, jak śledzić stan zadania elementu runbook.  Następnie zmodyfikujemy element Runbook, aby faktycznie zarządzać zasobami platformy Azure (w tym przypadku uruchomić maszynę wirtualną platformy Azure).  Następnie zakończymy samouczek, udoskonalając element runbook przez dodanie jego parametrów i połączeń warunkowych.

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków tego samouczka niezbędne są następujące elementy:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* [Konto usługi Automation](automation-offering-get-started.md) do przechowywania elementu Runbook i uwierzytelniania w zasobach platformy Azure.  To konto musi mieć uprawnienia do uruchamiania i zatrzymywania maszyny wirtualnej.
* Maszyna wirtualna platformy Azure. Będziemy uruchamiać i zatrzymywać tę maszynę, dlatego należy użyć maszyny innej niż produkcyjna.

## <a name="step-1---create-runbook"></a>Krok 1. Tworzenie elementu runbook
Rozpoczniemy od utworzenia prostego elementu runbook służącego do wyświetlania tekstu *Hello World*.

1. W witrynie Azure Portal otwórz konto usługi Automation.  
   Strona konta usługi Automation umożliwia szybki przegląd zasobów na tym koncie.  Konto powinno mieć już pewne elementy zawartości.  Większość z nich to moduły, które są automatycznie uwzględniane na nowym koncie usługi Automation.  Powinien istnieć również element zawartości Poświadczenie wymieniony w części dotyczącej [wymagań wstępnych](#prerequisites).
2. Kliknij kafelek **Elementy runbook**, aby otworzyć listę elementów runbook.<br> ![Kontrolka Elementy Runbook](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Utwórz nowy element Runbook, klikając przycisk **Dodaj element Runbook**, a następnie pozycję **Utwórz nowy element Runbook**.
4. Nadaj elementowi Runbook nazwę *MyFirstRunbook-Graphical*.
5. W tym przypadku będziemy tworzyć [graficzny element Runbook](automation-graphical-authoring-intro.md), dlatego wybierz wartość **Element graficzny** parametru **Typ elementu Runbook**.<br> ![Nowy element Runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Kliknij pozycję **Utwórz**, aby utworzyć element Runbook i otworzyć edytor graficzny.

## <a name="step-2---add-activities-to-the-runbook"></a>Krok 2. Dodawanie działań do elementu Runbook
Kontrolka Biblioteka po lewej stronie edytora umożliwia wybranie działań do dodania do elementu Runbook.  Dodamy polecenie cmdlet **Write-Output** do tekstu wyjściowego elementu Runbook.

1. W kontrolce Biblioteka kliknij pole tekstowe wyszukiwania i wpisz **Write-Output**.  Wyniki wyszukiwania zostaną wyświetlone poniżej. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Przewiń listę w dół.  Kliknij prawym przyciskiem myszy pozycję **Write-Output** i wybierz polecenie **Dodaj do kanwy** lub kliknij wielokropek obok polecenia cmdlet, a następnie wybierz pozycję **Dodaj do kanwy**.
3. Kliknij pozycję **Write-Output** na kanwie.  Spowoduje to otwarcie bloku kontrolki Konfiguracja, który umożliwia skonfigurowanie działania.
4. Wartość pola **Etykieta** jest domyślnie ustawiana na nazwę polecenia cmdlet, ale możemy zmienić ją na bardziej opisową. Zmień nazwę na *Zapisz ciąg Witaj, świecie w danych wyjściowych*.
5. Kliknij pozycję **Parametry**, aby podać wartości parametrów polecenia cmdlet.  
   Niektóre polecenia cmdlet mają wiele zestawów parametrów i konieczne jest wybranie zestawu do użycia. W tym przypadku polecenie **Write-Output** ma tylko jeden zestaw parametrów, więc nie musisz go wybierać. <br> ![Właściwości polecenia Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Wybierz parametr **InputObject**.  Jest to parametr służący do określania tekstu, który zostanie wysłany do strumienia wyjściowego.
7. Z listy rozwijanej **Źródło danych** wybierz pozycję **Wyrażenie programu PowerShell**.  Lista rozwijana **Źródło danych** zawiera różne źródła używane do wypełniania wartości parametrów.  
   Możesz używać danych wyjściowych ze źródeł, takich jak inne działanie, element zawartości usługi Automation lub wyrażenie programu PowerShell.  W tym przypadku chcemy tylko uzyskać tekst wyjściowy *Witaj, świecie*. Możemy użyć wyrażenia programu PowerShell i wprowadzić ciąg.
8. W polu **Wyrażenie** wpisz *„Witaj, świecie”* i kliknij dwukrotnie przycisk **OK**, aby wrócić do kanwy.<br> ![Wyrażenie programu PowerShell](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Zapisz element Runbook, klikając przycisk **Zapisz**.<br> ![Zapisywanie elementu Runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-the-runbook"></a>Krok 3. Testowanie elementu Runbook
Przed opublikowaniem elementu Runbook w celu udostępnienia go w środowisku produkcyjnym chcemy go przetestować, aby upewnić się, że działa prawidłowo.  Testowanie elementu Runbook polega na uruchomieniu jego **wersji roboczej** i interaktywnym przejrzeniu danych wyjściowych.

1. Kliknij pozycję **Okienko testowania**, aby otworzyć blok testowania.<br> ![Okienko testowania](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Kliknij opcję **Uruchom**, aby rozpocząć test.  Powinna to być jedyna włączona opcja.
3. Zostanie utworzone [zadanie elementu Runbook](automation-runbook-execution.md) i w okienku pojawi się jego stan.  
   Początkowy stan zadania to *W kolejce*, który wskazuje, że trwa oczekiwanie na udostępnienie procesu roboczego elementu runbook w chmurze.  Następnym stanem jest *Uruchamianie*, gdy proces roboczy pobiera zadanie, a następnie *Uruchomiono*, gdy element runbook faktycznie zacznie działać.  
4. Po zakończeniu zadania elementu Runbook zostaną wyświetlone jego dane wyjściowe. W naszym przypadku powinien być widoczny ciąg *Witaj, świecie*.<br> ![Witaj, świecie](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Zamknij blok testowania, aby wrócić do kanwy.

## <a name="step-4---publish-and-start-the-runbook"></a>Krok 4. Publikowanie i uruchamianie elementu Runbook
Nowo utworzony element Runbook nadal działa w trybie roboczym. Przed uruchomieniem elementu w środowisku produkcyjnym musimy go opublikować.  Podczas publikowania elementu Runbook można zastąpić istniejącą wersję opublikowaną wersją roboczą.  W naszym przypadku nie mamy jeszcze wersji opublikowanej, ponieważ element Runbook został dopiero utworzony.

1. Kliknij pozycję **Opublikuj**, aby opublikować element Runbook, a następnie kliknij pozycję **Tak** po wyświetleniu monitu.<br> ![Publikowanie](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Jeśli przewiniesz w lewo, aby wyświetlić element runbook w bloku **Elementy runbook**, element **Stan tworzenia** będzie mieć wartość **Opublikowano**.
3. Przewiń w prawo, aby wyświetlić blok elementu **MyFirstRunbook**.  
   Opcje w górnej części umożliwiają nam uruchamianie elementu Runbook, planowanie jego uruchomienia w przyszłości lub utworzenie [elementu webhook](automation-webhooks.md) w celu umożliwienia uruchamiania za pośrednictwem wywołania HTTP.
4. Chcemy tylko uruchomić element Runbook, dlatego kliknij pozycję **Uruchom**, a następnie pozycję **Tak** po wyświetleniu monitu.<br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Zostanie otwarty blok zadania elementu runbook, który został właśnie utworzony.  Możemy zamknąć ten blok, ale w tym przypadku pozostanie on otwarty, aby można było obserwować postęp zadania.
6. Stan zadania jest wyświetlany w oknie **Podsumowanie zadania** i odpowiada stanom obserwowanym podczas testowania elementu Runbook.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Gdy stanem elementu Runbook będzie *Ukończono*, kliknij pozycję **Dane wyjściowe**. Zostanie otwarty blok **Dane wyjściowe** z naszym ciągiem *Witaj, świecie*.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Zamknij blok danych wyjściowych.
9. Kliknij pozycję **Wszystkie dzienniki**, aby otworzyć blok strumieni dla zadania elementu Runbook.  W strumieniu danych wyjściowych powinien być widoczny tylko ciąg *Witaj, świecie*, ale mogą zostać wyświetlone inne strumienie zadania elementu Runbook, takie jak Pełne informacje i Błąd, jeśli element Runbook wykonuje w nich operacje zapisywania.<br> ![Podsumowanie zadania](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Zamknij blok Wszystkie dzienniki oraz blok zadania, aby wrócić do bloku MyFirstRunbook.
11. Kliknij pozycję **Zadania**, aby otworzyć blok zadań dla tego elementu Runbook.  Zawiera on listę wszystkich zadań utworzonych przez ten element runbook. Ponieważ uruchomiliśmy zadanie tylko raz, powinniśmy zobaczyć tylko jedno zadanie.<br> ![Zadania](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Możesz kliknąć to zadanie, aby otworzyć okienko zadania wyświetlone przez nas wcześniej po uruchomieniu elementu Runbook.  Dzięki temu możesz cofnąć się w czasie i wyświetlić szczegóły dowolnego zadania, które zostało utworzone dla określonego elementu Runbook.

## <a name="step-5---create-variable-assets"></a>Krok 5. Tworzenie zmiennych elementów zawartości
Nasz element Runbook został przetestowany i opublikowany, ale jak do tej pory nie wykonuje on żadnych użytecznych czynności. Chcemy, aby zarządzał zasobami platformy Azure.  Przed skonfigurowaniem elementu runbook do uwierzytelniania utworzymy zmienną do przechowywania identyfikatora subskrypcji i odwoływania się do niego po skonfigurowania działania do uwierzytelniania w poniższym kroku 6.  Uwzględnienie odwołania do kontekstu subskrypcji ułatwia pracę z wieloma subskrypcjami.  Przed kontynuowaniem skopiuj identyfikator subskrypcji z opcji Subskrypcje w okienku Nawigacja.  

1. W bloku Konta usługi Automation kliknij kafelek **Elementy zawartości**. Zostanie otwarty blok **Elementy zawartości**.
2. W bloku Elementy zawartości kliknij kafelek **Zmienne**.
3. W bloku zmiennych kliknij pozycję **Dodaj zmienną**.<br>![Zmienna usługi Automation](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. W bloku Nowa zmienna w polu **Nazwa** wprowadź ciąg **AzureSubscriptionId**, a w polu **Wartość** wprowadź identyfikator subskrypcji.  Zachowaj *ciąg* jako wartość pola **Typ** i wartość domyślną pola **Szyfrowanie**.  
5. Kliknij pozycję **Utwórz**, aby utworzyć zmienną.  

## <a name="step-6---add-authentication-to-manage-azure-resources"></a>Krok 6. Dodawanie uwierzytelniania w celu zarządzania zasobami platformy Azure
Teraz mamy zmienną służącą do przechowywania identyfikatora subskrypcji i możemy skonfigurować nasz element Runbook do uwierzytelniania przy użyciu poświadczeń Uruchom jako, które określono w części dotyczącej [wymagań wstępnych](#prerequisites).  W tym celu możemy dodać do kanwy połączenie platformy Azure Uruchom jako **Element zawartości** i polecenie cmdlet **Add-AzureRMAccount**.  

1. Otwórz edytor graficzny, klikając pozycję **Edytuj** w bloku MyFirstRunbook.<br> ![Edytowanie elementu Runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Nie potrzebujemy już pozycji **Zapisz ciąg Hello World w danych wyjściowych**, więc kliknij ją prawym przyciskiem myszy i wybierz pozycję **Usuń**.
3. W kontrolce Biblioteka rozwiń pozycję **Połączenia** i dodaj pozycję **AzureRunAsConnection** do kanwy, wybierając pozycję **Dodaj do kanwy**.
4. W kanwie wybierz pozycję **AzureRunAsConnection** i w okienku kontrolki Konfiguracja wpisz **Uzyskaj połączenie Uruchom jako** w polu tekstowym **Etykieta**.  To jest połączenie
5. W kontrolce Biblioteka wpisz ciąg **Add-AzureRmAccount** w polu tekstowym wyszukiwania.
6. Dodaj polecenie **Add-AzureRmAccount** do kanwy.<br> ![Add-AzureRMAccount](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Umieść kursor nad pozycją **Uzyskaj połączenie Uruchom jako** i zaczekaj, aż w dolnej części kształtu pojawi się okrąg. Kliknij okrąg i przeciągnij strzałkę do pozycji **Add-AzureRmAccount**.  Utworzona strzałka to *link*.  Element runbook rozpocznie pracę od pozycji **Uzyskaj połączenie Uruchom jako**, a następnie uruchomi polecenie **Add-AzureRmAccount**.<br> ![Tworzenie połączenia między działaniami](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. W kanwie wybierz pozycję **Add-AzureRmAccount** i w okienku kontrolki Konfiguracja wpisz ciąg **Zaloguj się do platformy Azure** w polu tekstowym **Etykieta**.
9. Kliknij pozycję **Parametry**. Zostanie wyświetlony blok Konfiguracja parametru działania.
10. Polecenie **Add-AzureRmAccount** ma wiele zestawów parametrów, dlatego musimy wybrać jeden przed podaniem wartości parametrów.  Kliknij pozycję **Zestaw parametrów**, a następnie wybierz zestaw parametrów **ServicePrincipalCertificatewithSubscriptionId**.
11. Po wybraniu zestawu parametrów parametry zostaną wyświetlone w bloku Działanie parametru konfiguracji.  Kliknij pozycję **APPLICATIONID**.<br> ![Dodawanie parametrów konta usługi Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. W bloku Wartość parametru wybierz pozycję **Wyjście działania** jako **źródła danych** i wybierz pozycję **Uzyskaj połączenie Uruchom jako** z listy, w polu tekstowym **Ścieżka pola** wpisz ciąg **ApplicationId**, a następnie kliknij przycisk **OK**.  Określamy nazwę właściwości ścieżki pola, ponieważ wyjściem działania jest obiekt z wieloma właściwościami.
13. Kliknij pozycję **CERTIFICATETHUMBPRINT** i w bloku Wartość parametru wybierz **Wyjście działania** jako **źródło danych**.  Wybierz z listy pozycję **Uzyskaj połączenie Uruchom jako**, w polu tekstowym **Ścieżka pola** wpisz ciąg **CertificateThumbprint**, a następnie kliknij przycisk **OK**.
14. Kliknij pozycję **SERVICEPRINCIPAL** i w bloku Wartość parametru wybierz **ConstantValue** jako **źródło danych**, kliknij opcję **True**, a następnie kliknij przycisk **OK**.
15. Kliknij pozycję **TENANTID** i w bloku Wartość parametru wybierz **Wyjście działania** jako **źródło danych**.  Wybierz pozycję **Uzyskaj połączenie Uruchom jako** z listy, w polu tekstowym **Ścieżka pola** wpisz ciąg **TenantId**, a następnie dwukrotnie kliknij przycisk **OK**.  
16. W kontrolce Biblioteka wpisz ciąg **Set-AzureRmContext** w polu tekstowym wyszukiwania.
17. Dodaj pozycję **Set-AzureRmContext** do kanwy.
18. W kanwie wybierz pozycję **Set-AzureRmContext** i w okienku kontrolki Konfiguracja wpisz ciąg **Określ identyfikator subskrypcji** w polu tekstowym **Etykieta**.
19. Kliknij pozycję **Parametry**. Zostanie wyświetlony blok Konfiguracja parametru działania.
20. Polecenie **Set-AzureRmContext** ma wiele zestawów parametrów, dlatego musimy wybrać jeden przed podaniem wartości parametrów.  Kliknij pozycję **Zestaw parametrów**, a następnie wybierz zestaw parametrów **SubscriptionId**.  
21. Po wybraniu zestawu parametrów parametry zostaną wyświetlone w bloku Działanie parametru konfiguracji.  Kliknij pozycję **SubscriptionID**.
22. W bloku Wartość parametru wybierz pozycję **Element zawartości zmiennej** jako **źródło danych**, wybierz pozycję **AzureSubscriptionId** z listy, a następnie dwukrotnie kliknij przycisk **OK**.   
23. Umieść kursor nad pozycją **Zaloguj się do platformy Azure** i zaczekaj, aż w dolnej części kształtu pojawi się okrąg. Kliknij okrąg i przeciągnij strzałkę do pozycji **Określ identyfikator subskrypcji**.

Element Runbook powinien na tym etapie wyglądać następująco: <br>![Konfiguracja uwierzytelniania elementu Runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-to-start-a-virtual-machine"></a>Krok 7. Dodawanie działania w celu uruchomienia maszyny wirtualnej
Teraz dodamy działanie **Start-AzureRmVM** w celu uruchomienia maszyny wirtualnej.  Możesz wybrać dowolną maszynę wirtualną w ramach subskrypcji Azure. Wybrana nazwa zostanie na razie umieszczona w kodzie polecenia cmdlet.

1. W kontrolce Biblioteka wpisz ciąg **Start-AzureRm** w polu tekstowym wyszukiwania.
2. Dodaj polecenie **Start-AzureRmVM** do kanwy, a następnie kliknij i przeciągnij go poniżej obszaru **Określ identyfikator subskrypcji**.
3. Umieść kursor nad pozycją **Określ identyfikator subskrypcji** i zaczekaj, aż w dolnej części kształtu pojawi się okrąg.  Kliknij okrąg i przeciągnij strzałkę do pozycji **Start-AzureRmVM**.
4. Wybierz pozycję **Start-AzureRmVM**.  Kliknij pozycję **Parametry**, a następnie pozycję **Zestaw parametrów**, aby wyświetlić zestawy dla pozycji **Start-AzureRmVM**.  Wybierz zestaw parametrów **ResourceGroupNameParameterSetName**. Zwróć uwagę, że obok parametrów **ResourceGroupName** i **Name** znajdują się wykrzykniki.  Oznacza to, że te parametry są wymagane.  Oczekiwane wartości obu parametrów to ciągi.
5. Wybierz pozycję **Nazwa**.  Wybierz pozycję **Wyrażenie programu PowerShell** jako **Źródło danych**, a następnie wpisz ujętą w cudzysłów nazwę maszyny wirtualnej, która zostanie uruchomiona przy użyciu tego elementu runbook.  Kliknij przycisk **OK**.<br>![Wartość parametru Name pozycji Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Wybierz pozycję **ResourceGroupName**. Użyj pozycji **Wyrażenie programu PowerShell** jako **źródła danych** i wpisz nazwę grupy zasobów ujętą w podwójne cudzysłowy.  Kliknij przycisk **OK**.<br> ![Parametry polecenia Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Kliknij pozycję Okienko testowania, aby umożliwić przetestowanie elementu Runbook.
8. Kliknij opcję **Uruchom**, aby rozpocząć test.  Po zakończeniu sprawdź, czy maszyna wirtualna została uruchomiona.

Element Runbook powinien na tym etapie wyglądać następująco: <br>![Konfiguracja uwierzytelniania elementu Runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-to-the-runbook"></a>Krok 8. Dodawanie dodatkowych parametrów wejściowych do elementu Runbook
Nasz element runbook aktualnie umożliwia uruchomienie maszyny wirtualnej w grupie zasobów określonej w poleceniu cmdlet **Start-AzureRmVM**.  Ten element runbook byłby jednak bardziej użyteczny, gdybyśmy mogli podać obydwie wartości podczas jego uruchamiania.  Aby to zrobić, dodamy teraz do elementu runbook parametry wejściowe.

1. Otwórz edytor graficzny, klikając pozycję **Edytuj** w okienku **MyFirstRunbook**.
2. Kliknij pozycję **Wejście i wyjście**, a następnie pozycję **Dodaj wejście**, aby otworzyć okienko parametru wejściowego elementu Runbook.<br> ![Wejście i wyjście elementu Runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Wprowadź wartość *VMName* parametru **Name**.  Zachowaj *ciąg* jak wartość pola **Typ**, ale zmień ustawienie pozycji **Obowiązkowy** na *Tak*.  Kliknij przycisk **OK**.
4. Utwórz drugi obowiązkowy parametr wejściowy o nazwie *ResourceGroupName*, a następnie kliknij przycisk **OK**, aby zamknąć okienko **Wejście i wyjście**.<br> ![Parametry wejściowe elementu Runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Wybierz działanie **Start-AzureRmVM**, a następnie kliknij pozycję **Parametry**.
6. Zmień **źródło danych** dla pozycji **Name** na **Wejście elementu Runbook**, a następnie wybierz pozycję **VMName**.<br>
7. Zmień **źródło danych** dla pozycji **ResourceGroupName** na **Wejście elementu Runbook**, a następnie wybierz pozycję **ResourceGroupName**.<br> ![Parametry polecenia Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Zapisz element Runbook, a następnie otwórz okienko testowania.  Zauważ, że teraz możesz podać wartości dwóch zmiennych wejściowych, które zostaną użyte w teście.
9. Zamknij okienko testowania.
10. Kliknij pozycję **Opublikuj**, aby opublikować nową wersję elementu Runbook.
11. Zatrzymaj maszynę wirtualną uruchomioną w poprzednim kroku.
12. Kliknij pozycję **Uruchom**, aby uruchomić element Runbook.  Wpisz wartości parametrów **VMName** i **ResourceGroupName** dla maszyny wirtualnej do uruchomienia.<br> ![Uruchamianie elementu Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Po zakończeniu działania elementu Runbook sprawdź, czy maszyna wirtualna została uruchomiona.

## <a name="step-9---create-a-conditional-link"></a>Krok 9. Tworzenie połączenia warunkowego
Teraz zmodyfikujemy element runbook w taki sposób, aby podejmował próbę uruchomienia maszyny wirtualnej tylko wtedy, gdy nie została jeszcze uruchomiona.  W tym celu do elementu runbook dodamy polecenie cmdlet **Get-AzureRmVM** służące do pobrania stanu poziomu wystąpienia maszyny wirtualnej. Następnie dodamy moduł kodu przepływu pracy programu PowerShell o nazwie **Pobieranie stanu** przy użyciu fragmentu kodu programu PowerShell, aby określić, czy stan maszyny wirtualnej wskazuje na jej uruchomienie, czy też na jej zatrzymanie.  Połączenie warunkowe z modułu **Pobieranie stanu** będzie powodować uruchomienie polecenia **Start-AzureRmVM** tylko w sytuacji, gdy bieżący stan działania wskazuje na zatrzymanie.  Na koniec utworzymy wiadomość wyjściową, aby za pomocą polecenia cmdlet programu PowerShell Write-Output poinformować Cię o tym, czy maszyna wirtualna została pomyślnie uruchomiona.

1. Otwórz element **MyFirstRunbook** w edytorze graficznym.
2. Usuń połączenie między elementami **Określ identyfikator subskrypcji** i **Start -AzureRmVM**, klikając je i naciskając klawisz *Delete*.
3. W kontrolce Biblioteka wpisz ciąg **Get-AzureRm** w polu tekstowym wyszukiwania.
4. Dodaj pozycję **Get-AzureRmVM** do kanwy.
5. Wybierz polecenie **Get-AzureRmVM**, a następnie pozycję **Zestaw parametrów**, aby wyświetlić zestawy polecenia **Get-AzureRmVM**.  Wybierz zestaw parametrów **GetVirtualMachineInResourceGroupNameParamSet**.  Zwróć uwagę, że obok parametrów **ResourceGroupName** i **Name** znajdują się wykrzykniki.  Oznacza to, że te parametry są wymagane.  Oczekiwane wartości obu parametrów to ciągi.
6. W obszarze **Źródło danych** dla pozycji **Name** wybierz pozycję **Wejście elementu Runbook**, a następnie wybierz pozycję **VMName**.  Kliknij przycisk **OK**.
7. W obszarze **Źródło danych** dla pozycji **ResourceGroupName** wybierz pozycję **Wejście elementu Runbook**, a następnie wybierz pozycję **ResourceGroupName**.  Kliknij przycisk **OK**.
8. W obszarze **Źródło danych** dla pozycji **Stan** wybierz opcję **Stała wartość**, a następnie kliknij pozycję **Prawda**.  Kliknij przycisk **OK**.  
9. Utwórz połączenie pozycji **Określ identyfikator subskrypcji** z poleceniem **Get-AzureRmVM**.
10. W kontrolce biblioteki rozwiń pozycję **Kontrola elementu Runbook** i dodaj pozycję **Kod** do kanwy.  
11. Utwórz połączenie między poleceniem **Get-AzureRmVM** i elementem **Kod**.  
12. Kliknij pozycję **Kod** i w okienku Konfiguracja zmień etykietę na **Pobieranie stanu**.
13. Wybierz parametr **Kod**. Zostanie wyświetlony blok **Edytor kodu**.  
14. W edytorze kodu wklej poniższy fragment kodu:
    
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
15. Utwórz połączenie elementu **Pobieranie stanu** z poleceniem **Start-AzureRmVM**.<br> ![Element Runbook z modułem kodu](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Wybierz połączenie, a następnie w okienku Konfiguracja zmień ustawienie pozycji **Zastosuj warunek** na **Tak**.   Zauważ, że połączenie zmieni się w linię przerywaną, co oznacza, że działanie docelowe będzie uruchamiane tylko w sytuacji, gdy warunek będzie spełniony.  
17. Dla **warunku wyrażenia** wpisz *$ActivityOutput [’Pobieranie stanu’] - eq "Zatrzymano"*.  Polecenie **Start-AzureRmVM** będzie teraz uruchamiane tylko wtedy, gdy maszyna wirtualna jest zatrzymana.
18. W kontrolce Biblioteka rozwiń pozycję **Polecenia cmdlet**, a następnie pozycję **Microsoft.PowerShell.Utility**.
19. Dwukrotnie dodaj pozycję **Write-Output** do kanwy.<br> ![Element Runbook z pozycją Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. W pierwszej kontrolce **Write-Output** kliknij pozycję **Parametry** i zmień wartość pola **Etykieta** na *Powiadamianie o uruchomieniu maszyny wirtualnej*.
21. Dla pozycji **InputObject** zmień **źródło danych** na **Wyrażenie programu PowerShell** i wpisz wyrażenie *„Maszyna wirtualna $VMName została pomyślnie uruchomiona”*.
22. W drugiej kontrolce **Write-Output** kliknij pozycję **Parametry** i zmień wartość pola **Etykieta** na *Powiadamianie o błędzie uruchomienia maszyny wirtualnej*.
23. Dla pozycji **InputObject** zmień **źródło danych** na **Wyrażenie programu PowerShell** i wpisz wyrażenie *„Nie można uruchomić maszyny wirtualnej $VMName”*.
24. Utwórz połączenie między poleceniem **Start-AzureRmVM** z wartościami **Powiadamianie o uruchomieniu maszyny wirtualnej** i **Powiadamianie o nieudanym uruchomieniu maszyny wirtualnej**.
25. Wybierz połączenie z wartością **Powiadamianie o uruchomieniu maszyny wirtualnej** i zmień ustawienie pozycji **Zastosuj warunek** na **True**.
26. W polu **Warunek wyrażenia** wpisz ciąg *$ActivityOutput['Start-AzureRmVM'].IsSuccessStatusCode -eq $true*.  Ta kontrolka Write-Output będzie teraz uruchamiana tylko w sytuacji, gdy maszyna wirtualna zostanie pomyślnie uruchomiona.
27. Wybierz połączenie z wartością **Powiadamianie o nieudanym uruchomieniu maszyny wirtualnej** i zmień ustawienie pozycji **Zastosuj warunek** na **True**.
28. W polu **Warunek wyrażenia** wpisz ciąg *$ActivityOutput['Start-AzureRmVM'].IsSuccessStatusCode -ne $true*.  Ta kontrolka Write-Output będzie teraz uruchamiana tylko w sytuacji, gdy maszyna wirtualna nie zostanie pomyślnie uruchomiona.
29. Zapisz element Runbook, a następnie otwórz okienko testowania.
30. Uruchom element Runbook przy zatrzymanej maszynie wirtualnej. Powinno to spowodować jej uruchomienie.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat tworzenia elementów graficznych, zobacz [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md) (Tworzenie elementów graficznych w usłudze Azure Automation).
* Aby rozpocząć pracę z elementami Runbook programu PowerShell, zobacz artykuł [My first PowerShell runbook](automation-first-runbook-textual-powershell.md) (Mój pierwszy element Runbook programu PowerShell).
* Aby rozpocząć pracę z elementami Runbook przepływu pracy programu PowerShell, zobacz artykuł [My first PowerShell workflow runbook](automation-first-runbook-textual.md) (Mój pierwszy element Runbook przepływu pracy programu PowerShell).

