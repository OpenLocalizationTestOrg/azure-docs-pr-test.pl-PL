---
title: "wdrożenie maszyny Wirtualnej w ramach usług Amazon Web Services aaaAutomating | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób toouse tworzenie tooautomate automatyzacji Azure maszyny wirtualnej usługi sieci Web firmy Amazon"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Scenariusz automatyzacji Azure - świadczenia usług AWS maszyny wirtualnej
W tym artykule przedstawiony sposób korzystać z usługi Automatyzacja Azure tooprovision maszyny wirtualnej w ramach subskrypcji usługi sieci Web firmy Amazon (AWS) i nadaj tej maszyny Wirtualnej określonej nazwy — które AWS odwołuje się tooas "znakowanie" hello maszyny Wirtualnej.

## <a name="prerequisites"></a>Wymagania wstępne
Dla celów hello w tym artykule należy toohave konto usługi Automatyzacja Azure i subskrypcję usług AWS. Aby uzyskać więcej informacji na temat ustawiania konto usługi Automatyzacja Azure i jego konfigurowania przy użyciu poświadczeń subskrypcji usług AWS Przejrzyj [Konfigurowanie uwierzytelniania za pomocą usług Amazon Web Services](automation-configure-aws-account.md).  To konto powinno utworzone lub zaktualizowane przy użyciu poświadczeń subskrypcji usług AWS przed kontynuowaniem, jak firma Microsoft będzie odwoływać się do tego konta w poniższych krokach hello.

## <a name="deploy-amazon-web-services-powershell-module"></a>Wdrażanie modułu programu PowerShell usługi sieci Web firmy Amazon
Nasze obsługi runbook maszyny Wirtualnej będzie korzystać toodo modułu programu PowerShell usług AWS hello swojej pracy. Wykonaj następujące kroki tooadd hello modułu tooyour automatyzacji konto skonfigurowane przy użyciu poświadczeń subskrypcji usług AWS hello.  

