---
title: Informacje o wersji zestawu Azure SDK dla platformy .NET 2.9
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
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="6c36c-103">Informacje o wersji zestawu Azure SDK dla programu .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="6c36c-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="6c36c-104">Ten temat zawiera informacje o wersji dla wersji 2.9 i 2.9.6 zestawu Azure SDK dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="6c36c-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="6c36c-105">Podsumowanie wersji zestawu Azure SDK dla platformy .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="6c36c-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="6c36c-106">Data wydania: 2016-11-16</span><span class="sxs-lookup"><span data-stu-id="6c36c-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="6c36c-107">W tej wersji zostały wprowadzone żadne zmiany podziału Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="6c36c-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="6c36c-108">Nie ma również żadnych procesów uaktualniania konieczne korzystać z tego zestawu SDK z istniejącymi projektami usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6c36c-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="6c36c-109">Visual Studio 2017 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="6c36c-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="6c36c-110">W programie Visual Studio RC 2017 tej wersji zestawu Azure SDK dla platformy .NET jest wbudowany w obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="6c36c-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="6c36c-111">Wszystkie narzędzia należy wykonać rozwoju platformy Azure będzie częścią programu Visual Studio RC 2017 idąc dalej.</span><span class="sxs-lookup"><span data-stu-id="6c36c-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="6c36c-112">Dla programu Visual Studio 2015 i Visual Studio 2013 zestawu SDK będą nadal dostępne za pośrednictwem WebPI.</span><span class="sxs-lookup"><span data-stu-id="6c36c-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="6c36c-113">Firma Microsoft będzie roku zestawu Azure SDK dla wersji platformy .NET dla programu Visual Studio 2013, gdy program Visual Studio 2017 zwalnia jako produktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6c36c-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="6c36c-114">Wykonaj to łącze, aby pobrać program Visual Studio RC 2017: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="6c36c-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="6c36c-115">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="6c36c-115">Azure Diagnostics</span></span>

