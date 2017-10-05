---
title: "Za pomocą aplikacji App-V z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z aplikacji App-V w usłudze Azure RemoteApp."
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Za pomocą aplikacji App-V w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

W kolekcji hybrydowej usługi Azure RemoteApp, co wymaga przyłączenie do domeny, można użyć aplikacji App-V.

Przed rozpoczęciem pracy, upewnij się zainstalować klienta App-V 5.1 z najnowszymi aktualizacjami. Musisz utworzyć [niestandardowego obrazu](remoteapp-create-custom-image.md) zawierającą klienta App-V.  

Jest to łatwe w użyciu istniejącej infrastruktury programu App-V z usługą Azure RemoteApp. Kolekcja hybrydowa jest wdrażana na sieć Wirtualną platformy Azure, który ma dostęp do kontrolera domeny i maszyn wirtualnych są przyłączone do domeny, można wykorzystać istniejące App-v infrastruktury i wdrożenie metody do aplikacji App-V host easyily w usłudze Azure RemoteApp. Poniżej przedstawiono pewne kwestie, które należy zwrócić uwagę na podstawie typu wdrożenia App-V, które obecnie ma:

| Opcje konfiguracji |  | Dodatnią | Ujemna |
| --- | --- | --- | --- |
| Metoda dostarczania |Przesyłania strumieniowego (na żądanie) |Aplikacja jest zawsze r i świeża |Pierwszy opóźnienia |
| Zainstalowany |Najszybszym; Aplikacja jest już obecny w maszynie Wirtualnej |Rozrostu - ma miejsce obrazu (limit 127 GB) | |
| Aplikacja lokalizacji magazynu |Zawartość udostępniona |Aplikacja jest uruchamiana w pamięci wystąpienia usługi Azure RemoteApp |Eats pamięci i dobre połączenie przesyłania strumieniowego serwera (plik), w którym znajduje się aplikacja |
| Dysku (buforowanej) |Szybkie wykonywanie. Aplikacja nie jest zależna od dostępności źródła zawartości |Rozrostu - ma miejsce obrazu (limit 127 GB) | |
| Określanie wartości docelowej |Użytkownik |Wymaga infrastruktury App-V pełne autonomiczny | |
| Global (komputer) |Wstępnie publikowania lub docelowych przy użyciu publikowania serwera |Należy zaktualizować obrazu platformy Azure, jeśli chcesz zaktualizować aplikację (dużych). Zajmie trochę miejsca na obrazie. | |

 Po utworzeniu niestandardowego obrazu i kolekcji hybrydowej opublikować aplikację, Przypisz użytkowników i korzystać z istniejących aplikacji App-V hostowanych w usłudze Azure RemoteApp dostarczane na dowolnych urządzeniach w dowolnym miejscu.

