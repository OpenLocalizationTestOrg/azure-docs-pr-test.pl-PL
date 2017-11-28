---
title: "aaaOptions migracji z usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat opcji hello migracji z usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="92631-103">Opcje migracji z usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="92631-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="92631-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="92631-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="92631-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="92631-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="92631-106">Jeśli zatrzymano przy użyciu usługi Azure RemoteApp z powodu hello [anonsu wycofania](https://go.microsoft.com/fwlink/?linkid=821148) lub ponieważ po zakończeniu oceny należy toomigrate wylogowuje usługi aplikacji tooanother usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="92631-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="92631-107">Istnieją dwa różne podejścia do migracji: samozarządzanej (często nazywane infrastruktura jako usługa [IaaS]) wdrożenia lub w pełni zarządzana (zwane często platforma jako usługa) lub oprogramowania jako usługi [PaaS/SaaS] oferty.</span><span class="sxs-lookup"><span data-stu-id="92631-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="92631-108">Samoobsługowe IaaS stanowi Zrób wdrożenia, które jest zarządzane, obsługiwana i należące do Ciebie bezpośrednio wdrożonych na maszynach wirtualnych (VM) lub systemów fizycznych.</span><span class="sxs-lookup"><span data-stu-id="92631-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="92631-109">Na powitania innych kończyć pełni zarządzana PaaS/SaaS oferty jest bardzo podobne do usługi Azure RemoteApp — partnera zapewnia warstwę usługi na rozwiązanie usług zdalnych, które obsługuje operacyjnej i obsługi podczas pracy, jak powitania klienta i do zarządzania niektórych obrazu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92631-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="92631-110">[Wyświetl seminaria Internetowe usługi Azure RemoteApp hello na opcje migracji](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), lub Dowiedz się więcej informacji (w tym przykłady hello różne opcje hostingu).</span><span class="sxs-lookup"><span data-stu-id="92631-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="92631-111">Samodzielnie zarządzanej rozwiązań (IaaS)</span><span class="sxs-lookup"><span data-stu-id="92631-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="92631-112">**Usługi pulpitu zdalnego na IaaS**</span><span class="sxs-lookup"><span data-stu-id="92631-112">**RDS on IaaS**</span></span>
<span data-ttu-id="92631-113">Można wdrożyć natywnego opartymi na sesji usług pulpitu zdalnego (w systemie Windows Server) wdrażania przy użyciu programów RemoteApp i pulpitów lokalnie lub w środowisku hostowanej (jak na maszynach wirtualnych Azure).</span><span class="sxs-lookup"><span data-stu-id="92631-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="92631-114">Usługi pulpitu zdalnego na wdrożenia IaaS są najlepsze w przypadku klientów już znasz i mają istniejących wiedzy technicznej z wdrożeniami usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="92631-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="92631-115">Należy licencjonowania zbiorowego z Software Assurance (SA) dla toouse licencji dostępu klienta usług pulpitu zdalnego tej opcji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="92631-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="92631-116">Wdrażanie usług pulpitu zdalnego na maszynach wirtualnych Azure jest łatwiejsze niż kiedykolwiek użycia wdrożenia i stosowania poprawek szablonów (odczytu [omówienie](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) , a następnie [pobrać je](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="92631-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="92631-117">Ci hello elastycznej takie same możliwości skalowania z zasobami modelu wdrażania klasycznego Azure (nie Model zasobów Azure zasobów) w usłudze Azure RemoteApp przy użyciu hello [automatyczne skalowanie skryptu](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), chociaż występują więcej Dostosowywanie i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="92631-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="92631-118">Podczas wdrażania usług pulpitu zdalnego na maszynach wirtualnych Azure jest obsługiwana w ramach [Azure obsługuje](https://azure.microsoft.com/support/plans/), hello tego samego pracowników pomocy technicznej, obsługiwane z usługą Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="92631-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="92631-119">Można pobrać koszt wartościami szacunkowymi określonymi na podstawie istniejących użycia kontaktując się z [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/plans/), lub wykonać obliczenia samodzielnie przy użyciu wkrótce toobe wydane Kalkulator kosztów.</span><span class="sxs-lookup"><span data-stu-id="92631-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="92631-120">Ponadto z maszynami wirtualnymi serii N (obecnie w podglądzie prywatnym) można dodać vGPU - usłyszeć więcej na temat dodawania vGPU i o tym, jak za[przewodów ulepszenia usług pulpitu zdalnego w systemie Windows Server 2016](https://myignite.microsoft.com/videos/2794) w naszym Ignite sesji.</span><span class="sxs-lookup"><span data-stu-id="92631-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="92631-121">Mamy przewodniki krok po kroku wdrożenia dla [systemu Windows Server 2012 R2](http://aka.ms/rdsonazure) i [systemu Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist z wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="92631-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="92631-122">Zapoznaj się z hello [blogu pulpitu zdalnego](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) uzyskać najnowsze wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="92631-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="92631-123">**Citrix na IaaS**</span><span class="sxs-lookup"><span data-stu-id="92631-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="92631-124">Natywny Citrix, wdrożenia oparte na sesji program XenApp lub XenDesktop może być wdrożona lokalnie lub w środowisku hostowanej (takich jak na maszynach wirtualnych Azure).</span><span class="sxs-lookup"><span data-stu-id="92631-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="92631-125">Zapoznaj się z hello przewodnik krok po kroku wdrażania, [7.6 XA Citrix na platformie Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="92631-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="92631-126">Przeczytaj więcej na temat [Citrix na platformie Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), w tym Kalkulator cen.</span><span class="sxs-lookup"><span data-stu-id="92631-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="92631-127">Możesz również znaleźć [kontaktu Citrix](http://citrix.com/English/contact/index.asp) toodiscuss opcji z.</span><span class="sxs-lookup"><span data-stu-id="92631-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="92631-128">Pełni zarządzana oferty (PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="92631-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="92631-129">Citrix program XenApp Essentials (wydane kwietnia 2017)</span><span class="sxs-lookup"><span data-stu-id="92631-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="92631-130">Teraz dostępne na powitania [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials)Essentials program XenApp Citrix jest hello nowej aplikacji usługi wirtualizacji, łączenie hello zasilania i elastyczność hello platformy w chmurze Citrix przy prostego powitania przetestowanego, i wizji łatwe korzystanie z funkcji RemoteApp systemu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="92631-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="92631-131">Istniejących klientów usługi Azure RemoteApp można [zarejestrować bezpłatnej wersji próbnej](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="92631-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="92631-132">Uwaga: Tylko opłat usługi Citrix jest wolnego, zastosuj Azure koszty zasobów obliczeniowych i magazynu</span><span class="sxs-lookup"><span data-stu-id="92631-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="92631-133">Dowiedz się więcej:</span><span class="sxs-lookup"><span data-stu-id="92631-133">Learn More:</span></span>
- [<span data-ttu-id="92631-134">Migrowanie z usługi Azure RemoteApp tooCitrix program XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="92631-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="92631-135">Citrix i firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="92631-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="92631-136">[Prezentacja Essentials program XenApp Citrix](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="92631-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="92631-137">Citrix program XenApp chmury i usługa XenDesktop</span><span class="sxs-lookup"><span data-stu-id="92631-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="92631-138">[Citrix program XenApp chmury i usługa XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) hello najlepszym rozwiązaniem w celu dostarczania hello zarówno aplikacje i komputerów stacjonarnych, oraz zaawansowanego zarządzania i możliwości monitorowania.</span><span class="sxs-lookup"><span data-stu-id="92631-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="92631-139">Conexlink (nazwa platformy: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="92631-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="92631-140">[MyCloudIT](https://mycloudit.com) jest to platforma automatyzacji dla toosimplify przedsiębiorstw IT, optymalizacji i skalować hello migracji i dostarczanie Pulpity zdalne, zdalne aplikacje i infrastrukturę w hello firmy Microsoft w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="92631-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="92631-141">Platforma MyCloudIT Hello skraca czas wdrażania przez 95% Azure koszt przez 30% i przenosi całą infrastrukturą informatyczną swoich klientów do chmury hello w sprawie kilku naciśniętych klawiszy.</span><span class="sxs-lookup"><span data-stu-id="92631-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="92631-142">Partnerzy mogą teraz zarządzać klientami z jedną globalnego pulpitu nawigacyjnego, usługi Użytkownicy końcowi wokół Witaj świecie, takich jak wcześniej i wzrostu przychodów bez dodawania dodatkowe obciążenie lub szeroką gamę szkolenia Azure.</span><span class="sxs-lookup"><span data-stu-id="92631-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="92631-143">Lokalizacją główną: Dallas, TX, USA</span><span class="sxs-lookup"><span data-stu-id="92631-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="92631-144">Operacja regionu: na całym świecie</span><span class="sxs-lookup"><span data-stu-id="92631-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="92631-145">Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="92631-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="92631-146">Dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-147">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-148">Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="92631-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="92631-149">Brianowi Garoutte, VP projektowania biznesowych</span><span class="sxs-lookup"><span data-stu-id="92631-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="92631-150">Telefon: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="92631-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="92631-151">Adres e-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="92631-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="92631-152">Ramki</span><span class="sxs-lookup"><span data-stu-id="92631-152">Frame</span></span>

<span data-ttu-id="92631-153">Działy IT w organizacji i dla instytucji rządowych, dostawców usług zarządzanych i wiodącymi dostawcami oprogramowania wybierz toocreate ramki i zarządzaj nimi ich bezpieczne, zdefiniowanych przez oprogramowanie obszarów roboczych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="92631-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="92631-154">Z organizacji małych toolarge ramki ułatwia użytkownikom bardzo łatwe toolet dostęp do aplikacji systemu Windows w dowolnej przeglądarce na dowolnym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="92631-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="92631-155">Hello platformy ramki zawiera wszystko, co administrator musi toodeploy aplikacje z chmury hello tym hello infrastruktury platformy Azure i licencji usług pulpitu zdalnego (dostarczają własne konto platformy Azure i licencji jest opcjonalny).</span><span class="sxs-lookup"><span data-stu-id="92631-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="92631-156">Dowiedz się więcej o [ramki na platformie Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="92631-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="92631-157">Lokalizacją główną: Mateo sieci San, urząd certyfikacji, USA</span><span class="sxs-lookup"><span data-stu-id="92631-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="92631-158">Operacja regionu: na całym świecie</span><span class="sxs-lookup"><span data-stu-id="92631-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="92631-159">Partnera firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="92631-160">Telefon: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="92631-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="92631-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="92631-161">Awingu</span></span>
<span data-ttu-id="92631-162">Awingu zapewnia rozwiązanie proste obszarów roboczych systemem starsze aplikacje, SaaS i dokumenty przy użyciu przeglądarki html5.</span><span class="sxs-lookup"><span data-stu-id="92631-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="92631-163">Tak udostępniania aplikacji bezpiecznego na typ urządzenia.</span><span class="sxs-lookup"><span data-stu-id="92631-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="92631-164">Usługi SaaS op Single-Sign-On opcje szeroki zakres jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="92631-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="92631-165">Również różnych (w chmurze) systemy plików mogą ściśle zintegrowana z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="92631-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="92631-166">Dalej toofull mobilności, jego Awingu sformatowanego obszarów roboczych zapewni optymalnych zabezpieczeń z szczegółową kontrolę (np. Pobieranie/przekazywanie), pełny użycia inspekcji, uwierzytelnianie wieloskładnikowe (np. Azure MFA), sesja rejestrowania i inne.</span><span class="sxs-lookup"><span data-stu-id="92631-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="92631-167">Out-of--box, Awingu umożliwia dokumentu i udostępnianie sesji aplikacji wersją zoptymalizowaną a bezpiecznej współpracy.</span><span class="sxs-lookup"><span data-stu-id="92631-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="92631-168">Rozwiązanie firmy Awingu jest wielodostępnej, usługi AD i otwarty interfejs API.</span><span class="sxs-lookup"><span data-stu-id="92631-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="92631-169">Jest on używany przez małych i dużych firmach, dostawcom usług w chmurze i [niezależnym dostawcom oprogramowania](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="92631-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="92631-170">Tych klientów docenia szczególnie hello łatwe użycia, łatwość do zainstalowania i niski całkowitego kosztu posiadania.</span><span class="sxs-lookup"><span data-stu-id="92631-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="92631-171">Awingu w-jednego jest [dostępne w portalu Azure Marketplace hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) z 2 wbudowanych równoczesnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92631-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="92631-172">Dodatkowe licencje nie są dostępne za pośrednictwem [szeroką gamę dystrybutorów i odsprzedawców](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="92631-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="92631-173">Dowiedz się więcej o [Awingu na jako alternatywne tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="92631-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="92631-174">Lokalizacją główną: Belgia</span><span class="sxs-lookup"><span data-stu-id="92631-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="92631-175">Operacyjny regionów: EMEA, Ameryki Północnej i Brazylia</span><span class="sxs-lookup"><span data-stu-id="92631-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="92631-176">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="92631-177">**Globalne**:</span><span class="sxs-lookup"><span data-stu-id="92631-177">**Global**:</span></span>
> 
> <span data-ttu-id="92631-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="92631-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="92631-179">Adres e-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="92631-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="92631-180">Telefon: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="92631-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="92631-181">**HQ Belgii**:</span><span class="sxs-lookup"><span data-stu-id="92631-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="92631-182">B44 Ottergemsesteenweg Zwid 808</span><span class="sxs-lookup"><span data-stu-id="92631-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="92631-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="92631-183">9000 Gent</span></span>
> 
> <span data-ttu-id="92631-184">Adres e-mail:[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="92631-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="92631-185">Numer telefonu: + 32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="92631-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="92631-186">**USA**:</span><span class="sxs-lookup"><span data-stu-id="92631-186">**USA**:</span></span>
> 
> <span data-ttu-id="92631-187">floor 7, Zapisz 1177 z hello Americas,</span><span class="sxs-lookup"><span data-stu-id="92631-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="92631-188">Nowy Jork, NY 10036</span><span class="sxs-lookup"><span data-stu-id="92631-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="92631-189">Adres e-mail:[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="92631-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="92631-190">Dostawcy usług hostowanych Microsoft</span><span class="sxs-lookup"><span data-stu-id="92631-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="92631-191">Partnerzy hostingowi oferują zwykle w pełni zarządzana hostowanej pulpitu systemu Windows i usługi aplikacji, która może obejmować zarządzanie hello zasobów platformy Azure, systemów operacyjnych, aplikacji i pomoc techniczna za pomocą hello partnera do licencjonowania umowy z firmą Microsoft i innych dostawców oprogramowania oraz jest umową licencyjną dotyczącą usługodawców usługi tooallow odsprzedaż z licencji dostępu subskrybenta (SAL).</span><span class="sxs-lookup"><span data-stu-id="92631-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="92631-192">Witaj zawiera następujące informacje szczegółowe informacje i informacje kontaktowe dla niektórych hello dostawcom usług hostingowych, które specialize udzielania pomocy użytkownikom ich migracji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="92631-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="92631-193">Zapoznaj się z [hello bieżącej listy obsługiwanych dostawców usług](http://aka.ms/rdsonazurecertified) który zakończył hello usług pulpitu zdalnego na IaaS uczenia ścieżkę i oceny.</span><span class="sxs-lookup"><span data-stu-id="92631-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="92631-194">Program dostawcy usługi Citrix</span><span class="sxs-lookup"><span data-stu-id="92631-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="92631-195">Witaj Program dostawcy usługi Citrix ułatwia dla uproszczenia przyjęto hello toodeliver dostawców usługi chmury wirtualne obliczeniowych tooSMBs, oferowanie ich hello usługi, które mają w modelu łatwe, z.</span><span class="sxs-lookup"><span data-stu-id="92631-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="92631-196">Dostawcy usług Citrix wzrostu ich firm SPLA firmy Microsoft i rozwiń inwestycji platformy usług pulpitu zdalnego z dowolnego urządzenia, dostęp z dowolnego miejsca, hello najszerszych obsługę aplikacji, bogate środowisko, zwiększyć bezpieczeństwo i zwiększenia skalowalności.</span><span class="sxs-lookup"><span data-stu-id="92631-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="92631-197">Z kolei Citrix usługodawców przyciągania więcej subskrybentów, bardziej zadowoleni i zmniejszyć koszty operacyjne, ich.</span><span class="sxs-lookup"><span data-stu-id="92631-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="92631-198">[Dowiedz się więcej](http://www.citrix.com/products/service-providers.html) lub [Znajdź partnera](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="92631-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="92631-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="92631-199">Acuutech</span></span>
<span data-ttu-id="92631-200">[Acuutech](http://www.acuutech.com) specjalizuje się w zapewnienie hostowanych rozwiązań pulpitu, dostarczania pełnego pulpitu i aplikacje niezależnego dostawcy oprogramowania środowiska oparty na technologii tooa globalne klienta Microsoft podstawowej z platformy Azure i ich centrów danych.</span><span class="sxs-lookup"><span data-stu-id="92631-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="92631-201">Lokalizacją główną: Londynie, UK; Singapur; Houston, TX</span><span class="sxs-lookup"><span data-stu-id="92631-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="92631-202">Operacja regionu: na całym świecie</span><span class="sxs-lookup"><span data-stu-id="92631-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="92631-203">Stan partnera: Gold</span><span class="sxs-lookup"><span data-stu-id="92631-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="92631-204">Dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-205">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-206">Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="92631-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="92631-207">**Zjednoczone Królestwo**:</span><span class="sxs-lookup"><span data-stu-id="92631-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="92631-208">5/6 Jorku dom, drogowej Langston</span><span class="sxs-lookup"><span data-stu-id="92631-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="92631-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="92631-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="92631-210">Numer telefonu: + 44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="92631-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="92631-211">**Singapuru**:</span><span class="sxs-lookup"><span data-stu-id="92631-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="92631-212">Ulica 100 Cecil, #09-02</span><span class="sxs-lookup"><span data-stu-id="92631-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="92631-213">Witaj świecie, Singapur 069532</span><span class="sxs-lookup"><span data-stu-id="92631-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="92631-214">Numer telefonu: + 65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="92631-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="92631-215">**Ameryka Północna**:</span><span class="sxs-lookup"><span data-stu-id="92631-215">**North America**:</span></span>
>   
> <span data-ttu-id="92631-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="92631-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="92631-217">Pakiet 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="92631-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="92631-218">Telefon: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="92631-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="92631-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="92631-219">ASPEX</span></span>
<span data-ttu-id="92631-220">[ASPEX](http://www.aspex.be/en) specjalizuje się w niezależnym dostawcom oprogramowania przejście toohello chmury i niezależnego dostawcy oprogramowania "Wyszukiwanie toooptimize ich bieżącej konfiguracji chmury.</span><span class="sxs-lookup"><span data-stu-id="92631-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="92631-221">ASPEX oferuje szeroką gamę usług zarządzanych, metodyki devops i usługi konsultingowe.</span><span class="sxs-lookup"><span data-stu-id="92631-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="92631-222">Lokalizacją główną: Antwerpia, Belgia</span><span class="sxs-lookup"><span data-stu-id="92631-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="92631-223">Operacja regionu: Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="92631-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="92631-224">Stan partnera: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="92631-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="92631-225">Dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-226">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-227">Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="92631-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="92631-228">Telefon: +3232202198</span><span class="sxs-lookup"><span data-stu-id="92631-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="92631-229">Poczty:[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="92631-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="92631-230">Sieci Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="92631-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="92631-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="92631-231">Caase.com</span></span>
<span data-ttu-id="92631-232">[Caase.com](http://www.caase.com/) pomaga firmom, lokalnych, szczebla, -rządowych treści i opieki zdrowotnej instytucje z podróży kierunku inteligentny sposób pracy w hello Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="92631-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="92631-233">Trwa produktywności i bezpieczeństwo w dowolnym miejscu z dowolnego urządzenia i niskich kosztach IT.</span><span class="sxs-lookup"><span data-stu-id="92631-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="92631-234">Caase.com jest wartość true, specjalistę ds dla Microsoft Office365, Azure, Enterprise Mobility i zabezpieczeń oraz systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="92631-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="92631-235">W naszym doradcze migracji usług, programy wdrożenia, szkolenia zarządzania i obsługi technicznej Caase.com tworzy zoptymalizowane i bezpieczne platformy współpracy dla klientów pracownikom, partnerom i dostawców.</span><span class="sxs-lookup"><span data-stu-id="92631-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="92631-236">Caase.com jest mastermind hello hello Azure zdalnego obszaru roboczego (przenośnych w miejscu pracy) i hello cyfrowych w miejscu pracy (społecznościowych intranetu).</span><span class="sxs-lookup"><span data-stu-id="92631-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="92631-237">Oba rozwiązania — realizowane za pomocą przyjęcia — są foundation hello, który gwarantuje, że użytkownicy hello tych rozwiązań hello przyjemne, pomyślnie i najbardziej efektywny doświadczenie w ich toohello trasy Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="92631-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="92631-238">Holenderski tłumaczenia ánd obsługi film, w tym miejscu: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="92631-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="92631-239">Operacja regionu: holenderski podstawie globalne</span><span class="sxs-lookup"><span data-stu-id="92631-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="92631-240">Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="92631-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="92631-241">Dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-242">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-243">Rozwiązania migracji w usłudze Azure RemoteApp: tak, [więcej](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="92631-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="92631-244">Holandia:</span><span class="sxs-lookup"><span data-stu-id="92631-244">Netherlands:</span></span>
> 
> <span data-ttu-id="92631-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="92631-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="92631-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="92631-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="92631-247">Telefon: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="92631-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="92631-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="92631-248">Nerdio</span></span>
<span data-ttu-id="92631-249">[Nerdio dla platformy Azure](http://getnerdio.com/nfa/) to platforma automatyzacji IT, która zapewnia było bardzo proste inicjowania obsługi, zarządzania i optymalizacji pełną środowisk IT w hello firmy Microsoft w chmurze.</span><span class="sxs-lookup"><span data-stu-id="92631-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="92631-250">Wstanie pulpitów wirtualnych, aplikacji zdalnych i serwery w kilka godzin.</span><span class="sxs-lookup"><span data-stu-id="92631-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="92631-251">Administrowanie środowiskiem hello w trzech kliknięć lub z portalu administracyjnego Nerdio.</span><span class="sxs-lookup"><span data-stu-id="92631-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="92631-252">Użyj inteligentnego automatyczne skalowanie i Zapisz 40 too60% zasobów IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92631-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="92631-253">Lokalizacją główną: region operacji Chicago, IL: status partnera na całym świecie: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-254">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-255">Rozwiązania migracji w usłudze Azure RemoteApp: tak</span><span class="sxs-lookup"><span data-stu-id="92631-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="92631-256">Zapisz Lincoln 8001</span><span class="sxs-lookup"><span data-stu-id="92631-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="92631-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="92631-257">Suite 212</span></span>
> 
> <span data-ttu-id="92631-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="92631-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="92631-259">Stany Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="92631-259">USA</span></span>
> 
> <span data-ttu-id="92631-260">Zewnętrzne 4NERDIO (844) 6</span><span class="sxs-lookup"><span data-stu-id="92631-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="92631-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="92631-261">**SaaSplaza**</span></span>
<span data-ttu-id="92631-262">[SaaSplaza](http://www.saasplaza.com/) oferuje pełną Microsoft Dynamics portfolio (NAV AX, zasad grupy, SL, CRM) chmury prywatnej i publicznej (Azure).</span><span class="sxs-lookup"><span data-stu-id="92631-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="92631-263">Lokalizacją główną: (Holandia)</span><span class="sxs-lookup"><span data-stu-id="92631-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="92631-264">Operacja regionu: na całym świecie</span><span class="sxs-lookup"><span data-stu-id="92631-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="92631-265">Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="92631-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="92631-266">Dostawcy usług w chmurze firmy Microsoft: tak</span><span class="sxs-lookup"><span data-stu-id="92631-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="92631-267">Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno</span><span class="sxs-lookup"><span data-stu-id="92631-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="92631-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="92631-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="92631-269">Prins Mauritslaan 29 35</span><span class="sxs-lookup"><span data-stu-id="92631-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="92631-270">Badhoevedorp 71 LP</span><span class="sxs-lookup"><span data-stu-id="92631-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="92631-271">Witaj (Holandia)</span><span class="sxs-lookup"><span data-stu-id="92631-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="92631-272">Telefon: 8060 547 20 +31</span><span class="sxs-lookup"><span data-stu-id="92631-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="92631-273">**Americas**:</span><span class="sxs-lookup"><span data-stu-id="92631-273">**Americas**:</span></span>
> 
> <span data-ttu-id="92631-274">105 171 Saksonii drogowej, Suite</span><span class="sxs-lookup"><span data-stu-id="92631-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="92631-275">92024 Encinitas, urząd certyfikacji</span><span class="sxs-lookup"><span data-stu-id="92631-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="92631-276">Diego sieci SAN</span><span class="sxs-lookup"><span data-stu-id="92631-276">San Diego</span></span>
> 
> <span data-ttu-id="92631-277">Stany Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="92631-277">United States</span></span>
> 
> <span data-ttu-id="92631-278">Telefon: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="92631-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="92631-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="92631-279">**APAC**:</span></span>
> 
> <span data-ttu-id="92631-280">105 Cecil ulica</span><span class="sxs-lookup"><span data-stu-id="92631-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="92631-281">\#11-08 hello ośmiokąt</span><span class="sxs-lookup"><span data-stu-id="92631-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="92631-282">Singapuru 069534</span><span class="sxs-lookup"><span data-stu-id="92631-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="92631-283">Singapur</span><span class="sxs-lookup"><span data-stu-id="92631-283">Singapore</span></span>
>   
> <span data-ttu-id="92631-284">Phone - Singapuru: 6591 6222 + 65</span><span class="sxs-lookup"><span data-stu-id="92631-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="92631-285">Phone - Australii: 5568 8310 2 +61</span><span class="sxs-lookup"><span data-stu-id="92631-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="92631-286">Phone — Nowa Zelandia: 0321 488 4 +64</span><span class="sxs-lookup"><span data-stu-id="92631-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="92631-287">Potrzebujesz dodatkowej pomocy?</span><span class="sxs-lookup"><span data-stu-id="92631-287">Need more help?</span></span>
<span data-ttu-id="92631-288">Nadal potrzebna pomoc, wybierając lub więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="92631-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="92631-289">Użyj jednej z hello następujące metody tooget pomocy.</span><span class="sxs-lookup"><span data-stu-id="92631-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="92631-290">Wiadomość e-mail na adres [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="92631-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="92631-291">Skontaktuj się z [pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="92631-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="92631-292">Uruchamianie przez otwarcie [sprawy pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="92631-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="92631-293">Rozmowa.</span><span class="sxs-lookup"><span data-stu-id="92631-293">Call us.</span></span> <span data-ttu-id="92631-294">[Znajdź lokalny numer sprzedaży](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="92631-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

