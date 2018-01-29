---
title: "Omówienie zabezpieczeń w usłudze Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak usługa Azure Data Lake Store jest bardziej bezpieczne przechowywania danych big data"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/28/2017
ms.author: nitinme
ms.openlocfilehash: 52e176711f512e8a3788309a58011c8484821a1e
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2017
---
# <a name="security-in-azure-data-lake-store"></a>Zabezpieczeń w usłudze Azure Data Lake Store
Wiele przedsiębiorstw są korzystanie z analizy danych big data szczegółowe informacje biznesowe ułatwić im podejmowanie decyzji inteligentne. Organizacja może mieć środowisko złożone i podlegającymi ochronie, z coraz większa liczba różnych użytkowników. Jest ważne dla organizacji upewnić się, że ważnych danych biznesowych jest bezpieczniejsza, przechowywane z odpowiedniego poziomu udzielono dostępu do poszczególnych użytkowników. Azure Data Lake Store ułatwia spełnia te wymagania dotyczące zabezpieczeń. W tym artykule, więcej informacji na temat funkcji zabezpieczeń w usłudze Data Lake Store, w tym:

* Authentication
* Autoryzacja
* Izolacja sieci
* Ochrona danych
* Inspekcja

## <a name="authentication-and-identity-management"></a>Uwierzytelnianie i tożsamość zarządzania
Uwierzytelnianie to proces, za pomocą którego tożsamość użytkownika została zweryfikowana, gdy użytkownik wchodzi w interakcję z usługą Data Lake Store lub z dowolnej usługi, który łączy do usługi Data Lake Store. Do uwierzytelniania i zarządzania tożsamościami, Data Lake Store używa [usługi Azure Active Directory](../active-directory/active-directory-whatis.md), kompleksowe tożsamościami i dostępem chmury rozwiązania zarządzania, które ułatwia zarządzanie użytkownikami i grupami.

Każda subskrypcja platformy Azure może być skojarzony z wystąpieniem usługi Azure Active Directory. Tylko użytkownicy i tożsamości usługi, które są zdefiniowane w usłudze Azure Active Directory można uzyskać dostęp do konta usługi Data Lake Store za pomocą portalu Azure, narzędzia wiersza polecenia lub przez aplikacje klienckie organizacji tworzy się przy użyciu zestawu SDK usługi Azure Data Lake Store. Zalety klucza przy użyciu usługi Azure Active Directory jako mechanizmu kontroli dostępu scentralizowane są następujące:

* Uproszczone zarządzanie cyklem życia tożsamości. Tożsamość użytkownika lub usługi (tożsamości głównej usługi) można szybko utworzyć i szybko odwołany przez po prostu usunięcie lub wyłączenie konta w katalogu.
* Uwierzytelnianie wieloskładnikowe. [Uwierzytelnianie wieloskładnikowe](../multi-factor-authentication/multi-factor-authentication.md) zapewnia dodatkową warstwę zabezpieczeń logowania użytkowników i transakcji.
* Uwierzytelnianie za pomocą dowolnego klienta przy użyciu standardowego protokołu open, takich jak uwierzytelniania OAuth lub OpenID.
* Federacja z usługami katalogu przedsiębiorstwa i dostawcy tożsamości w chmurze.

## <a name="authorization-and-access-control"></a>Autoryzacji i kontroli dostępu
Po usługi Azure Active Directory uwierzytelnia użytkownika, dzięki czemu użytkownik może uzyskać dostępu do usługi Azure Data Lake Store, formanty autoryzacji uprawnień dostępu dla usługi Data Lake Store. Data Lake Store oddziela autoryzacji dla działań związanych z kontem i związanych z danymi w następujący sposób:

* [Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md) (RBAC) jest dostarczany przez platformę Azure do zarządzania kontami
* Listy ACL POSIX do uzyskiwania dostępu do danych w magazynie

### <a name="rbac-for-account-management"></a>RBAC dla zarządzania kontem
Cztery podstawowe role są definiowane dla usługi Data Lake Store domyślnie. Role umożliwiają różnych operacji na koncie usługi Data Lake Store za pomocą portalu Azure, poleceń cmdlet programu PowerShell i interfejsów API REST. Role właściciela i współautor może wykonywać różne funkcje administracji na koncie. Można przypisać rolę czytelnika do użytkowników, którzy komunikować się tylko z danymi.

