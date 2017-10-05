---
title: "Rozwiązywanie problemów z Azure RBAC | Dokumentacja firmy Microsoft"
description: "Uzyskaj pomoc dotyczącą problemy lub pytania dotyczące zasobów kontroli dostępu opartej na rolach."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="81115-103">Oparta na rolach kontrola dostępu do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="81115-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="81115-104">W tym artykule dokumentu odpowiedzi na często zadawane pytania dotyczące określone prawa dostępu przyznane z rolami, aby wiedzieli, czego można oczekiwać, korzystając z ról w portalu Azure i może rozwiązać problemy z dostępem do.</span><span class="sxs-lookup"><span data-stu-id="81115-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="81115-105">Te trzy role opisano wszystkie typy zasobów:</span><span class="sxs-lookup"><span data-stu-id="81115-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="81115-106">Właściciel</span><span class="sxs-lookup"><span data-stu-id="81115-106">Owner</span></span>  
* <span data-ttu-id="81115-107">Współautor</span><span class="sxs-lookup"><span data-stu-id="81115-107">Contributor</span></span>  
* <span data-ttu-id="81115-108">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="81115-108">Reader</span></span>  

<span data-ttu-id="81115-109">Właściciele i współautorzy mają pełny dostęp do możliwości zarządzania, ale współautora nie może udzielić dostępu do innych użytkowników lub grup.</span><span class="sxs-lookup"><span data-stu-id="81115-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="81115-110">Elementy poznasz nieco bardziej interesującego z rolą czytnika, dzięki czemu to, gdzie będzie poświęcić trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="81115-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="81115-111">Zobacz [opartej na rolach kontrola dostępu get-started artykułu](role-based-access-control-configure.md) szczegółowe informacje na temat sposobu udzielić dostępu.</span><span class="sxs-lookup"><span data-stu-id="81115-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="81115-112">Obciążeń usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="81115-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="81115-113">Możliwości zapisu</span><span class="sxs-lookup"><span data-stu-id="81115-113">Write access capabilities</span></span>
<span data-ttu-id="81115-114">Przyznanie dostępu użytkowników tylko do odczytu w aplikacji sieci web jednej, niektóre funkcje zostały wyłączone, że nie może spodziewać się.</span><span class="sxs-lookup"><span data-stu-id="81115-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="81115-115">Następujące funkcje zarządzania wymagają **zapisu** dostęp do aplikacji sieci web (współautora lub właściciela), a nie są dostępne w jakimkolwiek scenariuszu tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="81115-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="81115-116">Polecenia (na przykład Uruchom, Zatrzymaj, itp.)</span><span class="sxs-lookup"><span data-stu-id="81115-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="81115-117">Zmiana ustawień, takich jak konfiguracja ogólna, ustawienia skalowania ustawienia kopii zapasowej i ustawienia monitorowania</span><span class="sxs-lookup"><span data-stu-id="81115-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="81115-118">Uzyskiwanie dostępu do poświadczeń publikowania i innych informacji poufnych, takich jak ustawienia aplikacji i parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="81115-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="81115-119">Dzienniki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="81115-119">Streaming logs</span></span>
* <span data-ttu-id="81115-120">Dzienniki diagnostyczne konfiguracji</span><span class="sxs-lookup"><span data-stu-id="81115-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="81115-121">W konsoli (wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="81115-121">Console (command prompt)</span></span>
* <span data-ttu-id="81115-122">Ostatnie i Active wdrożenia (ciągłe wdrażanie lokalnej git)</span><span class="sxs-lookup"><span data-stu-id="81115-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="81115-123">Szacowane wydatki</span><span class="sxs-lookup"><span data-stu-id="81115-123">Estimated spend</span></span>
* <span data-ttu-id="81115-124">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="81115-124">Web tests</span></span>
* <span data-ttu-id="81115-125">Sieć wirtualna (widoczne tylko dla czytnika, jeśli wcześniej skonfigurowano sieci wirtualnej przez użytkownika z uprawnieniami do zapisu).</span><span class="sxs-lookup"><span data-stu-id="81115-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="81115-126">Jeśli nie masz dostępu do żadnego z tych kafelków, należy skontaktować się z administratorem współautora dostępu do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="81115-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="81115-127">Zajmujących się zasoby pokrewne</span><span class="sxs-lookup"><span data-stu-id="81115-127">Dealing with related resources</span></span>
<span data-ttu-id="81115-128">Aplikacje sieci Web są skomplikowane obecności kilka różnych zasobów, które wzajemne oddziaływanie.</span><span class="sxs-lookup"><span data-stu-id="81115-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="81115-129">W tym miejscu jest grupą typowych zasobów z kilku witryn sieci Web:</span><span class="sxs-lookup"><span data-stu-id="81115-129">Here is a typical resource group with a couple websites:</span></span>

