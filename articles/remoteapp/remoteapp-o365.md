---
title: "aaaUsing Office z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Za pomocą pakietu Office z usługą Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Dostępne są dwie opcje do obsługi aplikacji pakietu Office w usłudze Azure RemoteApp: usługi Office 365 ProPlus lub Office 2013 Professional Plus w wersji próbnej.

**Witaj czy wiesz, że mamy nowy, lepiej artykułu, który zastąpi wkrótce to? Zapoznaj się z [jak toouse subskrypcji usługi Office 365 z usługą Azure RemoteApp](remoteapp-officesubscription.md). Obejmuje ona wszystkie informacje o hello potrzebnych przy użyciu usługi Office 365 + usługa Azure RemoteApp.**

## <a name="office-365-proplus"></a>Usługi Office 365 ProPlus
Można utworzyć przy użyciu obrazu szablonu usługi Office 365 ProPlus hello kolekcji usługi RemoteApp. Ta opcja umożliwia tooextend Twojego tooRemoteApp usługi Office 365. Musi mieć istniejący plan subskrypcji, a użytkownicy muszą mieć licencję dla usługi Office 365 ProPlus, jako produkt autonomiczny hello lub za pośrednictwem planów usługi hello usługi Office 365.

Połączenia programów RemoteApp obsługuje aktywacji udostępnionego komputera w programie Office 365. Po włączeniu udostępnionych aktywacji komputera i użyj hello [narzędzia wdrażania pakietu Office](http://www.microsoft.com/download/details.aspx?id=36778) w przypadku instalacji usługi Office 365 ProPlus instaluje bez aktywowane. Gdy loguje użytkownika do kolekcji zawierającej usługi Office 365, Office sprawdza toosee, zainicjowano hello użytkownika dla usługi Office 365 ProPlus. Jeśli tak, Office tymczasowo aktywuje usługi Office 365 ProPlus — Aktywacja utrzymuje się do tego użytkownicy znaki poza hello usługi.

toouse aktywacji udostępnionego komputera w programie Office 365, należy toocreate [szablonu niestandardowego](remoteapp-create-custom-image.md) i zainstaluj usługi Office 365 ProPlus, wykonując [te kierunkach](https://technet.microsoft.com/library/dn782858.aspx).

Możesz zarządzać użytkowników usługi Office 365 licencji na powitania [portalu administratora usługi Office 365](https://portal.office365.com/). Przeczytaj więcej informacji na temat [plany usługi Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus w wersji próbnej
Podczas z 30-dniowej wersji próbnej usługi RemoteApp można użyć hello Office 2013 Professional Plus (wersja próbna) szablonu obrazu toocreate kolekcji usługi RemoteApp. Można przypisać toothis użytkowników wersji próbnej kolekcji przy użyciu ich konta roboczych usługi Azure Active Directory lub konta Microsoft. Brak dodatkowych subskrypcji jest wymagana.

To jest testowany hello tookick doskonałe rozwiązanie i uzyskać dobrą wrażenie dla pakietu Office w usłudze RemoteApp. Jednak ta opcja jest przeznaczone do oceny i testowania tylko. Utworzone przy użyciu obrazu szablonu pakietu Office 2013 Professional Plus (wersja próbna) hello kolekcji usługi RemoteApp nie może być tryb tooproduction wykonano przejście i zostanie wyłączona po hello koniec okresu próbnego hello.

## <a name="switching-from-trial-tooproduction"></a>Zmiana typu zapytania z wersji próbnej tooproduction
Po uruchomieniu z 30-dniowej bezpłatnej wersji próbnej notatki w hello RemoteApp części portalu hello informuje o ile masz jeszcze w wersji próbnej hello przed tooa tootransition płatnej konta. Może aktywować konto i Przełącz tryb tooproduction za pomocą hello łącza w tej uwagi.

Po uaktywnieniu konta to będzie miało wpływ na wszystkich kolekcji usługi RemoteApp hello na Twoim koncie.

* Kolekcje, których są uruchomione hello systemu Windows Server 2012 R2 lub obrazy szablonów usługi Office 365 ProPlus hello przejdą tooproduction bezproblemowo. Wszystkie dane użytkownika i ustawień, takich jak bieżące sesje pozostają niezmienione.
* Jeśli zostały przekazane obrazy szablonów niestandardowych, kolekcji przy użyciu tych obrazów również przejdą bezproblemowo.
* obraz szablonu pakietu Office 2013 Professional Plus (wersja próbna) Hello jest przeznaczone do oceny tylko. Kolekcje z tego obrazu szablonu nie może być tooproduction wykonano przejście. Umieści w stanie "wyłączone".

Jeśli tryb tooproduction nie przejście przez hello wygaśnięciem okresu próbnego, kolekcji usługi RemoteApp zostanie wyłączone. Nie martw się — ustawienia i dane użytkowników są zapisywane dla innej 90 dni, więc nadal może aktywować tryb tooproduction usługi i przełącznika bez utraty danych.

