---
title: "wprowadzenie do usługi Azure AD Privileged Identity Management aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage uprzywilejowany tożsamości z hello aplikacji usługi Azure Active Directory Privileged Identity Management w portalu Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Rozpoczynanie używania aplikacji Azure AD Privileged Identity Management
Aplikacja Azure Active Directory (AD) Privileged Identity Management umożliwia kontrolę i monitorowanie dostępu, a także zarządzanie nim w ramach danej organizacji. Ten zakres obejmuje tooresources dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.

W tym artykule wyjaśniono, jak tooadd hello tooyour aplikacji Azure AD PIM pulpitu nawigacyjnego portalu Azure.

## <a name="add-hello-privileged-identity-management-application"></a>Dodawanie aplikacji Privileged Identity Management hello
Przed użyciem usługi Azure AD Privileged Identity Management należy tooyour aplikacji hello tooadd pulpitu nawigacyjnego portalu Azure.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) jako administrator globalny katalogu.
2. Jeśli Twoja organizacja ma więcej niż jeden katalog, w hello prawym górnym rogu hello portalu Azure wybierz nazwy użytkownika. Wybierz katalog hello miejscu toouse PIM.
3. Wybierz **więcej usług** i użyj hello filtru pole tekstowe toosearch dla **Azure AD Privileged Identity Management**.
4. Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**. Otwiera Hello aplikacji Privileged Identity Management.

Jeśli jest hello toouse pierwszą osobą Azure AD Privileged Identity Management w katalogu, są automatycznie przypisywane hello **administrator zabezpieczeń** i **administrator ról uprzywilejowanych** ról w katalogu hello. Tylko administratorzy ról uprzywilejowanych mogą zarządzać przypisaniami ról użytkowników. Ponadto można wybrać toorun hello [Kreator zabezpieczeń.](active-directory-privileged-identity-management-security-wizard.md) który przeprowadzi Cię przez hello początkowej obsługi wykrywania i przypisania.

## <a name="navigate-tooyour-tasks"></a>Przejdź tooyour zadań
Po skonfigurowaniu usługi Azure AD Privileged Identity Management, zobacz blok nawigacji hello przy każdym otwarciu aplikacji hello. Użyj tego bloku tooaccomplish zadania związane z zarządzaniem tożsamościami.

![Zrzut ekranu przedstawiający zadania najwyższego poziomu dla aplikacji PIM](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Moje ról** przejście tooa listę ról, które są przypisane tooyou. W tej sekcji będzie można aktywować wszystkie role, które danemu użytkownikowi przysługują.
* Opcja **Zatwierdzanie żądań (wersja zapoznawcza)** powoduje wyświetlenie listy oczekujących żądań aktywacji od użytkowników w katalogu. [Dowiedz się więcej.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **Oczekujące żądania (wersja zapoznawcza)** Wyświetla wszystkie bieżące tooactivate toohave wprowadzone żądania.
* **Przejrzyj dostępu** ma tooany oczekujących dostępu przegląda konieczność toocomplete, czy recenzowania dostępu dla użytkownika lub kogoś innego.
* **Role katalogu usługi Azure AD** znajduje się w sekcji "Zarządzaj" hello jest pulpit nawigacyjny hello przypisań ról toomanage Administratorzy ról uprzywilejowanych, Zmień ustawienia aktywacji roli, recenzje dostępu start i. Opcje Hello na tym pulpicie nawigacyjnym są wyłączone dla każdego, kto nie jest administratorem ról uprzywilejowanych.

## <a name="next-steps"></a>Następne kroki
Witaj [Omówienie usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) zawiera więcej informacji na temat sposobu zarządzania dostępem administracyjnym w organizacji.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
