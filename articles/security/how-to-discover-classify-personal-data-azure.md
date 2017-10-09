---
title: aaaDiscover, identyfikowanie i klasyfikowania danych osobowych w Microsoft Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat wyszukiwania, klasyfikacji, odnajdywania i identyfikowanie danych"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Wykryj, identyfikowanie i klasyfikowania danych osobowych w Microsoft Azure

Ten artykuł zawiera wskazówki dotyczące jak toodiscover, identyfikowanie i klasyfikowania danych osobowych w kilku narzędzi Azure i usługi, w tym za pomocą wykazu danych Azure, Azure Active Directory, baza danych SQL, dodatku Power Query dla klastrów platformy Hadoop w usłudze Azure HDInsight Azure Information Protection, usługi Azure Search i SQL kwerendy dla bazy danych Azure rozwiązania Cosmos.

## <a name="scenario-problem-statement-and-goal"></a>Scenariusz, opis problemu i cel

Firmy amerykańskiej sportowych zbiera różnorodnych danych prywatnych i innych. W tym klientów oraz danych o pracownikach. firmy Hello utrzymuje je w wielu baz danych i zapisuje je w różnych miejscach w środowisku Azure. Ponadto sprzęt sportowy tooselling, również hosta i Zarządzanie rejestracją najwyższej zdarzeń athletic wokół Witaj świecie, w tym w hello UE, oraz w niektórych przypadkach hello danych klienta, które pobierają informacje medyczne.

Ponieważ firma hello obsługuje wiele międzynarodowych przewodnikami bicycling co roku i tymczasowi pracownicy nie ma w lokalizacji na całym świecie hello, kilka zestawów danych hello są bardzo duże. Witaj firmy ma również wbudowane dewelopera aplikacji, używane przez klientów i pracowników.

Witaj, firma chce hello tooaddress następujące problemy:

- Dane osobowe klienta i pracownika musi być klasyfikowane/odróżnić od hello innych firmy hello dane są zbierane w kolejności tooensure właściwy dostęp i większe bezpieczeństwo.
- Witaj danych administrator musi tooeasily odnajdywanie lokalizacji powitania klienta danych osobowych przez różne obszary hello środowiska platformy Azure.
- Klienta i pracownika dane osobowe, która jest wyświetlana w udostępnionych dokumentów i wiadomości e-mail muszą być oznaczone toohelp upewnij się, że jest dobrze zabezpieczony.
- Deweloperzy aplikacji Hello firmy muszą tooeasily sposób wyszukiwanie danych osobowych klienta i pracownika w sieci web i aplikacji mobilnych.
- Deweloperzy również muszą tooquery ich bazą danych dokumentów dla danych osobowych.

### <a name="company-goals"></a>Cele firmy

- Wszystkie dane osobowe klienta i pracowników muszą być oznaczone/opatrzone adnotacjami w usłudze Azure Data Catalog, można je łatwo znaleźć. W idealnym przypadku klienta i pracownika danych osobowych są oznaczone adnotacji oddzielnie.
- Dane osobowe z klienta i pracownika profili użytkowników oraz informacje o pracy znajdujących się w usłudze Azure Active Directory muszą być łatwo odnaleźć.
- Można łatwo zbadać osobistych danych znajdujących się na wielu baz danych. 
- Niektóre firmy hello dużych zestawów danych są zarządzane za pomocą usługi Azure HDInsight i przechowywane w Hadoop. Muszą one zaimportowane do programu Excel, może być badana danych osobowych.
- Dane osobowe udostępnionych dokumentów i wiadomości e-mail muszą sklasyfikowane, etykietą i zabezpieczone z usługi Azure Information Protection.
- Witaj deweloperzy aplikacji firmy musi być możliwe toodiscover klienta i pracownika danych osobowych w aplikacji hello zostały one tworzone, które mogą je z usługi Azure Search.
- Deweloperzy muszą być stanie toofind danych osobowych w bazie danych tych dokumentów.

## <a name="azure-active-directory-data-discovery"></a>Usługi Azure Active Directory: Odnajdywanie danych

