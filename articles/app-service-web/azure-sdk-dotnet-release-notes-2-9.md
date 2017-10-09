---
title: aaaAzure zestawu SDK dla platformy .NET 2.9 informacje o wersji
description: Informacje o wersji zestawu Azure SDK dla platformy .NET 2.9
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="57508-103">Informacje o wersji zestawu Azure SDK dla programu .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="57508-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="57508-104">Ten temat zawiera informacje o wersji dla wersji 2.9 i 2.9.6 zestawu Azure SDK dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="57508-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="57508-105">Podsumowanie wersji zestawu Azure SDK dla platformy .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="57508-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="57508-106">Data wydania: 2016-11-16</span><span class="sxs-lookup"><span data-stu-id="57508-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="57508-107">Nie istotne zmiany toohello zestaw Azure SDK 2.9 zostały wprowadzone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="57508-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="57508-108">Nie jest również nie tooleverage procesu uaktualniania wymagane tego zestawu SDK z istniejącymi projektami usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="57508-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="57508-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="57508-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="57508-110">W programie Visual Studio RC 2017 tej wersji programu hello Azure SDK dla platformy .NET jest wbudowany w hello Azure obciążenia.</span><span class="sxs-lookup"><span data-stu-id="57508-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="57508-111">Wszystkie narzędzia hello należy toodo rozwoju platformy Azure będzie częścią programu Visual Studio RC 2017 idąc dalej.</span><span class="sxs-lookup"><span data-stu-id="57508-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="57508-112">Dla programu Visual Studio 2015 i Visual Studio 2013 hello zestawu SDK będą nadal dostępne za pośrednictwem WebPI.</span><span class="sxs-lookup"><span data-stu-id="57508-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="57508-113">Firma Microsoft będzie roku zestawu Azure SDK dla wersji platformy .NET dla programu Visual Studio 2013, gdy program Visual Studio 2017 zwalnia jako produktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="57508-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="57508-114">Wykonaj ten link toodownload programu Visual Studio RC 2017: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="57508-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="57508-115">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="57508-115">Azure Diagnostics</span></span>

