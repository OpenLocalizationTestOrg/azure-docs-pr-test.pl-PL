---
title: "aaaDeploy QuickBooks w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooshare QuickBooks z usługą Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="59aa2-103">Sposób wdrażania programu QuickBooks w usłudze Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="59aa2-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="59aa2-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="59aa2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="59aa2-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="59aa2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="59aa2-106">Użyj hello następujące informacje tooshare QuickBooks jako aplikacja w usłudze Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="59aa2-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="59aa2-107">QuickBooks 2015 Enterprise z usługą Azure RemoteApp można udostępniać w kolekcji hybrydowej lub chmury.</span><span class="sxs-lookup"><span data-stu-id="59aa2-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="59aa2-108">Witaj firmy plik musi znajdować się na maszynie Wirtualnej, na którym działa serwer bazy danych programu QuickBooks, która jest oddzielona od serwerów usługi Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="59aa2-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="59aa2-109">Nigdy nie przechowują hello plików firmy na obrazie usługi Azure RemoteApp — oczekiwano utraty danych w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="59aa2-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="59aa2-110">Tylko QuickBooks Enterprise obsługuje hostingu hello QuickBooks pliku w udziale zewnętrznych z serwerem bazy danych programu QuickBooks dostępny za pośrednictwem standardowych sieci systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="59aa2-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="59aa2-111">Hello serwera bazy danych programu QuickBooks obsługujący hello firmy plik musi znajdować się w oddzielnych maszyny Wirtualnej w ramach hello sam sieci Wirtualnej jako hello kolekcji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="59aa2-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="59aa2-112">Kroki toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="59aa2-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="59aa2-113">Tworzenie maszyny Wirtualnej platformy Azure i zainstaluj QuickBooks, serwera bazy danych programu QuickBooks i umieścić plik firmy hello na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59aa2-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="59aa2-114">Upewnij się, że tooproperly Konfigurowanie reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="59aa2-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="59aa2-115">Instalowanie programu QuickBooks na [niestandardowego obrazu](remoteapp-imageoptions.md) i Utwórz [kolekcji usługi Azure RemoteApp](remoteapp-collections.md), chmury lub hybrydowego, w ramach hello dokładnie gdzie hosting wirtualna hello hello QuickBooks serwera bazy danych z tej samej sieci Wirtualnej znajdują się pliki firmy.</span><span class="sxs-lookup"><span data-stu-id="59aa2-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="59aa2-116">[Publikowanie](remoteapp-publish.md) QuickBooks toousers aplikacji</span><span class="sxs-lookup"><span data-stu-id="59aa2-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="59aa2-117">Uruchomić powitania klienta QuickBooks hostowanych w usłudze Azure RemoteApp, nawigować przy użyciu standardowego sieci toohello wirtualna hostingu hello QuickBooks serwera bazy danych systemu Windows, a następnie otwórz plik firmy hello.</span><span class="sxs-lookup"><span data-stu-id="59aa2-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="59aa2-118">Odwołania do dokumentacji</span><span class="sxs-lookup"><span data-stu-id="59aa2-118">Documentation references</span></span>
* <span data-ttu-id="59aa2-119">QuickBooks [obsługiwane konfiguracje](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="59aa2-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="59aa2-120">QuickBooks [opcje wdrażania](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="59aa2-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="59aa2-121">Można również wyewidencjonować prezentacji Ignite [podstawowe informacje dotyczące programu Microsoft Azure RemoteApp zarządzania i administrowania](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -szybko przewinąć do przodu too1:02:45 tooget toohello QuickBooks części.</span><span class="sxs-lookup"><span data-stu-id="59aa2-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="59aa2-122">Architektura wdrażania</span><span class="sxs-lookup"><span data-stu-id="59aa2-122">Deployment architecture</span></span>
![QuickBooks + wdrożenia usługi Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

