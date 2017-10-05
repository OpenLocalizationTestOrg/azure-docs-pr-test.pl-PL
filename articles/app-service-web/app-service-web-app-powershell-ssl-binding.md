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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="4c448-103">Azure App Service powiązanie certyfikatu SSL za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c448-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="4c448-104">Wraz z wydaniem programu Microsoft Azure PowerShell w wersji 1.1.0 nowe polecenie cmdlet został dodany, który będzie uzyskanie użytkownika możliwość powiązania istniejących lub nowych certyfikatów SSL do istniejącej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4c448-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="4c448-105">Aby dowiedzieć się więcej o korzystaniu z poleceń cmdlet programu Azure PowerShell do zarządzania wyboru Twojej aplikacji sieci Web na podstawie usługi Azure Resource Manager [usługi Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4c448-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="4c448-106">Przekazywanie i powiązanie nowy certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="4c448-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="4c448-107">Scenariusz: Użytkownik chce powiązać certyfikatu SSL z jednej z jego aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4c448-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="4c448-108">Znajomość Nazwa grupy zasobów, która zawiera aplikację sieci web, nazwa aplikacji sieci web, ścieżka pliku PFX certyfikatu na komputerze użytkownika, hasło dla certyfikatu i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do tworzenia tego powiązania SSL:</span><span class="sxs-lookup"><span data-stu-id="4c448-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="4c448-109">Należy pamiętać, że przed dodaniem powiązanie SSL do aplikacji sieci web, musi mieć już skonfigurowane nazwy hosta (niestandardowe domeny).</span><span class="sxs-lookup"><span data-stu-id="4c448-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="4c448-110">Jeśli nie skonfigurowano nazwy hosta, a następnie będzie wyświetlany komunikat o błędzie "Nazwa hosta" nie istnieje podczas uruchamiania AzureRmWebAppSSLBinding nowy.</span><span class="sxs-lookup"><span data-stu-id="4c448-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="4c448-111">Bezpośrednio w portalu lub przy użyciu programu Azure PowerShell, można dodać nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="4c448-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="4c448-112">Poniższy fragment kodu programu PowerShell można skonfigurować przed uruchomieniem nowego AzureRmWebAppSSLBinding nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="4c448-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="4c448-113">Należy zrozumieć, że polecenia cmdlet Set-AzureRmWebApp zastępuje nazwy hostów dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4c448-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="4c448-114">Dlatego powyżej fragment programu PowerShell jest dołączenie do istniejącej listy nazwy hostów dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4c448-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="4c448-115">Przekazywanie i powiązanie istniejącego certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="4c448-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="4c448-116">Scenariusz: Użytkownik chce powiązać wcześniej przekazane certyfikaty SSL do jednego z jego aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4c448-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="4c448-117">Możemy uzyskać listę certyfikatów już przekazany do określonej grupy zasobów za pomocą następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="4c448-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="4c448-118">Należy pamiętać, że certyfikaty znajdują się lokalnie do określonej lokalizacji i grupy zasobów, użytkownik będzie musiał ponownie przekazać certyfikat, jeśli aplikacja sieci web skonfigurowana jest w innej lokalizacji i grupy zasobów, innego niż który potrzebny certyfikat</span><span class="sxs-lookup"><span data-stu-id="4c448-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="4c448-119">Znajomość nazwy grupy zasobów, która zawiera aplikacji sieci web, nazwa aplikacji sieci web, odcisk palca certyfikatu i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do tworzenia tego powiązania SSL:</span><span class="sxs-lookup"><span data-stu-id="4c448-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="4c448-120">Usuwanie istniejące powiązanie SSL</span><span class="sxs-lookup"><span data-stu-id="4c448-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="4c448-121">Scenariusz: Użytkownik chce usunąć istniejące powiązanie SSL.</span><span class="sxs-lookup"><span data-stu-id="4c448-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="4c448-122">Znajomość Nazwa grupy zasobów, który zawiera aplikacji sieci web, nazwa aplikacji sieci web i niestandardową nazwę hosta, możemy użyć następującego polecenia programu PowerShell do usunięcia tego powiązania SSL:</span><span class="sxs-lookup"><span data-stu-id="4c448-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="4c448-123">Należy pamiętać, że jeśli usunięte powiązanie SSL był ostatni powiązania przy użyciu tego certyfikatu w tej lokalizacji, domyślnie certyfikat będzie można usunąć, jeśli użytkownik chce zachować certyfikatów, może użyć opcji DeleteCertificate w celu zachowania certyfikatu</span><span class="sxs-lookup"><span data-stu-id="4c448-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="4c448-124">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="4c448-124">References</span></span>
* [<span data-ttu-id="4c448-125">Usługa Azure Resource Manager na podstawie poleceń programu PowerShell dla aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="4c448-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="4c448-126">Wprowadzenie do usługi App Service Environment</span><span class="sxs-lookup"><span data-stu-id="4c448-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="4c448-127">Używanie programu Azure PowerShell z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c448-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

