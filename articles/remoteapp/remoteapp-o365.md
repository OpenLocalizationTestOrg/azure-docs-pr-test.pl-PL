---
title: "Za pomocą pakietu Office z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pakietu Office i usługi Azure RemoteApp współdziałać ze sobą"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a776d877c764109f15c1025db2be3114eea2130a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Za pomocą pakietu Office z usługą Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Dostępne są dwie opcje do obsługi aplikacji pakietu Office w usłudze Azure RemoteApp: usługi Office 365 ProPlus lub Office 2013 Professional Plus w wersji próbnej.

**Witaj czy wiesz, że mamy nowy, lepiej artykułu, który zastąpi wkrótce to? Zapoznaj się z [sposobu korzystania z subskrypcji usługi Office 365 z usługą Azure RemoteApp](remoteapp-officesubscription.md). Obejmuje ona wszystkich informacji potrzebnych do przy użyciu usługi Office 365 + usługa Azure RemoteApp.**

## <a name="office-365-proplus"></a>Usługi Office 365 ProPlus
Można utworzyć kolekcji usługi RemoteApp przy użyciu usługi Office 365 ProPlus obrazu szablonu. Ta opcja umożliwia rozszerzanie usługi Office 365 do usługi RemoteApp. Musi mieć istniejący plan subskrypcji, a użytkownicy muszą mieć licencję na usługę Office 365 ProPlus, jako produkt autonomiczny lub za pośrednictwem usługi Office 365 usługi planów.

Połączenia programów RemoteApp obsługuje aktywacji udostępnionego komputera w programie Office 365. Po włączeniu udostępnionych aktywacji komputera i użyj [narzędzia wdrażania pakietu Office](http://www.microsoft.com/download/details.aspx?id=36778) w przypadku instalacji usługi Office 365 ProPlus instaluje bez aktywowane. Podczas loguje użytkownika do kolekcji zawierającej usługi Office 365, Office sprawdza, czy dla usługi Office 365 ProPlus zainicjowano użytkownika. Jeśli tak, Office tymczasowo aktywuje usługi Office 365 ProPlus - Aktywacja utrzymuje się do tego Wyrejestrowywuje użytkowników z usługi.

Aby korzystać z aktywacji udostępnionego komputera w programie Office 365, należy utworzyć [szablonu niestandardowego](remoteapp-create-custom-image.md) i zainstaluj usługi Office 365 ProPlus, wykonując [te kierunkach](https://technet.microsoft.com/library/dn782858.aspx).

Możesz zarządzać użytkowników usługi Office 365 licencji na [portalu administratora usługi Office 365](https://portal.office365.com/). Przeczytaj więcej informacji na temat [plany usługi Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus w wersji próbnej
Podczas z 30-dniowej wersji próbnej usługi RemoteApp można użyć obrazu pakietu Office 2013 Professional Plus (wersja próbna) szablonu do tworzenia kolekcji usługi RemoteApp. Można przypisać użytkowników do tej wersji próbnej kolekcji przy użyciu ich konta roboczych usługi Azure Active Directory lub konta Microsoft. Brak dodatkowych subskrypcji jest wymagana.

Jest to doskonałe rozwiązanie, aby rozpocząć testowany i uzyskać dobrą wrażenie dla pakietu Office w usłudze RemoteApp. Jednak ta opcja jest przeznaczone do oceny i testowania tylko. Utworzone przy użyciu obrazu pakietu Office 2013 Professional Plus (wersja próbna) szablonu kolekcji usługi RemoteApp nie może zostać przeniesieni do trybu produkcyjnego i zostanie wyłączona po zakończeniu okresu próbnego.

## <a name="switching-from-trial-to-production"></a>Przełączanie z wersji próbnej do produkcji
Po uruchomieniu z 30-dniowej bezpłatnej wersji próbnej Uwaga w sekcji RemoteApp portalu informuje o ile masz jeszcze w wersji próbnej zanim zajdzie konieczność przejścia do płatnej konta. Można aktywować konto i Przełącz do trybu produkcyjnego przy użyciu łącza w tej uwagi.

Po uaktywnieniu konta, to będzie miało wpływ na wszystkich kolekcji usługi RemoteApp na swoim koncie.

* Kolekcje z systemem Windows Server 2012 R2 lub usługi Office 365 ProPlus obrazy szablonów będzie łatwe przechodzenie do środowiska produkcyjnego. Wszystkie dane użytkownika i ustawień, takich jak bieżące sesje pozostają niezmienione.
* Jeśli zostały przekazane obrazy szablonów niestandardowych, kolekcji przy użyciu tych obrazów również przejdą bezproblemowo.
* Obraz pakietu Office 2013 Professional Plus (wersja próbna) szablonu jest przeznaczony tylko oceny. Kolekcje z tego obrazu szablonu nie może zostać przeniesieni do środowiska produkcyjnego. Umieści w stanie "wyłączone".

Jeśli nie przejście do trybu produkcyjnego przez po upływie okresu próbnego, kolekcji usługi RemoteApp zostanie wyłączone. Nie martw się — ustawienia i dane użytkowników są zapisywane w innym 90 dni, więc nadal można aktywować usługi i Przełącz do trybu produkcyjnego bez utraty danych.

