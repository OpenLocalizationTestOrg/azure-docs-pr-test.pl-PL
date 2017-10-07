---
title: zasoby aaaCredential automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Zasoby poświadczeń usługi Automatyzacja Azure zawierają poświadczenia zabezpieczeń, które mogą być używane przez element runbook hello lub konfiguracji DSC tooresources tooauthenticate używane. W tym artykule opisano sposób toocreate zasoby poświadczeń i używaj ich w element runbook lub konfiguracji DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Zasoby poświadczeń usługi Automatyzacja Azure
Zawiera zasób poświadczenia usługi automatyzacja [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) obiekt zawierający poświadczenia zabezpieczeń, takie jak nazwa użytkownika i hasło. Konfiguracje elementów Runbook i DSC może używać poleceń cmdlet, które akceptuje obiekt PSCredential, do uwierzytelniania lub ich może wyodrębnić hello nazwę użytkownika i hasło hello PSCredential obiektu tooprovide toosome aplikacji lub usługi wymagającej uwierzytelniania. Witaj właściwości dla poświadczenia są bezpiecznie przechowywane w usłudze Automatyzacja Azure i jest dostępny w hello runbook lub Konfiguracja DSC o hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) działania.

> [!NOTE]
> Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne. Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji. Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure. Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.  

## <a name="windows-powershell-cmdlets"></a>Polecenia cmdlet programu Windows PowerShell
polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate i zarządzać zasobami poświadczenie automatyzacji przy użyciu programu Windows PowerShell.  One dostarczane jako część hello [modułu Azure PowerShell](/powershell/azure/overview) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.

| Polecenia cmdlet | Opis |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Pobiera informacje o zasób poświadczeń. Można tylko pobieranie poświadczeń hello, sama z **Get-AutomationPSCredential** działania. |
| [Nowe AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Tworzy nowe poświadczenie automatyzacji. |
| [Remove - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Usuwa poświadczenie automatyzacji. |
| [Set - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Ustawia hello właściwości dla istniejących poświadczeń usługi Automatyzacja. |

## <a name="runbook-activities"></a>Działania elementu Runbook
Hello działania w poniższej tabeli hello są używane tooaccess poświadczeń w elemencie runbook i konfiguracji DSC.

| Działania | Opis |
|:--- |:--- |
| Get-AutomationPSCredential |Pobiera toouse poświadczenie, element runbook lub konfiguracji DSC. Zwraca [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) obiektu. |

> [!NOTE]
> Należy unikać używania zmiennych w hello — Nazwa parametru Get-AutomationPSCredential, ponieważ może to skomplikować wykrywanie zależności między elementami runbook lub konfiguracji DSC i poświadczeń zasobów w czasie projektowania.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Tworzenie nowego zasobu poświadczeń

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate nowego zasobu poświadczeń z hello portalu Azure
1. Twoje konto usługi Automatyzacja kliknij hello **zasoby** hello tooopen części **zasoby** bloku.
2. Kliknij przycisk hello **poświadczenia** hello tooopen części **poświadczenia** bloku.
3. Kliknij przycisk **Dodaj poświadczenie** u góry bloku hello hello.
4. Wypełnij formularz hello i kliknij przycisk **Utwórz** toosave hello nowe poświadczenie.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate nowego zasobu poświadczeń przy użyciu programu Windows PowerShell
Witaj następujące przykładowe polecenia pokazują, jak toocreate automatyzacji nowych poświadczeń. Obiekt PSCredential utworzenia hello nazwę i hasło i następnie używany zasób poświadczeń hello toocreate. Alternatywnie można użyć hello **Get-Credential** toobe polecenia cmdlet zostanie wyświetlony monit tootype nazwę i hasło.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate nowego zasobu poświadczeń z hello klasycznego portalu Azure
1. Twoje konto usługi Automatyzacja kliknij **zasoby** u góry hello hello okna.
2. U dołu hello hello, kliknij przycisk **Dodaj ustawienie**.
3. Kliknij przycisk **Dodaj poświadczenie**.
4. W hello **typ poświadczeń** listy rozwijanej wybierz **poświadczenie programu PowerShell**.
5. Ukończ Kreatora hello, a następnie kliknij przycisk hello wyboru toosave hello nowe poświadczenie.

## <a name="using-a-powershell-credential"></a>Używanie poświadczenia programu PowerShell
Pobieranie zasobu poświadczeń w element runbook lub Konfiguracja DSC o hello **Get-AutomationPSCredential** działania. To polecenie zwróci [obiektu PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) korzystając z działania lub polecenia cmdlet, które wymaga parametru PSCredential. Można również pobierać właściwości hello hello poświadczeń obiektu toouse indywidualnie. Hello obiekt ma właściwość hello nazwy użytkownika i hasła bezpiecznego hello, lub użyć hello **GetNetworkCredential** tooreturn metody [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) obiekt, który zapewni niezabezpieczona Wersja hello hasła.

### <a name="textual-runbook-sample"></a>Przykład tekstowy
Witaj następujące przykładowe polecenia pokazują, jak poświadczeń toouse programu PowerShell w elemencie runbook. W tym przykładzie poświadczenie hello są pobierane, a jego nazwę użytkownika i hasło przypisane toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Przykładowe graficznym elementem runbook
Możesz dodać **Get-AutomationPSCredential** działania tooa graficzny element runbook prawym przyciskiem myszy na powitania poświadczeń w okienku Biblioteka hello hello edytora graficznego i wybierając **dodać toocanvas**.

![Dodaj toocanvas poświadczeń](media/automation-credentials/credential-add-canvas.png)

Witaj poniższej ilustracji przedstawiono przykład przy użyciu poświadczeń w graficznym elementem runbook.  W takim przypadku jest on tooprovide używane uwierzytelniania dla zasobów tooAzure runbook zgodnie z opisem w [uwierzytelniania elementy Runbook za pomocą konta usługi Azure AD](automation-create-aduser-account.md).  Pierwsze działanie Hello pobiera hello poświadczeniami, które mają dostęp toohello subskrypcji platformy Azure.  Witaj **Add-AzureAccount** działania następnie używa tego poświadczenia uwierzytelniania tooprovide żadnych działań, które pochodzą po nim.  A [linku potoku](automation-graphical-authoring-intro.md#links-and-workflow) jest tutaj od **Get-AutomationPSCredential** oczekuje pojedynczego obiektu.  

![Dodaj toocanvas poświadczeń](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Używanie poświadczenia programu PowerShell w konfiguracji DSC
Podczas konfiguracji DSC automatyzacji Azure mogą odwoływać się zasoby poświadczeń przy użyciu **Get-AutomationPSCredential**, zasoby poświadczeń może również zostać przekazane za za pomocą parametrów, w razie potrzeby. Aby uzyskać więcej informacji, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat łącza w tworzeniu graficznego [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello różne metody uwierzytelniania przy użyciu automatyzacji, zobacz [zabezpieczeń usługi Automatyzacja Azure](automation-security-overview.md)
* tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md) 

