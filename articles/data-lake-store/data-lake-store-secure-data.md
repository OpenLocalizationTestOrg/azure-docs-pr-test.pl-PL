---
title: "aaaSecuring danych przechowywanych w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosecure danych w usłudze Azure Data Lake Store przy użyciu grup i dostępu kontrolować list"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Zabezpieczanie danych przechowywanych w usłudze Azure Data Lake Store
Zabezpieczanie danych w usłudze Azure Data Lake Store jest podejście trzech etapów.

1. Rozpocznij od utworzenia grupy zabezpieczeń w usłudze Azure Active Directory (AAD). Te grupy zabezpieczeń są używane tooimplement kontroli dostępu opartej na rolach (RBAC) w portalu Azure. Aby uzyskać więcej informacji, zobacz [opartej na rolach kontroli dostępu w systemie Microsoft Azure](../active-directory/role-based-access-control-configure.md).
2. Przypisywanie konta Azure Data Lake Store toohello grup hello AAD zabezpieczeń. Kontroluje do konta usługi Data Lake Store toohello dostępu do operacji zarządzania i portalu hello z portalu hello lub interfejsów API.
3. Listy kontroli dostępu (ACL) w systemie plików usługi Data Lake Store hello przypisywać grup zabezpieczeń usługi AAD hello.
4. Ponadto można również ustawić zakresu adresów IP dla klientów, którzy mają dostęp do danych hello w usłudze Data Lake Store.

