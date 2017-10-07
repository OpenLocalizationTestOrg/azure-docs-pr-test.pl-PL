---
title: "aaaOverview zabezpieczeń w usłudze Data Lake Store | Dokumentacja firmy Microsoft"
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
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Zabezpieczeń w usłudze Azure Data Lake Store
Wiele przedsiębiorstw są korzystanie z analizy danych big data dla toohelp szczegółowych informacji biznesowych, które je wykonać inteligentne decyzje. Organizacja może mieć środowisko złożone i podlegającymi ochronie, z coraz większa liczba różnych użytkowników. Istotne jest dla przedsiębiorstwa toomake się, że ważnych danych biznesowych jest bardziej bezpiecznie przechowywane z hello odpowiedni poziom dostępu przyznanego tooindividual użytkowników. Azure Data Lake Store jest przeznaczona toohelp spełnia te wymagania dotyczące zabezpieczeń. W tym artykule, więcej informacji na temat funkcji zabezpieczeń hello Data Lake Store, w tym:

* Authentication
* Autoryzacja
* Izolacja sieci
* Ochrona danych
* Inspekcja

## <a name="authentication-and-identity-management"></a>Uwierzytelnianie i tożsamość zarządzania
Uwierzytelnianie to proces hello za pomocą którego tożsamości użytkownika jest weryfikowane, gdy użytkownik hello wchodzi w interakcję z usługą Data Lake Store lub z dowolnej usługi, który łączy tooData Lake Store. Do uwierzytelniania i zarządzania tożsamościami, Data Lake Store używa [usługi Azure Active Directory](../active-directory/active-directory-whatis.md), kompleksowe tożsamościami i dostępem chmury rozwiązania zarządzania, które upraszcza zarządzanie hello użytkowników i grup.

Każda subskrypcja platformy Azure może być skojarzony z wystąpieniem usługi Azure Active Directory. Tylko użytkownicy i tożsamości usługi, które są zdefiniowane w usłudze Azure Active Directory mają dostęp do konta usługi Data Lake Store za pomocą hello portalu Azure, narzędzia wiersza polecenia lub za pośrednictwem aplikacji klienckich, kompilacje w organizacji za pomocą hello danych Azure Zestaw SDK Lake — magazyn. Zalety klucza przy użyciu usługi Azure Active Directory jako mechanizmu kontroli dostępu scentralizowane są następujące:

* Uproszczone zarządzanie cyklem życia tożsamości. można szybko utworzyć i szybko odwołany przez po prostu usunięcie lub wyłączenie konta hello w katalogu hello Hello tożsamości użytkownika lub usługi (tożsamości głównej usługi).
* Uwierzytelnianie wieloskładnikowe. [Uwierzytelnianie wieloskładnikowe](../multi-factor-authentication/multi-factor-authentication.md) zapewnia dodatkową warstwę zabezpieczeń logowania użytkowników i transakcji.
* Uwierzytelnianie za pomocą dowolnego klienta przy użyciu standardowego protokołu open, takich jak uwierzytelniania OAuth lub OpenID.
* Federacja z usługami katalogu przedsiębiorstwa i dostawcy tożsamości w chmurze.

## <a name="authorization-and-access-control"></a>Autoryzacji i kontroli dostępu
Po usługi Azure Active Directory uwierzytelnia użytkownika, dzięki czemu hello użytkownik może uzyskać dostęp do usługi Azure Data Lake Store, formanty autoryzacji uprawnień dostępu dla usługi Data Lake Store. Data Lake Store oddziela autoryzacji dla działań związanych z kontem i związanych z danymi w powitania po sposób:

* [Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md) (RBAC) jest dostarczany przez platformę Azure do zarządzania kontami
* Listy ACL POSIX do uzyskiwania dostępu do danych w magazynie hello

### <a name="rbac-for-account-management"></a>RBAC dla zarządzania kontem
Cztery podstawowe role są definiowane dla usługi Data Lake Store domyślnie. Witaj ról pozwala na różnych operacji na koncie usługi Data Lake Store za pomocą hello portalu Azure, poleceń cmdlet programu PowerShell i interfejsów API REST. Hello właściciela i współautor role można wykonywać różne funkcje administracji na hello konta. Można przypisać hello czytnika roli toousers, który komunikować się tylko z danymi.

![Role RBAC](./media/data-lake-store-security-overview/rbac-roles.png "role RBAC")