![Role RBAC](./media/data-lake-store-security-overview/rbac-roles.png "role RBAC")

Należy pamiętać, że chociaż role są przypisane do zarządzania kontami, niektóre role na dostęp do danych. Należy użyć listy kontroli dostępu do kontrolowania dostępu do operacji, które użytkownik może wykonywać w systemie plików. W poniższej tabeli przedstawiono podsumowanie management rights i prawa dostępu do danych dla domyślnych ról.

| Role | Uprawnienia do zarządzania | Prawa dostępu do danych | Wyjaśnienie |
| --- | --- | --- | --- |
| Nie przypisanej roli. |Brak |Wystawianych przez listy kontroli dostępu |Użytkownik nie można użyć portalu Azure lub poleceń cmdlet programu Azure PowerShell, aby przeglądać usługi Data Lake Store. Użytkownik może użyć tylko narzędzia wiersza polecenia. |
| Właściciel |Wszystkie |Wszystkie |Rola właściciela jest administratora. Tej roli mogą zarządzać wszystkim i ma pełny dostęp do danych. |
| Czytelnik |Tylko do odczytu |Wystawianych przez listy kontroli dostępu |Rolę czytelnika mogą przeglądać wszystko dotyczące zarządzania kontami, takie jak użytkownik jest przypisany do roli. Rolę czytelnika nie wprowadzać zmian. |
| Współautor |Wszystkie z wyjątkiem dodawania i usuwania ról |Wystawianych przez listy kontroli dostępu |Rola współautora można zarządzać niektórych aspektów konta, takich jak wdrożenia i tworzenie i Zarządzanie alertami. Rola współautora nie można dodać lub usunąć role. |
| Administrator dostępu użytkowników |Dodawanie i usuwanie ról |Wystawianych przez listy kontroli dostępu |Rola Administrator dostępu użytkowników można zarządzać użytkownikowi dostęp do konta. |