Ten artykuł zawiera instrukcje jak toouse hello hello Azure tooperform portalu powyżej zadania. Aby uzyskać szczegółowe informacje na temat jak Data Lake Store implementuje zabezpieczeń na poziomie konta i dane hello, zobacz [zabezpieczeń w usłudze Azure Data Lake Store](data-lake-store-security-overview.md). Aby szczegółowo informacji na temat sposobu implementacji listy kontroli dostępu w usłudze Azure Data Lake Store, zobacz [Omówienie kontroli dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Utwórz grupy zabezpieczeń w usłudze Azure Active Directory
Aby uzyskać instrukcje dotyczące grup zabezpieczeń usługi AAD toocreate i w jaki sposób tooadd grupy toohello użytkowników, zobacz [Zarządzanie grupami zabezpieczeń w usłudze Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> Można dodać użytkowników i grupy tooa innych grup w usłudze Azure AD przy użyciu hello portalu Azure. Jednak w kolejności tooadd grupy tooa głównej usługi, użyj [moduł PowerShell usługi Azure AD](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Przypisywanie użytkowników lub grup zabezpieczeń kont usługi Data Lake Store tooAzure
Przypisywanie użytkowników lub grup zabezpieczeń, kont usługi Data Lake Store tooAzure, możesz kontrolować dostęp do operacji zarządzania toohello na konto hello przy użyciu hello portalu Azure i interfejsów API usługi Azure Resource Manager. 

1. Otwieranie konta usługi Azure Data Lake Store. W okienku po lewej stronie powitania kliknij **Przeglądaj**, kliknij przycisk **usługi Data Lake Store**, a następnie w bloku Data Lake Store hello, kliknij toowhich nazwy konta hello ma tooassign użytkownikowi lub grupie zabezpieczeń.

2. W bloku ustawienia konta usługi Data Lake Store, kliknij przycisk **kontroli dostępu (IAM)**. Blok Hello przez domyślne listy **Administratorzy subskrypcji** grupy jako właściciela.
   
    ![Przypisz konta Data Lake Store tooAzure grupy zabezpieczeń](./media/data-lake-store-secure-data/adl.select.user.icon.png "Przypisz konta Data Lake Store tooAzure grupy zabezpieczeń")

    Istnieją dwa sposoby tooadd grupy i przypisz odpowiednie role.
   
    * Dodaj konto użytkownika/grupy toohello, a następnie przypisz rolę, lub
    * Dodaj rolę, a następnie przypisz toorole użytkowników i grup.
     
    W tej sekcji opisano hello pierwszego podejścia, dodawanie grupy, a następnie przypisywanie ról. Można wykonać podobne kroki toofirst wybierz rolę, a następnie przypisać rolę toothat grup.
4. W hello **użytkowników** bloku, kliknij przycisk **Dodaj** tooopen hello **Dodawanie dostępu** bloku. W hello **Dodawanie dostępu** bloku, kliknij przycisk **wybierz rolę**, a następnie wybierz rolę do grupy użytkowników hello.
   
    ![Dodaj rolę dla użytkownika hello](./media/data-lake-store-secure-data/adl.add.user.1.png "Dodaj rolę dla użytkownika hello")
   
    Witaj **właściciela** i **współautora** roli zapewniają dostęp do różnych tooa funkcji administracyjnych na hello konta usługi data lake. Dla użytkowników, którzy będą interakcji z danymi w usłudze data lake hello, możesz je dodać toohello ** czytnika ** roli. Hello zakres tych ról jest ograniczona toohello zarządzania operacji powiązanych toohello konta usługi Azure Data Lake Store.
   
    Dla danych uprawnienia systemu plików poszczególnych działań zdefiniować, co mogą zrobić użytkownicy hello. W związku z tym użytkownika mającego rolę czytelnika można tylko widok ustawień administracyjnych skojarzonych z kontem hello, ale może potencjalnie odczytu i zapisu danych oparte na toothem przypisane uprawnienia systemu plików. Uprawnienia systemu plików usługi Data Lake Store są opisane w [przypisanie grupy zabezpieczeń toohello listy ACL systemu plików usługi Azure Data Lake Store](#filepermissions).
5. W hello **Dodawanie dostępu** bloku, kliknij przycisk **dodawania użytkowników** tooopen hello **dodawania użytkowników** bloku. W tym bloku Wyszukaj grupę zabezpieczeń hello utworzonego wcześniej w usłudze Azure Active Directory. Jeśli masz wiele grup toosearch z używania pola tekstowego hello w górnym toofilter hello na powitania Nazwa grupy. Kliknij pozycję **Wybierz**.
   
    ![Dodaj grupę zabezpieczeń](./media/data-lake-store-secure-data/adl.add.user.2.png "Dodaj grupę zabezpieczeń")
   
    Jeśli chcesz tooadd grupy/użytkownika, który nie ma na liście, można zaprosić je przy użyciu hello **zaprosić** ikony, jak i określenie adresu e-mail hello grupy użytkownika hello.
6. Kliknij przycisk **OK**. Powinny pojawić się grupy zabezpieczeń hello dodane w sposób przedstawiony poniżej.
   
    ![Dodaje grupę zabezpieczeń](./media/data-lake-store-secure-data/adl.add.user.3.png "dodać grupę zabezpieczeń")

7. Grupy zabezpieczeń użytkowników/ma teraz konto usługi Azure Data Lake Store toohello dostępu. Jeśli chcesz tooprovide dostępu toospecific użytkownicy, można dodać je toohello grupy zabezpieczeń. Podobnie Chcąc toorevoke dostępu dla użytkownika, można je usunąć z grupy zabezpieczeń hello. Można także przypisać wiele grup zabezpieczeń tooan konta. 

## <a name="filepermissions"></a>Przypisywanie użytkowników lub grupy zabezpieczeń jako toohello listy ACL systemu plików usługi Azure Data Lake Store
Przypisując użytkownika/zabezpieczeń systemu plików usługi Azure Data Lake toohello, należy ustawić kontroli dostępu na powitania danych przechowywanych w usłudze Azure Data Lake Store.

1. W bloku konta usługi Data Lake Store kliknij pozycję **Eksplorator danych**.
   
    ![Tworzenie katalogów w ramach konta usługi Data Lake Store](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Tworzenie katalogów w ramach konta usługi Data Lake")
2. W hello **Eksploratora danych** bloku, kliknij hello plik lub folder, dla którego chcesz hello tooconfigure listy ACL, a następnie kliknij **dostępu**. Plik tooa ACL tooassign, należy kliknąć opcję **dostępu** z hello **podglądu pliku** bloku.
   
    ![Ustaw listy kontroli dostępu w systemie plików usługi Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Ustaw listy kontroli dostępu w systemie plików usługi Data Lake")
3. Witaj **dostępu** bloku wymieniono hello standardowy dostęp i niestandardowe dostępu jest już przypisany toohello głównego. Kliknij przycisk hello **Dodaj** Poziom niestandardowy ikona tooadd listy kontroli dostępu.
   
    ![Lista dostępu standardowe i niestandardowe](./media/data-lake-store-secure-data/adl.acl.2.png "listy dostępu standardowe i niestandardowe")
   
   * **Standardowy dostęp** jest hello dostępu typu UNIX, której możesz określić odczytu, zapisu, wykonywania klasy unikatowych użytkowników toothree (rwx): właściciela, grupy i inne.
   * **Niestandardowe dostępu** odpowiada toohello POSIX listy kontroli dostępu, umożliwiający tooset uprawnienia dla określonych użytkowników o nazwie lub grupy, a nie tylko hello właściciela pliku lub grupy. 
     
     Aby uzyskać więcej informacji, zobacz [listy ACL systemu plików HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Aby uzyskać więcej informacji dotyczących sposobu implementacji listy kontroli dostępu w usłudze Data Lake Store, zobacz [kontroli dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).
4. Kliknij przycisk hello **Dodaj** hello tooopen ikona **dodać niestandardowe dostępu** bloku. W tym bloku, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie w **Wybieranie użytkownika lub grupy** bloku, wyszukaj grupę zabezpieczeń hello został utworzony wcześniej w usłudze Azure Active Directory. Jeśli masz wiele grup toosearch z używania pola tekstowego hello w górnym toofilter hello na powitania Nazwa grupy. Kliknij grupę hello tooadd a następnie kliknij przycisk **wybierz**.
   
    ![Dodaj grupę](./media/data-lake-store-secure-data/adl.acl.3.png "Dodaj grupę")
5. Kliknij przycisk **wybierz uprawnienia**, wybierz hello uprawnienia i czy ma uprawnienia hello tooassign domyślnie ACL dostępu do listy kontroli dostępu i/lub. Kliknij przycisk **OK**.
   
    ![Przypisz uprawnienia toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "przypisać uprawnienia toogroup")
   
    Aby uzyskać więcej informacji na temat uprawnień w usłudze Data Lake Store i dostęp do i domyślnej listy kontroli dostępu, zobacz [kontroli dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).
6. W hello **dodać niestandardowe dostępu** bloku, kliknij przycisk **OK**. Witaj nowo dodanych grupy z uprawnieniami hello skojarzone będzie teraz wyświetlany w hello **dostępu** bloku.
   
    ![Przypisz uprawnienia toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "przypisać uprawnienia toogroup")
   
   > [!IMPORTANT]
   > W bieżącej wersji hello, może być tylko 9 wpisy w **dostępu niestandardowe**. Aby użytkownicy tooadd więcej niż 9, należy utworzyć grupy zabezpieczeń, Dodaj grupy toosecurity użytkowników, dodawanie uzyskanie dostępu do grupy zabezpieczeń toothose na powitania konta usługi Data Lake Store.
   > 
   > 
7. W razie potrzeby można również zmodyfikować uprawnienia dostępu powitania po dodaniu grupy hello. Hello zwykłego lub wybierz pole wyboru dla każdego uprawnienia, wpisz (Odczyt, zapis, wykonanie) oparte na czy chcesz tooremove lub przypisać tę grupę zabezpieczeń toohello uprawnienia. Kliknij przycisk **zapisać** toosave zmiany hello, lub **odrzucić** tooundo hello zmiany.

## <a name="set-ip-address-range-for-data-access"></a>Ustaw zakres adresów IP dla dostępu do danych
Azure Data Lake Store umożliwia toofurther blokowania dostępu do magazynu danych tooyour na poziomie sieci. Można włączyć zapory, podaj adres IP lub zdefiniuj zakres adresów IP dla zaufanych klientów. Po włączeniu tylko w przypadku klientów, którzy mają adresy IP hello zdefiniowanego zakresu można połączyć toohello magazynu.

![Ustawienia zapory i IP dostępu](./media/data-lake-store-secure-data/firewall-ip-access.png "ustawienia i adres IP zapory")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Usuwanie grupy zabezpieczeń dla konta usługi Azure Data Lake Store
Po usunięciu grupy zabezpieczeń z konta usługi Azure Data Lake Store zmieniany jest tylko operacje zarządzania toohello dostępu na koncie hello przy użyciu hello portalu Azure i interfejsów API usługi Azure Resource Manager.

1. W bloku konta usługi Data Lake Store, kliknij przycisk **ustawienia**. Z hello **ustawienia** bloku, kliknij przycisk **użytkowników**.
   
    ![Przypisz konta Data Lake tooAzure grupy zabezpieczeń](./media/data-lake-store-secure-data/adl.select.user.icon.png "Przypisz konta Data Lake tooAzure grupy zabezpieczeń")
2. W hello **użytkowników** bloku kliknij grupę zabezpieczeń hello ma tooremove.
   
    ![Tooremove grupy zabezpieczeń](./media/data-lake-store-secure-data/adl.add.user.3.png "tooremove grupy zabezpieczeń")
3. W bloku hello hello grupy zabezpieczeń, kliknij przycisk **Usuń**.
   
    ![Grupa zabezpieczeń usunięte](./media/data-lake-store-secure-data/adl.remove.group.png "usunięta grupa zabezpieczeń")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Usuń grupę zabezpieczeń listy kontroli dostępu w systemie plików usługi Azure Data Lake Store
Po usunięciu grupy zabezpieczeń listy kontroli dostępu w systemie plików usługi Azure Data Lake Store możesz zmienić dane toohello dostępu w hello usługi Data Lake Store.

1. W bloku konta usługi Data Lake Store kliknij pozycję **Eksplorator danych**.
   
    ![Tworzenie katalogów w ramach konta usługi Data Lake](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Tworzenie katalogów w ramach konta usługi Data Lake")
2. W hello **Eksploratora danych** bloku, kliknij hello plik lub folder, dla której ma zostać hello tooremove listy ACL, a następnie w bloku konta, kliknij przycisk hello **dostępu** ikony. tooremove listy ACL dla pliku, należy kliknąć opcję **dostępu** z hello **podglądu pliku** bloku.
   
    ![Ustaw listy kontroli dostępu w systemie plików usługi Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Ustaw listy kontroli dostępu w systemie plików usługi Data Lake")
3. W hello **dostępu** bloku z hello **dostępu niestandardowe** kliknij opcję grupy zabezpieczeń hello ma tooremove. W hello **dostępu niestandardowe** bloku, kliknij przycisk **Usuń** , a następnie kliknij przycisk **OK**.
   
    ![Przypisz uprawnienia toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "przypisać uprawnienia toogroup")

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
* [Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Wprowadzenie do usługi Data Lake Store za pomocą programu PowerShell](data-lake-store-get-started-powershell.md)
* [Wprowadzenie do usługi Data Lake Store przy użyciu zestawu .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Dostęp do dzienników diagnostycznych usługi Data Lake Store](data-lake-store-diagnostic-logs.md)

