---
title: "Pojęcia dotyczące zdarzeń siatki aaaAzure"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia. Definiuje kilka najważniejszych składników zdarzeń siatki."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Pojęcia dotyczące usługi Azure Event siatki

główne pojęcia Hello w siatce zdarzeń Azure są:

## <a name="events"></a>Zdarzenia

Zdarzenie jest hello najmniejsza ilość informacji opisujący pełni coś się stało hello systemu.  Każde zdarzenie zawiera typowe informacje, takie jak: źródło hello zdarzenia, czas hello zdarzenia miały miejsce i unikatowym identyfikatorem.  Każde zdarzenie ma również informacje, na które jest tylko odpowiednie toohello konkretnego zdarzenia. Na przykład zdarzenie o nowy plik tworzony w usłudze Azure Storage zawiera szczegółowe informacje o pliku hello, takich jak hello lastTimeModified wartość. Lub zdarzenia o ponowny rozruch maszyny wirtualnej zawiera nazwę hello hello maszyny wirtualnej i hello przyczynę ponownego uruchomienia.

## <a name="event-sourcespublishers"></a>Wydawcy źródła zdarzeń

Źródłem zdarzenia jest, gdzie hello zdarzenie. Na przykład usługi Azure Storage jest hello źródła zdarzeń dla zdarzenia utworzony obiekt blob. Sieci szkieletowej maszyny Wirtualnej Azure jest hello źródła zdarzeń dla zdarzenia maszyny wirtualnej. Źródła zdarzeń są zobowiązani do publikowania zdarzeń tooEvent siatki.

## <a name="topics"></a>Tematy

Wydawcy kategoryzowanie zdarzeń do tematów. temat Hello zawiera punkt końcowy, gdzie wydawcy hello wysyła zdarzenia. toorespond toocertain typy zdarzeń, subskrybentów zdecyduj, które toosubscribe tematów do. Tematy zawierają również schematu zdarzeń, aby subskrybenci mogą odnajdować jak tooconsume hello zdarzenia odpowiednio.

System tematy dotyczą wbudowanych udostępnionego przez usługi Azure. Tematy niestandardowe są tematy innych firm i aplikacji.

## <a name="event-subscriptions"></a>Subskrypcja zdarzeń

Subskrypcję nakazuje siatki zdarzeń na zdarzenia na temat otrzymywać jest subskrybenta.  Subskrypcja zawiera również informacji na temat sposobu powinien dostarczania zdarzeń toohello subskrybenta.

## <a name="event-handlers"></a>Uchwyty zdarzeń

Z perspektywy siatki zdarzeń program obsługi zdarzeń jest miejsce hello wysyłania hello zdarzeń. Obsługa Hello przełączy niektóre dodatkowe zdarzenie hello tooprocess akcji.  Siatka zdarzeń obsługuje wiele typów subskrybenta. W zależności od typu hello subskrybenta siatki zdarzeń wynika różnych mechanizmów tooguarantee hello dostarczania hello zdarzenia.  Dla programów obsługi zdarzeń elementu webhook HTTP, zdarzenie hello jest ponawiana dopóki obsługi hello zwraca kod stanu `200 – OK`. Dla kolejki magazynu Azure zdarzenia hello są ponawiana dopóki hello usługi kolejki jest możliwe toosuccessfully procesu hello komunikat wypychania do kolejki hello.

## <a name="filters"></a>Filtry

Gdy subskrypcja tematu tooa, można filtrować hello zdarzenia, które są wysyłane do punktu końcowego toohello. Można filtrować według typu zdarzenia lub wzorca podmiotu. Aby uzyskać więcej informacji, zobacz [schematu subskrypcji zdarzeń siatki](subscription-creation-schema.md).

## <a name="security"></a>Bezpieczeństwo

Zdarzenie zawiera zabezpieczeń dla subskrypcji tootopics i publikowania tematów. Gdy subskrypcja, musi mieć odpowiednie uprawnienia na powitania zasobów lub tematu. Podczas publikowania, musi mieć tokenu sygnatury dostępu Współdzielonego lub uwierzytelniania opartego na kluczu hello tematu. Aby uzyskać więcej informacji, zobacz [siatki zdarzeń zabezpieczeń i uwierzytelniania](security-authentication.md).

## <a name="failed-delivery"></a>Dostarczenie nie powiodło się

Gdy siatki zdarzenia nie mogą potwierdzić, że zdarzenie zostały odebrane przez punkt końcowy hello subskrybenta, redelivers hello zdarzeń. Aby uzyskać więcej informacji, zobacz [dostarczanie komunikatów zdarzeń siatki i ponów próbę](delivery-and-retry.md).

## <a name="next-steps"></a>Następne kroki

* Aby tooEvent wprowadzenie siatki, zobacz [o siatki zdarzeń](overview.md).
* tooquickly rozpocząć korzystanie z siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).
