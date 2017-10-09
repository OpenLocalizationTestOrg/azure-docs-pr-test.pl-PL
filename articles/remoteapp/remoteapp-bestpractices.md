---
title: najlepsze praktyki RemoteApp aaaAzure | Dokumentacja firmy Microsoft
description: "Najlepsze praktyki dotyczące konfigurowania i korzystania z usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Najlepsze praktyki dotyczące konfigurowania i korzystania z usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) szczegółowe informacje.
> 
> 

Hello następujące informacje ułatwiają konfigurowanie i używanie usługi Azure RemoteApp efektywnie.

## <a name="connectivity"></a>Łączność
* Należy zawsze używać najnowszej wersji klienta hello. Przy użyciu starszych klientów może spowodować problemy z łącznością i inne obniżeniem środowiska. Włączanie aktualizacje automatyczne stosowanie dla urządzenia zostanie upewnij się, że tego hello najnowszego klienta jest zawsze instalowany.
* Zawsze używaj hello stabilny i najbardziej niezawodne internet połączenia dostępne tooyou.  
* Użyj obsługiwane są tylko połączenia serwera proxy dla łączności optymalną wydajność.  Serwer proxy SOCKS Hello nie jest obsługiwane.

## <a name="applications"></a>Aplikacje
* Zapisz i zamknij aplikacje usługi RemoteApp po zakończeniu aplikacji hello. Nie zamknięcia aplikacji hello może spowodować utratę danych.
* Sprawdź poprawność niestandardowych aplikacji przed ich użyciem w usłudze Azure RemoteApp. Obejmuje to zapewnienie działa na platformie wielu sesji i nie używać niepotrzebnych zasobów, np. pamięci i procesora CPU, który może blokować go innego użytkownika w hello tej samej kolekcji. Informacje, należy pobrać i przejrzyj hello [zgodności aplikacji najlepsze rozwiązania dotyczące usług pulpitu zdalnego](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Konfiguracja i zarządzanie nim
* Zachowaj obrazów szablonu się toodate, instalowania aktualizacji oprogramowania i innych krytycznych poprawek, zgodnie z potrzebami. Dzięki temu, że zgodnie z usługi Azure RemoteApp auto skale toomeet poprawiono wydajność, każde wystąpienie.  
* Upewnij się, że wdrożenie usługi Active Directory Federation Services (AD FS) jest bezpieczny i niezawodny. W przeciwnym razie uwierzytelnianie klienta może zakończyć się niepowodzeniem, uniemożliwia użytkownikom uzyskiwanie dostępu do usługi Azure RemoteApp.
* Skonfiguruj obrazy szablonów z zainstalowanymi aplikacjami, ról lub funkcji tak, aby były one bezstanowe. Należy nie opierają się na wszystkie wystąpienia hello maszyn wirtualnych za pośrednictwem usługi RemoteApp jest w stanie trwałych.
  * Takie jak lokalnymi udziały plików lub OneDrive przechowywane są wszystkie dane użytkownika w innej usługi toohello zewnętrznej lokalizacji magazynu lub profilów użytkowników.
  * Magazyn danych udostępnionych w usługi zewnętrzne toohello lokalizacje magazynu, takich jak lokalnymi udziały plików lub OneDrive.
  * Skonfiguruj ustawienia systemowe w hello obrazu szablonu, a nie na poszczególnych maszyn wirtualnych w usłudze.
  * Wyłącz automatyczne aktualizacje oprogramowania dla opublikowanych aplikacji — zamiast tego je ręcznie zastosować toohello obrazu szablonu i testowane przed wdrożeniem z hello szablonu.