[Usługa Azure Active Directory](https://azure.microsoft.com/services/active-directory/) jest oparta na chmurze, wielodostępne katalogami i tożsamościami zarządzania usługi Microsoft. Możesz znaleźć klienta i pracownika profili użytkowników oraz informacje o pracy użytkownika, które zawierają dane osobowe w Twojej [usługi Azure Active Directory](https://azure.microsoft.com/services/active-directory/) środowiska (AAD) przy użyciu hello [portalu Azure](https://portal.azure.com/).

Jest to szczególnie pomocne, jeśli chcesz toofind lub zmień danych osobowych dla określonego użytkownika. Można również dodać lub zmienić profil użytkownika i informacje o pracy. Należy zalogować się przy użyciu konta administratora globalnego dla katalogu hello.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Jak znaleźć lub wyświetlanie profilu użytkownika i informacje o pracy?

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.

2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![jak znaleźć profilu użytkownika i informacje o pracy](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Na powitania **użytkowników i grup** bloku, wybierz opcję **użytkowników**.

  ![Otwieranie użytkowników i grup](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Na powitania **użytkowników i grup — Użytkownicy** bloku, wybierz użytkownika z listy hello, a następnie w bloku hello hello wybranego użytkownika, wybierz opcję **profilu** tooview informacje o profilu użytkownika, który może zawierać dane osobowe .

  ![Wybierz użytkownika](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Jeśli konieczne tooadd lub zmienić informacje o profilu użytkownika, możesz to zrobić, a następnie, na pasku poleceń hello, wybierz **zapisać.**
6. W bloku hello hello wybranego użytkownika, wybierz **pracy informacji** tooview użytkownika pracy informacje, które mogą zawierać dane osobowe.

 ![wyświetlanie informacje o pracy](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Jeśli konieczne tooadd lub zmienić informacje o użytkowniku pracy, możesz to zrobić, a następnie, na pasku poleceń hello, wybierz **zapisać.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database: Odnajdywanie danych

[Baza danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) jest chmury bazy danych, która ułatwia deweloperom tworzenie i obsługa aplikacji. Dane osobowe znajdują się w [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) przy użyciu standardowego zapytania SQL. Azure elastycznej zapytania SQL (wersja zapoznawcza) umożliwia użytkownikom tooperform między bazami danych zapytania.

Szczegółowe [bazy danych SQL](../sql-database/sql-database-technical-overview.md) samouczek wyjaśnia sposób wiele aspektów przy użyciu bazy danych SQL, w tym jak toobuild jedną i w jaki sposób toorun kwerend danych. Hello poniżej znajduje się podsumowanie hello informacje są dostępne w samouczku hello sekcje toospecific łącza.

### <a name="how-do-i-build-a-sql-database"></a>Jak utworzyć bazę danych SQL

Istnieją trzy sposoby toodo go:

- Baza danych Azure SQL mogą być tworzone w hello [portalu Azure](https://portal.azure.com/). W samouczku hello użyjesz określonego zestawu zasobów obliczeniowych i magazynu w ramach grupy zasobów i serwer logiczny. Użyjesz przykładowych danych fikcyjnej firmy o nazwie AdventureWorks. Będzie także utworzyć regułę zapory poziomu serwera. toolearn jak toodo hello, odwiedź stronę [tworzenie bazy danych Azure SQL w portalu Azure hello](../sql-database/sql-database-get-started-portal.md) samouczka.

  ![Utwórz bazę danych Azure SQL](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Można także utworzyć bazę danych SQL w hello [powłoki chmury Azure](https://azure.microsoft.com/features/cloud-shell/) interfejsu wiersza polecenia, narzędzie wiersza polecenia opartego na przeglądarce. Narzędzie Hello jest dostępna w portalu Azure hello i można uruchomić bezpośrednio z niego. W tym samouczku można uruchomić narzędzia hello, zdefiniuj zmienne skryptu Tworzenie grupy zasobów i serwer logiczny i skonfigurować reguły zapory serwera. Następnie utwórz bazę danych z przykładowymi danymi. toolearn jak toocreate bazy danych w ten sposób można znaleźć hello [tworzenia pojedynczej bazy danych Azure SQL przy użyciu interfejsu wiersza polecenia Azure hello](../sql-database/sql-database-get-started-cli.md) samouczka.

  ![Samouczek CLIT](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Interfejs wiersza polecenia platformy Azure to powszechnie używane przez administratorów systemu Linux i deweloperów. W przypadku niektórych użytkowników być łatwiejsze i bardziej intuicyjne niż środowiska PowerShell, czyli z trzecia opcja.

- Na koniec można utworzyć bazę danych SQL przy użyciu programu PowerShell, który jest toocreate narzędzia wiersza polecenia skryptu i zarządzania Azure i innych zasobów. W tym samouczku można uruchomić narzędzia hello, zdefiniuj zmienne skryptu Tworzenie grupy zasobów i serwer logiczny i skonfigurować reguły zapory serwera. Następnie utworzysz bazę danych z przykładowymi danymi.

Samouczek Hello wymaga hello Azure PowerShell modułu w wersji 4.0 lub nowszej. Uruchom Get-Module - ListAvailable AzureRM toofind wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz modułu instalacji programu Azure PowerShell.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn jak toocreate bazy danych w ten sposób można znaleźć hello [tworzenia pojedynczej bazy danych Azure SQL przy użyciu programu Powershell](../sql-database/sql-database-get-started-powershell.md) samouczka.

>[!Note]
Administratorzy systemu Windows często toouse programu PowerShell, ale niektóre z nich użyć wiersza polecenia platformy Azure.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Jak wyszukać danych osobowych w bazie danych SQL w portalu Azure hello? **

Narzędzie edytora wbudowaną kwerendę hello wewnątrz hello toosearch portalu Azure można użyć danych osobowych. Będzie rejestrować w narzędziu toohello przy użyciu identyfikator logowania administratora serwera SQL i hasło, a następnie wprowadź kwerendę.

  ![Wyszukiwanie za pomocą portalu hello sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Krok 5 samouczka hello przedstawiono przykładowe zapytanie w okienku edytora zapytań hello, ale nie skupić się na informacje poufne lub osobiste (także łączy dane z dwóch tabel i tworzy aliasów dla kolumny źródłowej hello w zestawie danych hello zwracanych). Witaj Poniższy zrzut ekranu przedstawia hello zapytania z kroku 5, a także hello okienko wyników, która jest zwracana:

  ![edytor zapytań](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Jeśli baza danych została wywołana MyTable, przykładowego zapytania o informacje osobiste może obejmować nazwę, numer ubezpieczenia społecznego i numer identyfikacyjny i będzie wyglądać następująco:

"Wybierz nazwę, SSN, identyfikator numer z MyTable"

Czy uruchomić zapytanie hello, a następnie zobacz hello powoduje hello **wyniki** okienka.

Więcej informacji dotyczących sposobu tooquery SQL bazy danych w hello portalu Azure, można znaleźć hello [hello zapytanie do bazy danych SQL](../sql-database/sql-database-get-started-portal.md) sekcji samouczka hello.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Jak wyszukiwać dane między wieloma bazami danych

Elastyczne zapytania SQL (wersja zapoznawcza) umożliwia możesz tooperform między bazami danych i wielu zapytań bazy danych i wróć pojedynczego wyniku. Witaj [samouczek Przegląd](../sql-database/sql-database-elastic-query-overview.md) zawiera szczegółowy opis scenariuszy i objaśniono różnicę hello partycjonowania poziome i pionowe bazy danych. Poziomy Partycjonowanie jest nazywany "dzielenia na fragmenty."

  ![Partycjonowanie pionowe](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![Partycjonowanie pozioma](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget pracę, odwiedź stronę hello [bazy danych SQL Azure elastycznej zapytań — omówienie (wersja zapoznawcza)](../sql-database/sql-database-elastic-query-overview.md) strony.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Dodatek Power Query (w przypadku importowania klastrów platformy Azure HDInsight Hadoop): Odnajdywanie danych w przypadku dużych zestawów danych

Hadoop jest typu open source Apache usługi przechowywania i przetwarzania w przypadku dużych zestawów danych, które są analizowane i przechowywane w klastrów platformy Hadoop. [Usługa Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) umożliwia toowork użytkowników z usługi Hadoop clusters na platformie Azure. Dodatek Power Query jest dodatek programu Excel, która między innymi ułatwia użytkownikom odnajdywanie dane z różnych źródeł.

Dane osobowe skojarzone z klastrów platformy Hadoop w usłudze Azure HDInsight można tooExcel zaimportowane z dodatku Power Query. Po hello danych w programie Excel tooidentify kwerendy można użyć go.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Jak używać klastrów platformy Hadoop tooimport dodatku Power Query dla programu Excel w usłudze Azure HDInsight do programu Excel

Samouczek HDInsight objaśniają całego procesu. Opisano wymagania wstępne i obejmuje tooa łącze [Rozpoczynanie pracy z usługą Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) samouczka. Instrukcje obejmują Excel 2016, a także 2010 i 2013 (kroki są nieco inne hello starszej wersji programu Excel). Jeśli nie masz dodatku Excel Power Query hello hello samouczek pokazuje, jak tooget go. Początek samouczka hello w programie Excel i będzie konieczne toohave konta magazynu obiektów Blob Azure skojarzonego z klastrem.

  ![Zapytania w programie Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn jak toodo hello, odwiedź stronę [tooHadoop łączenie programu Excel za pomocą dodatku Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) samouczka.

Źródło: [tooHadoop Połącz Excel za pomocą dodatku Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Usługa Azure Information Protection: Klasyfikacja danych osobowych dla dokumentów i wiadomości e-mail

[Usługa Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) umożliwia klientom Azure zastosować tooclassify etykiety i ochronę wewnętrznych lub zewnętrznych udostępnionych dokumentów i wiadomości e-mail komunikacji. Niektóre z tych elementów może zawierać informacje osobiste klienta lub pracowników. Zasady i warunki można definiować automatycznie lub ręcznie przez administratorów lub użytkowników. Na przykład jeśli użytkownik zapisuje dokument, który zawiera informacje o karcie kredytowej, użytkownik zobaczy zalecenie etykiety, które zostały skonfigurowane przez administratora hello.

### <a name="how-do-i-try-it"></a>Jak spróbuj go

Jeśli chcesz toogive usługi Azure Information Protection try toosee, jeśli może być odpowiednie dla Twojej organizacji, odwiedź stronę hello [samouczek Szybki Start](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Przeprowadza użytkownika przez pięć podstawowych kroków — z instalacji tooconfiguring zasad tooseeing klasyfikacji, etykietowania i udostępnianie w akcji — i powinno zająć mniej niż pół godziny.

### <a name="how-do-i-deploy-it"></a>Jak wdrożyć go

Jeśli chcesz toodeploy usługi Azure Information Protection dla swojej organizacji, odwiedź hello [planu wdrożenia dla klasyfikacji, etykietowania i ochrony](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Czy jest coś innego trzeba wiedzieć?

Informacje uzupełniające pomoże Ci przemyślenie jak tooset go, odwiedź stronę hello [gotowe, należy ustawić należy chronić!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
wpis w blogu. I wyboru hello Dowiedz się więcej łączy wymienionych poniżej, aby uzyskać więcej informacji na temat usługi Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Usługa wyszukiwanie Azure: danych odnajdywania dla deweloperów aplikacji

[Usługa Azure Search](https://azure.microsoft.com/services/search/) jest rozwiązania wyszukiwania w chmurze dla deweloperów i zapewnia obsługę wyszukiwania danych rozbudowanych aplikacji. Wyszukiwanie Azure umożliwia toolocate danych między indeksów zdefiniowane przez użytkownika z bazy danych Azure kosmetyczka, baza danych SQL Azure, magazyn obiektów Blob Azure, magazynem tabel Azure lub klienta niestandardowe dane JSON. Można również struktury zapytań Lucene przy użyciu hello interfejsu API REST wyszukiwania Azure toosearch dla typów danych osobowych lub hello dane osobiste z określonym osobom. Cechy wyszukiwania pełnotekstowego, prosta składnia zapytań i składnia zapytań Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Jak używać danych tooquery SQL?

toobegin z podstawy hello odwiedź hello [bazy danych Azure CosmosD: jak tooquery przy użyciu programu SQL](../cosmos-db/tutorial-query-documentdb.md) samouczka. Samouczek Hello zawiera przykładowy dokument i dwa przykładowe zapytania SQL oraz wyniki.

Więcej szczegółowe wskazówki dotyczące tworzenia zapytania SQL, odwiedź stronę [kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych dokumentów bazy danych.](../cosmos-db/documentdb-sql-query.md)

Jeśli jest nowy tooAzure rozwiązania Cosmos bazy danych i jak toolearn sposobu toocreate bazy danych, Dodaj kolekcji, a także dodać dane, odwiedzić hello [bazy danych Azure rozwiązania Cosmos: tworzenie aplikacji sieci web interfejsu API usługi DocumentDB](../cosmos-db/create-documentdb-dotnet.md) samouczek Szybki Start. Jeśli chcesz toodo to w języku innym niż .NET, takie jak Java lub Python, wystarczy wybrać preferowany język po pobraniu toohello lokacji.

## <a name="next-steps"></a>Następne kroki

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[Co to jest SQL Database?](../sql-database/sql-database-technical-overview.md)

[SQL edytora zapytań bazy danych dostępne w portalu Azure] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Co to jest Azure Information Protection?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Co to jest usługa Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Usługa Azure Information Protection: Gotowe, ustawianie, ochrona!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
