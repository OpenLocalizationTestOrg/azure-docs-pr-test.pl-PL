---
title: "aaaAzure wysoką dostępność usług Analysis Services | Dokumentacja firmy Microsoft"
description: "Zapewnienie wysokiej dostępności usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="b6195-103">Wysoka dostępność usługi analizy</span><span class="sxs-lookup"><span data-stu-id="b6195-103">Analysis Services high availability</span></span>
<span data-ttu-id="b6195-104">W tym artykule opisano, zapewniając wysoką dostępność dla serwerów usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b6195-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="b6195-105">Zapewnienie wysokiej dostępności podczas przerw w działaniu usługi</span><span class="sxs-lookup"><span data-stu-id="b6195-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="b6195-106">Gdy przypadkach centrum danych platformy Azure mogą mieć awarii.</span><span class="sxs-lookup"><span data-stu-id="b6195-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="b6195-107">W przypadku wystąpienia awarii powoduje zakłócenia biznesowych, może trwać kilka minut lub może trwać godzin.</span><span class="sxs-lookup"><span data-stu-id="b6195-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="b6195-108">Wysoka dostępność najczęściej jest to osiągane z nadmiarowością serwera.</span><span class="sxs-lookup"><span data-stu-id="b6195-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="b6195-109">Z usług Azure Analysis Services można osiągnąć nadmiarowość przez utworzenie dodatkowych, pomocnicze serwery w regionach co najmniej jeden.</span><span class="sxs-lookup"><span data-stu-id="b6195-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="b6195-110">Podczas tworzenia nadmiarowych serwerów, tooassure hello danych i metadanych na tych serwerach jest zsynchronizowana z serwerem hello w regionie, który przeszedł do trybu offline, można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b6195-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="b6195-111">Wdrażanie serwerów tooredundant modeli w różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="b6195-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="b6195-112">Ta metoda wymaga przetwarzania danych na serwerze podstawowym i nadmiarowego serwerów w równolegle, zapewniając wszystkie serwery są w synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b6195-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="b6195-113">Wykonaj kopię zapasową baz danych z serwera podstawowego i przywracania na serwerach nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="b6195-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="b6195-114">Na przykład można zautomatyzować magazynu tooAzure kopii zapasowych w nocy i przywrócić tooother nadmiarowe serwerami w różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="b6195-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="b6195-115">W obu przypadkach Jeśli serwer podstawowy ulegnie awarii, należy zmienić hello parametry połączenia w programie reporting server toohello tooconnect klientów w różnych regionalnych centrach danych.</span><span class="sxs-lookup"><span data-stu-id="b6195-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="b6195-116">Tej zmiany należy traktować jako ostateczność i występuje tylko w przypadku awarii centrum danych w wyniku katastrofy regionalne.</span><span class="sxs-lookup"><span data-stu-id="b6195-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="b6195-117">Jest bardziej prawdopodobne, awarii centrum danych podstawowego serwera hostingu przybyły trybu online przed można zaktualizować połączenia na wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="b6195-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="b6195-118">Informacje pokrewne</span><span class="sxs-lookup"><span data-stu-id="b6195-118">Related information</span></span>
<span data-ttu-id="b6195-119">[Kopia zapasowa i przywracanie](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="b6195-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="b6195-120">Zarządzanie usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b6195-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