![Grupa zasobów aplikacji sieci Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="81115-131">Dzięki temu, jeśli ktoś dostępu tylko w aplikacji sieci web, wiele funkcji w bloku witryny sieci Web w portalu Azure jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="81115-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="81115-132">Te elementy wymagają **zapisu** dostęp do **planu usługi aplikacji** odnosi się do witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="81115-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="81115-133">Wyświetlanie aplikacji sieci web firmy cenowym (wolne lub standardowy)</span><span class="sxs-lookup"><span data-stu-id="81115-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="81115-134">Skala konfiguracji (liczba wystąpień, rozmiar maszyny wirtualnej, ustawienia skalowania automatycznego)</span><span class="sxs-lookup"><span data-stu-id="81115-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="81115-135">Przydziały (magazynu, przepustowości, procesor CPU)</span><span class="sxs-lookup"><span data-stu-id="81115-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="81115-136">Te elementy wymagają **zapisu** dostęp do całego **grupy zasobów** zawierający witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="81115-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="81115-137">Certyfikaty SSL i powiązań (certyfikaty SSL można udostępniać między lokacjami w tej samej grupie zasobów i lokalizacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="81115-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="81115-138">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="81115-138">Alert rules</span></span>  
* <span data-ttu-id="81115-139">Ustawienia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="81115-139">Autoscale settings</span></span>  
* <span data-ttu-id="81115-140">Application insights składników</span><span class="sxs-lookup"><span data-stu-id="81115-140">Application insights components</span></span>  
* <span data-ttu-id="81115-141">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="81115-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="81115-142">Obciążenia maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="81115-142">Virtual machine workloads</span></span>
<span data-ttu-id="81115-143">Wiele takich jak z aplikacjami sieci web, niektóre funkcje w bloku maszyny wirtualnej wymagają dostęp do zapisu do maszyny wirtualnej lub do innych zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="81115-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="81115-144">Maszyny wirtualne są powiązane z nazwy domeny, sieci wirtualne, konta magazynu i reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="81115-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="81115-145">Te elementy wymagają **zapisu** dostęp do **maszyny wirtualnej**:</span><span class="sxs-lookup"><span data-stu-id="81115-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="81115-146">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="81115-146">Endpoints</span></span>  
* <span data-ttu-id="81115-147">Adresy IP</span><span class="sxs-lookup"><span data-stu-id="81115-147">IP addresses</span></span>  
* <span data-ttu-id="81115-148">Dyski</span><span class="sxs-lookup"><span data-stu-id="81115-148">Disks</span></span>  
* <span data-ttu-id="81115-149">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="81115-149">Extensions</span></span>  

<span data-ttu-id="81115-150">Wymagają one wykonywania **zapisu** dostęp do **maszyny wirtualnej**i **grupy zasobów** (wraz z nazwą domeny) jest it:</span><span class="sxs-lookup"><span data-stu-id="81115-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="81115-151">Zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="81115-151">Availability set</span></span>  
* <span data-ttu-id="81115-152">Zestawu o zrównoważonym obciążeniu</span><span class="sxs-lookup"><span data-stu-id="81115-152">Load balanced set</span></span>  
* <span data-ttu-id="81115-153">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="81115-153">Alert rules</span></span>  

<span data-ttu-id="81115-154">Jeśli nie masz dostępu do żadnego z tych kafelków, skontaktuj się z administratorem współautora dostępu do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="81115-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="81115-155">Zobacz więcej</span><span class="sxs-lookup"><span data-stu-id="81115-155">See more</span></span>
* <span data-ttu-id="81115-156">[Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81115-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="81115-157">[Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji dotyczących ról, które standardowo w RBAC.</span><span class="sxs-lookup"><span data-stu-id="81115-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="81115-158">[Role niestandardowe w Azure RBAC](role-based-access-control-custom-roles.md): Dowiedz się, jak tworzyć role niestandardowe, aby spełniały Twoje potrzeby dostępu.</span><span class="sxs-lookup"><span data-stu-id="81115-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="81115-159">[Tworzenie raportu historii zmian dostępu](role-based-access-control-access-change-history-report.md): informacje o zmieniania przypisań ról w RBAC.</span><span class="sxs-lookup"><span data-stu-id="81115-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

