---
title: "aaaHow tooremove użytkownikowi na dostęp do aplikacji tooan | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu tooremove użytkownika dostępu tooan aplikacji"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Jak tooremove użytkownikowi uzyskiwanie dostępu do aplikacji tooan

W tym artykule pomóc toounderstand jak tooremove użytkownika dostępu tooan aplikacji.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Chcę tooremove określonego użytkownika lub grupy aplikacji tooan przypisania

tooremove użytkownika lub grupę przypisania tooan aplikację, wykonaj kroki hello na liście hello [Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artykułu.

. ## Ma toodisable wszystkich aplikacji tooan dostępu dla każdego użytkownika

toodisable wszystkie użytkownika logowania tooan aplikacji, wykonaj kroki hello na liście hello [wyłączyć logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artykułu.

## <a name="i-want-toodelete-an-application-entirely"></a>Chcę całkowicie toodelete aplikacji

zbyt**usunąć aplikację**, postępuj zgodnie z poniższymi instrukcjami hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

   * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma toodelete.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **usunąć** ikony z aplikacji top hello **omówienie** bloku.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Chcę toodisable wszystkie przyszłe użytkownika zgody operacji tooany aplikacji

Wyłączanie zgody użytkownika dla użytkowników końcowych z aplikacji tooany zgodę zapobiec całego katalogu. Administratorzy mogą nadal oznacza zgodę na behalves użytkownika. zgoda toolearn więcej informacji na temat aplikacji, oraz dlaczego może lub nie możesz toodo tego odczytu [zgody administratora i użytkownika opis](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

zbyt**Wyłącz wszystkie operacje zgody użytkownika w przyszłości w katalogu cały**, postępuj zgodnie z poniższymi instrukcjami hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **ustawienia użytkownika**.

6.  Wyłącz wszystkie operacje zgody użytkownika w przyszłości przez ustawienie hello **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku.


# <a name="next-steps"></a>Następne kroki
[Zarządzanie tooapps dostępu](active-directory-managing-access-to-apps.md)
