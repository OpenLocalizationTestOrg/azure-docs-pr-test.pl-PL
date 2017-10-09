---
title: "toomultiple Azure usługi Azure API Management aaaDeploy regionów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Azure API Management usługi toomultiple wystąpienia Azure regionów."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Jak toodeploy Azure API Management usługi toomultiple wystąpienia Azure regionów
Zarządzanie interfejsami API obsługuje wdrożenia w przypadku, dzięki czemu interfejsu API wydawców toodistribute pojedynczą usługę zarządzania interfejsu API przez dowolną liczbę żądaną regiony platformy Azure. Pozwala to zmniejszyć żądania opóźnienia postrzegane przez rozproszone geograficznie konsumentów interfejsu API i zwiększa również dostępność usługi, jeśli jeden region przejdzie do trybu offline. 

Podczas tworzenia usługi Zarządzanie interfejsami API w początkowo zawiera tylko jeden [jednostki] [ unit] znajdują się w pojedynczym regionie Azure, który jest wybrany jako hello regionu podstawowego. Dodatkowe regiony można łatwo dodać za pośrednictwem hello portalu Azure. Zarządzanie interfejsami API serwera bramy jest region tooeach wdrożone i ruchu wywołania będzie routingiem toohello najbliższego bramy. Jeśli region przejdzie do trybu offline, hello jest automatycznie ponownie ukierunkowanej toohello dalej najbliższego bramy. 

> [!IMPORTANT]
> W przypadku wdrażania jest dostępna tylko w hello  **[Premium] [ Premium]**  warstwy.
> 
> 

## <a name="add-region"></a>Wdrażanie zarządzanie interfejsami API usługi wystąpienia tooa nowy region
> [!NOTE]
> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

W portalu Azure hello Przejdź toohello **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API. 

![Kartę Skala][api-management-scale-service]

toodeploy tooa nowy region, kliknij polecenie **+ Dodaj region** z hello paska narzędzi.

![Dodawanie regionu][api-management-add-region]

Wybierz z listy rozwijanej hello hello lokalizacji i ustaw hello liczba jednostek z hello suwaka.

![Określ jednostki][api-management-select-location-units]

Kliknij przycisk **Dodaj** tooplace wybór hello lokalizacji tabeli. 

Powtórz ten proces, dopóki nie uzyskasz wszystkich skonfigurowanych lokalizacji, a następnie kliknij przycisk **zapisać** z procesu wdrażania hello hello narzędzi toostart.

## <a name="remove-region"></a>Usunąć wystąpienie usługi API Management z lokalizacji
W portalu Azure hello Przejdź toohello **skali i cenach** strony wystąpienia usługi Zarządzanie interfejsami API. 

![Kartę Skala][api-management-scale-service]

Dla lokalizacji hello chcesz tooremove Otwórz menu kontekstowe hello przy użyciu hello **...**  przycisku po prawej stronie powitania hello tabeli. Wybierz hello **usunąć** opcji.

![Usuń region][api-management-remove-region]

Potwierdź usunięcie hello, a następnie kliknij przycisk **zapisać** tooapply hello zmiany.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

