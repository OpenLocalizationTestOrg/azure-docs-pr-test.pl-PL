---
title: "aaaHow toouse usługi Azure RemoteApp z kontami użytkowników usługi Office 365 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Azure RemoteApp z kont użytkowników usługi Office 365"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Jak toouse usługi Azure RemoteApp z kontami użytkowników usługi Office 365
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Jeśli masz subskrypcję usługi Office 365, Azure usługa Active Directory przechowującym nazwy użytkownika i hasła używane tooaccess usługi Office 365. Na przykład gdy użytkownicy aktywują usługi Office 365 ProPlus one uwierzytelniania usługi Azure AD toocheck licencje. Większość klientów może jak toouse hello sam katalogu z usługą Azure RemoteApp.

Jeśli wdrażana jest usługa Azure RemoteApp są najprawdopodobniej przy użyciu subskrypcji platformy Azure, która jest skojarzona z inną usługą Azure AD. W kolejności toouse katalogu usługi Office 365, konieczne będzie toomove hello subskrypcji platformy Azure do tego katalogu.

Aby uzyskać informacje na temat aplikacji klienckich toodeploy usługi Office 365, zobacz [jak toouse subskrypcji usługi Office 365 z usługą Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Faza 1: Zarejestruj bezpłatna subskrypcja usługi Office 365 Azure Active Directory
Jeśli używasz hello klasycznego portalu Azure, wykonaj kroki hello w [zarejestrować bezpłatna subskrypcja usługi Azure Active Directory](https://technet.microsoft.com/library/dn832618.aspx) tooget tooyour dostęp administracyjny usługi Azure AD za pomocą hello portalu zarządzania Azure. Hello wyniku tego procesu możesz powinny być możliwe toolog do hello portalu Azure i katalogu istnieje — w tym momencie nie zobaczysz bardziej ponieważ hello pełnej subskrypcja platformy Azure są używane z usługą Azure RemoteApp jest w innym katalogu.

Zapamiętaj hello nazwę i hasło konta administratora hello utworzone w tym kroku — będą one potrzebne w fazy 2.

Jeśli używasz hello portalu Azure, zapoznaj się [jak tooregister i Aktywuj bezpłatnej usługi Azure Active Directory przy użyciu portalu usługi Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Faza 2: Hello zmiany usługi Azure AD skojarzone z subskrypcją platformy Azure.
Zamierzamy toochange subskrypcji platformy Azure z jego bieżącym katalogu do katalogu usługi Office 365 hello możemy działał z fazy 1.

Postępuj zgodnie z instrukcjami hello opisane w [dzierżawy usługi Azure Active Directory hello zmiany w usłudze Azure RemoteApp](remoteapp-changetenant.md). Należy zwrócić szczególną uwagę toohello następujące kroki:

* Krok #1: Jeśli usługi Azure RemoteApp (ARA) zostały wdrożone w ramach tej subskrypcji, upewnij się, że usunięciu wszystkich kont użytkowników usługi Azure AD z wszystkie kolekcje ARA najpierw, przed podjęciem próby inaczej. Alternatywnie można rozważyć usunięcie wszelkich istniejących zbiorach.
* Krok #2: Jest to krok krytyczne. Należy toouse konta Microsoft (np. @outlook.com) jako administratora usługi dla subskrypcji hello; wynika to z faktu, firma Microsoft nie może mieć żadnych kont użytkowników z istniejących subskrypcji toohello usługi Azure AD dołączony — w przypadku hello nie będziemy mogli toomove go tooa różne usługi Azure AD.
* Krok #4: Dodając istniejącym katalogiem, hello system wyświetli monit toosign się przy użyciu konta administratora powitania dla tego katalogu. Upewnij się, że konto administratora hello toouse z fazy 1.
* Krok #5: Zmień katalog nadrzędny hello hello subskrypcji usługi Office 365 tooyour katalogu. wynik końcowy Hello należy, że w obszarze Ustawienia -> Subskrypcje subskrypcji wymieniono katalogu hello usługi Office 365. 
  ![Zmień katalog nadrzędny hello hello subskrypcji](./media/remoteapp-o365user/settings.png)

W tym momencie subskrypcję usługi Azure RemoteApp jest skojarzony z pakietu Office 365, Azure AD; Możesz użyć hello istniejących kont użytkowników usługi Office 365 z usługą Azure RemoteApp!

