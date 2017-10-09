---
title: "aaaAssign licencji tooa grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooassign licencje toousers za pomocą usługi Azure Active Directory grupy licencji"
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
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Przypisz licencje toousers przez członkostwo w grupie w usłudze Azure Active Directory

W tym artykule przedstawiono sposób przypisywania produktu licencji tooa grupy użytkowników w usłudze Azure Active Directory (Azure AD), a następnie sprawdź, czy są one prawidłowo licencjonowane.

W tym przykładzie dzierżawcy hello zawiera grupę zabezpieczeń o nazwie **zarządzania zasobami Ludzkimi stosują**. Do tej grupy należą wszyscy członkowie działu kadr hello (około 1000 użytkowników). Chcesz, aby dział cały toohello licencji tooassign Office 365 Enterprise E3. Hello usługi Yammer przedsiębiorstwa, która jest zawarta w produkcie hello musi tymczasowo wyłączone, aż do działu hello jest gotowy toostart przy jej użyciu. Należy także toodeploy pakietu Enterprise Mobility + Security licencji toohello tej samej grupy użytkowników.

> [!NOTE]
> Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Przed tooa użytkownika można przypisać licencji, hello administrator ma właściwość location użycia hello toospecify hello użytkownika.

> Przypisywaniu licencji grupy użytkowników bez użycia lokalizacji określonej będzie dziedziczyć hello lokalizację katalogu hello. Jeśli użytkownicy w wielu lokalizacjach, zaleca się zawsze ustawienie lokalizacji użytkowania jako część programu przepływu tworzenia użytkownika w usłudze Azure AD (np. za pomocą AAD Connect) -, który zapewni hello wynik przypisania licencji zawsze jest poprawna i użytkownicy nie będą odbierać usługi w lokalizacjach, które nie są dozwolone.

## <a name="step-1-assign-hello-required-licenses"></a>Krok 1: Przypisywanie licencji hello wymagane

