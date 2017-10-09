---
title: "aaaWhat jest hello zawierają obrazy szablonów usługi Azure RemoteApp? | Microsoft Docs"
description: "Więcej informacji na temat hello obrazów szablonów dołączonych do usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Co to jest hello zawierają obrazy szablonów usługi Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Subskrypcja usługi Azure RemoteApp obejmuje trzy obrazy szablonów:

* Windows Server 2012
* Microsoft Office 365 ProPlus (wymagana jest subskrypcja usługi Office 365)
* Microsoft Office 2013 Professional Plus (tylko wersja próbna)

> [!IMPORTANT]
> Subskrypcja usługi Azure RemoteApp daje dostęp toohello oprogramowania w obrazach hello, z wyjątkiem hello usługi Office 365 ProPlus, która wymaga oddzielnej subskrypcji, i Office 2013, którego nie można używać w środowisku produkcyjnym. Oznacza to, że można udostępniać programy hello lub aplikacji na powitania obrazy szablonów użytkowników. Na przykład utworzyć kolekcję, która używa obrazu systemu Windows Server 2012 R2 hello, można opublikować programu System Center Endpoint Protection dla użytkowników tooaccess za pośrednictwem usługi RemoteApp.
> 
> Zapoznaj się z hello [szczegółowe informacje o licencjonowaniu usługi RemoteApp](remoteapp-licensing.md) Aby uzyskać więcej informacji. I [korzystanie z pakietu Office z usługą Azure RemoteApp](remoteapp-o365.md) dla hello informacji licencjonowania pakietu Office.
> 
> 

Poniżej podano szczegółowe informacje o zawartości każdego obrazu.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("Witaj obraz podstawowy)
Ten obraz jest oparty na system operacyjny Microsoft Windows Server 2012 R2 Datacenter i hello następujące role i funkcje zainstalował toomeet hello wymagania dotyczące obrazów szablonów usługi Azure RemoteApp:

* .NET Framework 4.5, 3.5.1, 3.5
* Środowisko pulpitu
* Usługi dotyczące pisma ręcznego i odręcznego
* Platforma Media Foundation
* Host sesji usług pulpitu zdalnego
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Obsługa środowiska WoW64

Ten obraz zawiera także hello następujące aplikacje zainstalowane:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (wymagana jest subskrypcja)
Usługi Office 365 jest hello najbardziej pożądaną aplikacją, dlatego utworzyliśmy "niestandardowy" obraz dla Ciebie toowork z.

Ten obraz jest rozszerzeniem obrazu podstawowego hello i ma hello zainstalowane następujące składniki programu Microsoft Office 365 ProPlus oprócz składników toohello zawartych w obrazie systemu Windows Server 2012 R2 hello:

* Dostęp
* Excel
* Lync
* OneNote
* OneDrive dla firm (należy pamiętać, że agent synchronizacji hello nie jest obsługiwane do użycia z usługą Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Narzędzia sprawdzające pakietu Office

Obraz powitania obejmuje również Visio Pro i Project Pro.

I aplikacji, jak również następujące hello:

* SQL Native Client
* Sterownik ODBC
* SQL Server Data Mining Client
* MasterDataServices Client
* Microsoft Publisher
* PowerQuery
* PowerMap

Pełna funkcjonalność aplikacji usługi Office 365 ProPlus jest dostępna tylko dla użytkowników, którzy posiadają plan usługi Office 365 ProPlus. Więcej informacji o subskrypcji usługi Office 365 hello planów dla [plany usługi Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Nadal masz pytania? Zapoznaj się z hello [usługi Office 365 + usługa RemoteApp](remoteapp-o365.md) informacji. Zobacz także nowy artykuł hello [jak toouse subskrypcji usługi Office 365 z usługą Azure RemoteApp](remoteapp-officesubscription.md).

Należy pamiętać, że należy oddzielnie toolicense usługi Office 365 ProPlus, programu Visio Pro i Project Pro — każdy z nich ma własny licencji.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (tylko wersja próbna)
Podczas hello bezpłatnym okresie próbnym można testować usługi hello z obrazem hello pakietu Office 2013.

Ten obraz jest rozszerzeniem obrazu podstawowego hello i ma hello zainstalowane następujące składniki programu Microsoft Office 2013 Professional Plus oprócz składników toohello zawartych w obrazie systemu Windows Server 2012 R2 hello:

* Dostęp
* Excel
* Lync
* OneNote
* OneDrive dla firm (należy pamiętać, że agent synchronizacji hello nie jest obsługiwane do użycia z usługą Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Narzędzia sprawdzające pakietu Office

> [!IMPORTANT]
> **Informacje prawne:** ten obraz nie zawiera licencji pakietu Microsoft Office i *nie może być używany w środowisku produkcyjnym*. Obraz pakietu Office 2013 Professional Plus Hello jest przeznaczony tylko do użycia próbnego. Jeśli chcesz toouse aplikacje pakietu Office w usłudze Azure RemoteApp w środowisku produkcyjnym należy obrazu usługi Office 365 ProPlus hello toouse. Aby uzyskać więcej szczegółowych informacji na temat licencjonowania usługi Office, zobacz temat [Korzystanie z usługi Office 365 z usługą Azure RemoteApp](remoteapp-o365.md)
> 
> 

