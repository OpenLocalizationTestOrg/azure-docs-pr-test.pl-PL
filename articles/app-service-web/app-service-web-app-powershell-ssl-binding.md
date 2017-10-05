---
title: "Powiązanie certyfikatów SSL przy użyciu programu PowerShell"
description: "Dowiedz się, jak można powiązać certyfikaty SSL do aplikacji sieci web przy użyciu programu PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Azure App Service powiązanie certyfikatu SSL za pomocą programu PowerShell
Wraz z wydaniem programu Microsoft Azure PowerShell w wersji 1.1.0 nowe polecenie cmdlet został dodany, który będzie uzyskanie użytkownika możliwość powiązania istniejących lub nowych certyfikatów SSL do istniejącej aplikacji sieci Web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Aby dowiedzieć się więcej o korzystaniu z poleceń cmdlet programu Azure PowerShell do zarządzania wyboru Twojej aplikacji sieci Web na podstawie usługi Azure Resource Manager [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Przekazywanie i powiązanie nowy certyfikat SSL
Scenariusz: Użytkownik chce powiązać certyfikatu SSL z jednej z jego aplikacji sieci web.

Znajomość Nazwa grupy zasobów, która zawiera aplikację sieci web, nazwa aplikacji sieci web, ścieżka pliku PFX certyfikatu na komputerze użytkownika, hasło dla certyfikatu i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do tworzenia tego powiązania SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Należy pamiętać, że przed dodaniem powiązanie SSL do aplikacji sieci web, musi mieć już skonfigurowane nazwy hosta (niestandardowe domeny). Jeśli nie skonfigurowano nazwy hosta, a następnie będzie wyświetlany komunikat o błędzie "Nazwa hosta" nie istnieje podczas uruchamiania AzureRmWebAppSSLBinding nowy. Bezpośrednio w portalu lub przy użyciu programu Azure PowerShell, można dodać nazwę hosta. Poniższy fragment kodu programu PowerShell można skonfigurować przed uruchomieniem nowego AzureRmWebAppSSLBinding nazwy hosta.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Należy zrozumieć, że polecenia cmdlet Set-AzureRmWebApp zastępuje nazwy hostów dla aplikacji sieci web. Dlatego powyżej fragment programu PowerShell jest dołączenie do istniejącej listy nazwy hostów dla aplikacji sieci web.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Przekazywanie i powiązanie istniejącego certyfikatu SSL
Scenariusz: Użytkownik chce powiązać wcześniej przekazane certyfikaty SSL do jednego z jego aplikacji sieci web.

Możemy uzyskać listę certyfikatów już przekazany do określonej grupy zasobów za pomocą następującego polecenia

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Należy pamiętać, że certyfikaty znajdują się lokalnie do określonej lokalizacji i grupy zasobów, użytkownik będzie musiał ponownie przekazać certyfikat, jeśli aplikacja sieci web skonfigurowana jest w innej lokalizacji i grupy zasobów, innego niż który potrzebny certyfikat 

Znajomość nazwy grupy zasobów, która zawiera aplikacji sieci web, nazwa aplikacji sieci web, odcisk palca certyfikatu i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do tworzenia tego powiązania SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Usuwanie istniejące powiązanie SSL
Scenariusz: Użytkownik chce usunąć istniejące powiązanie SSL.

Znajomość Nazwa grupy zasobów, który zawiera aplikacji sieci web, nazwa aplikacji sieci web i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do usunięcia tego powiązania SSL:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Należy pamiętać, że jeśli usunięte powiązanie SSL był ostatni powiązania przy użyciu tego certyfikatu w tej lokalizacji, domyślnie certyfikat będzie można usunąć, jeśli użytkownik chce zachować certyfikatów, może użyć opcji DeleteCertificate w celu zachowania certyfikatu

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Dokumentacja
* [Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Wprowadzenie do usługi App Service Environment](app-service-app-service-environment-intro.md)
* [Używanie programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)