Należy pamiętać, że chociaż role są przypisane do zarządzania kontami, niektóre role na toodata dostępu. Należy toouse toooperations dostępu toocontrol listy kontroli dostępu, które użytkownik może wykonywać na powitania systemu plików. Witaj w poniższej tabeli przedstawia podsumowanie management rights i prawa dostępu do danych dla hello domyślne role.

| Role | Uprawnienia do zarządzania | Prawa dostępu do danych | Wyjaśnienie |
| --- | --- | --- | --- |
| Nie przypisanej roli. |Brak |Wystawianych przez listy kontroli dostępu |Witaj, użytkownik nie może używać hello Azure portalu lub Azure PowerShell polecenia cmdlet toobrowse usługi Data Lake Store. Witaj, użytkownik może korzystać tylko narzędzia wiersza polecenia. |
| Właściciel |Wszystkie |Wszystkie |Rola właściciela Hello jest administratora. Tej roli mogą zarządzać wszystkim i ma pełny dostęp toodata. |
| Czytelnik |tylko do odczytu |Wystawianych przez listy kontroli dostępu |rolę czytelnika Hello mogą przeglądać wszystko dotyczące zarządzania kontami, takie jak użytkownik jest przypisany toowhich roli. rolę czytelnika Hello nie wprowadzać zmian. |
| Współautor |Wszystkie z wyjątkiem dodawania i usuwania ról |Wystawianych przez listy kontroli dostępu |Rola współautora Hello można zarządzać niektórych aspektów konta, takich jak wdrożenia i tworzenie i Zarządzanie alertami. Rola współautora Hello nie można dodać lub usunąć role. |
| Administrator dostępu użytkowników |Dodawanie i usuwanie ról |Wystawianych przez listy kontroli dostępu |Witaj roli Administrator dostępu użytkowników można zarządzać tooaccounts dostępu użytkownika. |

