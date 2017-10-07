---
title: dane osobowe aaaManage na platformie Microsoft Azure | Dokumentacja firmy Microsoft
description: "wskazówki dotyczące jak toocorrect, aktualizowanie, usuwanie i eksportowanie danych osobowych w usłudze Azure Active Directory i bazy danych SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Zarządzanie danych osobowych w Microsoft Azure

Ten artykuł zawiera wskazówki dotyczące jak toocorrect, aktualizowanie, usuwanie i eksportowanie danych osobowych w usłudze Azure Active Directory i bazy danych SQL Azure.

## <a name="scenario"></a>Scenariusz

Na podstawie Dublin firmę kompleksowych zakup Śluby docelowego górną granicę w Irlandii i wokół Witaj świecie bazy klientów lokalnych i międzynarodowe. Mają one oddziałów, klientów, pracowników i dostawców znajdujących się wokół systemu hello world toofully usługi hello miejsc oferują.

Wśród wielu innych elementów firmy hello przechowuje informacje o zbędne obejmujących alergii żywności i ustalenia preferencji. Goście wesele można zarejestrować dla różnych działań, takich jak horseback jazda, przeglądania, łodzi było itp. i nawet współdziałać ze sobą na stronie sieci web centralnej w miesiącach hello doprowadziły toohello zdarzeń. firmy Hello zbiera dane osobowe z pracowników, dostawców, klientów i wesele gości. Ze względu na powitania międzynarodowe rodzaj hello firm hello firmy muszą być zgodne z różnych poziomach rozporządzenia.

## <a name="problem-statement"></a>Opis problemu

- Administratorzy danych musi być w stanie toocorrect niedokładne osobiste informacje i aktualizacji niekompletne lub zmieniania informacji osobistych.

- Potrzeby administratorzy danych musi być możliwe toodelete informacji osobistych na żądanie hello podmiotu danych.

- Administratorzy danych konieczne tooexport danych i dostarczyć tooa dotyczą dane w formacie wspólnego, strukturalnych na jego żądanie.

## <a name="company-goals"></a>Cele firmy

- Nieprawidłowe lub niepełne klienta, gościa wesele pracowników i informacje osobiste dostawcy musi poprawione lub zaktualizowane w usłudze Azure Active Directory i bazy danych SQL Azure.

- Informacje osobiste, muszą zostać usunięte w usłudze Azure Active Directory i usługi Azure SQL Database na żądanie hello na temat danych.

- Dane osobowe musi być eksportowany w formacie wspólnego, strukturalnych na żądanie hello na temat danych.

## <a name="solutions"></a>Rozwiązania

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Usługi Azure Active Directory: rozwiązać/Popraw nieprawidłowe lub niekompletne dane osobowe i wymazywanie/usuwania osobistych danych/profili użytkowników

