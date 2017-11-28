---
title: aaaTroubleshoot Azure RBAC | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="ebd8f-103">Oparta na rolach kontrola dostępu do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="ebd8f-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="ebd8f-104">W tym artykule dokumentu odpowiedzi na często zadawane pytania dotyczące hello określone prawa dostępu przyznane z rolami, aby wiedzieć, jaki tooexpect po przy użyciu hello ról w hello portalu Azure i rozwiązywać problemy z dostępem do.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="ebd8f-105">Te trzy role opisano wszystkie typy zasobów:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="ebd8f-106">Właściciel</span><span class="sxs-lookup"><span data-stu-id="ebd8f-106">Owner</span></span>  
* <span data-ttu-id="ebd8f-107">Współautor</span><span class="sxs-lookup"><span data-stu-id="ebd8f-107">Contributor</span></span>  
* <span data-ttu-id="ebd8f-108">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="ebd8f-108">Reader</span></span>  

<span data-ttu-id="ebd8f-109">Właściciele i współautorzy mają pełny dostęp toohello zarządzania środowisko, ale współautora nie może udzielić dostępu tooother użytkowników lub grup.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="ebd8f-110">Rzeczy interesujący nieco z rolą czytnika hello, dlatego gdy będzie poświęcić trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="ebd8f-111">Zobacz hello [opartej na rolach kontrola dostępu get-started artykułu](role-based-access-control-configure.md) szczegółowe informacje na temat sposobu uzyskiwania dostępu toogrant.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="ebd8f-112">Obciążeń usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="ebd8f-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="ebd8f-113">Możliwości zapisu</span><span class="sxs-lookup"><span data-stu-id="ebd8f-113">Write access capabilities</span></span>
<span data-ttu-id="ebd8f-114">Jeśli przyznasz aplikacji sieci web pojedynczego użytkownika dostęp tylko do odczytu tooa niektóre funkcje zostały wyłączone, że nie może spodziewać się.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="ebd8f-115">Wymagaj Hello następujące możliwości zarządzania **zapisu** dostępu do aplikacji sieci web tooa (współautora lub właściciela), a nie są dostępne w jakimkolwiek scenariuszu tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="ebd8f-116">Polecenia (na przykład Uruchom, Zatrzymaj, itp.)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="ebd8f-117">Zmiana ustawień, takich jak konfiguracja ogólna, ustawienia skalowania ustawienia kopii zapasowej i ustawienia monitorowania</span><span class="sxs-lookup"><span data-stu-id="ebd8f-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="ebd8f-118">Uzyskiwanie dostępu do poświadczeń publikowania i innych informacji poufnych, takich jak ustawienia aplikacji i parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="ebd8f-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="ebd8f-119">Dzienniki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="ebd8f-119">Streaming logs</span></span>
* <span data-ttu-id="ebd8f-120">Dzienniki diagnostyczne konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ebd8f-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="ebd8f-121">W konsoli (wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-121">Console (command prompt)</span></span>
* <span data-ttu-id="ebd8f-122">Ostatnie i Active wdrożenia (ciągłe wdrażanie lokalnej git)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="ebd8f-123">Szacowane wydatki</span><span class="sxs-lookup"><span data-stu-id="ebd8f-123">Estimated spend</span></span>
* <span data-ttu-id="ebd8f-124">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="ebd8f-124">Web tests</span></span>
* <span data-ttu-id="ebd8f-125">Sieć wirtualna (tylko widoczne tooa czytnika Jeśli wcześniej skonfigurowano sieci wirtualnej przez użytkownika z uprawnieniami do zapisu).</span><span class="sxs-lookup"><span data-stu-id="ebd8f-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="ebd8f-126">Jeśli nie masz dostępu do żadnego z tych kafelków, należy tooask administratora dla aplikacji sieci web toohello dostępu współautora.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="ebd8f-127">Zajmujących się zasoby pokrewne</span><span class="sxs-lookup"><span data-stu-id="ebd8f-127">Dealing with related resources</span></span>
<span data-ttu-id="ebd8f-128">Aplikacje sieci Web są skomplikowane hello obecności kilka różnych zasobów, które wzajemne oddziaływanie.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="ebd8f-129">W tym miejscu jest grupą typowych zasobów z kilku witryn sieci Web:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-129">Here is a typical resource group with a couple websites:</span></span>

![Grupa zasobów aplikacji sieci Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="ebd8f-131">W związku z tym jeśli udzielić aplikacji sieci web hello toojust dostępu ktoś większość funkcji hello na powitania bloku witryny sieci Web w portalu Azure hello jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="ebd8f-132">Te elementy wymagają **zapisu** dostępu toohello **planu usługi aplikacji** tooyour witryny sieci Web, który odpowiada:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="ebd8f-133">Aplikacja sieci web hello wyświetlania obiektu cenowym (wolne lub standardowy)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="ebd8f-134">Skala konfiguracji (liczba wystąpień, rozmiar maszyny wirtualnej, ustawienia skalowania automatycznego)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="ebd8f-135">Przydziały (magazynu, przepustowości, procesor CPU)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="ebd8f-136">Te elementy wymagają **zapisu** toohello dostępu do całej **grupy zasobów** zawierający witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="ebd8f-137">Certyfikaty SSL i powiązań (certyfikaty SSL może być udostępniana między lokacjami hello tej samej grupie zasobów i lokalizacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="ebd8f-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="ebd8f-138">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="ebd8f-138">Alert rules</span></span>  
* <span data-ttu-id="ebd8f-139">Ustawienia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="ebd8f-139">Autoscale settings</span></span>  
* <span data-ttu-id="ebd8f-140">Application insights składników</span><span class="sxs-lookup"><span data-stu-id="ebd8f-140">Application insights components</span></span>  
* <span data-ttu-id="ebd8f-141">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="ebd8f-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="ebd8f-142">Obciążenia maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ebd8f-142">Virtual machine workloads</span></span>
<span data-ttu-id="ebd8f-143">Wiele takich jak z aplikacjami sieci web, niektóre funkcje w bloku maszyny wirtualnej hello wymagają maszyny wirtualnej toohello zapisu lub tooother zasoby w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="ebd8f-144">Maszyny wirtualne są powiązane tooDomain nazwy, sieci wirtualnych, kont magazynu i reguł alertów.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="ebd8f-145">Te elementy wymagają **zapisu** dostępu toohello **maszyny wirtualnej**:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="ebd8f-146">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="ebd8f-146">Endpoints</span></span>  
* <span data-ttu-id="ebd8f-147">Adresy IP</span><span class="sxs-lookup"><span data-stu-id="ebd8f-147">IP addresses</span></span>  
* <span data-ttu-id="ebd8f-148">Dyski</span><span class="sxs-lookup"><span data-stu-id="ebd8f-148">Disks</span></span>  
* <span data-ttu-id="ebd8f-149">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="ebd8f-149">Extensions</span></span>  

<span data-ttu-id="ebd8f-150">Wymagają one wykonywania **zapisu** hello tooboth dostępu **maszyny wirtualnej**i hello **grupy zasobów** (wraz z nazwą domeny hello) jest jego:</span><span class="sxs-lookup"><span data-stu-id="ebd8f-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="ebd8f-151">Zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="ebd8f-151">Availability set</span></span>  
* <span data-ttu-id="ebd8f-152">Zestawu o zrównoważonym obciążeniu</span><span class="sxs-lookup"><span data-stu-id="ebd8f-152">Load balanced set</span></span>  
* <span data-ttu-id="ebd8f-153">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="ebd8f-153">Alert rules</span></span>  

<span data-ttu-id="ebd8f-154">Jeśli nie masz dostępu do żadnego z tych kafelków, poproś administratora dla grupy zasobów toohello dostępu współautora.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="ebd8f-155">Zobacz więcej</span><span class="sxs-lookup"><span data-stu-id="ebd8f-155">See more</span></span>
* <span data-ttu-id="ebd8f-156">[Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="ebd8f-157">[Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji o rolach hello, które standardowo w RBAC.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="ebd8f-158">[Role niestandardowe w Azure RBAC](role-based-access-control-custom-roles.md): Dowiedz się, jak toofit role niestandardowe toocreate Twojego dostępu wymaga.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="ebd8f-159">[Tworzenie raportu historii zmian dostępu](role-based-access-control-access-change-history-report.md): informacje o zmieniania przypisań ról w RBAC.</span><span class="sxs-lookup"><span data-stu-id="ebd8f-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

