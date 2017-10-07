---
title: "Licencjonowanie usługi RemoteApp aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działa licencjonowanie w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Jak działa licencjonowanie w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Umożliwiające został skonfigurowany z usługą Azure RemoteApp, utworzono szablony i są gotowe toopublish aplikacji tooyour użytkowników. Występuje nadal jeden ostatniego toofigure operacją limit: licencjonowania. Podobnie jak działa Licencjonowanie usługi RemoteApp i aplikacji hello udostępnianych za pośrednictwem usługi RemoteApp?

Usługa RemoteApp nie wymaga licencji dostępowych systemu Windows ani pulpitu zdalnego. Subskrypcja zapewnia obsługę powitania po stronie usługi RemoteApp, sam. (Zobacz szczegóły hello hello [planów cenowych](https://azure.microsoft.com/pricing/details/remoteapp).)

Jeśli używasz jednego z obrazów hello, które jest zawarte w ramach subskrypcji, można udostępnić dowolne aplikacji hello zainstalowane w tym obrazie bez konieczności posiadania oddzielnej licencji. Na przykład jeśli używasz toobuild obrazu szablonu systemu Windows Server 2012 R2 hello kolekcji, można udostępniać System Center Endpoint Protection użytkownikom. Witaj tylko wyjątki toothis reguły są usługi Office 365 ProPlus, która wymaga oddzielnej subskrypcji, i Office 2013, którego nie można udostępniać w kolekcji dla środowiska produkcyjnego.

Jeśli chcesz obrazu szablonu usługi Office 365 hello toouse dołączanego do usługi RemoteApp musi mieć *istniejących* plan usługi Office 365 ProPlus. Witaj, który sam ma wartość true dla wszystkich aplikacji usługi Office 365 publikowania za pomocą szablonu niestandardowego. Należy tooactivate hello aplikacji przy użyciu posiadanej subskrypcji. Dotyczy to zarówno wersji próbnych, jak i subskrypcji płatnych. Jeśli chcesz obrazu szablonu usługi Office 365 hello toouse okresie próbnym hello *i nie masz już subskrypcję*, przejdź toohello usługi Office 365 za[Zarejestruj](https://go.microsoft.com/fwlink/p/?LinkID=403802) dla subskrypcji wersji próbnej. Aby znaleźć więcej informacji, zobacz temat [Jak programy pakietu Office współpracują z usługą RemoteApp?](remoteapp-o365.md).

Jeśli podczas okresu próbnego hello, nie ma subskrypcji wersji próbnej tooget usługi Office 365, należy użyć obrazu szablonu pakietu Office 2013 Professional Plus hello dołączanego do usługi RemoteApp. Ten obraz szablonu może być używany tylko przez 30 dni i nie można go konwertować na kolekcję płatną.

W przypadku innych aplikacji należy upewnić się, że aplikacja hello tooshare licencji hello toomake.

Ma to sens, prawda? Możesz opublikować dowolną aplikację, że są uprawnieni legalnie tooshare. I trzeba się, że są naprawdę toomake prawo tooshare programy.

Należy pamiętać, że w przypadku kolekcji w chmurze nie można użyć umowy licencji zbiorczej ani licencji dostępowej. Możesz *można* korzystają z aplikacji tooactivate umowy licencjonowania zbiorowego w kolekcji hybrydowej (z wyjątkiem pakietu Office). Wystarczy tooinstall je w szablonie obraz z hello nośnika licencji zbiorczej. Wykonaj hello informacji z licencji tooinstall dostawcy aplikacji hello w środowisku pulpitu zdalnego.