[Usługa Azure Active Directory](https://azure.microsoft.com/services/active-directory/) jest oparta na chmurze, wielodostępne katalogami i tożsamościami zarządzania usługi Microsoft.
Można poprawić, zaktualizować lub usunąć klientów i pracownika profili użytkowników oraz informacje o pracy użytkownika, które zawierają dane osobowe, takie jak nazwa użytkownika, tytuł pracy, adres lub numer telefonu, w Twojej [usługi Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) środowisko przy użyciu hello [portalu Azure](https://portal.azure.com/).

Należy zalogować się przy użyciu konta administratora globalnego dla katalogu hello.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Jak skorygować lub zaktualizować profil użytkownika i pracy informacji w usłudze Azure Active Directory?

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.

2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

    ![nośnik/image1.png](media/manage-personal-data-azure/image001.png)

3. Na powitania **użytkowników i grup** bloku, wybierz opcję **użytkowników**.

    ![nośnik/image2.png](media/manage-personal-data-azure/image003.png)

4. Na powitania **użytkowników i grup — Użytkownicy** bloku, wybierz użytkownika z listy hello, a następnie w bloku hello hello wybranego użytkownika, wybierz opcję **profilu** tooview hello informacje o profilu użytkownika wymagające toobe rozwiązany lub zaktualizowane.

    ![nośnik/image3.png](media/manage-personal-data-azure/image005.png)

5. Popraw lub zaktualizować hello informacje, a następnie, na pasku poleceń hello, wybierz **zapisać.**

6.  W bloku hello hello wybranego użytkownika, wybierz **pracy informacji** tooview pracy informacje o użytkowniku wymagające toobe poprawione lub aktualizowane.

    ![nośnik/image4.png](media/manage-personal-data-azure/image007.png)

7. Popraw lub zaktualizować informacje o pracy użytkownika hello, a następnie na pasku poleceń hello, wybierz opcję **zapisać.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Jak usunąć profil użytkownika w usłudze Azure Active Directory?

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.

2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

    ![](media/manage-personal-data-azure/image001.png)

3. Na powitania **użytkowników i grup** bloku, wybierz opcję **użytkowników**.

    ![nośnik/image2.png](media/manage-personal-data-azure/image003.png)

4. Na powitania **użytkowników i grup — Użytkownicy** bloku, wybierz użytkownika z listy hello.

    ![nośnik/image3.png](media/manage-personal-data-azure/image007.png)

5. W bloku hello hello wybranego użytkownika, wybierz **omówienie**, a następnie na pasku poleceń hello, wybierz **usunąć**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>Baza danych SQL: rozwiązać Popraw nieprawidłowe lub niekompletne dane osobowe; wymazywanie lub Usuń dane osobowe; Eksportuj dane osobowe 

[Baza danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) jest chmury bazy danych, która ułatwia deweloperom tworzenie i obsługa aplikacji.

Można aktualizować dane osobowe w [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) przy użyciu standardowego zapytania SQL, a także mogą być również usuwane. Ponadto można wyeksportować dane osobowe z bazy danych SQL przy użyciu różnych metod, w tym hello importu serwera Azure SQL i Kreator eksportu i w różnych formatach, łącznie z plikiem pliku BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Jak rozwiązać, zaktualizować lub wymazanie danych osobowych w bazie danych SQL?

toolearn jak toocorrect lub aktualizacji danych osobowych w bazie danych SQL, odwiedź stronę hello [aktualizacji (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Aktualizowanie tekstu](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [zaktualizować o wspólnym wyrażeniem tabeli](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), lub [ Aktualizowanie tekstu zapisu](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) dokumentacji.

toolearn jak toodelete danych osobowych w bazie danych SQL, odwiedź stronę hello [usunąć (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) dokumentacji.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Jak eksportować dane osobowe tooa pliku BACPAC pliku w bazie danych SQL

Plik pliku BACPAC zawiera hello danych bazy danych SQL i metadanych i plik zip z rozszerzeniem pliku BACPAC. Można to zrobić przy użyciu hello [portalu Azure](https://portal.azure.com/), hello SQLPackage narzędzie wiersza polecenia, programu SQL Server Management Studio (SSMS) lub programu PowerShell.

toolearn jak tooexport tooa pliku BACPAC plik danych hello odwiedziny [Eksportowanie pliku pliku BACPAC tooa bazy danych Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-export) strony, który zawiera szczegółowe instrukcje dotyczące każdej z metod wymienionych powyżej.

Jak wyeksportować dane osobowe z bazy danych SQL z hello importu serwera SQL i Kreator eksportu?

Ten kreator pomaga skopiować dane z docelowym tooa źródła. Aby Kreator toohello wprowadzenie, w tym jak tooget go, informacje o uprawnieniach i jak ułatwić tooget za pomocą narzędzia hello odwiedź hello [i eksportowanie danych z hello programu SQL Server zaimportuj Kreatora importu i eksportu](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) strony sieci web.

Omówienie kroków kreatora hello, odwiedź stronę hello [etapami hello importu serwera SQL i Kreator eksportu](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) strony sieci web.

## <a name="next-steps"></a>Następne kroki:

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

