---
title: "wymagania wstępne aaaTechnical do tworzenia obrazu maszyny wirtualnej dla hello Azure Marketplace | Dokumentacja firmy Microsoft"
description: "Poznaj hello wymagania dotyczące tworzenia i wdrażania toohello obrazu maszyny wirtualnej Azure Marketplace innym toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Techniczne wymagania wstępne dotyczące tworzenia obrazu maszyny wirtualnej dla hello Azure Marketplace
Proces hello dokładnie przed rozpoczęciem należy dokładnie zapoznać się gdzie i dlaczego jest wykonywane każdego kroku. Jak to możliwe, należy należy przygotować informacji o swojej firmie i innych danych, Pobierz niezbędne narzędzia i/lub tworzenia składników techniczne przed rozpoczęciem procesu tworzenia oferty hello. Te elementy powinno być wolne od przeglądania w tym artykule.  

## <a name="download-needed-tools--applications"></a>Pobierz potrzebne narzędzia i aplikacje
Musisz mieć hello poniższych elementach gotowe przed rozpoczęciem procesu hello:

* W zależności od systemu operacyjnego przeznaczonych, zainstaluj hello [poleceń cmdlet programu Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) lub [Linux interfejsu wiersza polecenia narzędzia](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) z hello [Azure pobiera](https://azure.microsoft.com/downloads/) Strona.
* Instalowanie Eksploratora usługi Storage platformy Azure w witrynie CodePlex.
* Pobierz i zainstaluj hello narzędzia Test certyfikacji dla certyfikowane Azure:
  * [http://go.microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Należy narzędzie certyfikacji hello toorun komputer z systemem Windows. Jeśli nie masz komputera z systemem Windows dostępne, można uruchomić narzędzie hello na platformie Azure przy użyciu maszyny Wirtualnej z systemem Windows.

## <a name="platforms-supported"></a>Obsługiwane platformy
Można tworzyć maszyn wirtualnych w usłudze Azure w systemie Windows lub Linux. Niektóre elementy hello procesu — takich jak tworzenie Azure zgodnego wirtualnego dysku twardego (VHD)--Użyj różnych narzędzi i kroki w zależności od systemu operacyjnego są przy użyciu publikowania:  

* Jeśli używasz systemu Linux można znaleźć toohello "Tworzenie wirtualnego dysku twardego zgodnego Azure (opartych na systemie Linux)" sekcji hello [Podręcznik publikowania obrazu maszyny wirtualnej](marketplace-publishing-vm-image-creation.md).
* Jeśli używasz systemu Windows można znaleźć toohello "Tworzenie wirtualnego dysku twardego zgodnego Azure (z systemem Windows)" sekcji hello [Podręcznik publikowania obrazu maszyny wirtualnej](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Należy uzyskać dostęp do tooa maszyny z systemem Windows do:
> 
> * Uruchom narzędzie sprawdzania poprawności hello certyfikacji.
> * Utwórz adres URL sygnatury dostępu udostępnionego wirtualnego dysku twardego hello na powitania przesyłanie certyfikacji wirtualnego dysku twardego.
> 
> 

## <a name="develop-your-vhd"></a>Opracowywanie dysk VHD
Można tworzyć wirtualne dyski twarde Azure w chmurze hello lub lokalnie:

* Programowanie oparte na chmurze oznacza, że wszystkie kroki tworzenia są wykonywane zdalnie na dysku VHD znajdują się na platformie Azure.
* Programowanie lokalnymi wymaga pobierania wirtualnego dysku twardego i tworzenie za pomocą infrastruktury lokalnej. Jest to możliwe, zaleca się jej. Należy pamiętać, że tworzenie aplikacji dla systemu Windows lub SQL lokalnymi wymaga kluczy licencji odpowiednich lokalnymi hello toohave. Nie można dołączyć lub instalowania programu SQL Server po utworzeniu maszyny Wirtualnej. Należy utworzyć ofertę również na zatwierdzonych SQL z obrazu hello portalu Azure. Jeśli zdecydujesz się toodevelop lokalnymi, niektóre kroki należy wykonać inaczej niż jeśli zostały tworzenie aplikacji w chmurze hello. Odpowiednie informacje w można znaleźć [Tworzenie obrazu maszyny Wirtualnej lokalnymi](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