1. Zaloguj się toohello [ **portalu Azure** ](https://portal.azure.com) przy użyciu konta administratora. licencje toomanage, hello konta musi być kontem administratora konta administratora globalnego, jak rolę lub użytkownika.

2. Wybierz **więcej usług** w lewym okienku nawigacji hello, a następnie wybierz **usługi Azure Active Directory**. Można dodać tego bloku tooFavorites lub przypiąć go toohello pulpitu nawigacyjnego portalu.

3. Na powitania **usługi Azure Active Directory** bloku, wybierz opcję **licencji**. Spowoduje to otwarcie bloku, w którym możesz wyświetlić i zarządzać wszystkich produktów objętego w dzierżawie powitalnych.

4. W obszarze **wszystkich produktów**, wybierz Office 365 Enterprise E3 i Enterprise Mobility + Security wybierając hello nazwy produktu. Przypisanie hello toostart, wybierz opcję **przypisać** u góry bloku hello hello.

   ![Wszystkie produkty, przypisywanie licencji](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Na powitania **przypisanie licencji** bloku, kliknij przycisk **użytkowników i grup** tooopen hello **użytkowników i grup** bloku. Wyszukiwanie nazwy grupy hello *zarządzania zasobami Ludzkimi stosują*, wybierz grupę hello i będzie się tooconfirm klikając **wybierz** u dołu hello hello bloku.

   ![Wybierz grupę](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Na powitania **przypisanie licencji** bloku, kliknij przycisk **opcje przydziału (opcjonalnie)**, który zawiera wszystkie plany usługi uwzględnione w hello dwóch produktów, które wcześniej wybrano. Znajdź **usługi Yammer Enterprise** i włączyć ją **poza** toodisable, że usługi od licencji produktu hello. Upewnij się, klikając **OK** u dołu hello **opcje przydziału**.

   ![Opcje przydziału](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. przypisania hello toocomplete na powitania **przypisanie licencji** bloku, kliknij przycisk **przypisać** u dołu hello hello bloku.

8. W hello prawym górnym rogu pokazujący stan hello i wynik hello procesu zostanie wyświetlone powiadomienie. Jeśli hello przypisania toohello grupy nie można ukończyć (na przykład ze względu na istniejące licencji w grupie hello), kliknij przycisk Szczegóły tooview powiadomienia hello hello awarii.

Firma Microsoft już teraz określić szablon licencji dla grupy zarządzania zasobami Ludzkimi stosują hello. Proces w tle w usłudze Azure AD został uruchomiony tooprocess wszystkie istniejące elementy członkowskie tej grupy. Początkowa operacja może potrwać pewien czas w zależności od bieżącego rozmiaru hello hello grupy. W następnym kroku hello możemy opisano, jak tooverify procesu hello zakończył i określić, czy uwagi dodatkowe jest wymagana tooresolve problemów.

> [!NOTE]
> Możesz rozpocząć hello przypisania tego samego z alternatywną lokalizację: **użytkowników i grup** w usłudze Azure AD. Przejdź za**usługi Azure Active Directory** > **użytkowników i grup** > **wszystkich grup**. Następnie znajdź hello grupy, zaznacz go, a następnie przejdź toohello **licencji** hello kartę **przypisać** przycisk u góry bloku hello Otwiera blok przypisania licencji hello.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Krok 2: Sprawdź zakończenie hello początkowej przypisania

1. Przejdź za**usługi Azure Active Directory** > **użytkowników i grup** > **wszystkich grup**. Następnie znajdź hello **zarządzania zasobami Ludzkimi stosują** grupy, które zostały przypisane licencje.

2. Na powitania **zarządzania zasobami Ludzkimi stosują** bloku grupy, wybierz opcję **licencji**. Dzięki temu można szybko upewnij się, jeśli licencje zostały całkowicie przypisane toousers i wystąpiły żadne błędy, wymagające toolook do. dostępna jest Hello następujących informacji:

   - Lista licencje produktów, które są obecnie przypisane toohello grupy. Wybierz wpis tooshow hello określonych usług, które zostały włączone i toomake zmiany.

   - Stan hello najnowsze licencji wprowadzonych zmian grupy toohello (jeśli są przetwarzane zmiany hello lub Zakończono przetwarzanie dla wszystkich członków użytkownika).

   - Informacje o użytkownikach, którzy są w stanie błędu, ponieważ nie można przypisać licencje toothem.

   ![Opcje przydziału](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Zobacz szczegółowe informacje o licencji przetwarzania pod **usługi Azure Active Directory** > **użytkowników i grup** > *Nazwa grupy* > **dzienniki inspekcji**. Należy zwrócić uwagę hello następujące działania:

   - Działanie: **rozpocząć stosowanie toousers licencji na podstawie grupy**. To jest rejestrowane, gdy hello system przejmuje hello zmiany przypisania licencji na powitania grupie i rozpoczyna się stosowania jej tooall członkowie. Zawiera informacje o zmianie hello, który został utworzony.

   - Działanie: **zastosowaniu toousers licencji na podstawie grupy**. To jest rejestrowane, gdy hello system zakończy przetwarzanie wszyscy użytkownicy w grupie hello. Zawiera podsumowanie pomyślnie przetworzono ilu użytkowników i ilu użytkowników nie można przypisać do grupy licencji.

   [Przeczytaj tę sekcję](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn więcej informacji na temat sposobu dzienników inspekcji mogą być używane tooanalyze zmian na podstawie grupy licencji.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Krok 3: Sprawdź licencji problemów i ich rozwiązania

1. Przejdź za**usługi Azure Active Directory** > **użytkowników i grup** > **wszystkich grup**i Znajdź hello **zarządzania zasobami Ludzkimi stosują**grupy, które zostały przypisane licencje.
2. Na powitania **zarządzania zasobami Ludzkimi stosują** bloku grupy, wybierz opcję **licencji**. Hello powiadomienia u góry bloku hello wskazuje, że 10 użytkowników, których nie można przypisać licencje do użytkowników. Kliknięcie go otwiera listę wszystkich użytkowników w stan błędu licencjonowania dla tej grupy.
3. Witaj **nie powiodło się przypisania** kolumna zawiera informacje nam nie można przypisać użytkowników toohello zarówno licencji produktu. Witaj **najważniejsze przyczyny niepowodzenia** kolumna zawiera hello przyczynę błędu na powitania. W takim przypadku ma **planów usługi powodujące konflikt**.

   ![Przypisania nie powiodło się](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Wybierz hello tooopen użytkownika **licencji** bloku. Blok ten zawiera wszystkie licencje, które są obecnie przypisane toohello użytkownika. W tym przykładzie użytkownik hello ma licencji hello Office 365 Enterprise E1, która została odziedziczona z hello **użytkowników kiosku** grupy. To powoduje konflikt z licencji hello E3 hello tooapply systemu nastąpiła z hello **zarządzania zasobami Ludzkimi stosują** grupy. W związku z tym Brak licencji hello z tej grupy zostały przypisane toohello użytkownika.

   ![Widok licencji dla użytkownika](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve ten konflikt, Usuń hello użytkownika z hello **użytkowników kiosku** grupy. Po usługi Azure AD przetwarza hello zmiany, hello **zarządzania zasobami Ludzkimi stosują** poprawnie przypisanych licencji.

   ![Poprawnie przypisanej licencji](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat funkcji hello ustawić do zarządzania licencji za pomocą grup, zobacz następujące artykuły hello:

* [Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identyfikowanie i rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Jak osoba toomigrate — licencjonowani użytkownicy toogroup na podstawie Licencjonowanie w usłudze Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze](active-directory-licensing-group-advanced.md)
