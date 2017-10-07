---
title: zasoby aaaConnection automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Trwałe połączenie z usługi Automatyzacja Azure zawierają hello informacje wymagane tooconnect tooan zewnętrznej usługi lub aplikacji z elementu runbook lub konfiguracji DSC. W tym artykule opisano hello szczegółowe informacje dotyczące połączenia i jak toowork z nimi w tworzeniu zarówno tekstową i graficznego."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Trwałe połączenie z usługi Automatyzacja Azure

Zasób połączenia usługi Automatyzacja zawiera hello informacje wymagane tooconnect tooan zewnętrznej usługi lub aplikacji z elementu runbook lub konfiguracji DSC. Może to obejmować informacje wymagane do uwierzytelniania, takie jak nazwa użytkownika i hasło w dodatkowych informacji tooconnection, takie jak adres URL lub portu. wartość Hello połączenia przechowywanie wszystkich właściwości hello podłączania tooa określonej aplikacji w jeden zasób jako min. toocreating wiele zmiennych. Hello użytkownik może edytować wartości hello połączenia w jednym miejscu, a można przekazać hello nazwy elementu runbook tooa połączenia lub konfiguracji DSC w jeden parametr. Witaj właściwości dla połączenia można uzyskać w hello runbook lub Konfiguracja DSC o hello **Get AutomationConnection** działania.

