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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="897c8-103">Azure App Service powiązanie certyfikatu SSL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="897c8-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="897c8-104">Hello wersji programu Microsoft Azure PowerShell w wersji 1.1.0 dodano nowe polecenia cmdlet, które będzie powodują hello użytkownika hello możliwości toobind istniejącego lub nowego SSL certyfikatów tooan istniejącą aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="897c8-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="897c8-105">toolearn dotyczące korzystania z usługi Azure Resource Manager toomanage poleceń cmdlet programu PowerShell systemu Azure na podstawie wyboru Twojej aplikacji sieci Web [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="897c8-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="897c8-106">Przekazywanie i powiązanie nowy certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="897c8-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="897c8-107">Scenariusz: hello użytkownika ma zostać toobind tooone certyfikatu SSL w swojej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="897c8-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="897c8-108">Znajomość hello Nazwa grupy zasobów, zawierającą hello aplikacji sieci web, nazwa aplikacji sieci web hello, ścieżka pliku PFX certyfikatu hello na komputerze użytkownika hello, hello hasło dla certyfikatu hello i hello niestandardową nazwę hosta, możemy użyć powitania po toocreate polecenia programu PowerShell który Powiązanie SSL:</span><span class="sxs-lookup"><span data-stu-id="897c8-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="897c8-109">Należy pamiętać, że przed dodaniem aplikacji sieci web tooa powiązania SSL, musi mieć nazwę hosta (domeny niestandardowej) już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="897c8-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="897c8-110">Jeśli nie skonfigurowano hello nazwy hosta, a następnie wystąpi błąd "Nazwa hosta" nie istnieje podczas uruchamiania AzureRmWebAppSSLBinding nowy.</span><span class="sxs-lookup"><span data-stu-id="897c8-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="897c8-111">Możesz dodać nazwę hosta bezpośrednio z portalu hello lub przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="897c8-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="897c8-112">Witaj poniższy fragment PowerShell może być tooconfigure hello hostname przed uruchomieniem nowego AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="897c8-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="897c8-113">Jest ważne toounderstand, który hello polecenia cmdlet Set-AzureRmWebApp zastępuje nazwy hostów hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="897c8-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="897c8-114">Dlatego hello powyżej fragment programu PowerShell jest dodanie toohello istniejącej listy nazw hostów hello hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="897c8-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="897c8-115">Przekazywanie i powiązanie istniejącego certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="897c8-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="897c8-116">Scenariusz: hello użytkownika ma zostać toobind wcześniej przekazane tooone certyfikatu SSL w swojej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="897c8-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="897c8-117">Firma Microsoft można uzyskać hello Lista certyfikatów już przekazane tooa określonej grupy zasobów za pomocą następującego polecenia hello</span><span class="sxs-lookup"><span data-stu-id="897c8-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="897c8-118">Należy pamiętać, że certyfikaty hello są określonej grupy lokalizacji i zasobów lokalnych tooa hello użytkownik musiał przekazywania toore hello certyfikatu, jeśli aplikacja sieci web skonfigurowana hello jest w innej lokalizacji i grupy zasobów, innego niż, który z hello wymagany certyfikat</span><span class="sxs-lookup"><span data-stu-id="897c8-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="897c8-119">Znajomość hello Nazwa grupy zasobów, który zawiera aplikację sieci web hello, hello Nazwa aplikacji sieci web, hello odcisk palca certyfikatu i hello niestandardową nazwę hosta, możemy użyć powitania po toocreate polecenia programu PowerShell tego powiązania SSL:</span><span class="sxs-lookup"><span data-stu-id="897c8-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="897c8-120">Usuwanie istniejące powiązanie SSL</span><span class="sxs-lookup"><span data-stu-id="897c8-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="897c8-121">Scenariusz: hello użytkownika ma zostać toodelete istniejące powiązanie SSL.</span><span class="sxs-lookup"><span data-stu-id="897c8-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="897c8-122">Znajomość hello Nazwa grupy zasobów, który zawiera aplikację sieci web hello, hello Nazwa aplikacji sieci web i hello niestandardową nazwę hosta, możemy użyć powitania po tooremove polecenia programu PowerShell tego powiązania SSL:</span><span class="sxs-lookup"><span data-stu-id="897c8-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="897c8-123">Należy pamiętać, że jeśli hello usunięte powiązanie SSL został hello ostatnio powiązanie, używając tego certyfikatu w tym miejscu przez domyślny hello certyfikat zostaną usunięte, użytkownik hello certyfikatu hello tookeep on użyć hello DeleteCertificate opcji tookeep hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="897c8-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="897c8-124">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="897c8-124">References</span></span>
* [<span data-ttu-id="897c8-125">Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="897c8-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="897c8-126">Wprowadzenie tooApp środowiska usługi</span><span class="sxs-lookup"><span data-stu-id="897c8-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="897c8-127">Używanie programu Azure PowerShell z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="897c8-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

