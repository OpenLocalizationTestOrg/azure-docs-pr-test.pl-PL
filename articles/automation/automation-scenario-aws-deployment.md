---
title: "Automatyzacja wdrażania maszyny Wirtualnej w ramach usług Amazon Web Services | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób użycia usługi Automatyzacja Azure można zautomatyzować tworzenie maszyny wirtualnej usługi sieci Web firmy Amazon"
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/29/2017
ms.author: tiandert; bwren
ms.openlocfilehash: 5f81150a0ef60cbf10010374f1ec80b0c05b6c6f
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Scenariusz automatyzacji Azure - świadczenia usług AWS maszyny wirtualnej
W tym artykule przedstawiony sposób mogą korzystać z automatyzacji Azure, aby udostępnić maszynie wirtualnej w ramach subskrypcji usługi sieci Web firmy Amazon (AWS) i nadaj tej maszyny Wirtualnej określonej nazwy — czyli usług AWS jako "znakowanie" maszyny Wirtualnej.

## <a name="prerequisites"></a>Wymagania wstępne
Do celów tego artykułu musisz mieć konto usługi Automatyzacja Azure i subskrypcję usług AWS. Aby uzyskać więcej informacji na temat ustawiania konto usługi Automatyzacja Azure i jego konfigurowania przy użyciu poświadczeń subskrypcji usług AWS Przejrzyj [Konfigurowanie uwierzytelniania za pomocą usług Amazon Web Services](automation-config-aws-account.md).  To konto powinno można utworzyć ani zaktualizować przy użyciu poświadczeń subskrypcji usług AWS przed kontynuowaniem, jak firma Microsoft będzie odwoływać się do tego konta w poniższych krokach.

## <a name="deploy-amazon-web-services-powershell-module"></a>Wdrażanie modułu programu PowerShell usługi sieci Web firmy Amazon
Nasze obsługi runbook maszyny Wirtualnej będzie korzystać z modułu programu PowerShell usług AWS, aby wykonać swoją pracę. Wykonaj poniższe kroki, aby dodać do swojego konta automatyzacji, który jest skonfigurowany przy użyciu poświadczeń subskrypcji usług AWS modułu.  

