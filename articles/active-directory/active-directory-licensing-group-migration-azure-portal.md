---
title: "toomigrate aaaHow Twojego tooa poszczególnych licencjonowani użytkownicy grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooswitch z indywidualnego użytkownika licencje na podstawie toogroup licencjonowania przy użyciu usługi Azure Active Directory"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Jak tooadd licencjonowana grupy Użytkownicy tooa licencjonowania w usłudze Azure Active Directory

Masz istniejących toousers licencji wdrożone w organizacjach hello za pośrednictwem "bezpośredniego przypisania"; oznacza to za pomocą skryptów programu PowerShell lub innych narzędzi tooassign użytkownika licencji. Jeśli chcesz toostart przy użyciu oparte na grupach licencji toomanage licencjonowania w organizacji, konieczne będzie przeprowadzenie migracji planu tooseamlessly zastąpić istniejące rozwiązania oparte na grupach licencji.

Hello najważniejszy element tookeep pamiętać jest, że należy unikać sytuacji, w którym licencjonowania na podstawie toogroup Migrowanie spowoduje użytkownicy tymczasowo utraty ich aktualnie przypisane licencje. Każdy proces, który może spowodować usunięcie licencji należy unikać tooremove hello ryzyko utraty dostępu tooservices i ich danych.

## <a name="recommended-migration-process"></a>Proces migracji zalecane

1. Masz istniejącej automatyzacji (na przykład programu PowerShell), zarządzanie przypisania licencji i usuwania dla użytkowników. Usługa będzie działać, ponieważ jest.

2. Utwórz nową grupę licencji (lub zdecydować, które istniejących grup toouse) i upewnij się, czy wszystkie wymagane użytkownicy zostaną dodane jako członkowie.

3. Przypisywanie licencji hello wymaganych grup toothose; Celem powinno być tooreflect hello samej licencyjnymi z istniejącej automatyzacji (na przykład programu PowerShell) jest stosowanie toothose użytkowników.

4. Upewnij się, że licencje zostały zastosowane tooall użytkownicy w tych grupach. Można to zrobić, sprawdzając stan przetwarzania hello w każdej grupie oraz przez sprawdzanie dzienników inspekcji.

  - Patrząc na ich szczegóły licencji można kontroli poszczególnych użytkowników. Aby mieć hello samej licencji przypisanych "bezpośrednio" i "odziedziczony" zostanie wyświetlony z grup.

  - Należy uruchomić skrypt programu PowerShell za[Sprawdź sposób przypisywania licencji toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Hello tego samego produktu licencji jest przypisany użytkownik toohello bezpośrednio i za pośrednictwem grupy, tylko jedna licencja jest używane przez użytkownika hello. Dlatego żadne dodatkowe licencje nie są wymagane tooperform migracji.

5. Upewnij się, że nie przypisań licencji nie sprawdzając każdej grupy użytkowników w stanie błędu. Aby uzyskać więcej informacji, zobacz [zidentyfikowanie i rozwiązywaniu problemów z licencji dla grupy](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Rozważ usunięcie oryginalnego przypisania bezpośredniego hello; może być toodo najpierw go stopniowo etapami"", toomonitor hello wyników na podzestaw użytkowników.

  Można pozostanie hello oryginalnych przypisań bezpośrednio na użytkowników, ale podczas hello użytkownicy opuszczają ich grup licencji, które nadal zachowa oryginalnej licencji hello, który jest prawdopodobnie nie mają, które chcesz.

## <a name="an-example"></a>Przykład

Mamy organizacji z 1000 użytkowników. Wszyscy użytkownicy wymagają Enterprise Mobility + Security (EMS) licencji. 200 użytkowników znajdują się w hello działu finansowego i wymagają licencji Office 365 Enterprise E3. Mamy uruchomiony lokalnie, dodawanie i usuwanie licencji od użytkowników, jak długo będą pochodzić i przejdź skryptów środowiska PowerShell. Chcemy tooreplace hello skryptu na podstawie grupy licencji, licencje są zarządzane automatycznie przez usługę Azure AD.

Oto, jakie hello proces migracji może wyglądać:

1. Przy użyciu hello Przypisz portalu Azure hello EMS licencji toohello **wszyscy użytkownicy** grupy w usłudze Azure AD. Przypisz hello E3 licencji toohello **działu finansowego** grupy zawierającej wszystkich użytkowników hello wymagane.

2. Dla każdej grupy upewnij się, że przypisanie licencji zostało zakończone dla wszystkich użytkowników. Przejdź toohello bloku dla każdej grupy, wybierz opcję **licencji**i sprawdzić stan przetwarzania hello u góry hello hello **licencji** bloku.

  - Szukaj dla "najnowsze zmiany licencji zostały zastosowane tooall użytkowników" tooconfirm przetwarzanie zostało zakończone.

  - Poszukaj powiadomienia w górnej części o wszyscy użytkownicy, dla których licencji mogą nie zostały pomyślnie przypisane. Czy możemy zabraknie licencji dla niektórych użytkowników? W przypadku niektórych użytkowników, czy mają powodujące konflikt licencji jednostki magazynowe, które uniemożliwiają dziedziczenie grupy licencji?

3. Miejsce Sprawdź tooverify niektórych użytkowników, których mają zarówno hello bezpośredniego, jak i grupy licencji zastosowane. Przejdź toohello bloku dla użytkownika, zaznacz **licencji**i sprawdź, czy stan hello licencji.

  - Jest to hello oczekiwano stanu użytkownika podczas migracji:

      ![Stan użytkownika oczekiwany](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Potwierdza to, które użytkownik hello ma zarówno bezpośrednie i dziedziczonych licencji. Firma Microsoft wyświetlana zarówno **EMS** i **E3** są przypisane.

  - Wybierz szczegóły każdego tooshow licencji usług hello włączone. Może to być toocheck używane, jeśli hello bezpośredniego i grupy licencji Włącz hello dokładnie tego samego planów usługi dla użytkownika hello.

      ![Sprawdź planów usługi](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Po potwierdzeniu, że zarówno bezpośrednio, jak i grupy licencji są równoważne, można uruchomić, usunięcie licencji bezpośrednio od użytkowników. Można to sprawdzić, usuwając je dla poszczególnych użytkowników w portalu hello, a następnie uruchom toohave skryptów automatyzacji, usunąć je masowo. Oto przykład tego samego użytkownika z licencjami bezpośredniego hello usunięte za pośrednictwem portalu hello hello. Zwróć uwagę, stan licencji hello pozostaje bez zmian, że firma Microsoft nie jest już wyświetlana bezpośredniego przypisania.

  ![bezpośrednie licencje usunięte](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Następne kroki

więcej informacji na temat innych scenariuszy zarządzania licencji za pomocą grup, odczytać toolearn

* [Przypisywanie licencji tooa grupy w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identyfikowanie i rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze](active-directory-licensing-group-advanced.md)
