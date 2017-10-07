---
title: "Rozwiązywanie problemów: Element usługi Active Directory jest lub jest ona niedostępna | Dokumentacja firmy Microsoft"
description: "Toodo gdy element menu usługi Active Directory nie jest wyświetlane w portalu zarządzania Azure hello."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Rozwiązywanie problemów: Element usługi Active Directory jest lub jest niedostępna
Wiele hello instrukcje dotyczące korzystania z funkcji usługi Azure Active Directory i usług rozpoczynać się od "Przejdź toohello portalu zarządzania Azure i kliknij polecenie **usługi Active Directory**." Ale co zrobić, jeśli nie ma elementu menu lub rozszerzenie usługi Active Directory hello lub jest on oznaczony **nie jest dostępny**? Ten temat jest zaprojektowana toohelp. Opisuje warunki hello, w którym **usługi Active Directory** nie pojawia się lub jest niedostępna i wyjaśniono, jak tooproceed.

## <a name="active-directory-is-missing"></a>Brak usługi Active Directory
Zazwyczaj **usługi Active Directory** element będzie wyświetlany w menu nawigacji po lewej stronie powitania. Hello instrukcjami procedury usługi Azure Active Directory założono, że ten element jest w danym widoku.

![Zrzut ekranu: usługi Active Directory na platformie Azure](./media/active-directory-troubleshooting/typical-view.png)

Witaj usługi Active Directory element będzie wyświetlany w menu nawigacji po lewej stronie powitania, gdy spełniony jest dowolny z hello następujące warunki. W przeciwnym razie nie ma elementu hello.

* bieżący użytkownik Hello zalogować się przy użyciu konta Microsoft (znanego wcześniej jako identyfikator Windows Live ID).
  
    LUB
* Witaj dzierżawą platformy Azure ma katalogu i hello bieżącego konta administratora katalogu.
  
    LUB
* Hello dzierżawy Azure ma co najmniej jedną przestrzeń nazw kontroli dostępu usługi Azure AD (ACS). Aby uzyskać więcej informacji, zobacz [Namespace kontroli dostępu](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    LUB
* Witaj dzierżawy Azure ma co najmniej jednego dostawcę usługi Azure Multi-Factor Authentication. Aby uzyskać więcej informacji, zobacz [administrowanie dostawców uwierzytelniania wieloskładnikowego Azure](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate kontroli dostępu przestrzeni nazw lub dostawcę usługi Multi-Factor Authentication kliknij **+ nowy** > **usługi aplikacji** > **usługi Active Directory**.

tooget prawa administracyjne tooa katalogu, ma administrator przypisać administrator konta tooyour roli. Aby uzyskać więcej informacji, zobacz [przypisywanie ról administratorów](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory nie jest dostępna
Po kliknięciu **+ nowy** > **usługi aplikacji**, **usługi Active Directory** element będzie wyświetlany. W szczególności hello usługi Active Directory element jest wyświetlany, gdy hello funkcji usługi Active Directory, takich jak katalog, kontroli dostępu lub Dostawca uwierzytelniania MFA, są dostępne toohello bieżącego użytkownika.

Jednak podczas ładowania strony hello elementu hello jest przyciemnione i jest oznaczony jako **nie jest dostępny**. Jest to stan przejściowy. Jeśli Poczekaj kilka sekund, hello element staje się dostępna. Jeśli opóźnienie hello zostanie przedłużony, odświeżanie strony sieci web hello często rozwiązuje hello problem.

![Zrzut ekranu: Active Directory nie jest dostępna](./media/active-directory-troubleshooting/not-available.png)