- <span data-ttu-id="6c36c-116">Zmienić zachowanie, które będzie przechowywać parametry połączenia z częściowa tylko przy użyciu klucza zastępuje token dla parametrów połączenia magazynu diagnostyki usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6c36c-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="6c36c-117">Klucz magazynu rzeczywista są obecnie przechowywane w folderze profilu użytkownika, można kontrolować dostęp do niej.</span><span class="sxs-lookup"><span data-stu-id="6c36c-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="6c36c-118">Visual Studio odczyta klucza magazynu z folderu profilu użytkownika dla debugowania lokalnego i proces publikowania.</span><span class="sxs-lookup"><span data-stu-id="6c36c-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="6c36c-119">W odpowiedzi na zmianę opisane powyżej zespołu Visual Studio Online rozszerzone szablon zadania wdrożenia usługi w chmurze Azure, użytkownicy można określić klucz magazynu do ustawiania rozszerzenia diagnostyki podczas publikowania na platformie Azure w ciągłej integracji i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6c36c-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="6c36c-120">Ułatwiliśmy możliwość przechowywania i tokenizacji dla Azure Diagnostics (WAD), aby ułatwić rozwiązywanie problemów z konfiguracją w environements ciąg bezpiecznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="6c36c-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="6c36c-121">Maszyny wirtualne systemu Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6c36c-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="6c36c-122">Program Visual Studio teraz obsługuje wdrażanie usługi w chmurze do maszyn wirtualnych 5 rodziny systemu operacyjnego (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="6c36c-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="6c36c-123">Istniejących usług w chmurze można zmienić ustawienia pod kątem nowych rodziny systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6c36c-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="6c36c-124">Podczas tworzenia nowych usług w chmurze, jeśli użytkownik chce utworzyć usługę przy użyciu platformy .net 4.6 lub nowszej, będzie on domyślnej usługi do 5 rodziny systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6c36c-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="6c36c-125">Aby uzyskać więcej informacji, możesz przejrzeć [rodziny systemów operacyjnych gościa obsługuje tabeli](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="6c36c-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="6c36c-126">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="6c36c-126">Known issues</span></span>

- <span data-ttu-id="6c36c-127">Azure .NET SDK 2.9.6 wprowadzone ograniczeń, która blokuje wdrożenie projektów przy użyciu nieobsługiwanego platformy .NET (np. .NET 4.6) do dowolnego rodziny systemów operacyjnych < 5.</span><span class="sxs-lookup"><span data-stu-id="6c36c-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="6c36c-128">Udostępniono obejście [tutaj](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="6c36c-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="6c36c-129">Pamięć podręczna na roli Azure</span><span class="sxs-lookup"><span data-stu-id="6c36c-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="6c36c-130">Obsługa kończy się na roli Azure w pamięci podręcznej w dniu 30 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="6c36c-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="6c36c-131">Aby uzyskać więcej informacji, kliknij przycisk [tutaj](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="6c36c-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="6c36c-132">Stack — szablony usługi Azure Resource Manager dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c36c-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="6c36c-133">Dodaliśmy stosu Azure jako cel wdrożenia szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c36c-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="6c36c-134">Zestaw Azure SDK dla platformy .NET 2.9 podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6c36c-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="6c36c-135">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6c36c-135">Overview</span></span>
<span data-ttu-id="6c36c-136">Ten dokument zawiera informacje o wersji dla zestawu Azure SDK dla platformy .NET 2.9 wydania.</span><span class="sxs-lookup"><span data-stu-id="6c36c-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="6c36c-137">Aby uzyskać szczegółowe informacje na temat aktualizacji w tej wersji, zobacz [post anonsu zestaw Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="6c36c-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="6c36c-138">Zestaw Azure SDK 2.9 dla programu Visual Studio 2015 Update 2 do programu Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="6c36c-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="6c36c-139">Ta aktualizacja obejmuje następujące poprawki:</span><span class="sxs-lookup"><span data-stu-id="6c36c-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="6c36c-140">Problem związany z REST API generowania klienta w, w którym ciąg "Nieznany typ" zostanie wyświetlony jako nazwa folderu generacji kodu i/lub nazwę przestrzeni nazw upuścić na wygenerowany kod.</span><span class="sxs-lookup"><span data-stu-id="6c36c-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="6c36c-141">Problem związany z zaplanowanych zadań Webjob, w którym sprawdzano informacje dotyczące uwierzytelniania do przekazania do harmonogramu, w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="6c36c-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="6c36c-142">Ta aktualizacja obejmuje następującą nową funkcję:</span><span class="sxs-lookup"><span data-stu-id="6c36c-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="6c36c-143">Obsługa dodatkowej usługi aplikacji na karcie "Usługi" okno dialogowe zastrzegania usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c36c-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="6c36c-144">Narzędzia usługi Azure Data Lake Tools dla Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="6c36c-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="6c36c-145">Tej aktualizacji obejmuje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="6c36c-145">This updates includes the following:</span></span>

* <span data-ttu-id="6c36c-146">**Azure Data Lake Tools** dla programu Visual Studio teraz jest scalany zestawu Azure SDK dla wersji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="6c36c-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="6c36c-147">Narzędzie jest automatycznie instalowany podczas instalowania zestawu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="6c36c-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="6c36c-148">Narzędzie jest często aktualizowana, przejdź [tutaj](http://aka.ms/datalaketool) pobierania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6c36c-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="6c36c-149">**W Eksploratorze serwera** umożliwia teraz wyświetlanie wszystkich i tworzenie niektóre jednostki metadanych U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6c36c-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="6c36c-150">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.</span><span class="sxs-lookup"><span data-stu-id="6c36c-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="6c36c-151">Narzędzia HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="6c36c-151">HDInsight Tools</span></span>
<span data-ttu-id="6c36c-152">**Narzędzia HDInsight Tools** dla programu Visual Studio teraz obsługuje HDInsight wersji 3.3, łącznie z wykazem wykresach Tez i inny język poprawki.</span><span class="sxs-lookup"><span data-stu-id="6c36c-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="6c36c-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c36c-153">Azure Resource Manager</span></span>
<span data-ttu-id="6c36c-154">Ta wersja dodaje [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) obsługę szablony Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c36c-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c36c-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6c36c-155">See also</span></span>
[<span data-ttu-id="6c36c-156">Azure SDK 2.9 anonsu post</span><span class="sxs-lookup"><span data-stu-id="6c36c-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