Podczas tworzenia połączenia, należy określić *typ połączenia*. Typ połączenia Hello jest szablon, który definiuje zestaw właściwości. połączenie Hello definiuje wartości dla każdej właściwości w jego typie połączenia. Typy połączeń są dodane tooAzure automatyzacji w modułach integracji lub utworzone za pomocą hello [interfejsu API usługi Automatyzacja Azure](http://msdn.microsoft.com/library/azure/mt163818.aspx) Jeśli modułu integracji hello zawiera typ połączenia i jest importowany do Twojego konta automatyzacji. W przeciwnym razie trzeba będzie toocreate toospecify pliku metadanych typu połączenia usługi Automatyzacja.  Aby uzyskać dodatkowe informacje dotyczące tego, zobacz [moduły integracji](automation-integration-modules.md).  

>[!NOTE] 
>Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne. Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji. Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure. Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.

## <a name="windows-powershell-cmdlets"></a>Polecenia cmdlet programu Windows PowerShell

polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate i zarządzanie połączeniami automatyzacji za pomocą środowiska Windows PowerShell. One dostarczane jako część hello [modułu Azure PowerShell](/powershell/azure/overview) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.

|Polecenie cmdlet|Opis|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Pobiera połączenie. Obejmuje tablicy skrótów hello wartościami pól hello połączeń.|
|[Nowe AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Tworzy nowe połączenie.|
|[Usuń AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Usuń istniejące połączenie.|
|[Zestaw AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Ustawia hello wartość określonego pola dla istniejącego połączenia.|

## <a name="activities"></a>Działania

Hello działania w poniższej tabeli hello są używane tooaccess połączenia w element runbook lub konfiguracji DSC.

|Działania|Opis|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Pobiera toouse połączenia. Zwraca tabelę wyznaczania wartości skrótu z właściwościami hello hello połączenia.|

>[!NOTE] 
>Należy unikać używania zmiennych o hello — Nazwa parametru **Get - AutomationConnection** ponieważ może to skomplikować wykrywanie zależności między elementami runbook lub konfiguracji DSC i zasoby połączenia w czasie projektowania.

## <a name="creating-a-new-connection"></a>Tworzenie nowego połączenia

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate nowe połączenie z hello portalu Azure

1. Twoje konto usługi Automatyzacja kliknij hello **zasoby** hello tooopen części **zasoby** bloku.
2. Kliknij przycisk hello **połączeń** hello tooopen części **połączeń** bloku.
3. Kliknij przycisk **dodać połączenie** u góry bloku hello hello.
4. W hello **typu** listy rozwijanej wybierz hello typu połączenia mają toocreate. Formularz Hello przedstawi hello właściwości dla tego typu.
5. Wypełnij formularz hello i kliknij przycisk **Utwórz** toosave hello nowego połączenia.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate nowe połączenie z hello klasycznego portalu Azure

1. Twoje konto usługi Automatyzacja kliknij **zasoby** u góry hello hello okna.
2. U dołu hello hello, kliknij przycisk **Dodaj ustawienie**.
3. Kliknij przycisk **Dodaj połączenie**.
4. W hello **typ połączenia** listy rozwijanej wybierz hello typu połączenia mają toocreate.  Witaj Kreator przedstawi hello właściwości dla tego typu.
5. Ukończ Kreatora hello, a następnie kliknij przycisk hello wyboru toosave hello nowego połączenia.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate nowe połączenie przy użyciu programu Windows PowerShell

Utworzyć nowe połączenie za pomocą programu Windows PowerShell przy użyciu hello [AzureRmAutomationConnection nowy](/powershell/module/azurerm.automation/new-azurermautomationconnection) polecenia cmdlet. To polecenie cmdlet ma parametr o nazwie **ConnectionFieldValues** który oczekuje [tablicy skrótów](http://technet.microsoft.com/library/hh847780.aspx) definiowanie wartości dla każdej właściwości hello zdefiniowany przez typ połączenia hello.

Jeśli znasz hello automatyzacji [konta Uruchom jako](automation-sec-configure-azure-runas-account.md) tooauthenticate elementów runbook przy użyciu nazwy głównej usługi hello, hello skrypt programu PowerShell w hello hello toocreating alternatywne konto Uruchom jako z portalu hello Tworzy nowy zasób połączenia przy użyciu hello następujące przykładowe polecenia.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Są zasób połączenia hello toocreate toouse stanie hello skryptu, ponieważ podczas tworzenia konta automatyzacji automatycznie zawiera kilka modułów globalnych domyślnie wraz z typu połączenia hello **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** trwałego połączenia.  Jest to ważne tookeep pamiętać, ponieważ jeśli toocreate nową usługę tooa tooconnect trwałego połączenia lub aplikacji z innej metody uwierzytelniania, nie będzie ponieważ hello typ połączenia nie jest już zdefiniowany w Twoje konto usługi Automatyzacja.  Więcej informacji na temat sposobu toocreate własne połączenia wpisz niestandardowy lub modułu na podstawie hello [galerii programu PowerShell](https://www.powershellgallery.com), zobacz [moduły integracji](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Za pomocą połączenia w element runbook lub konfiguracji DSC

Pobieranie połączenia elementu runbook lub Konfiguracja DSC o hello **Get-AutomationConnection** polecenia cmdlet.  Nie można użyć hello [Get AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) działania.  To działanie pobiera wartości hello hello różnych pól na powitania połączenia i zwraca je jako [tablicy skrótów](http://go.microsoft.com/fwlink/?LinkID=324844) której następnie można użyć z hello odpowiednich poleceń w hello runbook lub konfiguracji DSC.

### <a name="textual-runbook-sample"></a>Przykład tekstowy

Witaj następujące przykładowe polecenia pokazują, jak hello toouse konta Uruchom jako wspomniano wcześniej, tooauthenticate z zasobami usługi Azure Resource Manager w elemencie runbook.  Używa połączenia hello zasobów reprezentujący hello konta Uruchom jako, który odwołuje się do nazwy głównej usługi oparte na certyfikatach hello, nie poświadczeń.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Przykłady graficznym elementem runbook

Możesz dodać **Get-AutomationConnection** działania tooa graficznego elementu runbook przez kliknięcie prawym przyciskiem myszy połączenie hello w okienku Biblioteka hello hello edytora graficznego i wybierając **dodać toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Witaj poniższej ilustracji przedstawiono przykład za pomocą połączenia w graficznym elementem runbook.  Jest to hello tym samym przykładzie pokazano powyżej w celu uwierzytelniania przy użyciu konta Uruchom jako hello z tekstowy.  W tym przykładzie użyto hello **wartości stałej** zestaw danych na potrzeby hello **uzyskać połączenia RunAs** działania do uwierzytelniania używa obiektu połączenia.  A [linku potoku](automation-graphical-authoring-intro.md#links-and-workflow) tutaj jest używany, ponieważ zestaw parametrów ServicePrincipalCertificate hello oczekuje pojedynczego obiektu.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Następne kroki

- Przegląd [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand jak hello toodirect i sterowania przepływem logiki w elementach runbook.  

- toolearn więcej informacji na temat automatyzacji Azure użycie moduły programu PowerShell i najlepsze rozwiązania do tworzenia własnych toowork moduły programu PowerShell jako moduły integracji w automatyzacji Azure, zobacz [moduły integracji](automation-integration-modules.md).  