1. Otwórz przeglądarkę sieci web i przejdź toohello [galerii programu PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) i kliknij na powitania **Wdróż tooAzure automatyzacji przycisk**.<br><br> ![Importowanie modułów usług AWS PS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Podjęto toohello strony logowania do systemu Azure i po uwierzytelnieniu będzie kierowany toohello portalu Azure i prezentowany powitania po bloku.<br><br> ![Importowanie modułu bloku](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Wybierz hello grupy zasobów z hello **grupy zasobów** rozwijania listy i w bloku parametrów hello, podaj hello następujących informacji:
   
   * Z hello **nowego lub istniejącego konta automatyzacji (ciąg)** listy rozwijanej wybierz **istniejące**.  
   * W hello **nazwa konta automatyzacji (ciąg)** pola typu hello dokładną nazwę hello obejmuje hello poświadczeń dla Twojej subskrypcji usług AWS konta automatyzacji.  Na przykład, jeśli utworzono dedykowanego konta o nazwie **AWSAutomation**, a następnie wpisz w polu hello jest.
   * Wybierz hello odpowiedni region z hello **Lokalizacja konta automatyzacji** listy rozwijanej.
4. Po zakończeniu wprowadzania hello wymaganych informacji kliknij **Utwórz**.
   
   > [!NOTE]
   > Podczas importowania modułu programu PowerShell do automatyzacji Azure, jego również wyodrębnia hello poleceń cmdlet, a te działania będą widoczne dopiero modułu hello całkowicie zakończył importowania i wyodrębnianie hello polecenia cmdlet. Może to potrwać kilka minut.  
   > <br>
   > 
   > 
5. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja, do których odwołuje się w kroku 3.
6. Polecenie hello **zasoby** Kafelek i na powitania **zasoby** bloku, wybierz hello **modułów** kafelka.
7. Na powitania **modułów** bloku zobaczysz hello **AWSPowerShell** modułu hello na liście.

## <a name="create-aws-deploy-vm-runbook"></a>Tworzenie usług AWS wdrażania elementu runbook maszyny Wirtualnej
Raz hello wdrożonej usług AWS modułu programu PowerShell, można teraz tworzymy tooautomate elementu runbook, obsługi maszyny wirtualnej w AWS za pomocą skryptu programu PowerShell. Poniższe kroki Hello pokazują, jak tooleverage natywnego programu PowerShell skryptów automatyzacji Azure.  

> [!NOTE]
> Dodatkowe opcje i informacje dotyczące tego skryptu, można znaleźć na powitania [galerii programu PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Pobierz skrypt programu PowerShell hello AwsVM nowy z hello galerii programu PowerShell, otwierając sesję programu PowerShell i wpisując następujące hello:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Z hello portalu Azure, Twoje konto usługi Automatyzacja i kliknij hello **elementów Runbook** kafelka.  
3. Z hello **Runbook** bloku, wybierz opcję **Dodaj element runbook**.
4. Na powitania **Dodaj element runbook** bloku, wybierz opcję **szybkie tworzenie** (Utwórz nowy element runbook).
5. Na powitania **Runbook** bloku właściwości, wpisz nazwę w polu Nazwa hello element runbook oraz od hello **typ elementu Runbook** listy rozwijanej wybierz **PowerShell**, a następnie kliknij przycisk  **Utwórz**.<br><br> ![Importowanie modułu bloku](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Gdy pojawi się hello bloku Edytuj element Runbook programu PowerShell, skopiuj i Wklej hello skrypt programu PowerShell do tworzenia obszaru roboczego runbook hello.<br><br> ![Skrypt programu PowerShell elementu Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Uwaga poniżej hello podczas pracy z hello przykładowy skrypt programu PowerShell:
    > 
    > * Element runbook Hello zawiera szereg domyślne wartości parametrów. Oceń wszystkie wartości domyślne i aktualizować w miarę potrzeby.
    > * Jeśli poświadczenia usług AWS są przechowywane jako zasób poświadczeń o nazwie inaczej niż **AWScred**, konieczne będzie tooupdate hello skryptu w wierszu 57 toomatch odpowiednio.  
    > * Podczas pracy z hello polecenia interfejsu wiersza polecenia usług AWS w programie PowerShell, szczególnie w przypadku tego Przykładowy element runbook, należy określić region usług AWS hello. W przeciwnym razie poleceń cmdlet hello zakończy się niepowodzeniem.  Widok usług AWS tematu [Określ Region usług AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) w hello narzędzia usług AWS dla dokumentu programu PowerShell, aby uzyskać więcej informacji.  
    >

7. tooretrieve listę nazw obrazu z subskrypcji usług AWS uruchamiania programu PowerShell ISE i zaimportuj hello usług AWS modułu programu PowerShell.  Uwierzytelniania usług AWS zastępując **Get-AutomationPSCredential** w środowisku platformy ISE przy **AWScred = Get-Credential**.  To spowoduje wyświetlenie monitu o podanie poświadczeń oraz zapewnić Twojej **identyfikator klucza dostępu** dla nazwy username hello i **klucz tajny klucz dostępu** hello hasła.  Zobacz poniższy przykład hello:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Witaj następujące dane wyjściowe są zwracane:<br><br>
   ![Pobierz usług AWS obrazów](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Skopiuj i Wklej hello jedną z nazw obraz powitania w zmiennej automatyzacji zgodnie z informacjami zawartymi w elemencie runbook hello jako **$InstanceType**. Ponieważ w tym przykładzie używamy hello AWS bezpłatna do warstwy subskrypcji, użyjemy **t2.micro** w naszym przykładzie elementu runbook.  
9. Zapisz hello elementu runbook, a następnie kliknij przycisk **publikowania** toopublish hello runbook, a następnie **tak** po wyświetleniu monitu.

### <a name="testing-hello-aws-vm-runbook"></a>Testowanie hello runbook usług AWS maszyny Wirtualnej
Aby można było kontynuować z testowania hello elementu runbook, potrzebujemy tooverify kilka rzeczy. W szczególności:  

* Zasób, do uwierzytelniania względem usług AWS została utworzona o nazwie **AWScred** lub skryptu hello został zaktualizowany tooreference nazwę hello zawartości poświadczeń.    
* Moduł PowerShell usług AWS Hello został zaimportowany w automatyzacji Azure  
* Nowy element runbook został utworzony i wartości parametrów została zweryfikowana i aktualizowane w miarę potrzeby  
* **Rejestrowania rekordów pełnych** i opcjonalnie **rejestrowania rekordów postępu** w obszarze Ustawienia elementu runbook hello **rejestrowania i śledzenia** ustawiono zbyt**na**.<br><br> ![Element Runbook rejestrowania i śledzenia](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Firma Microsoft ma toostart hello runbook, więc klikamy **Start** , a następnie kliknij przycisk **OK** po otwarciu hello Start bloku elementu Runbook.
2. W bloku Uruchom element Runbook hello, podaj **VMname**.  Zaakceptuj wartości domyślne hello hello innych parametrów, wstępnie w skrypcie hello wcześniej.  Kliknij przycisk **OK** toostart hello runbook zadania.<br><br> ![Uruchom nowy AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Okienko zadania został otwarty do hello zadanie elementu runbook, który właśnie utworzony. Zamknij to okienko.
4. Firma Microsoft może wyświetlić postęp danych wyjściowych zadania i widoku hello **strumieni** wybierając hello **wszystkie dzienniki** kafelka w bloku zadania elementu runbook hello.<br><br> ![Strumień wyjściowy](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. tooconfirm powitalne maszyny Wirtualnej jest inicjowana, zaloguj się do hello konsoli zarządzania usług AWS, jeśli użytkownik nie jest aktualnie zalogowany.<br><br> ![Konsoli usług AWS wdrożyć maszyny Wirtualnej](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Następne kroki
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md)
* Zobacz tooknow więcej informacji na temat typów elementów runbook, ich zalety i ograniczenia, [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)
* Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz artykuł [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).

