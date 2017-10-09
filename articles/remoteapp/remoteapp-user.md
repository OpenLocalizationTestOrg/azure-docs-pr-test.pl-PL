---
title: "aaaAdd tooyour użytkownika kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd użytkowników tooyour kolekcji usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a>Jak tooadd tooyour użytkownika kolekcji usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Zanim użytkownicy mogą zobaczyć i użyć aplikacji w usłudze Azure RemoteApp, należy je uzyskać dostępu do kolekcji tooyour toogrant. To jest część łatwe hello: na powitania **dostępu użytkownika** , wprowadź informacje o koncie hello hello użytkownika, a następnie kliknij znacznik wyboru hello.

Jakie informacje o koncie potrzebujesz? Witaj typ kolekcji to zależy od utworzonego (w chmurze czy hybrydowa) i określa, czy używasz usługi Office 365 ProPlus w tej kolekcji.

## <a name="supported-user-identities"></a>Tożsamości użytkowników obsługiwanych
typy kolekcji różnych Hello (w chmurze i hybrydowa) obsługuje tooapplications dostępu przy użyciu tożsamości innego użytkownika.  

Dla kolekcji hybrydowej RemoteApp możesz muszą tooset się infrastruktury domeny usługi Active Directory, lokalne i dzierżawy usługi Azure Active Directory o integracji katalogów (i opcjonalnie logowanie jednokrotne). Ponadto należy toocreate niektóre obiekty usługi Active Directory w katalogu lokalnym hello.  

Dla kolekcji usługi RemoteApp w chmurze każdy użytkownik, który ma obsługiwać tożsamości usługi Azure Active Directory może zostać przydzielony tooinclude tooRemoteApp dostępu użytkownika Accounts firmy Microsoft.  Zobacz hello w poniższej tabeli.

Użytkownicy usługi Office 365 korzystają z usługi Azure Active Directory. Jeśli dysponują hybrydowe usługi Azure Active Directory, katalog zsynchronizowany kont, ich może otrzymać dostępu użytkowników w ramach wdrożenia hybrydowego usługi RemoteApp.   

Korzystając z tej tabeli, jako odwołanie szybki, dla której tożsamość jest obsługiwana w kolekcji i jakie są wymagania dotyczące usługi Active Directory hello.

| Konta użytkowników | Chmura | Połączenie hybrydowe |
| --- | --- | --- |
| Konto Microsoft |Tak |Nie |
| Azure Active Directory (Azure AD) | | |
| Azure AD cloud |Tak |Nie |
| Synchronizacja z synchronizacją haseł |Tak |Tak |
| ADsync bez synchronizacji haseł |Tak |Nie |
| Synchronizacja z usługami AD FS |Tak |Tak |
| [Azure 3rd firm obsługiwanych dostawców tożsamości](https://msdn.microsoft.com/library/azure/jj679342.aspx) (przykład Ping) |Tak |Tak |
| Multi-Factor Authentication |Tak |Tak |

Zapoznaj się z [więcej informacji](remoteapp-ad.md) o konfigurowaniu usługi Active Directory do usługi RemoteApp.

> [!NOTE]
> Hello użytkowników usługi Azure Active Directory muszą pochodzić z dzierżawy hello, który został skojarzony z subskrypcją. (Można wyświetlać i modyfikować subskrypcji na powitania **ustawienia** kartę w portalu hello. Zobacz [dzierżawy usługi Azure Active Directory hello zmiany używanej przez usługę RemoteApp](remoteapp-changetenant.md) Aby uzyskać więcej informacji.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Informacje o koncie usługi Office 365 ProPlus użytkownika
Jeśli używasz obrazu szablonu usługi Office 365 ProPlus hello w kolekcji *lub* Jeśli utworzony niestandardowy obraz, który korzysta z usługi Office 365 są dozwolone tylko tooadd usługi Azure Active Directory użytkowników, którzy mają subskrypcji usługi Office 365 dla hello Domyślna domena Twojej subskrypcji. Zobacz [przy użyciu usługi Office 365 z usługą Azure RemoteApp](remoteapp-o365.md) Aby uzyskać więcej informacji.

