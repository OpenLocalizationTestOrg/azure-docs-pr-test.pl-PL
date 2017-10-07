---
title: "aaaIntegrate usługi Automatyzacja Azure z kontroli źródła Visual Stuido Team Services | Dokumentacja firmy Microsoft"
description: "Scenariusz przeprowadzi Cię przez proces konfigurowania integracji z kontroli źródła Visual Stuido Team Services i konto usługi Automatyzacja Azure."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "Program Azure powershell, VSTS, kontroli źródła, automatyzacji"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Scenariusz automatyzacji Azure - automatyzacji integracji kontroli źródła z Visual Studio Team Services

W tym scenariuszu masz projektu Visual Studio Team Services używasz toomanage elementu runbook usługi Automatyzacja Azure lub konfiguracji DSC pod kontrolą źródła.
W tym artykule opisano sposób toointegrate VSTS ze środowiskiem usługi Automatyzacja Azure tak się stanie w tym ciągłej integracji dla każdego wyboru.

## <a name="getting-hello-scenario"></a>Pobieranie hello scenariusza

W tym scenariuszu składa się z dwóch elementów runbook programu PowerShell, które można importować bezpośrednio z hello [galerię elementów Runbook](automation-runbook-gallery.md) w portalu Azure hello lub pobrać z hello [galerii programu PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Elementy Runbook

Element Runbook | Opis| 
--------|------------|
VSTS synchronizacji | Importowanie elementów runbook lub konfiguracje z kontroli źródła programu VSTS podczas ewidencjonowania. Jeśli ręcznie uruchom zaimportuje i opublikować wszystkie elementy runbook lub konfiguracje do hello konta automatyzacji.| 
VSTSGit synchronizacji | Importowanie elementów runbook lub konfiguracji z programu VSTS pod kontrolą źródła Git podczas ewidencjonowania. Jeśli ręcznie uruchom zaimportuje i opublikować wszystkie elementy runbook lub konfiguracje do hello konta automatyzacji.|

### <a name="variables"></a>Zmienne

Zmienna | Opis|
-----------|------------|
VSToken | Bezpieczne zasób zmiennej utworzysz zawierający hello VSTS osobisty token dostępu. Dowiedz się jak toocreate osobiste VSTS uzyskują dostęp do tokenu na powitania [strony uwierzytelniania programu VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Instalowanie i konfigurowanie scenariusza

Utwórz [osobisty token dostępu](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) w VSTS, że na koncie automatyzacji będzie używać elementów runbook hello toosync lub konfiguracji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Utwórz [bezpiecznego zmiennej](automation-variables.md) w Twojej hello toohold konta automatyzacji osobiste dostępu token, aby hello runbook mógł uwierzytelnić tooVSTS i synchronizacji elementów runbook hello lub konfiguracje do hello konta automatyzacji. Można określić nazwę tego VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importowanie elementu runbook hello, która zsynchronizuje się z elementów runbook lub konfiguracje pod uwagę automatyzacji hello. Można użyć hello [VSTS przykładowego elementu runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) lub hello [programu VSTS z Git przykładowego elementu runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) z hello PowerShellGallery.com w zależności od tego, jeśli używasz programu VSTS źródłowy formant lub VSTS za pomocą narzędzia Git i wdrażanie tooyour konta automatyzacji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Możesz teraz [publikowania](automation-creating-importing-runbook.md#publishing-a-runbook) ten element runbook, dzięki czemu można tworzyć elementu webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Utwórz [webhook](automation-webhooks.md) dla tego elementu runbook programu VSTS synchronizacji i wypełnij hello parametrów, jak pokazano poniżej. Upewnij się, że skopiuj adres url elementu webhook hello jak będą one potrzebne dla usługi haka w VSTS. Witaj VSAccessTokenVariableName jest nazwą hello (VSToken) hello zmiennej bezpiecznego utworzony wcześniej toohold hello osobisty token dostępu. 

Integrowanie z programu VSTS (synchronizacji VSTS.ps1) potrwa hello następujące parametry.
### <a name="sync-vsts-parameters"></a>Parametry programu VSTS synchronizacji

Parametr | Opis| 
--------|------------|
WebhookData | To będzie zawierać hello zaewidencjonowania informacje wysyłane z punktu zaczepienia usługi VSTS hello. Ten parametr należy pozostawić pusty.| 
ResourceGroup | Jest to nazwa hello hello grupy zasobów, które konto automatyzacji hello.|
AutomationAccountName | Nazwa Hello hello automatyzacji konta, które zostaną zsynchronizowane z usługi VSTS.|
VSFolder | Nazwa folderu hello w VSTS, jeśli istnieje hello elementów runbook i konfiguracji.|
VSAccount | Nazwa Hello hello konta usługi Visual Studio Team Services.| 
VSAccessTokenVariableName | Nazwa Hello zmiennej bezpiecznego hello (VSToken), która przechowuje hello VSTS osobisty token dostępu.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Jeśli używasz programu VSTS z usługą GIT (synchronizacji VSTSGit.ps1) potrwa hello następujące parametry.

Parametr | Opis|
--------|------------|
WebhookData | To będzie zawierać hello zaewidencjonowania informacje wysyłane z punktu zaczepienia usługi VSTS hello. Ten parametr należy pozostawić pusty.| ResourceGroup | Ta nazwa hello hello grupy zasobów, które hello konto automatyzacji jest.|
AutomationAccountName | Nazwa Hello hello automatyzacji konta, które zostaną zsynchronizowane z usługi VSTS.|
VSAccount | Nazwa Hello hello konta usługi Visual Studio Team Services.|
VSProject | Nazwa Hello hello projektu w VSTS, jeśli istnieje hello elementów runbook i konfiguracji.|
GitRepo | Nazwa Hello hello repozytorium Git.|
GitBranch | Nazwa Hello hello gałęzi w repozytorium Git programu VSTS.|
Folder | Nazwa Hello folderu hello w gałęzi VSTS Git.|
VSAccessTokenVariableName | Nazwa Hello zmiennej bezpiecznego hello (VSToken), która przechowuje hello VSTS osobisty token dostępu.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Utworzyć haka usługi w VSTS dla folderu toohello zaewidencjonowania, który wyzwala ten element webhook na ewidencjonowania kodu. Wybierz techniki Web Hooks jako hello toointegrate usługi z podczas tworzenia nowej subskrypcji. Możesz dowiedzieć się więcej o punktach wpięcia usług na [punkty zaczepienia usługi VSTS dokumentacji](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Powinny teraz być stanie toodo zaewidencjonowania wszystkich elementów runbook i konfiguracji do programu VSTS i są automatycznie synchronizowane miał na koncie automatyzacji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Jeśli ten element runbook zostanie uruchomiony ręcznie bez inicjowane przez VSTS, można pozostawić pusty parametr webhookdata hello i wykona pełną synchronizację z określonego folderu programu VSTS hello.

W razie potrzeby scenariusza hello toouninstall usuwanie hello haku usługi VSTS, Usuń hello runbook i hello VSToken zmiennej.
