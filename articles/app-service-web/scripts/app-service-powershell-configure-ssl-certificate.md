---
title: "Przykładowy skrypt programu PowerShell - aaaAzure powiązać niestandardowej aplikacji sieci web tooa certyfikatu SSL | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — Bind niestandardowej aplikacji sieci web tooa certyfikat SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a>Powiąż niestandardowej aplikacji sieci web tooa certyfikat protokołu SSL

Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie powiązania certyfikatu SSL hello tooit nazwy domeny niestandardowej. 

Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview). Ponadto upewnij się, że:

- Utworzono połączenie z platformą Azure, za pomocą hello `az login` polecenia.
- Masz strony konfiguracji rejestratora dostępu tooyour domen DNS.
- Masz prawidłowe. Plik PFX i jego hasło dla hello SSL certyfikatów można mają tooupload i ich powiązania.

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Tworzy plan usługi App Service. |
| [Nowe AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Tworzy aplikację sieci web. |
| [Zestaw AzureRmAppServicePlan](/powershell/module/azurerm.websites/set-azurermappserviceplan) | Modyfikuje jego warstwy cenowej toochange planu usługi aplikacji. |
| [Zestaw AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | Modyfikuje konfigurację aplikacji sieci web. |
| [Nowe AzureRmWebAppSSLBinding](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | Tworzy powiązanie certyfikatu SSL dla aplikacji sieci web. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).
