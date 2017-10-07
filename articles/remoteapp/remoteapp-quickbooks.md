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
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Sposób wdrażania programu QuickBooks w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Użyj hello następujące informacje tooshare QuickBooks jako aplikacja w usłudze Azure RemoteApp.

QuickBooks 2015 Enterprise z usługą Azure RemoteApp można udostępniać w kolekcji hybrydowej lub chmury. Witaj firmy plik musi znajdować się na maszynie Wirtualnej, na którym działa serwer bazy danych programu QuickBooks, która jest oddzielona od serwerów usługi Azure RemoteApp hello. Nigdy nie przechowują hello plików firmy na obrazie usługi Azure RemoteApp — oczekiwano utraty danych w takim przypadku. Tylko QuickBooks Enterprise obsługuje hostingu hello QuickBooks pliku w udziale zewnętrznych z serwerem bazy danych programu QuickBooks dostępny za pośrednictwem standardowych sieci systemu Windows.   

> [!IMPORTANT]
> Hello serwera bazy danych programu QuickBooks obsługujący hello firmy plik musi znajdować się w oddzielnych maszyny Wirtualnej w ramach hello sam sieci Wirtualnej jako hello kolekcji usługi Azure RemoteApp.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Kroki toodeploy QuickBooks
1. Tworzenie maszyny Wirtualnej platformy Azure i zainstaluj QuickBooks, serwera bazy danych programu QuickBooks i umieścić plik firmy hello na maszynie Wirtualnej platformy Azure.  Upewnij się, że tooproperly Konfigurowanie reguł zapory.
2. Instalowanie programu QuickBooks na [niestandardowego obrazu](remoteapp-imageoptions.md) i Utwórz [kolekcji usługi Azure RemoteApp](remoteapp-collections.md), chmury lub hybrydowego, w ramach hello dokładnie gdzie hosting wirtualna hello hello QuickBooks serwera bazy danych z tej samej sieci Wirtualnej znajdują się pliki firmy. 
3. [Publikowanie](remoteapp-publish.md) QuickBooks toousers aplikacji
4. Uruchomić powitania klienta QuickBooks hostowanych w usłudze Azure RemoteApp, nawigować przy użyciu standardowego sieci toohello wirtualna hostingu hello QuickBooks serwera bazy danych systemu Windows, a następnie otwórz plik firmy hello. 

## <a name="documentation-references"></a>Odwołania do dokumentacji
* QuickBooks [obsługiwane konfiguracje](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [opcje wdrażania](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Można również wyewidencjonować prezentacji Ignite [podstawowe informacje dotyczące programu Microsoft Azure RemoteApp zarządzania i administrowania](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -szybko przewinąć do przodu too1:02:45 tooget toohello QuickBooks części.

## <a name="deployment-architecture"></a>Architektura wdrażania
![QuickBooks + wdrożenia usługi Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

