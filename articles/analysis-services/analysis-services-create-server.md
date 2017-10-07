---
title: "aaaCreate serwerem usług Analysis Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wystąpienie toocreate serwerem usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Tworzenie serwera usług Azure Analysis Services w portalu Azure
W tym artykule przedstawiono tworzenie zasobu serwera usług Analysis Services w ramach subskrypcji platformy Azure.

## <a name="before-you-begin"></a>Przed rozpoczęciem
toocomplete tego przewodnika Szybki Start, należy:

* **Subskrypcja platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate konta.
* **Usługa Azure Active Directory**: subskrypcji musi być skojarzony z dzierżawy usługi Azure Active Directory. I należy toobe zalogowany tooAzure przy użyciu konta w tej usłudze Azure Active Directory. Konta Microsoft nie są obsługiwane. toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).
* **Grupa zasobów**: Użyj masz już grupę zasobów lub [Utwórz nową](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> Utworzenie serwera może skutkować powstaniem nowej usługi płatnej. toolearn więcej, zobacz [cennik usług Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate serwera w portalu Azure
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).  
2. Kliknij przycisk **+ nowy** > **dane i analiza** > **usług Analysis Services**.
3. W hello **usług Analysis Services** bloku, wypełnij pola hello wymagane, a następnie naciśnij klawisz **Utwórz**.
   
    ![Tworzenie serwera](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nazwa serwera**: wpisz unikatową nazwę używaną tooreference powitania serwera.
   * **Subskrypcja**: Wybierz subskrypcję hello rachunków tego serwera do.
   * **Grupa zasobów**: kontenery są zaprojektowane toohelp zarządzanie kolekcją zasobów systemu Azure. toolearn więcej, zobacz [grup zasobów](../azure-resource-manager/resource-group-overview.md).
   * **Lokalizacja**: hostów lokalizację centrum danych Azure to hello serwera. Wybierz lokalizację najbliżej największy bazy użytkowników.
   * **Warstwa cenowa**: Wybierz warstwę cenową. Modele tabelaryczne zapasowej too400 GB są obsługiwane. toolearn więcej, zobacz [cennik usług Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Kliknij przycisk **Utwórz**.

Utwórz potrzebuje zazwyczaj w obszarze chwilę. często tylko kilka sekund. W przypadku wybrania **dodać tooPortal**, przejdź toosee portalu tooyour nowego serwera. Lub zbyt Przejdź**więcej usług** > **usług Analysis Services** toosee, jeśli serwer jest gotowy.

 ![Pulpit nawigacyjny](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Następne kroki
Po utworzeniu serwera, możesz [wdrożenia modelu](analysis-services-deploy.md) tooit za pomocą narzędzi SSDT lub z narzędzia SSMS.

Jeśli model wdrażania serwera tooyour łączy tooon lokalnych źródeł danych, należy tooinstall [bramy danych lokalnych](analysis-services-gateway.md) na komputerze w sieci.

