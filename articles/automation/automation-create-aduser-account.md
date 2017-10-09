---
title: "aaaCreate konta usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate konta usługi Azure AD użytkownika poświadczeń dla elementów runbook w automatyzacji Azure tooauthenticate Azure i klasycznego Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "konto użytkownika usługi Azure Active Directory, azure service management, konto użytkownika usługi Azure AD"
ms.assetid: fcfe266d-b22e-4dfb-8272-adcab09fc0cf
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 7c6ed4182dbab074d0bc5da7057f74ad321d8884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-azure-classic-deployment-and-resource-manager"></a>Uwierzytelnianie elementów Runbook za pomocą klasycznego wdrożenia platformy Azure i usługi Resource Manager
W tym artykule opisano kroki hello tooconfigure konta usługi Azure AD użytkownika należy wykonać w przypadku uruchamiania Azure klasycznego modelu wdrażania lub zasobów usługi Azure Resource Manager elementu runbook usługi Automatyzacja Azure.  Gdy to nadal toobe tożsamość uwierzytelniania obsługiwanych dla Menedżera zasobów Azure na podstawie elementów runbook, hello zaleca się, że metoda jest przy użyciu konta Uruchom jako platformy Azure.       

## <a name="create-a-new-azure-active-directory-user"></a>Tworzenie nowego użytkownika usługi Azure Active Directory
1. Zaloguj się za toohello klasycznego portalu Azure jako administrator usługi dla subskrypcji platformy Azure ma toomanage hello.
2. Wybierz **usługi Active Directory**, a następnie wybierz nazwę hello katalogu organizacji.
3. Wybierz hello **użytkowników** karcie, a następnie wybierz w obszarze polecenia hello **Dodaj użytkownika**.
4. Na powitania **Poinformuj nas o tym użytkowniku** w obszarze **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.
5. Wprowadź nazwę użytkownika.  
6. Wybierz nazwę katalogu hello skojarzony z subskrypcją platformy Azure na stronie usługi Active Directory hello.
7. Na powitania **profilu użytkownika** Podaj pierwszy i ostatni nazwę, przyjazna nazwa i użytkownika z hello **ról** listy.  Nie wybieraj opcji **Włącz uwierzytelnianie wieloskładnikowe**.
8. Należy pamiętać, pełna nazwa hello użytkownika i hasło tymczasowe.
9. Wybierz opcje **Ustawienia > Administratorzy > Dodaj**.
10. Wpisz nazwę użytkownika pełne hello hello użytkownika, który został utworzony.
11. Wybierz subskrypcję hello, która ma być hello toomanage użytkownika.
12. Wyloguj się z platformy Azure, a następnie zaloguj się ponownie przy użyciu hello właśnie utworzonego konta. Będzie użytkownik hello toochange zostanie wyświetlony monit o hasło.

## <a name="create-an-automation-account-in-azure-classic-portal"></a>Tworzenie konta usługi Automation w klasycznej witrynie Azure Portal
W tej sekcji możesz wykonać następujące kroki toocreate konto usługi Automatyzacja Azure w hello portalu Azure do użycia z elementy runbook zarządzania zasobami Azure wdrożenie klasyczne hello.  

> [!NOTE]
> Konta automatyzacji utworzone przy użyciu hello klasycznego portalu Azure można zarządzać zarówno hello Azure klasycznego portalu Azure i albo zestaw poleceń cmdlet. Po utworzeniu konta hello nie ma różnicy sposób tworzenia i zarządzania zasobami w ramach konta hello. Jeśli planujesz toocontinue toouse hello klasycznego portalu Azure, użyj jej zamiast hello Azure toocreate portalu kont automatyzacji.
> 
> 

1. Zaloguj się za toohello klasycznego portalu Azure jako administrator usługi dla subskrypcji platformy Azure ma toomanage hello.
2. Wybierz opcję **Automatyzacja**.
3. Na powitania **automatyzacji** wybierz pozycję **Utwórz konto automatyzacji**.
4. W hello **utworzyć konto usługi automatyzacja** , wpisz nazwę nowego konta automatyzacji i wybierz pozycję **Region** z listy rozwijanej hello.  
5. Kliknij przycisk **OK** tooaccept ustawień i Utwórz konto hello.
6. Po utworzeniu zostaną wyświetlone na powitania **automatyzacji** strony.
7. Kliknij konto hello i zostanie wyświetlone zostanie toohello strony pulpitu nawigacyjnego.  
8. Na stronie pulpitu nawigacyjnego automatyzacji hello zaznacz **zasoby**.
9. Na powitania **zasoby** wybierz pozycję **Dodaj ustawienia** znajdujący się u dołu hello hello strony.
10. Na powitania **Dodaj ustawienia** wybierz pozycję **Dodaj poświadczenie**.
11. Na powitania **zdefiniuj poświadczeń** wybierz pozycję **poświadczenie programu PowerShell systemu Windows** z hello **typ poświadczeń** listy rozwijanej listy i podaj nazwę dla hello poświadczenia.
12. Po hello **zdefiniuj poświadczenia** stronie wpisz użytkownika hello hello AD konto użytkownika utworzone we wcześniejszej części hello **nazwy użytkownika** pola i hello hasło w hello **hasło**i **Potwierdź hasło** pola. Kliknij przycisk **OK** toosave zmiany.