- <span data-ttu-id="57508-116">Zmienione hello zachowanie tooonly przechowywać parametry połączenia z częściowa kluczem hello zastępuje token dla parametrów połączenia magazynu diagnostyki usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="57508-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="57508-117">Klucz magazynu rzeczywista Hello są obecnie przechowywane w folderze profilu użytkownika hello, można kontrolować dostęp do niej.</span><span class="sxs-lookup"><span data-stu-id="57508-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="57508-118">Visual Studio odczyta hello klucza magazynu z folderu profilu użytkownika dla debugowania lokalnego i proces publikowania.</span><span class="sxs-lookup"><span data-stu-id="57508-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="57508-119">W przypadku zmiany toohello odpowiedzi opisane powyżej Visual Studio Online zespołu rozszerzone hello szablon zadania wdrożenia usługi w chmurze Azure, użytkownicy można określić klucz magazynu hello do ustawiania rozszerzenia diagnostyki podczas publikowania tooAzure w ciągłej integracji i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="57508-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="57508-120">Ułatwiliśmy ciągu bezpiecznego połączenia możliwe toostore i tokenizacji dla Azure Diagnostics (WAD), toohelp rozwiązuje problemy związane z konfiguracją w environements.</span><span class="sxs-lookup"><span data-stu-id="57508-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="57508-121">Maszyny wirtualne systemu Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="57508-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="57508-122">Program Visual Studio teraz obsługuje wdrażanie usługi w chmurze tooOS rodziny 5 (z systemem Windows Server 2016), maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57508-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="57508-123">Istniejące usługi w chmurze, można zmienić Twojego tootarget ustawienia hello nowej rodziny systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="57508-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="57508-124">Podczas tworzenia nowych usług w chmurze, jeśli wybierzesz toocreate hello usługi przy użyciu platformy .net 4.6 lub nowszej, będzie on domyślnej hello usługi toouse 5 rodziny systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="57508-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="57508-125">Aby uzyskać więcej informacji, możesz przejrzeć hello [rodziny systemów operacyjnych gościa obsługuje tabeli](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="57508-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="57508-126">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="57508-126">Known issues</span></span>

- <span data-ttu-id="57508-127">Azure .NET SDK 2.9.6 wprowadzone ograniczeń, która blokuje wdrożenie projektów przy użyciu nieobsługiwanego .NET tooany platform (np. .NET 4.6) rodziny systemów operacyjnych < 5.</span><span class="sxs-lookup"><span data-stu-id="57508-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="57508-128">Udostępniono obejście [tutaj](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="57508-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="57508-129">Pamięć podręczna na roli Azure</span><span class="sxs-lookup"><span data-stu-id="57508-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="57508-130">Obsługa kończy się na roli Azure w pamięci podręcznej w dniu 30 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="57508-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="57508-131">Aby uzyskać więcej informacji, kliknij przycisk [tutaj](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="57508-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="57508-132">Stack — szablony usługi Azure Resource Manager dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57508-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="57508-133">Dodaliśmy stosu Azure jako cel wdrożenia szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57508-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="57508-134">Zestaw Azure SDK dla platformy .NET 2.9 podsumowanie</span><span class="sxs-lookup"><span data-stu-id="57508-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="57508-135">Omówienie</span><span class="sxs-lookup"><span data-stu-id="57508-135">Overview</span></span>
<span data-ttu-id="57508-136">Ten dokument zawiera informacje o wersji hello hello Azure SDK dla platformy .NET 2.9 wydania.</span><span class="sxs-lookup"><span data-stu-id="57508-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="57508-137">Aby uzyskać szczegółowe informacje na temat aktualizacji w tej wersji, zobacz hello [post anonsu zestaw Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="57508-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="57508-138">Zestaw Azure SDK 2.9 dla programu Visual Studio 2015 Update 2 do programu Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="57508-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="57508-139">Ta aktualizacja obejmuje hello następujące poprawki:</span><span class="sxs-lookup"><span data-stu-id="57508-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="57508-140">Wystawiać pokrewne tooREST Generowanie klienta interfejsu API w w ciągu których hello "Nieznany typ" zostanie wyświetlony jako nazwa hello hello generacji kodu folderu i/lub nazwę hello nazw hello upuścić na powitania wygenerowany kod.</span><span class="sxs-lookup"><span data-stu-id="57508-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="57508-141">Należy wystawić tooScheduled powiązanych zadań Webjob w których hello informacje dotyczące uwierzytelniania sprawdzano toobe przekazany procesu inicjowania obsługi administracyjnej toohello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="57508-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="57508-142">Ta aktualizacja obejmuje powitania po nowej funkcji:</span><span class="sxs-lookup"><span data-stu-id="57508-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="57508-143">Obsługa dodatkowej usługi aplikacji na karcie "Usługi" hello powitalne okno dialogowe udostępniania usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57508-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="57508-144">Narzędzia usługi Azure Data Lake Tools dla Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="57508-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="57508-145">Tej aktualizacji obejmuje następujące hello:</span><span class="sxs-lookup"><span data-stu-id="57508-145">This updates includes hello following:</span></span>

* <span data-ttu-id="57508-146">**Azure Data Lake Tools** dla programu Visual Studio teraz jest scalany hello Azure SDK dla wersji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="57508-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="57508-147">Narzędzie Hello jest automatycznie instalowany podczas instalowania zestawu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="57508-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="57508-148">Narzędzie Hello jest często aktualizowana, przejdź [tutaj](http://aka.ms/datalaketool) tooget hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="57508-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="57508-149">**W Eksploratorze serwera** teraz pozwala tooview wszystkich i utworzyć niektóre jednostki metadanych U-SQL.</span><span class="sxs-lookup"><span data-stu-id="57508-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="57508-150">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.</span><span class="sxs-lookup"><span data-stu-id="57508-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="57508-151">Narzędzia HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="57508-151">HDInsight Tools</span></span>
<span data-ttu-id="57508-152">**Narzędzia HDInsight Tools** dla programu Visual Studio teraz obsługuje HDInsight wersji 3.3, łącznie z wykazem wykresach Tez i inny język poprawki.</span><span class="sxs-lookup"><span data-stu-id="57508-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="57508-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57508-153">Azure Resource Manager</span></span>
<span data-ttu-id="57508-154">Ta wersja dodaje [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) obsługę szablony Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="57508-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="57508-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="57508-155">See also</span></span>
[<span data-ttu-id="57508-156">Azure SDK 2.9 anonsu post</span><span class="sxs-lookup"><span data-stu-id="57508-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