Aby uzyskać instrukcje, zobacz [przypisać tooData Lake — magazyn kont użytkowników lub grup zabezpieczeń](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Przy użyciu listy ACL dla operacji w systemach plików
Data Lake Store jest systemem plików hierarchiczna jak Hadoop Distributed pliku System (HDFS) i obsługuje [listy ACL POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Kontroluje odczytu (r), zapisu (w) i wykonywania (tooresources uprawnienia hello właściciela roli, grupy Właściciele hello i dla innych użytkowników i grup x). W hello Data Lake magazynu publicznej wersji zapoznawczej (hello bieżącej wersji) można włączyć listy kontroli dostępu w folderze głównym hello, podfoldery i poszczególnych plików. Aby uzyskać więcej informacji na temat sposobu działania list kontroli dostępu w kontekście usługi Data Lake Store, zobacz [Kontrola dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).

Firma Microsoft zaleca definiować listy ACL dla wielu użytkowników za pomocą [grup zabezpieczeń](../active-directory/active-directory-accessmanagement-manage-groups.md). Dodaj grupy zabezpieczeń użytkownicy tooa, a następnie przypisz hello listy kontroli dostępu dla grupy zabezpieczeń toothat pliku lub folderu. Jest to przydatne należy tooprovide niestandardowych dostępu, ponieważ są ograniczone tooadding maksymalnie dziewięć wpisy dla niestandardowych dostępu. Aby uzyskać więcej informacji o sposobie toobetter zabezpieczyć dane przechowywane w usłudze Data Lake Store przy użyciu grup zabezpieczeń usługi Azure Active Directory, zobacz [Przypisz użytkowników lub grupy zabezpieczeń jako toohello listy ACL systemu plików usługi Azure Data Lake Store](data-lake-store-secure-data.md#filepermissions).

![Lista dostępu standardowe i niestandardowe](./media/data-lake-store-security-overview/adl.acl.2.png "listy dostępu standardowe i niestandardowe")

## <a name="network-isolation"></a>Izolacja sieci
Przechowywać dane tooyour Użyj Data Lake Store toohelp kontroli dostępu na poziomie sieci hello. Można ustanowić zapory i zdefiniować zakres adresów IP dla zaufanych klientów. Zakres adresów IP tylko klientów, którzy mają adres IP zakresu hello zdefiniowane może się łączyć tooData Lake Store.

![Ustawienia zapory i IP dostępu](./media/data-lake-store-security-overview/firewall-ip-access.png "ustawienia i adres IP zapory")

## <a name="data-protection"></a>Ochrona danych
Azure Data Lake Store zapewnia ochronę danych w całym cyklu życia. Dla danych podczas przesyłania Data Lake Store używa danych toosecure protokołu hello branżowych standardów zabezpieczeń TLS (Transport Layer) za pośrednictwem sieci hello.

![Szyfrowanie w usłudze Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "szyfrowania w usłudze Data Lake Store")

Data Lake Store zapewnia również szyfrowanie danych przechowywanych w hello konta. Można wybrać toohave dane szyfrowane lub wybrać opcję bez szyfrowania. Jeśli zgłosić się do szyfrowania danych przechowywanych w usłudze Data Lake Store jest zaszyfrowanych wcześniejsze toostoring na nośniku trwałe. W takim przypadku Data Lake Store szyfruje toopersisting wcześniejszych danych i automatycznie odszyfrowuje tooretrieval wcześniejszych danych, dzięki czemu podczas uzyskiwania dostępu do danych powitania klienta toohello całkowicie niewidoczne. Nie ma żadnej zmiany kodu, wymagane na powitania klienta po stronie tooencrypt/odszyfrowywania danych.

Zarządzania kluczami Data Lake Store zapewnia dwa tryby zarządzania kluczy szyfrowania głównego (MEKs), które są wymagane do odszyfrowywania danych przechowywanych w hello usługi Data Lake Store. Można albo programowi Data Lake Store Zarządzanie hello MEKs, lub wybierz własność tooretain MEKs hello przy użyciu konta usługi Azure Key Vault. Należy określić tryb hello zarządzania kluczami podczas podczas tworzenia konta usługi Data Lake Store. Aby uzyskać więcej informacji na temat konfiguracji tooprovide związane z szyfrowaniem, zobacz [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Dzienniki inspekcji i diagnostyczne
Można użyć dzienników inspekcji lub diagnostycznych, w zależności od tego, czy jest wyświetlany dla dzienników dla działań związanych z zarządzaniem lub działań związanych z danymi.

* Działania związane z zarządzania przy użyciu interfejsów API Menedżera zasobów Azure i są udostępniane w hello portalu Azure za pomocą dzienników inspekcji.
* Działania związane z danymi przy użyciu interfejsów API REST WebHDFS i są udostępniane w hello portalu Azure za pomocą dzienników diagnostycznych.

### <a name="auditing-logs"></a>Dzienniki inspekcji
toocomply z przepisami, organizacja może wymagać wykonywania odpowiednich audytu wymaga toodig na określone zdarzenia. Data Lake Store ma wbudowaną funkcję monitorowania i przeprowadzania inspekcji i rejestruje wszystkie działania związane z zarządzaniem konta.

Zapisy inspekcji zarządzania kontem, przeglądanie i wybierz hello kolumny, które mają toolog. Można także wyeksportować tooAzure dzienniki inspekcji magazynu.

![Dzienniki inspekcji](./media/data-lake-store-security-overview/audit-logs.png "Dzienniki inspekcji")

### <a name="diagnostic-logs"></a>Dzienniki diagnostyczne
Można ustawić zapisy inspekcji dostępu do danych w hello portalu Azure (w ustawieniach diagnostycznych) i tworzyć konta magazynu obiektów Blob platformy Azure, gdzie są przechowywane dzienniki hello.

![Dzienniki diagnostyczne](./media/data-lake-store-security-overview/diagnostic-logs.png "dzienniki diagnostyczne")

Po skonfigurowaniu ustawień diagnostycznych hello dzienniki można wyświetlać na powitania **dzienników diagnostycznych** kartę.

Aby uzyskać więcej informacji na temat pracy z dzienników diagnostycznych z usługi Azure Data Lake Store, zobacz [dostęp do dzienników diagnostycznych dla usługi Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Podsumowanie
Klienci korporacyjni wymaga platformy chmury analizy danych, który jest bezpieczne i łatwe toouse. Azure Data Lake Store jest przeznaczona toohelp spełnić te wymagania za pośrednictwem zarządzania tożsamościami i uwierzytelniania za pomocą integracji Azure Active Directory, autoryzacji na podstawie listy ACL, izolacji sieci, szyfrowanie danych przesyłanych i przechowywanych (przychodzących hello przyszłe) i inspekcji.

Jeśli chcesz toosee nowych funkcji w usłudze Data Lake Store, Prześlij nam swoją opinię w hello [forum usługi Data Lake magazynu UserVoice](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Rozpoczynanie pracy z usługą Data Lake Store](data-lake-store-get-started-portal.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)

