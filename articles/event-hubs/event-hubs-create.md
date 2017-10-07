---
title: "aaaCreate Centrum zdarzeń platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Azure Event Hubs i Centrum zdarzeń za pomocą hello portalu Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Tworzenie przestrzeni nazw usługi Event Hubs i Centrum zdarzeń za pomocą hello portalu Azure

## <a name="create-an-event-hubs-namespace"></a>Tworzenie przestrzeni nazw usługi Event Hubs
1. Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.
1. Kliknij przycisk **Internetu rzeczy**, a następnie kliknij przycisk **usługi Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw. system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Po co czy hello przestrzeni nazw jest dostępna, należy wybrać hello cenowym (Basic lub Standard). Ponadto Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w zasobów hello toocreate. 
1. Kliknij przycisk **Utwórz** toocreate hello w przestrzeni nazw. Toowait może mieć kilka minut, aż hello systemu toofully Zapewnij hello zasoby.
2. Witaj portalu obszarów nazw kliknij na liście hello nowo utworzonego obszaru nazw.
2. Kliknij przycisk **zasady dostępu współużytkowanego**, a następnie kliknij przycisk **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Kliknij przycisk hello toocopy przycisku Kopiuj hello **RootManageSharedAccessKey** Schowka toohello ciągu połączenia. Zapisz te parametry połączenia w tymczasowej lokalizacji, takiego jak Notatnik, toouse później.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Tworzenie centrum zdarzeń

1. Na liście przestrzeni nazw usługi Event Hubs hello kliknij hello nowo utworzonego obszaru nazw.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. W bloku przestrzeni nazw powitania kliknij **usługi Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. U góry hello hello bloku, kliknij przycisk **dodać Centrum zdarzeń**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Wpisz nazwę Centrum zdarzeń, a następnie kliknij przycisk **Utwórz**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Centrum zdarzeń został utworzony i uzyskano parametry połączenia hello muszą toosend i odbierania zdarzeń.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Event Hubs, odwiedź te linki:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Omówienie interfejsu API usługi Event Hubs](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/