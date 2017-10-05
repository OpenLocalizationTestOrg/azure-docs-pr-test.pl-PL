---
title: "Role usługi w chmurze Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi w chmurze Azure. Odpowiedzi na często zadawane pytania dotyczące certyfikatów, role sieci web i roli proces roboczy."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="90214-104">Cloud Services — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="90214-104">Cloud Services FAQ</span></span>
<span data-ttu-id="90214-105">Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące usługi w chmurze Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90214-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="90214-106">Możesz również odwiedzić [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083) ogólne informacje Azure cennik i pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="90214-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="90214-107">Można również znaleźć [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="90214-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="90214-108">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="90214-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="90214-109">Gdzie zainstalować certyfikatu?</span><span class="sxs-lookup"><span data-stu-id="90214-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="90214-110">**Moje**</span><span class="sxs-lookup"><span data-stu-id="90214-110">**My**</span></span>  
  <span data-ttu-id="90214-111">Aplikacja certyfikatu z kluczem prywatnym (\*PFX, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="90214-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="90214-112">**URZĄD CERTYFIKACJI**</span><span class="sxs-lookup"><span data-stu-id="90214-112">**CA**</span></span>  
  <span data-ttu-id="90214-113">Wszystkie certyfikaty pośrednie Przejdź w tym magazynie (zasad i podrzędne urzędy certyfikacji).</span><span class="sxs-lookup"><span data-stu-id="90214-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="90214-114">**GŁÓWNY**</span><span class="sxs-lookup"><span data-stu-id="90214-114">**ROOT**</span></span>  
  <span data-ttu-id="90214-115">Główny urząd certyfikacji sklepu, więc Twojego głównego certyfikatu urzędu certyfikacji należy tutaj wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="90214-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="90214-116">Nie można usunąć wygasłego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="90214-116">I can't remove expired certificate</span></span>
<span data-ttu-id="90214-117">Azure uniemożliwia usunięcie certyfikatu, gdy jest używany.</span><span class="sxs-lookup"><span data-stu-id="90214-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="90214-118">Należy usunąć wdrożenia, który używa certyfikatu lub aktualizuje wdrożenie przy użyciu różnych lub odnowionego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="90214-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="90214-119">Usuwanie wygasłego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="90214-119">Delete an expired certificate</span></span>
<span data-ttu-id="90214-120">Tak długo, jak certyfikat nie jest używany, można użyć [AzureCertificate Usuń](https://msdn.microsoft.com/library/azure/mt589145.aspx) polecenia cmdlet programu PowerShell, aby usunąć certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="90214-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="90214-121">Wygasnąć certyfikatów o nazwie zarządzania usługą Windows Azure dla rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="90214-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="90214-122">Te certyfikaty są tworzone w każdym przypadku, gdy rozszerzenie zostanie dodane do usługi w chmurze np. rozszerzenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="90214-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="90214-123">Te certyfikaty są używane tylko do szyfrowania i odszyfrowywania prywatna Konfiguracja rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="90214-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="90214-124">Nie ma znaczenia, jeśli te certyfikaty wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="90214-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="90214-125">Data wygaśnięcia nie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="90214-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="90214-126">Certyfikaty, usuwać I nadal wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="90214-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="90214-127">Te ciągle pojawiają się prawdopodobnie z powodu narzędzia, którego używasz, takiego jak Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90214-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="90214-128">Przy każdym ponownym połączeniu z narzędziem, które używa certyfikatu, ponownie zostanie przekazany do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90214-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="90214-129">Zachowaj zniknął certyfikatów</span><span class="sxs-lookup"><span data-stu-id="90214-129">My certificates keep disappearing</span></span>
<span data-ttu-id="90214-130">Gdy wystąpienie maszyny wirtualnej jest odtwarzany, wszystkie lokalne zmiany zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="90214-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="90214-131">Użyj [zadanie uruchamiania](cloud-services-startup-tasks.md) instalowanie certyfikatów do maszyny wirtualnej w każdym uruchomieniu roli.</span><span class="sxs-lookup"><span data-stu-id="90214-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="90214-132">Nie można znaleźć w portalu certyfikatów zarządzania</span><span class="sxs-lookup"><span data-stu-id="90214-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="90214-133">[Certyfikaty zarządzania](../azure-api-management-certs.md) są dostępne tylko w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="90214-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="90214-134">Bieżącego portalu platformy Azure nie korzysta z certyfikatów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="90214-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="90214-135">Jak wyłączyć certyfikatu zarządzania</span><span class="sxs-lookup"><span data-stu-id="90214-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="90214-136">[Certyfikaty zarządzania](../azure-api-management-certs.md) nie może zostać wyłączone.</span><span class="sxs-lookup"><span data-stu-id="90214-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="90214-137">Należy usunąć je za pośrednictwem klasycznego portalu Azure, jeśli nie chcesz, aby go już używać.</span><span class="sxs-lookup"><span data-stu-id="90214-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="90214-138">Jak utworzyć certyfikat SSL dla określonego adresu IP?</span><span class="sxs-lookup"><span data-stu-id="90214-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="90214-139">Postępuj zgodnie z instrukcjami w [utworzyć samouczek certyfikatu](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="90214-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="90214-140">Użyj adresu IP z nazwą DNS.</span><span class="sxs-lookup"><span data-stu-id="90214-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="90214-141">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="90214-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="90214-142">Wyłączyć protokół SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="90214-142">Disable SSL 3.0</span></span>
<span data-ttu-id="90214-143">Aby wyłączyć protokół SSL 3.0 i korzystanie z zabezpieczeń TLS, należy utworzyć zadanie uruchamiania, który jest udokumentowany na ten wpis w blogu: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="90214-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="90214-144">Dodaj **nosniff** do witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="90214-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="90214-145">Aby uniemożliwić klientom wykrywanie typów MIME, Dodaj ustawienie w Twojej *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="90214-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="90214-146">Można również dodać to ustawienie w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="90214-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="90214-147">Użyj następującego polecenia z [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.</span><span class="sxs-lookup"><span data-stu-id="90214-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="90214-148">Dostosowywanie usług IIS dla roli sieci web</span><span class="sxs-lookup"><span data-stu-id="90214-148">Customize IIS for a web role</span></span>
<span data-ttu-id="90214-149">Użyj skryptu uruchamiania usług IIS z [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.</span><span class="sxs-lookup"><span data-stu-id="90214-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="90214-150">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="90214-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="90214-151">Nie można skalować poza X wystąpień</span><span class="sxs-lookup"><span data-stu-id="90214-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="90214-152">Subskrypcji platformy Azure ma limit liczby rdzeni, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="90214-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="90214-153">Skalowanie nie będzie działać, jeśli zostały użyte wszystkie dostępne rdzenie.</span><span class="sxs-lookup"><span data-stu-id="90214-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="90214-154">Na przykład jeśli istnieje limit liczby rdzeni (100), oznacza to, może mieć 100 wystąpień maszyna wirtualna A1 o rozmiarze dla usługi w chmurze lub wystąpieniu maszyny wirtualnej o rozmiarze 50 A2.</span><span class="sxs-lookup"><span data-stu-id="90214-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="90214-155">Sieć</span><span class="sxs-lookup"><span data-stu-id="90214-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="90214-156">I nie można zastrzec adresu IP w usłudze chmury wielu wirtualnych adresów IP</span><span class="sxs-lookup"><span data-stu-id="90214-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="90214-157">Najpierw upewnij się, że wystąpienie maszyny wirtualnej, który próbujesz zastrzec adresu IP dla jest włączona.</span><span class="sxs-lookup"><span data-stu-id="90214-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="90214-158">Po drugie upewnij się, że używasz zastrzeżonych adresów IP dla odblokowane wdrożeń tymczasowych i produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="90214-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="90214-159">**Nie** zmiany ustawień podczas uaktualniania jest wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="90214-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="90214-160">Pulpit zdalny</span><span class="sxs-lookup"><span data-stu-id="90214-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="90214-161">Jak Pulpit zdalny gdy grupa NSG?</span><span class="sxs-lookup"><span data-stu-id="90214-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="90214-162">Dodaj reguły do grupy NSG, które zezwalają na ruch na portach **3389** i **20000**.</span><span class="sxs-lookup"><span data-stu-id="90214-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="90214-163">Pulpit zdalny używa portu **3389**.</span><span class="sxs-lookup"><span data-stu-id="90214-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="90214-164">Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować którego wystąpienia, aby nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="90214-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="90214-165">*RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i umożliwić klientom wysyłanie plików cookie protokołu RDP i określ poszczególne wystąpienia do nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="90214-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="90214-166">*RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="90214-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