1. Otwórz przeglądarkę sieci web i przejdź do [galerii programu PowerShell](http://www.powershellgallery.com/packages/AWSPowerShell/) i wybierz polecenie **wdrażanie na przycisku usługi Automatyzacja Azure**.<br><br> ![Importowanie modułów usług AWS PS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Zostają przeniesieni do strony logowania do systemu Azure i po uwierzytelnieniu, użytkownik zostanie przekierowany do portalu Azure i wyświetlana następująca strona.<br><br> ![Zaimportuj moduł strony](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Wybierz grupę zasobów z **grupy zasobów** rozwijania listy i w okienku parametrów, wprowadź następujące informacje:
   
   * Z **nowego lub istniejącego konta automatyzacji (ciąg)** listy rozwijanej wybierz **istniejące**.  
   * W **nazwa konta automatyzacji (ciąg)** , wpisz w dokładną nazwę konta automatyzacji, który obejmuje również poświadczenia dla Twojej subskrypcji usług AWS.  Na przykład, jeśli utworzono dedykowanego konta o nazwie **AWSAutomation**, a następnie wpisz w polu jest.
   * Wybierz odpowiedni region z **Lokalizacja konta automatyzacji** listy rozwijanej.
4. Po wykonaniu wprowadzenie wymaganych informacji, kliknij przycisk **Utwórz**.
   
   > [!NOTE]
   > Podczas importowania modułu programu PowerShell do automatyzacji Azure, jego również wyodrębnia poleceń cmdlet, a te działania nie będą widoczne do czasu modułu całkowicie zakończył importowania i wyodrębnianie polecenia cmdlet. Może to potrwać kilka minut.  
   > <br>
   > 
   > 
5. W portalu Azure Otwórz Twoje konto usługi Automatyzacja, do których odwołuje się w kroku 3.
6. Polecenie **zasoby** Kafelek i na **zasoby** okienku wybierz **modułów** kafelka.
7. Na **modułów** wyświetlona zostanie strona **AWSPowerShell** moduł na liście.

## <a name="create-aws-deploy-vm-runbook"></a>Tworzenie usług AWS wdrażania elementu runbook maszyny Wirtualnej
Po wdrożeniu modułu środowiska PowerShell dla usług AWS mamy teraz Tworzenie elementu runbook do automatyzacji obsługi maszyny wirtualnej w AWS za pomocą skryptu programu PowerShell. Poniższe kroki pokazują, jak korzystać z natywnych skrypt programu PowerShell w automatyzacji Azure.  

> [!NOTE]
> Dodatkowe opcje i informacje dotyczące tego skryptu można znaleźć [galerii programu PowerShell](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Pobierz skrypt programu PowerShell, New-AwsVM z galerii programu PowerShell, otwierając sesję programu PowerShell i wpisując następujące:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. W portalu Azure, otwórz Twoje konto usługi Automatyzacja i wybierz **Runbook** w sekcji **automatyzacji procesu** po lewej stronie.  
3. Z **Runbook** wybierz pozycję **Dodaj element runbook**.
4. Na **Dodaj element runbook** okienku wybierz **szybkie tworzenie** (Utwórz nowy element runbook).
5. Na **Runbook** okienko właściwości, wpisz nazwę w polu Nazwa elementu runbook i z **typ elementu Runbook** listy rozwijanej wybierz **PowerShell**, a następnie kliknij przycisk **Utworzyć**.<br><br> ![Utwórz okienko elementu runbook](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Gdy pojawi się Strona Edytuj element Runbook programu PowerShell, skopiuj i wklej skrypt programu PowerShell do tworzenia obszaru roboczego elementu runbook.<br><br> ![Skrypt programu PowerShell elementu Runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Sprawdź należy pamiętać, że podczas pracy z przykładowego skryptu programu PowerShell:
    > 
    > * Element runbook zawiera szereg domyślne wartości parametrów. Oceń wszystkie wartości domyślne i aktualizować w miarę potrzeby.
    > * Jeśli poświadczenia usług AWS są przechowywane jako zasób poświadczeń o nazwie inaczej niż **AWScred**, musisz zaktualizować ten skrypt, w wierszu 57, aby dopasować odpowiednio.  
    > * Podczas pracy z poleceń interfejsu wiersza polecenia usług AWS w programie PowerShell, szczególnie w przypadku tego Przykładowy element runbook, należy określić region usług AWS. W przeciwnym razie cmdlet zakończy się niepowodzeniem.  Widok usług AWS tematu [Określ Region usług AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) w narzędziach usług AWS dla dokumentu programu PowerShell, aby uzyskać więcej informacji.  
    >

7. Aby pobrać listę nazw obrazu z subskrypcją usług AWS, uruchom PowerShell ISE i zaimportuj moduł programu PowerShell usług AWS.  Uwierzytelniania usług AWS zastępując **Get-AutomationPSCredential** w środowisku platformy ISE przy **AWScred = Get-Credential**.  To spowoduje wyświetlenie monitu o podanie poświadczeń oraz zapewnić Twojej **identyfikator klucza dostępu** nazwy użytkownika i **klucz tajny klucz dostępu** hasła.  Zobacz poniższy przykład:  

        #Sample to get the AWS VM available images
        #Please provide the path where you have downloaded the AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up the environment to access AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Zwrócono następujące dane wyjściowe:<br><br>
   ![Pobierz usług AWS obrazów](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Skopiuj i Wklej do jednej z nazwy obrazów w zmiennej automatyzacji zgodnie z informacjami zawartymi w elemencie runbook jako **$InstanceType**. Ponieważ w tym przykładzie są nam przy użyciu wolnego usług AWS warstwowej subskrypcji, użyjemy **t2.micro** w naszym przykładzie elementu runbook.  
9. Zapisz element runbook, a następnie kliknij przycisk **publikowania** opublikować elementu runbook, a następnie **tak** po wyświetleniu monitu.

### <a name="testing-the-aws-vm-runbook"></a>Testowanie elementu runbook usług AWS maszyny Wirtualnej
Aby można było kontynuować testowania elementu runbook, musimy zweryfikować kilka rzeczy. W szczególności:  

* Zasób, do uwierzytelniania względem usług AWS została utworzona o nazwie **AWScred** lub skrypt została zaktualizowana, aby odwoływać się do nazwy zawartości poświadczeń.    
* Moduł PowerShell usług AWS został zaimportowany w automatyzacji Azure  
* Nowy element runbook został utworzony i wartości parametrów została zweryfikowana i aktualizowane w miarę potrzeby  
* **Rejestrowania rekordów pełnych** i opcjonalnie **rejestrowania rekordów postępu** w obszarze Ustawienia elementu runbook **rejestrowania i śledzenia** zostały ustawione na **na**.<br><br> ![Element Runbook rejestrowania i śledzenia](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Jeśli chcesz uruchomić element runbook, więc klikamy **Start** , a następnie kliknij przycisk **OK** po otwarciu w okienku Uruchom element Runbook.
2. W okienku Uruchom element Runbook, podaj **VMname**.  Zaakceptuj wartości domyślne dla parametrów, wstępnie w skrypcie wcześniej.  Kliknij przycisk **OK** można uruchomić zadania elementu runbook.<br><br> ![Uruchom nowy AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Zostanie otwarte okienko zadania elementu Runbook, który właśnie utworzyliśmy. Zamknij to okienko.
4. Możemy wyświetlić postęp zadania i Wyświetl dane wyjściowe **strumieni** wybierając **wszystkie dzienniki** kafelka ze strony zadania elementu runbook.<br><br> ![Strumień wyjściowy](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. Aby upewnić się, że maszyna wirtualna jest inicjowana, zaloguj się do konsoli zarządzania usług AWS, jeśli użytkownik nie jest aktualnie zalogowany.<br><br> ![Konsoli usług AWS wdrożyć maszyny Wirtualnej](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Następne kroki
* Aby rozpocząć pracę z graficznymi elementami Runbook, zobacz artykuł [My first graphical runbook](automation-first-runbook-graphical.md) (Mój pierwszy graficzny element Runbook).
* Aby rozpocząć pracę z elementami Runbook przepływu pracy programu PowerShell, zobacz artykuł [My first PowerShell workflow runbook](automation-first-runbook-textual.md) (Mój pierwszy element Runbook przepływu pracy programu PowerShell).
* Aby dowiedzieć się więcej na temat typów elementów Runbook, ich zalet i ograniczeń, zobacz [Azure Automation runbook types](automation-runbook-types.md) (Typy elementów Runbook usługi Azure Automation).
* Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Obsługa natywnych skryptów programu PowerShell w usłudze Azure Automation).

