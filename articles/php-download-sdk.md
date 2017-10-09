---
title: Witaj aaaDownload zestaw Azure SDK for PHP
description: "Dowiedz się, jak toodownload i zainstaluj hello zestawu Azure SDK dla języka PHP."
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
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="99e4c-103">Pobierz hello Azure SDK dla języka PHP</span><span class="sxs-lookup"><span data-stu-id="99e4c-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="99e4c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="99e4c-104">Overview</span></span>
<span data-ttu-id="99e4c-105">zestaw Azure SDK for PHP Hello obejmuje składniki, które pozwalają toodevelop, wdrażania i zarządzania aplikacji PHP dla systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="99e4c-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="99e4c-106">W szczególności hello zestaw Azure SDK for PHP zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="99e4c-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="99e4c-107">**Witaj bibliotek klienckich PHP na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="99e4c-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="99e4c-108">Te biblioteki klas zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="99e4c-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="99e4c-109">**Witaj interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="99e4c-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="99e4c-110">Jest to zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99e4c-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="99e4c-111">Praca z wiersza polecenia platformy Azure na dowolnej platformie, w tym Mac, Linux i Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="99e4c-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="99e4c-112">**Program Azure PowerShell (tylko system Windows)**.</span><span class="sxs-lookup"><span data-stu-id="99e4c-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="99e4c-113">Jest to zestaw poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure, takich jak usługi w chmurze i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="99e4c-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="99e4c-114">**Hello (tylko system Windows) Azure emulatory**.</span><span class="sxs-lookup"><span data-stu-id="99e4c-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="99e4c-115">emulatory Hello obliczeniowych i przestrzeni dyskowej są emulatory lokalne usługi w chmurze i usług zarządzania danych, które pozwalają tootest aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="99e4c-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="99e4c-116">emulatory Azure Hello uruchamianie tylko w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="99e4c-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="99e4c-117">w poniższych rozdziałach Hello opisano, jak toodownload i zainstaluj hello składniki opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="99e4c-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="99e4c-118">Witaj instrukcje w tym temacie założono, że istnieje [PHP] [ install-php] zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="99e4c-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="99e4c-119">Musi mieć PHP 5.5 lub wyższej toouse hello PHP bibliotek klienta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99e4c-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="99e4c-120">Biblioteki klienckie języka PHP dla systemu Azure</span><span class="sxs-lookup"><span data-stu-id="99e4c-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="99e4c-121">Witaj PHP klienta biblioteki dla platformy Azure zapewniają interfejs do uzyskiwania dostępu do funkcji platformy Azure, takich jak dane usługi zarządzania i usługami w chmurze, z dowolnego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="99e4c-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="99e4c-122">Te biblioteki można zainstalować za pomocą hello Composer.</span><span class="sxs-lookup"><span data-stu-id="99e4c-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="99e4c-123">Informacje, jak toouse hello PHP bibliotek klienta platformy Azure, zobacz [jak tooUse hello usługa Blob][blob-service], [jak tooUse hello usługi tabel] [ table-service] i [jak tooUse hello usługi kolejki][queue-service].</span><span class="sxs-lookup"><span data-stu-id="99e4c-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="99e4c-124">Zainstaluj za pośrednictwem Composer</span><span class="sxs-lookup"><span data-stu-id="99e4c-124">Install via Composer</span></span>
1. <span data-ttu-id="99e4c-125">[Zainstaluj usługę Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="99e4c-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="99e4c-126">W systemie Windows należy również zmiennej środowiskowej ŚCIEŻKA pliku wykonywalnego tooyour tooadd hello Git.</span><span class="sxs-lookup"><span data-stu-id="99e4c-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="99e4c-127">Utwórz plik o nazwie **composer.json** w hello katalogu głównym projektu i dodać powitania po tooit kodu:</span><span class="sxs-lookup"><span data-stu-id="99e4c-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="99e4c-128">Pobierz  **[composer.phar] [ composer-phar]**  w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="99e4c-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="99e4c-129">Otwórz wiersz polecenia i wykonania tej operacji w katalogu głównym projektu</span><span class="sxs-lookup"><span data-stu-id="99e4c-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="99e4c-130">Program Azure PowerShell i emulatory Azure</span><span class="sxs-lookup"><span data-stu-id="99e4c-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="99e4c-131">Program Azure PowerShell jest zestawem poleceń cmdlet programu PowerShell dotyczące wdrażania i zarządzania usługami Azure (takie jak usługi w chmurze i maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="99e4c-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="99e4c-132">emulatory Azure Hello są emulatory usługi w chmurze i usług zarządzania danych, które pozwalają tootest aplikacji lokalnie.</span><span class="sxs-lookup"><span data-stu-id="99e4c-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="99e4c-133">Te składniki są obsługiwane tylko w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="99e4c-133">These components are supported Windows only.</span></span>

<span data-ttu-id="99e4c-134">Witaj tooinstall zalecany sposób programu Azure PowerShell i hello Azure emulatory jest toouse hello [Instalatora platformy sieci Web firmy Microsoft][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="99e4c-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="99e4c-135">Należy pamiętać, że można także tooinstall inne składniki programowanie, takich jak PHP, SQL Server, hello Drivers firmy Microsoft dla programu SQL Server dla PHP i programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="99e4c-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="99e4c-136">Aby uzyskać informacje na temat toouse programu Azure PowerShell, zobacz [jak tooUse programu Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="99e4c-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="99e4c-137">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="99e4c-137">Azure CLI</span></span>
<span data-ttu-id="99e4c-138">Hello Azure CLI jest zestaw poleceń służących do wdrażania i zarządzania usługami Azure, takich jak witryny sieci Web Azure i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99e4c-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="99e4c-139">Aby uzyskać informacje o instalowaniu interfejsu wiersza polecenia Azure, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="99e4c-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e4c-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99e4c-140">Next steps</span></span>
<span data-ttu-id="99e4c-141">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="99e4c-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
