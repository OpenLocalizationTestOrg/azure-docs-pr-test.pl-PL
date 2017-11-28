---
title: "Role usługi w chmurze aaaAzure — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="81e66-104">Cloud Services — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="81e66-104">Cloud Services FAQ</span></span>
<span data-ttu-id="81e66-105">Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące usługi w chmurze Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="81e66-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="81e66-106">Możesz również odwiedzić hello [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083) ogólne informacje Azure cennik i pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="81e66-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="81e66-107">Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="81e66-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="81e66-108">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="81e66-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="81e66-109">Gdzie zainstalować certyfikatu?</span><span class="sxs-lookup"><span data-stu-id="81e66-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="81e66-110">**Moje**</span><span class="sxs-lookup"><span data-stu-id="81e66-110">**My**</span></span>  
  <span data-ttu-id="81e66-111">Aplikacja certyfikatu z kluczem prywatnym (\*PFX, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="81e66-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="81e66-112">**URZĄD CERTYFIKACJI**</span><span class="sxs-lookup"><span data-stu-id="81e66-112">**CA**</span></span>  
  <span data-ttu-id="81e66-113">Wszystkie certyfikaty pośrednie Przejdź w tym magazynie (zasad i podrzędne urzędy certyfikacji).</span><span class="sxs-lookup"><span data-stu-id="81e66-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="81e66-114">**GŁÓWNY**</span><span class="sxs-lookup"><span data-stu-id="81e66-114">**ROOT**</span></span>  
  <span data-ttu-id="81e66-115">Witaj głównego urzędu certyfikacji sklepu, więc Twojego głównego certyfikatu urzędu certyfikacji należy tutaj wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="81e66-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="81e66-116">Nie można usunąć wygasłego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="81e66-116">I can't remove expired certificate</span></span>
<span data-ttu-id="81e66-117">Azure uniemożliwia usunięcie certyfikatu, gdy jest używany.</span><span class="sxs-lookup"><span data-stu-id="81e66-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="81e66-118">Należy tooeither usunięcie hello wdrożenia korzystającego z certyfikatu hello lub wdrożenia hello aktualizacji przy użyciu różnych lub odnowionego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="81e66-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="81e66-119">Usuwanie wygasłego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="81e66-119">Delete an expired certificate</span></span>
<span data-ttu-id="81e66-120">Tak długo, jak hello certyfikatu nie jest używany, można użyć hello [AzureCertificate Usuń](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove polecenia cmdlet programu PowerShell certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="81e66-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="81e66-121">Wygasnąć certyfikatów o nazwie zarządzania usługą Windows Azure dla rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="81e66-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="81e66-122">Te certyfikaty są tworzone w każdym przypadku, gdy rozszerzenie zostanie dodane usługi w chmurze toohello takich jak hello rozszerzenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="81e66-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="81e66-123">Te certyfikaty są używane tylko do szyfrowania i odszyfrowywania hello prywatna Konfiguracja rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="81e66-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="81e66-124">Nie ma znaczenia, jeśli te certyfikaty wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="81e66-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="81e66-125">Data wygaśnięcia Hello nie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="81e66-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="81e66-126">Certyfikaty, usuwać I nadal wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="81e66-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="81e66-127">Te ciągle pojawiają się prawdopodobnie z powodu narzędzia, którego używasz, takiego jak Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81e66-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="81e66-128">Przy każdym ponownym połączeniu z narzędziem, które używa certyfikatu, konieczne będzie ponownie tooAzure przekazane.</span><span class="sxs-lookup"><span data-stu-id="81e66-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="81e66-129">Zachowaj zniknął certyfikatów</span><span class="sxs-lookup"><span data-stu-id="81e66-129">My certificates keep disappearing</span></span>
<span data-ttu-id="81e66-130">Podczas odtwarzania hello wystąpienie maszyny wirtualnej, wszystkie lokalne zmiany zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="81e66-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="81e66-131">Użyj [zadanie uruchamiania](cloud-services-startup-tasks.md) maszyny wirtualnej toohello certyfikaty tooinstall każdej roli hello czasu uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="81e66-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="81e66-132">Nie można znaleźć certyfikatów zarządzania w portalu hello</span><span class="sxs-lookup"><span data-stu-id="81e66-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="81e66-133">[Certyfikaty zarządzania](../azure-api-management-certs.md) są dostępne tylko w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81e66-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="81e66-134">Witaj bieżącego portalu platformy Azure nie korzysta z certyfikatów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="81e66-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="81e66-135">Jak wyłączyć certyfikatu zarządzania</span><span class="sxs-lookup"><span data-stu-id="81e66-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="81e66-136">[Certyfikaty zarządzania](../azure-api-management-certs.md) nie może zostać wyłączone.</span><span class="sxs-lookup"><span data-stu-id="81e66-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="81e66-137">Należy usunąć je za pośrednictwem hello klasycznego portalu Azure, jeśli nie chcesz, aby je toobe już używać.</span><span class="sxs-lookup"><span data-stu-id="81e66-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="81e66-138">Jak utworzyć certyfikat SSL dla określonego adresu IP?</span><span class="sxs-lookup"><span data-stu-id="81e66-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="81e66-139">Postępuj zgodnie ze wskazówkami hello hello [utworzyć samouczek certyfikatu](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="81e66-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="81e66-140">Użyj adresu IP hello, jak hello nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="81e66-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="81e66-141">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="81e66-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="81e66-142">Wyłączyć protokół SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="81e66-142">Disable SSL 3.0</span></span>
<span data-ttu-id="81e66-143">toodisable protokołu SSL 3.0 i użycie zabezpieczeń TLS, Utwórz zadanie uruchamiania, który jest udokumentowany na ten wpis w blogu: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="81e66-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="81e66-144">Dodaj **nosniff** tooyour witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="81e66-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="81e66-145">tooprevent klientom wykrywanie typy MIME hello, Dodaj ustawienie w Twojej *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="81e66-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="81e66-146">Można również dodać to ustawienie w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="81e66-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="81e66-147">Użyj hello następujące polecenie z hello [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.</span><span class="sxs-lookup"><span data-stu-id="81e66-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="81e66-148">Dostosowywanie usług IIS dla roli sieci web</span><span class="sxs-lookup"><span data-stu-id="81e66-148">Customize IIS for a web role</span></span>
<span data-ttu-id="81e66-149">Użyj skryptu uruchamiania usług IIS hello z hello [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artykułu.</span><span class="sxs-lookup"><span data-stu-id="81e66-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="81e66-150">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="81e66-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="81e66-151">Nie można skalować poza X wystąpień</span><span class="sxs-lookup"><span data-stu-id="81e66-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="81e66-152">Subskrypcji platformy Azure ma limit na powitania liczba rdzeni, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="81e66-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="81e66-153">Skalowanie nie będzie działać, jeśli zostały użyte wszystkie dostępne rdzenie hello.</span><span class="sxs-lookup"><span data-stu-id="81e66-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="81e66-154">Na przykład jeśli istnieje limit liczby rdzeni (100), oznacza to, może mieć 100 wystąpień maszyna wirtualna A1 o rozmiarze dla usługi w chmurze lub wystąpieniu maszyny wirtualnej o rozmiarze 50 A2.</span><span class="sxs-lookup"><span data-stu-id="81e66-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="81e66-155">Sieć</span><span class="sxs-lookup"><span data-stu-id="81e66-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="81e66-156">I nie można zastrzec adresu IP w usłudze chmury wielu wirtualnych adresów IP</span><span class="sxs-lookup"><span data-stu-id="81e66-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="81e66-157">Najpierw upewnij się, że to wystąpienie maszyny wirtualnej hello, który próbujesz tooreserve hello IP dla jest włączony.</span><span class="sxs-lookup"><span data-stu-id="81e66-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="81e66-158">Po drugie upewnij się, wdrożeń odblokowane hello tymczasowych i produkcyjnych używasz zastrzeżonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="81e66-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="81e66-159">**Nie** ustawień hello podczas uaktualniania jest hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="81e66-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="81e66-160">Pulpit zdalny</span><span class="sxs-lookup"><span data-stu-id="81e66-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="81e66-161">Jak Pulpit zdalny gdy grupa NSG?</span><span class="sxs-lookup"><span data-stu-id="81e66-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="81e66-162">Dodaj toohello reguły NSG, które zezwalają na ruch na portach **3389** i **20000**.</span><span class="sxs-lookup"><span data-stu-id="81e66-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="81e66-163">Pulpit zdalny używa portu **3389**.</span><span class="sxs-lookup"><span data-stu-id="81e66-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="81e66-164">Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować tooconnect wystąpienia, które do.</span><span class="sxs-lookup"><span data-stu-id="81e66-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="81e66-165">Witaj *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i Zezwalaj na powitania klienta toosend pliku cookie protokołu RDP i określ tooconnect poszczególnych wystąpień do.</span><span class="sxs-lookup"><span data-stu-id="81e66-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="81e66-166">Witaj *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="81e66-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
