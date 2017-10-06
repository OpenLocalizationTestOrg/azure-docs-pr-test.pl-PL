---
title: "Certyfikaty aaaSSL powiązania przy użyciu programu PowerShell"
description: "Dowiedz się, jak toobind SSL certyfikaty tooyour aplikacji sieci web przy użyciu programu PowerShell."
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
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Azure App Service powiązanie certyfikatu SSL za pomocą programu PowerShell
Hello wersji programu Microsoft Azure PowerShell w wersji 1.1.0 dodano nowe polecenia cmdlet, które będzie powodują hello użytkownika hello możliwości toobind istniejącego lub nowego SSL certyfikatów tooan istniejącą aplikację sieci Web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn dotyczące korzystania z usługi Azure Resource Manager toomanage poleceń cmdlet programu PowerShell systemu Azure na podstawie wyboru Twojej aplikacji sieci Web [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Przekazywanie i powiązanie nowy certyfikat SSL
Scenariusz: hello użytkownika ma zostać toobind tooone certyfikatu SSL w swojej aplikacji sieci web.

Znajomość hello Nazwa grupy zasobów, zawierającą hello aplikacji sieci web, nazwa aplikacji sieci web hello, ścieżka pliku PFX certyfikatu hello na komputerze użytkownika hello, hello hasło dla certyfikatu hello i hello niestandardową nazwę hosta, możemy użyć powitania po toocreate polecenia programu PowerShell który Powiązanie SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Należy pamiętać, że przed dodaniem aplikacji sieci web tooa powiązania SSL, musi mieć nazwę hosta (domeny niestandardowej) już skonfigurowane. Jeśli nie skonfigurowano hello nazwy hosta, a następnie wystąpi błąd "Nazwa hosta" nie istnieje podczas uruchamiania AzureRmWebAppSSLBinding nowy. Możesz dodać nazwę hosta bezpośrednio z portalu hello lub przy użyciu programu Azure PowerShell. Witaj poniższy fragment PowerShell może być tooconfigure hello hostname przed uruchomieniem nowego AzureRmWebAppSSLBinding.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Jest ważne toounderstand, który hello polecenia cmdlet Set-AzureRmWebApp zastępuje nazwy hostów hello hello aplikacji sieci web. Dlatego hello powyżej fragment programu PowerShell jest dodanie toohello istniejącej listy nazw hostów hello hello aplikacji sieci web.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Przekazywanie i powiązanie istniejącego certyfikatu SSL
Scenariusz: hello użytkownika ma zostać toobind wcześniej przekazane tooone certyfikatu SSL w swojej aplikacji sieci web.

Firma Microsoft można uzyskać hello Lista certyfikatów już przekazane tooa określonej grupy zasobów za pomocą następującego polecenia hello

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Należy pamiętać, że certyfikaty hello są określonej grupy lokalizacji i zasobów lokalnych tooa hello użytkownik musiał przekazywania toore hello certyfikatu, jeśli aplikacja sieci web skonfigurowana hello jest w innej lokalizacji i grupy zasobów, innego niż, który z hello wymagany certyfikat 

Znajomość hello Nazwa grupy zasobów, który zawiera aplikację sieci web hello, hello Nazwa aplikacji sieci web, hello odcisk palca certyfikatu i hello niestandardową nazwę hosta, możemy użyć powitania po toocreate polecenia programu PowerShell tego powiązania SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Usuwanie istniejące powiązanie SSL
Scenariusz: hello użytkownika ma zostać toodelete istniejące powiązanie SSL.

Znajomość hello Nazwa grupy zasobów, który zawiera aplikację sieci web hello, hello Nazwa aplikacji sieci web i hello niestandardową nazwę hosta, możemy użyć powitania po tooremove polecenia programu PowerShell tego powiązania SSL:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Należy pamiętać, że jeśli hello usunięte powiązanie SSL został hello ostatnio powiązanie, używając tego certyfikatu w tym miejscu przez domyślny hello certyfikat zostaną usunięte, użytkownik hello certyfikatu hello tookeep on użyć hello DeleteCertificate opcji tookeep hello certyfikatu

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Dokumentacja
* [Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Wprowadzenie tooApp środowiska usługi](app-service-app-service-environment-intro.md)
* [Używanie programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md)