## <a name="create-an-automation-account-in-hello-azure-portal"></a>Utwórz konto usługi Automatyzacja w hello portalu Azure
W tej sekcji wykonaj następujące kroki toocreate konto usługi Automatyzacja Azure w hello portalu Azure do użycia z elementy runbook zarządzania zasobami w trybie Azure Resource Manager hello.  

1. Zaloguj się za toohello portalu Azure jako administrator usługi dla subskrypcji platformy Azure ma toomanage hello.
2. Wybierz opcję **Konta automatyzacji**.
3. W bloku konta automatyzacji powitania kliknij **Dodaj**.<br><br>![Dodawanie konta usługi Automation](media/automation-create-aduser-account/add-automation-acct-properties.png)
4. W hello **Dodaj konto automatyzacji** bloku w hello **nazwa** wpisz nazwę nowego konta automatyzacji.
5. Jeśli masz więcej niż jedną subskrypcję, określ jedną hello hello nowe konto, a także nowy lub istniejący **grupy zasobów** i centrum danych Azure **lokalizacji**.
6. Wybierz wartość hello **tak** dla hello **tworzenia konta Uruchom jako Azure** opcji, a następnie kliknij przycisk hello **Utwórz** przycisku.  
   
    > [!NOTE]
    > Po wybraniu toonot utworzyć hello konta Uruchom jako, wybierając opcję hello **nr**, użytkownik zobaczy komunikat ostrzegawczy w hello **Dodaj konto automatyzacji** bloku.  Gdy utworzono konto hello i przypisane toohello **współautora** roli w ramach subskrypcji hello nie będzie miała odpowiednich tożsamość uwierzytelniania w usłudze katalogowej subskrypcji i w związku z tym brak dostępu do zasoby w ramach subskrypcji.  To spowoduje żadnych elementów runbook odwołuje się do tego konta przed tooauthenticate może zapobiec i wykonywać zadania względem zasobów usługi Azure Resource Manager.
    > 
    >

    <br>![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-create-aduser-account/add-automation-acct-properties-error.png)<br>  
7. Gdy Azure tworzy konto automatyzacji hello, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

Po zakończeniu tworzenia hello poświadczenia hello należy toocreate hello tooassociate zasób poświadczeń konta automatyzacji o hello konta użytkownika AD utworzony wcześniej.  Pamiętaj, że utworzyliśmy tylko konto automatyzacji hello i nie jest skojarzony z tożsamością uwierzytelniania.  Wykonaj kroki hello opisane w hello [poświadczeń zasoby w artykule usługi Automatyzacja Azure](automation-credentials.md#creating-a-new-credential-asset) , a następnie wprowadź wartość hello **username** w formacie hello **domena\użytkownik**.

## <a name="use-hello-credential-in-a-runbook"></a>Użyj poświadczeń hello w elemencie runbook
Można pobrać poświadczeń hello w elemencie runbook za pomocą hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/dn940015.aspx) działania, a następnie użyć go przy użyciu [Add-AzureAccount](http://msdn.microsoft.com/library/azure/dn722528.aspx) tooyour tooconnect subskrypcji platformy Azure. Jeśli poświadczenia hello jest administratorem wielu subskrypcji platformy Azure, a następnie należy też używać [AzureSubscription wybierz](http://msdn.microsoft.com/library/dn495203.aspx) toospecify hello właściwy. Przedstawiono to w próbka hello poniżej ze środowiska Windows PowerShell, która zwykle pojawiają się u góry hello większość elementów runbook automatyzacji Azure.

    $cred = Get-AutomationPSCredential –Name "myuseraccount.onmicrosoft.com"
    Add-AzureAccount –Credential $cred
    Select-AzureSubscription –SubscriptionName "My Subscription"

Te wiersze należy powtórzyć po każdym [punkcie kontrolnym](http://technet.microsoft.com/library/dn469257.aspx#bk_Checkpoints) w elemencie Runbook. Jeśli hello runbook jest wstrzymana, a następnie kontynuowanie na innego procesu roboczego, następnie należy ponownie tooperform hello uwierzytelniania.

## <a name="next-steps"></a>Następne kroki
* Przejrzyj hello runbook różnych typów i procedury służące do tworzenia własnych elementów runbook z hello poniższego artykułu [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)

