---
title: "aaaUsing programu Outlook w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure i korzystać z programu Outlook w usłudze Azure RemoteApp | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Używanie programu Microsoft Outlook w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp obsługuje program Microsoft Outlook usługi O365. Dowiedz się więcej na temat [działania pakietu Office w usłudze Azure RemoteApp](remoteapp-officesubscription.md). Istnieje kilka zalecanych ustawień dla programu Outlook używanego w usłudze Azure RemoteApp.

## <a name="cached-mode"></a>Tryb buforowany
Tryb buforowany jest zalecaną konfiguracją w przypadku korzystania z programu Outlook w usłudze Azure RemoteApp. Podczas konfigurowania programu Outlook 2013 konta toouse tryb buforowanej wymiany, Outlook 2013 współpracuje z lokalną kopią hello użytkownika skrzynki pocztowej programu Microsoft Exchange, który jest przechowywany w pliku danych w trybie offline (pliku OST) na komputerze użytkownika hello, wraz z hello książki adresowej Offline (OAB). Witaj buforowana Skrzynka pocztowa i Książka adresowa offline są okresowo aktualizowane danymi z hello usługi O365. Przeczytaj więcej na temat [hello różnice między buforowanym a trybem online](https://technet.microsoft.com/library/jj683103.aspx).

Witaj, użytkownik może wybrać **trybu buforowanej wymiany** lub **trybu Online** podczas konfigurowania konta lub zmienić ustawienia konta hello. Można także wdrożyć jeden tryb lub hello innych za pomocą hello narzędzia dostosowywania pakietu Office (OCT) lub zasad grupy.  

Przeczytaj [instrukcje krok po kroku dotyczące włączania trybu buforowanego](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Wyszukiwanie
Wyszukiwanie w programie Outlook w usłudze Azure RemoteApp ma pewne ograniczenia. Usługa Azure RemoteApp używa puli sesji użytkownika tooaccommodate maszyn wirtualnych. Indeksowanie wyszukiwania zależy od Identyfikatora komputera hello, która jest różna dla różnych maszyn wirtualnych. Istnieje możliwość, że za każdym razem, gdy użytkownik loguje się do usługi Azure RemoteApp, są one ukierunkowanej tooa nowej maszyny Wirtualnej. Oznacza to, czy włączyliśmy Wyszukiwanie lokalne powitania indeksator będzie uruchamiany przy każdej zmianie Identyfikatora komputera hello (gdy hello użytkownika znajduje się w innej maszyny Wirtualnej). W zależności od wielkości hello hello. Pliku OST indeksatora hello może potrwać toocomplete dużo czasu i zużywać zasoby potrzebne dla innych aplikacji. Wyszukiwanie nie tylko jest powolne, ale może nie dawać wyników. Przy użyciu profilu konta w trybie Online czy obejść ten problem, ale ogólną wydajność może się pogorszyć ze względu na brak toohello lokalnej pamięci podręcznej (zobacz hello link powyżej, aby uzyskać więcej informacji o hello różnica między buforowanym a trybem online). Niestety, nie można wyłączyć indeksowanego/lokalnego wyszukiwania ani włączyć wyszukiwania w trybie online jako domyślnego w programie Outlook 2013.

