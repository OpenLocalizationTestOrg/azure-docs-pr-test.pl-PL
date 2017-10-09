---
title: "narzędzia oceny rozwiązania analizy aaaCortana | Dokumentacja firmy Microsoft"
description: "Jako partnera firmy Microsoft w tym miejscu są wszystkie kroki hello należy toofollow toopublish Twojego tooAppSource rozwiązania Cortana Intelligence."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Narzędzie oceny rozwiązania Cortana Intelligence
## <a name="overview"></a>Omówienie
Można użyć hello tooassess narzędzie oceny rozwiązania Cortana Intelligence rozwiązań zaawansowana analityka dla zgodności z najlepszymi rozwiązaniami z zalecanymi przez firmę Microsoft. Firma Microsoft dokłada radością toowork z naszych partnerów (niezależnym dostawcom oprogramowania / SIs) tooprovide wysokiej jakości rozwiązania dla klientów, odsprzedawców i implementacji. Ten przewodnik Przeprowadź proces hello za pomocą narzędzia oceny hello rozwiązania z rozwiązania i opisz hello określonych — najlepsze praktyki sprawdza, czy.

## <a name="getting-started"></a>Wprowadzenie
Sprawdź [Pobierz](https://aka.ms/aa-evaluation-tool-download) i zainstalować narzędzia oceny rozwiązania Cortana Intelligence hello.

Wymagania wstępne:
- Windows 10: [oficjalna witryna dla systemu Windows 10](https://www.microsoft.com/en-us/windows)
- Program Azure Powershell: [Instalowanie i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).

## <a name="identifying-your-app"></a>Identyfikowanie aplikacji
Po zakończeniu instalacji, Otwórz narzędzie hello i rozpocząć pierwszej oceny.

![Narzędzia oceny otwarte](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Podaj informacje identyfikujące rozwiązania.

![Łączenie subskrypcji platformy Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Połącz tooyour subskrypcji platformy Azure i podaj hello grupę zasobów zawierającą aplikację.

![Wybierz zasoby](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Po załadowaniu hello grupy zasobów wybierz hello zasobów, które są zawarte w rozwiązaniu i zidentyfikować hello dostępności zasobów danych jako:
- Wprowadzanie
- Zużycie
- wewnętrzny

Używamy tych informacji toobetter zrozumieć sposób rozwiązania jest przy użyciu różnych składników i składniki uwzględniającym działania użytkownika tooensure są zgodne z najlepszymi rozwiązaniami.

### <a name="ingestion"></a>Wprowadzanie
Wprowadzanie oznacza w tym przypadku wszystkie źródła danych, które są używane toopull danych z rozwiązania poza hello lub że wszystkich usług poza rozwiązania hello użyć danych toopush do niego.

### <a name="consumption"></a>Zużycie
Użycie w takim przypadku oznacza, że wszystkie zestawy danych, które są używane toopush danych tooend użytkowników, bezpośrednio lub pośrednio. Na przykład:
- Zestawów danych użytych w zapytania bezpośredniego z usługi Power BI.
- Zestawy danych w aplikacji sieci Web.

>[!NOTE]
Użycie zasobów specyficznych dla wprowadzanie i zużycia wybierz **zużycie**.

### <a name="internal"></a>wewnętrzny
Użyj wewnętrznego dla wszystkich zasobów danych, które są używane tylko podczas przetwarzania aplikacji wewnętrznych.

Następnie można tooprovide zostanie wyświetlony monit o prawidłowe poświadczenia dla żadnych baz danych określonego w kroku wcześniejsze hello:

![Wymagania wstępne dotyczące zestawu testów](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Rozwiązanie przypadków testowych
Narzędzie rozwiązania Hello wykona zbiór testów automatycznych w rozwiązaniu.

![Wykonanie testowego zestawu](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Po ukończeniu testów hello użytkownik zostanie poproszony tooprovide wyjaśnienie lub uzasadnienie, dlaczego rozwiązania nie spełnia wymagań hello.

![Podaj uzasadnienie biznesowe](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Na przykład rozwiązania publikuje tooAzure magazynu danych SQL, oceny hello testy wymagają tooalso możesz opublikować tooAzure Analysis Services. 

Rozwiązania mogą używać maszyny wirtualne IaaS z usługami Sql Server Analysis Services, zamiast usług Azure Analysis Services. Będzie to dopuszczalne Przyczyna niepowodzenia hello testu.
## <a name="packaging-your-evaluation-results"></a>Pakowanie wyników oceny
Po zakończeniu hello przypadków testowych, pakietu oceny będą tooa wyeksportowanego pliku zip, a użytkownik zostanie poproszony tooprovide opinię na temat narzędzia do oceny hello. 

Należy ten test powoduje pliku zip z firmy Microsoft dla Twojego toobe rozwiązania oceniane przed pobraniem toobe zatwierdzenia dodane tooshare tooAppSource

![Klasa narzędzia oceny](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Powyżej sekcji tego artykułu opisano różne funkcje narzędzia hello, teraz Daj nam sprawdzić typy najlepszych rozwiązań, które ocenia tego narzędzia.

## <a name="security-evaluation-considerations"></a>Zagadnienia dotyczące zabezpieczeń oceny
### <a name="databases-should-use-azure-active-directory-authentication"></a>Bazy danych należy używać uwierzytelniania usługi Azure Active Directory
Wszystkie zasoby bazy danych Azure SQL lub magazynu danych SQL Azure w hello sloution powinna być włączona przy użyciu uwierzytelniania usługi Azure Active Directory (AAD). Udostępnia usługi AAD toomanage jednego miejsca, wszystkie tożsamości i ról.

| Aby uzyskać więcej informacji o | Znajduje się w artykule |
| --- | --- |
| Usługi AAD z bazy danych SQL i magazyn danych SQL | [Użyj uwierzytelniania usługi Azure Active Directory do uwierzytelniania przy użyciu bazy danych SQL lub SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Konfigurowanie i zarządzanie nimi w usłudze AAD | [Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Azure używanie uwierzytelniania | [Uwierzytelnianie i autoryzację w usłudze Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Skonfigurować używanie przy użyciu usługi AAD | [Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi aplikacji](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Użytkownicy tooend dostępne zestawy danych powinny obsługiwać kontroli dostępu opartej na rolach
Podczas wykonywania narzędzia oceny hello, będzie zadawane toospecify, raportowania ani publikowanie zasobów. Zakłada się, że te zasoby są przeznaczone dla dostępu przez użytkowników końcowych, deweloperzy nie. Te zasoby powinny, należy podać kontroli dostępu opartej na rolach (RBAC) w kolejności tooensure że użytkownicy końcowi są tylko stanie tooaccess autoryzowany danych.

W szczególności żadnego z następujących zasobów platformy Azure hello można skonfigurować za pomocą RBAC i są uważane za akceptowalne:
- Zabezpieczanie usługi HDInsight, zobacz [zabezpieczeń tooHadoop wprowadzenie z klastrami HDInsight przyłączonych do domeny](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL, zobacz [uwierzytelniania w usłudze AAD z usługi Azure SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)
- Azure Analysis Services, zobacz [Zarządzanie ról bazy danych i użytkowników dla usług Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users)
- Usługa Azure SQL Data Warehouse (należy pamiętać, że ponieważ magazynu danych SQL obsługuje RBAC, nie jest zalecane dla użytkownika końcowego bezpośredniego dostępu).

Jeśli używasz inny typ zasobu, który obsługuje RBAC Określ który w hello przypadek testowy uzasadnienie.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store należy używać szyfrowania na rest
Azure Data Lake — magazyn (ADLS) obsługuje szyfrowanie na rest domyślnie przy użyciu kluczy szyfrowania zarządzane ADLS. Można również skonfigurować szyfrowanie przy użyciu usługi Azure Key Vault.

Informacje dotyczące określania ustawień szyfrowania ADLS [Tworzenie konta usługi Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL i magazyn danych SQL Azure należy korzystać z szyfrowania
Azure SQL i magazynu danych SQL Azure obsługują przezroczysty danych szyfrowania (funkcji TDE), która zapewnia w czasie rzeczywistym szyfrowania i odszyfrowywania plików dziennika i danych.

| Aby uzyskać więcej informacji o | Znajduje się w artykule |
| --- | --- |
| Przezroczystego szyfrowania danych (funkcji TDE) | [Przezroczystego szyfrowania danych](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL Data Warehouse przy użyciu funkcji TDE | [Encrption funkcji TDE TSQL magazyn danych SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Konfigurowanie usługi Azure SQL przy użyciu funkcji TDE | [Przezroczystego szyfrowania danych z bazy danych Azure SQL](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Konfigurowanie usługi Azure SQL z zawsze zaszyfrowane | [Baza danych SQL zawsze zaszyfrowane usługi Azure Key Vault](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Ponadto tooTDE, Azure SQL obsługuje również zawsze zaszyfrowane, nowej technologii szyfrowania danych, które zapewnia, że dane są szyfrowane, nie tylko na rest i podczas przenoszenia między klientem a serwerem, ale również podczas danych jest używany podczas wykonywania polecenia na serwerze hello.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Wszystkie maszyny wirtualne muszą być wdrożone z hello Azure Marketplace
W kolejności tooprovide spójne poziom zabezpieczeń między AppSource możemy wymagają, aby wszystkie maszyny wirtualne wdrażane w ramach rozwiązania Cortana Intelligence można certyfikowane i publikowane na hello Azure Marketplace.

toosearch hello bieżącej listy obrazów w portalu Azure Marketplace, zobacz [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Informacje dotyczące sposobu toopublish, obrazów maszyny wirtualnej, do portalu Azure Marketplace, sekcji [toocreate przewodnik obrazu maszyny wirtualnej dla hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Zagadnienia dotyczące skalowalności oceny
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Rozwiązania Cortana Intelligence powinna zawierać platformy skalowalne danych big data
Rozwiązania Cortana Intelligence powinny być skalowane toovery rozmiary dużej ilości danych. Na platformie Azure oznacza to, że powinny obejmować jeden Witaj dwie skali Petabajt danych platformy:
- Azure Data Lake Store
- Azure SQL Data Warehouse

Jeśli rozwiązania nie wymaga obsługi rozmiary danych lub jeśli używasz platformy alternatywnych danych Wyjaśnij to w hello przypadek testowy uzasadnienie.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Rozwiązania Cortana Intelligence powinna zawierać dedykowanych wprowadzanie danych środowiska
Rozwiązania Cortana Intelligence ogólnie należy unikać bezpośrednio Wstawianie danych do źródła danych relacyjnych. Zamiast tego nieprzetworzone dane powinny być przechowywane w środowisku bez struktury z idempotentności wstawiania/aktualizacji do wszystkich sklepów relacyjne przy użyciu fabryki danych Azure.

Aby uzyskać więcej informacji o kopiowaniu danych z fabryką danych Azure [samouczek: tworzenie potoku z działania kopiowania za pomocą programu Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Usługa Azure SQL Data Warehouse PolyBase musi być używane na wprowadzanie danych
Azure SQL DW obsługuje PolyBase wprowadzanie danych wysoce skalowalną, równoległe. Program PolyBase pozwala toouse Azure SQL DW tooissue zapytań dotyczących zewnętrznych zestawów danych przechowywanych w magazynie obiektów Blob Azure lub usługi Azure Data Lake Store. Zapewnia to lepszą wydajność tooalternative metody aktualizacji zbiorczej.

Aby uzyskać instrukcje na wprowadzenie PolyBase i magazynu danych SQL Azure, zobacz [ładowanie danych przy użyciu programu PolyBase w usłudze SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Aby uzyskać więcej informacji na temat najlepszych rozwiązań z PolyBase i magazynu danych SQL Azure, zobacz [przewodnik przy użyciu programu PolyBase w usłudze SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Zagadnienia dotyczące obliczania dostępności

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Użytkownicy tooend dostępne zestawy danych powinny obsługiwać dużej liczby równoczesnych użytkowników
Podczas wykonywania narzędzia oceny hello, będzie zadawane toospecify, raportowania ani publikowanie zasobów. Zakłada się, że te zasoby są przeznaczone dla dostępu przez użytkowników końcowych, deweloperzy nie. Te zasoby powinny obsługiwać średnich i dużych liczby równoczesnych użytkowników.

W szczególności magazyn danych SQL Azure nie może być hello wyłącznie danych źródła tooend dostępnych użytkowników. W przypadku magazynu danych SQL Azure jako zasób dla użytkowników zaawansowanych usług Azure Analysis Services należy tootypical dostępnych użytkowników.

Aby uzyskać więcej informacji na temat limitów współbieżności Azure SQL DW, zobacz [zarządzania współbieżności i obciążenia w usłudze SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Aby uzyskać więcej informacji na temat usług Azure Analysis Services, zobacz [Omówienie usług Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Zasoby usługi Azure SQL powinien mieć tylko do odczytu repliki do trybu failover
Bazy danych SQL Azure obsługuje — replikacja geograficzna tooa dodatkowej wystąpienia. To wystąpienie może następnie służyć jako trybu failover wystąpienia tooprovide wysoką dostępność aplikacji.

Aby uzyskać więcej informacji na temat — replikacja geograficzna baz danych Azure SQL, zobacz [omówienie replikacja geograficzna bazy danych SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Aby uzyskać instrukcje dotyczące replikacja geograficzna tooconfigure dla bazy danych SQL Azure, zobacz [skonfigurować aktywna replikacja geograficzna bazy danych SQL Azure z Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Usługa Azure SQL Data Warehouse powinny mieć geograficznie nadmiarowego kopie zapasowe włączone
Azure SQL DW obsługuje codziennych kopii zapasowych magazynu geograficznie nadmiarowego toogeo. Replikacja geograficzna gwarantuje, że można przywrócić hello hurtowni danych, nawet w sytuacjach, w których nie można uzyskać dostępu migawek przechowywanych w Twoim regionie podstawowym. Ta funkcja jest domyślnie włączona i nie należy wyłączyć dla rozwiązań Cortana Intelligence.

Aby uzyskać więcej informacji na temat Azure SQL DW kopie zapasowe i przywracanie widoczną w tym miejscu [kopii zapasowych magazynu danych SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Maszyny wirtualne należy skonfigurować zestawy dostępności
Maszyny wirtualne platformy Azure powinna być skonfigurowana w zestawów dostępności w kolejności toominimize hello wpływ zdarzeń planowanych lub nieplanowanych konserwacji.

Aby uzyskać więcej informacji na temat dostępności maszyny wirtualnej platformy Azure, zobacz [Zarządzanie hello dostępność maszyn wirtualnych systemu Windows na platformie Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Inne zagadnienia oceny
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Aplikacje Cortana Intelligence powinny używać scentralizowane narzędzia dla danych aranżacji
Za pomocą jednego narzędzia do zarządzania i planowania przenoszenia danych i transformacja zapewnia spójność wokół kluczowych danych. Zapewnia on wyczyść logiki wokół logika ponowień, zarządzania zależności, alert/rejestrowania itp. Firma Microsoft zaleca użycie hello [fabryki danych Azure](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) do aranżacji danych na platformie Azure.

Jeśli używasz narzędzia innego niż fabryki danych Azure dla danych aranżacji, opisz które narzędzie lub korzystasz z narzędzia.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Modele uczenia maszynowego Azure powinna być retrained przy użyciu fabryki danych Azure
Azure Machine Learning (uczenie maszynowe Azure) zawiera narzędzia łatwe toouse hello tworzenia i wdrażania modelowania predykcyjnego i potoki uczenia maszynowego. Jednak ważne jest wdrożeń produkcyjnych tych modeli uczenie maszynowe Azure nie jest oparty na jednym stałego zestawu danych, ale zamiast tego dostosowuje toohello zmieni dynamics zjawiska rzeczywistych.

Aby uzyskać więcej informacji na temat tworzenia usług sieci web ponownego trenowania w uczenie maszynowe Azure, zobacz [Retrain Machine Learning programowo modele](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Aby uzyskać więcej informacji na temat automatyzacji procesu uczenia modelu hello przy użyciu fabryki danych Azure, zobacz [modeli aktualizowanie uczenia maszynowego Azure przy użyciu działanie aktualizacji zasobu](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Istniejąca dokumentacja
[Microsoft Azure certyfikowane toogrow firmy chmury](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Certified for Cortana Intellignece](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

