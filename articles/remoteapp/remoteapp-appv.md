---
title: "aplikacje App-V aaaUsing z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje toouse App-V w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Za pomocą aplikacji App-V w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

W kolekcji hybrydowej usługi Azure RemoteApp, co wymaga przyłączenie do domeny, można użyć aplikacji App-V.

Przed rozpoczęciem pracy należy upewnić się, że klient App-V 5.1 hello tooinstall o hello najnowsze aktualizacje. Konieczne będzie toocreate [niestandardowego obrazu](remoteapp-create-custom-image.md) zawierającą klienta hello App-V.  

Jest łatwy toouse istniejącej infrastruktury programu App-V z usługą Azure RemoteApp. Ponieważ kolekcji hybrydowej jest wdrażana na sieć Wirtualną platformy Azure ma kontroler domeny tooyour dostępu i maszyn wirtualnych hello są przyłączone do domeny, można wykorzystać istniejące App-v infrastruktury i wdrożenie metody tooeasyily App-V aplikacji hosta w usłudze Azure RemoteApp. Poniżej przedstawiono pewne kwestie, które należy zwrócić uwagę na podstawie hello typu wdrożenia App-V, które obecnie ma:

| Opcje konfiguracji |  | Dodatnią | Ujemna |
| --- | --- | --- | --- |
| Metoda dostarczania |Przesyłania strumieniowego (na żądanie) |Aplikacja jest zawsze hello najnowsze i gotowości do pracy |Pierwszy opóźnienia |
| Zainstalowany |Najszybszym; Aplikacja jest już obecny na powitania maszyny Wirtualnej |Rozrostu - ma miejsce obrazu (limit 127 GB) | |
| Aplikacja lokalizacji magazynu |Zawartość udostępniona |Aplikacja jest uruchamiana w pamięci wystąpienia usługi Azure RemoteApp |Eats pamięci i dobre połączenie serwera toostreaming (plik), w którym znajduje się aplikacja hello |
| Dysku (buforowanej) |Szybkie wykonywanie. Aplikacja nie jest zależna od dostępności źródła zawartości |Rozrostu - ma miejsce obrazu (limit 127 GB) | |
| Określanie wartości docelowej |Użytkownik |Wymaga infrastruktury App-V pełne autonomiczny | |
| Global (komputer) |Wstępnie publikowania lub docelowych przy użyciu publikowania serwera |Musi tooupdate obrazu platformy Azure, jeśli chcesz aplikacji hello tooupdate (dużych). Zajmie trochę miejsca na obrazie. | |

 Po utworzeniu niestandardowego obrazu i kolekcji hybrydowej opublikować aplikację, Przypisz użytkowników i korzystać z istniejących aplikacji App-V hostowanych w usłudze Azure RemoteApp dostarczyć urządzenia tooany w dowolnym miejscu.

