---
title: zasoby aaaCertificate automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Certyfikaty można bezpiecznie przechowywane w usłudze Automatyzacja Azure, są one dostępne przez elementy runbook lub tooauthenticate konfiguracji DSC dla platformy Azure i zasobów firm zewnętrznych.  W tym artykule opisano szczegóły hello certyfikatów i w jaki sposób toowork z nimi w tworzeniu zarówno tekstową i graficznego."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Zasoby certyfikatu usługi Automatyzacja Azure

Certyfikaty mogą być bezpiecznie przechowywane w automatyzacji Azure, są one dostępne przez elementy runbook lub przy użyciu hello konfiguracji DSC **Get AzureRmAutomationRmCertificate** działania dla zasobów usługi Azure Resource Manager. To pozwala toocreate elementów runbook i konfiguracji DSC, które korzystają z certyfikatów do uwierzytelniania lub dodaje je tooAzure lub innych firm.

> [!NOTE] 
> Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne. Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji. Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure. Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.
> 

## <a name="windows-powershell-cmdlets"></a>Polecenia cmdlet programu Windows PowerShell

polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate i zarządzać zasobami certyfikatu usługi Automatyzacja przy użyciu programu Windows PowerShell. One dostarczane jako część hello [modułu Azure PowerShell](../powershell-install-configure.md) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.

|Polecenia cmdlet|Opis|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Pobiera informacje o toouse certyfikatu, element runbook lub konfiguracji DSC. Sam certyfikat hello można pobrać tylko z działania Get AutomationCertificate.|
|[Nowe AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Tworzy nowy certyfikat w automatyzacji Azure.|
[Usuń AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Usuwa certyfikat usługi Automatyzacja Azure.|Tworzy nowy certyfikat w automatyzacji Azure.
|[Zestaw AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Ustawia właściwości hello istniejącego certyfikatu, takich jak przekazywanie pliku certyfikatu hello i ustawienie hello hasło dla pliku pfx.|
|[Dodaj AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Przekazywanie certyfikatu usługi dla hello określona usługa w chmurze.|


## <a name="creating-a-new-certificate"></a>Tworzenie nowego certyfikatu

Podczas tworzenia nowego certyfikatu, możesz przekazać cer lub PFX pliku tooAzure automatyzacji. Jeśli certyfikat hello jako możliwy do wyeksportowania, następnie można przenieść go z magazynu certyfikatów usługi Automatyzacja Azure hello. Jeśli nie jest możliwy do wyeksportowania, następnie można można używać tylko do podpisywania w ramach elementu runbook hello lub konfiguracji DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate nowy certyfikat z hello portalu Azure

1. Twoje konto usługi Automatyzacja kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.
1. Kliknij przycisk hello **certyfikaty** hello tooopen kafelka **certyfikaty** bloku.
1. Kliknij przycisk **Dodawanie certyfikatu** u góry bloku hello hello.
2. Wpisz nazwę certyfikatu hello hello **nazwa** pole.
2. Kliknij przycisk **wybierz plik** w obszarze **przekazać plik certyfikatu** toobrowse dla pliku cer lub pfx.  W przypadku wybrania pliku PFX, określ hasło oraz czy jej powinno być dozwolone toobe wyeksportowane.
1. Kliknij przycisk **Utwórz** toosave hello nowy zasób certyfikatu.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate nowy certyfikat przy użyciu programu Windows PowerShell

Hello poniższym przykładzie pokazano, jak toocreate automatyzacji nowego certyfikatu i oznacz ją jako eksportowalny. To importuje istniejący plik pfx.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Przy użyciu certyfikatu

Należy użyć hello **Get-AutomationCertificate** toouse działania certyfikatu. Nie można użyć hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) polecenia cmdlet, ponieważ zwraca informacje o hello zasób certyfikatu, ale nie hello sam certyfikat.

### <a name="textual-runbook-sample"></a>Przykład tekstowy

powitania po przykładowy kod pokazuje, jak tooadd tooa certyfikatu w chmurze usługi w elemencie runbook. W tym przykładzie hasło hello jest pobierana z zmiennej automatyzacji zaszyfrowane.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Przykładowe graficznym elementem runbook

Możesz dodać **Get-AutomationCertificate** tooa graficznym elementem runbook, klikając prawym przyciskiem myszy na powitania certyfikatu w okienku Biblioteka hello hello edytora graficznego i wybierając **dodać toocanvas**.

![Dodaj certyfikat toohello kanwy](media/automation-certificates/automation-certificate-add-to-canvas.png)

Witaj poniższej ilustracji przedstawiono przykład za pomocą certyfikatu w graficznym elementem runbook.  Jest to hello tym samym przykładzie pokazano powyżej dodawania usługi w chmurze tooa certyfikatu z poziomu tekstowy.

![Przykład tworzenia graficznego ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Następne kroki

- więcej informacji na temat pracy z łącza toocontrol hello logicznego przepływu działania elementu runbook jest toolearn zaprojektowane tooperform, zobacz [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow). 
