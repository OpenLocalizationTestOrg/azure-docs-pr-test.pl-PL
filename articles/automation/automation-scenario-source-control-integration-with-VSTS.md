---
title: "Integracja usługi Automatyzacja Azure z kontroli źródła Visual Stuido Team Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Scenariusz automatyzacji Azure - automatyzacji integracji kontroli źródła z Visual Studio Team Services

W tym scenariuszu masz projektu Visual Studio Team Services, używanej do zarządzania elementami runbook usługi Automatyzacja Azure lub konfiguracji DSC pod kontrolą źródła.
W tym artykule opisano sposób integrowania programu VSTS ze środowiskiem usługi Automatyzacja Azure dzięki temu ciągłej integracji odbywa się dla każdego wyboru.

## <a name="getting-the-scenario"></a>Uzyskiwanie scenariusza

W tym scenariuszu składa się z dwóch elementów runbook programu PowerShell, które można importować bezpośrednio z [galerię elementów Runbook](automation-runbook-gallery.md) w portalu Azure lub pobrać z [galerii programu PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Elementy Runbook

Element Runbook | Opis| 
--------|------------|
VSTS synchronizacji | Importowanie elementów runbook lub konfiguracje z kontroli źródła programu VSTS podczas ewidencjonowania. Jeśli ręcznie uruchom zaimportuje i opublikować wszystkie elementy runbook lub konfiguracje do konta automatyzacji.| 
VSTSGit synchronizacji | Importowanie elementów runbook lub konfiguracji z programu VSTS pod kontrolą źródła Git podczas ewidencjonowania. Jeśli ręcznie uruchom zaimportuje i opublikować wszystkie elementy runbook lub konfiguracje do konta automatyzacji.|

### <a name="variables"></a>Zmienne

Zmienna | Opis|
-----------|------------|
VSToken | Bezpieczne zasób zmiennej utworzysz zawierający VSTS osobisty token dostępu. Znajdują się informacje dotyczące tworzenia VSTS osobisty token dostępu na [strony uwierzytelniania programu VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Instalowanie i konfigurowanie scenariusza

Utwórz [osobisty token dostępu](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) w VSTS, który będzie używany do synchronizacji elementów runbook lub konfiguracje na koncie automatyzacji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Utwórz [bezpiecznego zmiennej](automation-variables.md) na Twoim koncie automatyzacji do przechowywania osobisty token dostępu, aby element runbook mógł uwierzytelniania programu VSTS i synchronizacji elementów runbook i konfiguracji do konta automatyzacji. Można określić nazwę tego VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Zaimportuj element runbook, która zsynchronizuje się z elementów runbook lub konfiguracje do konta automatyzacji. Można użyć [VSTS przykładowego elementu runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) lub [programu VSTS z Git przykładowego elementu runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) z PowerShellGallery.com w zależności od tego, jeśli do kontroli źródła programu VSTS lub VSTS za pomocą narzędzia Git i wdrożyć na koncie automatyzacji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Możesz teraz [publikowania](automation-creating-importing-runbook.md#publishing-a-runbook) ten element runbook, dzięki czemu można tworzyć elementu webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Utwórz [webhook](automation-webhooks.md) dla tego elementu runbook programu VSTS synchronizacji i wypełnij parametrów, jak pokazano poniżej. Upewnij się, że skopiuj adres url elementu webhook, ponieważ będzie potrzebny dla usługi haka w VSTS. VSAccessTokenVariableName jest nazwą (VSToken) bezpiecznego zmiennej utworzoną wcześniej do przechowywania osobisty token dostępu. 

Integrowanie z programu VSTS (synchronizacji VSTS.ps1) potrwa następujące parametry.
### <a name="sync-vsts-parameters"></a>Parametry programu VSTS synchronizacji

Parametr | Opis| 
--------|------------|
WebhookData | To będzie zawierać informacje zaewidencjonowania wysyłane z haku usługi VSTS. Ten parametr należy pozostawić pusty.| 
ResourceGroup | Jest to nazwa grupy zasobów jest konta automatyzacji.|
AutomationAccountName | Nazwa konta automatyzacji, która zsynchronizuje się z usługi VSTS.|
VSFolder | Nazwa folderu w VSTS, jeśli istnieją elementy runbook i konfiguracji.|
VSAccount | Nazwa konta usługi Visual Studio Team Services.| 
VSAccessTokenVariableName | Nazwa zmiennej bezpiecznego (VSToken), która przechowuje VSTS osobisty token dostępu.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Jeśli używasz programu VSTS z usługą GIT (synchronizacji VSTSGit.ps1) potrwa następujące parametry.

Parametr | Opis|
--------|------------|
WebhookData | To będzie zawierać informacje zaewidencjonowania wysyłane z haku usługi VSTS. Ten parametr należy pozostawić pusty.| ResourceGroup | Ta nazwa grupy zasobów jest konto automatyzacji.|
AutomationAccountName | Nazwa konta automatyzacji, która zsynchronizuje się z usługi VSTS.|
VSAccount | Nazwa konta usługi Visual Studio Team Services.|
VSProject | Nazwa projektu w VSTS, jeśli istnieją elementy runbook i konfiguracji.|
GitRepo | Nazwa repozytorium Git.|
GitBranch | Nazwa gałęzi w repozytorium Git programu VSTS.|
Folder | Nazwa folderu w gałęzi VSTS Git.|
VSAccessTokenVariableName | Nazwa zmiennej bezpiecznego (VSToken), która przechowuje VSTS osobisty token dostępu.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Utworzyć haka usługi w VSTS do zaewidencjonowania do folderu, który wyzwala ten element webhook na ewidencjonowania kodu. Wybierz techniki Web Hooks jako usługa integracji z podczas tworzenia nowej subskrypcji. Możesz dowiedzieć się więcej o punktach wpięcia usług na [punkty zaczepienia usługi VSTS dokumentacji](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Teraz powinno być możliwe zaewidencjonowania wszystkich elementów runbook i konfiguracji do programu VSTS i są automatycznie d synchronizacji na koncie automatyzacji.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Jeśli ten element runbook zostanie uruchomiony ręcznie bez inicjowane przez VSTS, można pozostawić pusty parametr webhookdata i wykona pełną synchronizację z folderu programu VSTS określony.

Jeśli chcesz odinstalować scenariusz, Usuń haku usługi z programu VSTS, Usuń element runbook, a zmienna VSToken.
