---
title: "Pobierz zestaw Azure SDK dla języka PHP"
description: "Dowiedz się, jak pobrać i zainstalować zestaw Azure SDK for PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="562aa-103">Pobierz zestaw Azure SDK dla języka PHP</span><span class="sxs-lookup"><span data-stu-id="562aa-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="562aa-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="562aa-104">Overview</span></span>
<span data-ttu-id="562aa-105">Zestaw Azure SDK for PHP zawiera składniki, które umożliwiają tworzenie, wdrażanie i zarządzanie aplikacji PHP dla systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="562aa-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="562aa-106">W szczególności zestaw Azure SDK for PHP obejmuje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="562aa-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="562aa-107">**PHP bibliotek klienta platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="562aa-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="562aa-108">Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="562aa-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="562aa-109">**Interfejs wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="562aa-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="562aa-110">Jest to zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="562aa-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="562aa-111">Praca wiersza polecenia platformy Azure na dowolnej platformie, w tym Mac, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="562aa-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="562aa-112">**Program Azure PowerShell (tylko system Windows)**.</span><span class="sxs-lookup"><span data-stu-id="562aa-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="562aa-113">Jest to zestaw poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure, takich jak usługi w chmurze i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="562aa-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="562aa-114">**Emulatory Azure (tylko system Windows)**.</span><span class="sxs-lookup"><span data-stu-id="562aa-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="562aa-115">Emulatory obliczeniowych i przestrzeni dyskowej są emulatory lokalne usługi w chmurze i usług zarządzania danych, dzięki którym można przetestować aplikację lokalnie.</span><span class="sxs-lookup"><span data-stu-id="562aa-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="562aa-116">Emulatory Azure uruchamianie tylko w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="562aa-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="562aa-117">W poniższych rozdziałach opisano, jak pobrać i zainstalować składniki opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="562aa-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="562aa-118">Instrukcje w tym temacie założono, że istnieje [PHP] [ install-php] zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="562aa-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="562aa-119">Musi mieć PHP 5.5 lub nowszego, aby użyć bibliotek klienckich PHP na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="562aa-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="562aa-120">Biblioteki klienckie języka PHP dla systemu Azure</span><span class="sxs-lookup"><span data-stu-id="562aa-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="562aa-121">PHP bibliotek klienta platformy Azure zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługami z dowolnego systemu operacyjnego w chmurze.</span><span class="sxs-lookup"><span data-stu-id="562aa-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="562aa-122">Te biblioteki można zainstalować za pomocą Composer.</span><span class="sxs-lookup"><span data-stu-id="562aa-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="562aa-123">Aby uzyskać informacje o sposobie używania bibliotek klienckich PHP na platformie Azure, zobacz [jak używać usługi Blob][blob-service], [sposobu korzystania z usługi tabel] [ table-service]i [jak używać usługi kolejki][queue-service].</span><span class="sxs-lookup"><span data-stu-id="562aa-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="562aa-124">Zainstaluj za pośrednictwem Composer</span><span class="sxs-lookup"><span data-stu-id="562aa-124">Install via Composer</span></span>
1. <span data-ttu-id="562aa-125">[Zainstaluj usługę Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="562aa-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="562aa-126">W systemie Windows należy również dodać Git pliku wykonywalnego do Twojej zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="562aa-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="562aa-127">Utwórz plik o nazwie **composer.json** w folderze głównym projektu i Dodaj do niej następujący kod:</span><span class="sxs-lookup"><span data-stu-id="562aa-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="562aa-128">Pobierz  **[composer.phar] [ composer-phar]**  w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="562aa-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="562aa-129">Otwórz wiersz polecenia i wykonania tej operacji w katalogu głównym projektu</span><span class="sxs-lookup"><span data-stu-id="562aa-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="562aa-130">Program Azure PowerShell i emulatory Azure</span><span class="sxs-lookup"><span data-stu-id="562aa-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="562aa-131">Program Azure PowerShell jest zestawem poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure (takie jak usługi w chmurze i maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="562aa-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="562aa-132">Emulatory Azure są emulatory usługi w chmurze i usług zarządzania danych, dzięki którym można przetestować aplikację lokalnie.</span><span class="sxs-lookup"><span data-stu-id="562aa-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="562aa-133">Te składniki są obsługiwane tylko w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="562aa-133">These components are supported Windows only.</span></span>

<span data-ttu-id="562aa-134">Zalecanym sposobem instalowania programu Azure PowerShell i emulatory Azure jest użycie [Instalatora platformy sieci Web firmy Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="562aa-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="562aa-135">Należy pamiętać, że użytkownik można również zainstalować inne składniki programowanie, takich jak PHP, SQL Server, Drivers firmy Microsoft dla programu SQL Server dla PHP i programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="562aa-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="562aa-136">Aby uzyskać informacje o sposobie używania programu Azure PowerShell, zobacz [jak używać programu Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="562aa-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="562aa-137">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="562aa-137">Azure CLI</span></span>
<span data-ttu-id="562aa-138">Azure CLI jest zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="562aa-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="562aa-139">Aby uzyskać informacje o instalowaniu interfejsu wiersza polecenia Azure, zobacz [instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="562aa-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="562aa-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="562aa-140">Next steps</span></span>
<span data-ttu-id="562aa-141">Aby uzyskać więcej informacji, zobacz [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="562aa-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