Aby uzyskać instrukcje, zobacz [przypisać użytkowników lub grup zabezpieczeń do kont usługi Data Lake Store](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Przy użyciu listy ACL dla operacji w systemach plików
Data Lake Store jest systemem plików hierarchiczna jak Hadoop Distributed pliku System (HDFS) i obsługuje [listy ACL POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Kontroluje odczytu (r), zapisu (w) i wykonywania (x) uprawnienia do zasobów dla właściciela roli, grupy Właściciele i dla innych użytkowników i grup. W publicznej wersji zapoznawczej usługi Data Lake Store (bieżąca wersja) listy ACL można włączyć w folderze głównym, podfolderach i w poszczególnych plikach. Aby uzyskać więcej informacji na temat sposobu działania list kontroli dostępu w kontekście usługi Data Lake Store, zobacz [Kontrola dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).

Firma Microsoft zaleca definiować listy ACL dla wielu użytkowników za pomocą [grup zabezpieczeń](../active-directory/active-directory-groups-create-azure-portal.md). Dodawanie użytkowników do grupy zabezpieczeń, a następnie przypisz list ACL dla pliku lub folderu do tej grupy zabezpieczeń. Jest to przydatne, gdy chcesz zapewnić dostęp niestandardowy, ponieważ jest ograniczona do dodawania maksymalnie dziewięć wpisy dla niestandardowych dostępu. Aby uzyskać więcej informacji o tym, jak lepiej zabezpieczyć dane przechowywane w usłudze Data Lake Store przy użyciu grup zabezpieczeń usługi Azure Active Directory, zobacz [Przypisz użytkowników lub grupy zabezpieczeń jako listy kontroli dostępu w systemie plików usługi Azure Data Lake Store](data-lake-store-secure-data.md#filepermissions).

![Lista dostępu standardowe i niestandardowe](./media/data-lake-store-security-overview/adl.acl.2.png "listy dostępu standardowe i niestandardowe")

## <a name="network-isolation"></a>Izolacja sieci
Użyj Data Lake Store ułatwiają kontrolowanie dostępu do magazynu danych na poziomie sieci. Można ustanowić zapory i zdefiniować zakres adresów IP dla zaufanych klientów. Z zakresu adresów IP tylko w przypadku klientów, którzy mają adres IP ze zdefiniowanego zakresu można nawiązać połączenia usługi Data Lake Store.

![Ustawienia zapory i IP dostępu](./media/data-lake-store-security-overview/firewall-ip-access.png "ustawienia i adres IP zapory")

## <a name="data-protection"></a>Ochrona danych
Azure Data Lake Store zapewnia ochronę danych w całym cyklu życia. Dla danych podczas przesyłania Data Lake Store używa standardowy protokół zabezpieczeń TLS (Transport Layer) do zabezpieczania danych za pośrednictwem sieci.

![Szyfrowanie w usłudze Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "szyfrowania w usłudze Data Lake Store")

Usługa Data Lake Store umożliwia także szyfrowanie danych przechowywanych w ramach konta. Możesz wybrać szyfrowanie danych lub jego brak. Jeśli zgłosić się do szyfrowania danych przechowywanych w usłudze Data Lake Store są szyfrowane przed przechowywanie na nośniku trwałych. W takim przypadku Data Lake Store szyfruje dane przed wprowadzeniem trwałych i automatycznie odszyfrowuje dane przed pobierania, dlatego jest całkowicie niewidoczne dla klienta podczas uzyskiwania dostępu do danych. Nie ulega zmianie kod wymagany po stronie klienta do szyfrowania/odszyfrowywania danych.

Zarządzania kluczami Data Lake Store zapewnia dwa tryby zarządzania kluczy szyfrowania głównego (MEKs), które są wymagane do odszyfrowywania danych przechowywanych w usłudze Data Lake Store. Można albo programowi Data Lake Store Zarządzanie MEKs lub zachować prawa własności MEKs przy użyciu konta usługi Azure Key Vault. Należy określić tryb zarządzania kluczami podczas podczas tworzenia konta usługi Data Lake Store. Aby uzyskać więcej informacji na temat sposobu zapewnienia konfiguracji odnoszącej się do szyfrowania, zobacz [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Dzienniki inspekcji i diagnostyczne
Można użyć dzienników inspekcji lub diagnostycznych, w zależności od tego, czy jest wyświetlany dla dzienników dla działań związanych z zarządzaniem lub działań związanych z danymi.

* Działania związane z zarządzania przy użyciu interfejsów API Menedżera zasobów Azure i są udostępniane w portalu Azure za pomocą dzienników inspekcji.
* Działania związane z danymi przy użyciu interfejsów API REST WebHDFS i są udostępniane w portalu Azure za pomocą dzienników diagnostycznych.

### <a name="auditing-logs"></a>Dzienniki inspekcji
Aby zachować zgodność z przepisami, organizacja może wymagać wykonywania odpowiednich audytu wymaga szczegółowej na określone zdarzenia. Data Lake Store ma wbudowaną funkcję monitorowania i przeprowadzania inspekcji i rejestruje wszystkie działania związane z zarządzaniem konta.

Zapisy inspekcji zarządzania kontem przeglądanie i Wybieranie kolumn, które mają być rejestrowane. Dzienniki inspekcji możesz również wyeksportować do magazynu Azure.

![Dzienniki inspekcji](./media/data-lake-store-security-overview/audit-logs.png "Dzienniki inspekcji")

### <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Można ustawić zapisy inspekcji dostępu do danych w portalu Azure (w ustawieniach diagnostycznych) i tworzyć konta magazynu obiektów Blob platformy Azure, gdzie są przechowywane dzienniki.

![Dzienniki diagnostyczne](./media/data-lake-store-security-overview/diagnostic-logs.png "dzienniki diagnostyczne")

Po skonfigurowaniu ustawień diagnostycznych można wyświetlać dzienniki na **dzienników diagnostycznych** kartę.

Aby uzyskać więcej informacji na temat pracy z dzienników diagnostycznych z usługi Azure Data Lake Store, zobacz [dostęp do dzienników diagnostycznych dla usługi Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Podsumowanie
Klienci korporacyjni wymaga platformy chmury analizy danych, który jest bezpieczne i łatwe w użyciu. Azure Data Lake Store ułatwia adres, który wymagania w zakresie zarządzania tożsamościami i uwierzytelniania za pomocą integracji Azure Active Directory, autoryzacji na podstawie listy ACL, izolacji sieci, szyfrowanie danych przesyłanych i rest (dostępne w przyszłości) i inspekcji.

Jeśli chcesz zobaczyć nowe funkcje w usłudze Data Lake Store, Prześlij nam swoją opinię [forum usługi Data Lake magazynu UserVoice](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Rozpoczynanie pracy z usługą Data Lake Store](data-lake-store-get-started-portal.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)

