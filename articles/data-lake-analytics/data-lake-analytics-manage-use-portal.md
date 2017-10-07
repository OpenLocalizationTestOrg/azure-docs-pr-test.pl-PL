---
title: "aaaManage Azure Data Lake Analytics przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage kont usługi Data Lake Analytics, danych źródła, użytkowników i zadania."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Zarządzanie usługą Azure Data Lake Analytics przy użyciu hello portalu Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Dowiedz się, jak toomanage kont usługi Azure Data Lake Analytics, źródłami danych konta użytkowników i zadań za pomocą hello portalu Azure. Tematy dotyczące zarządzania toosee o przy użyciu innych narzędzi, kliknij kartę u góry hello hello strony.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Zarządzanie kontami usługi Data Lake Analytics

### <a name="create-an-account"></a>Tworzenie konta usługi

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **Nowy** > **Zbieranie danych i analiza** > **Data Lake Analytics**.
3. Wybierz wartości hello następujące elementy: 
   1. **Nazwa**: Nazwa hello hello konta usługi Data Lake Analytics.
   2. **Subskrypcja**: hello używane jako konto hello subskrypcji platformy Azure.
   3. **Grupa zasobów**: hello grupy zasobów platformy Azure, w które konto hello toocreate. 
   4. **Lokalizacja**: hello centrum danych Azure dla konta usługi Data Lake Analytics hello. 
   5. **Data Lake Store**: hello toobe magazynu domyślne używane jako konto usługi Data Lake Analytics hello. Konto usługi Azure Data Lake Store Hello i hello musi należeć do konta usługi Data Lake Analytics hello tej samej lokalizacji.
4. Kliknij przycisk **Utwórz**. 

### <a name="delete-a-data-lake-analytics-account"></a>Usuwanie konta usługi Data Lake Analytics

Aby usunąć konto usługi Data Lake Analytics, usuń jego domyślne konto usługi Data Lake Store.

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij polecenie **Usuń**.
3. Nazwa konta hello typu.
4. Kliknij polecenie **Usuń**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Zarządzaj źródłami danych

Data Lake Analytics obsługuje hello następujące źródła danych:

* Data Lake Store
* Azure Storage

Można używać źródeł danych toobrowse Eksploratora danych i wykonywać operacje zarządzania pliku podstawowego. 

### <a name="add-a-data-source"></a>Dodawanie źródła danych

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij przycisk **źródeł danych**.
3. Kliknij przycisk **Dodaj źródło danych**.
    
   * tooadd konto usługi Data Lake Store, musisz mieć konto hello toohello nazwy i dostępu do konta toobe tooquery mogli go.
   * tooadd magazynu obiektów Blob platformy Azure, należy hello konto magazynu i klucza konta hello. toofind konta magazynu toohello ich, przejdź w portalu hello.

## <a name="set-up-firewall-rules"></a>Konfigurowanie reguł zapory

Data Lake Analytics toofurther blokowania tooyour dostępu do konta usługi Data Lake Analytics można użyć na poziomie sieci hello. Można włączyć zapory, podaj adres IP lub zdefiniuj zakres adresów IP dla zaufanych klientów. Po włączeniu tych środków tylko klientów, którzy mają hello adresów IP w zakresie hello zdefiniowane można połączyć toohello magazynu.

Jeśli innymi usługami Azure, takich jak fabryki danych Azure lub maszyn wirtualnych, połączyć konto usługi Data Lake Analytics toohello, upewnij się, że **Zezwalaj usług Azure** włączono **na**. 

### <a name="set-up-a-firewall-rule"></a>Konfigurowanie reguł zapory

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Polecenie hello menu po lewej stronie powitania **zapory**.

## <a name="add-a-new-user"></a>Dodaj nowego użytkownika

Można użyć hello **Kreatora dodawania użytkownika** tooeasily obsługi administracyjnej nowych użytkowników do usługi Data Lake.

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Na powitania po lewej, w obszarze **wprowadzenie**, kliknij przycisk **Kreatora dodawania użytkownika**.
3. Wybierz użytkownika, a następnie kliknij przycisk **wybierz**.
4. Wybierz rolę, a następnie kliknij przycisk **wybierz**. tooset się nowych toouse dewelopera usługi Azure Data Lake, wybierz hello **Data Lake Analytics Developer** roli.
5. Wybierz z listy kontroli dostępu hello (kontroli dostępu ACL) dla baz danych hello U-SQL. Po zakończeniu wybrane opcje, kliknij przycisk **wybierz**.
6. Wybierz hello listy kontroli dostępu dla plików. Witaj domyślny magazyn, nie zmieniaj hello listy kontroli dostępu dla folderu głównego hello "/" i hello/system folderu. Kliknij pozycję **Wybierz**.
7. Przejrzyj wybrane ustawienia, a następnie kliknij przycisk **Uruchom**.
8. Po zakończeniu pracy Kreatora powitania kliknij przycisk **gotowe**.

## <a name="manage-role-based-access-control"></a>Zarządzanie kontrolą dostępu opartą na rolach

Podobnie jak innymi usługami Azure można użyć toocontrol kontroli dostępu opartej na rolach (RBAC) interakcji użytkowników z usługą hello.

standardowe role RBAC Hello mają hello następujące możliwości:
* **Właściciel**: można przesyłania zadań, monitorowania zadań anulować zadania z dowolnego użytkownika i skonfigurować konto hello.
* **Współautor**: można przesyłania zadań, monitorowania zadań anulować zadania z dowolnego użytkownika i skonfigurować konto hello.
* **Czytnik**: można monitorować zadania.

Za pomocą hello Data Lake Analytics Developer roli tooenable U-SQL deweloperzy toouse hello usługi Data Lake Analytics usługi. Program hello Data Lake Analytics Developer rolę:
* Przesyłanie zadań.
* Monitorowania stanu i hello postępu zadania zadań wysłanego przez każdego użytkownika.
* Zobacz hello skryptów U-SQL z zadań wysłanego przez każdego użytkownika.
* Anulowanie tylko własnych zadań.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Dodaj użytkowników lub tooa grup zabezpieczeń konta usługi Data Lake Analytics

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij przycisk **(IAM) kontroli dostępu** > **Dodaj**.
3. Wybierz rolę.
4. Dodawanie użytkownika.
5. Kliknij przycisk **OK**.

>[!NOTE]
>Jeśli użytkownik lub grupa zabezpieczeń wymaga toosubmit zadań, muszą uprawnienie hello konta magazynu. Aby uzyskać więcej informacji, zobacz [zabezpieczyć dane przechowywane w usłudze Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Zarządzanie zadaniami

### <a name="submit-a-job"></a>Prześlij zadanie

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.

2. Kliknij przycisk **nowe zadanie**. Dla każdego zadania należy skonfigurować:

    1. **Nazwa zadania**: Nazwa hello hello zadania.
    2. **Priorytet**: niższych numerach mają wyższy priorytet. Dwa zadania są umieszczane w kolejce, pierwszy uruchamia hello jedną z niższą wartość priorytetu.
    3. **Równoległość**: Maksymalna liczba obliczeń hello procesów tooreserve dla tego zadania.

3. Kliknij przycisk **Prześlij zadanie**.

### <a name="monitor-jobs"></a>Monitorowanie zadań

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij przycisk **wyświetlić wszystkie zadania**. Listy wszystkich hello active i ostatnio zakończonych zadań na koncie hello jest wyświetlany.
3. Opcjonalnie kliknij **filtru** toohelp znaleźć hello zadania według **zakres czasu**, **Nazwa zadania**, i **autora** wartości. 

### <a name="monitoring-pipeline-jobs"></a>Monitorowanie zadań w potoku
Zadania, które są częścią potoku działają razem, zwykle po kolei, tooaccomplish danego scenariusza. Na przykład można mieć potok, który czyści, wyodrębnianie, przekształca, agreguje użycia klienta szczegółowe informacje o. Potok zadania są identyfikowane za pomocą właściwości "Potoku" hello, gdy hello zadanie zostało przesłane. Zadania zaplanowane przy użyciu fabryki danych AZURE w wersji 2 ma automatycznie tej właściwości wypełnione. 

tooview listę zadań U-SQL, które są częścią potoków: 

1. W hello portalu Azure Przejdź tooyour kont usługi Data Lake Analytics.
2. Kliknij przycisk **zadania Insights**. powitalne kartę "Wszystkie zadania" zostanie przywrócona domyślna, przedstawiający listę uruchomiona, w kolejce i zakończenia zadania.
3. Kliknij przycisk hello **zadania potoku** kartę. Lista zadań potoku pojawi się wraz z zagregowanych danych statystycznych dla każdego potoku.

### <a name="monitoring-recurring-jobs"></a>Monitorowanie zadań cyklicznych
Cyklicznych zadań to taki, który ma hello tej samej logiki biznesowej, ale używa innego danych wejściowych każdym uruchomieniu. W idealnym przypadku cyklicznych zadań należy zawsze powiodło się i mają względnie stały czas wykonania; monitorowanie zachowania te pomogą upewnij się, że zadanie hello jest w dobrej kondycji. Cykliczne zadania są identyfikowane za pomocą właściwości "Cyklu" hello. Zadania zaplanowane przy użyciu fabryki danych AZURE w wersji 2 ma automatycznie tej właściwości wypełnione.

tooview listę zadań U-SQL, które są cykliczne: 

1. W hello portalu Azure Przejdź tooyour kont usługi Data Lake Analytics.
2. Kliknij przycisk **zadania Insights**. powitalne kartę "Wszystkie zadania" zostanie przywrócona domyślna, przedstawiający listę uruchomiona, w kolejce i zakończenia zadania.
3. Kliknij przycisk hello **cyklicznych zadań** kartę. Lista zadań cyklicznych pojawi się wraz z zagregowanych danych statystycznych dla każdego zadania cyklicznego.

## <a name="manage-policies"></a>Zarządzanie zasadami

### <a name="account-level-policies"></a>Zasady na poziomie konta

Te zasady są stosowane tooall zadań w ramach konta usługi Data Lake Analytics.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Maksymalna liczba AUs w ramach konta usługi Data Lake Analytics
Zasady regulują hello łączną liczbę jednostek Analytics (AUs), można użyć konta usługi Data Lake Analytics. Domyślnie wartość hello jest ustawiana too250. Na przykład, jeśli ta wartość jest ustawiana too250 AUs, program może jedno zadanie uruchomione z 250 tooit AUs przypisane lub 10 zadań uruchamianych z 25 AUs każdego. Dodatkowe zadania, które są przesyłane są umieszczane w kolejce zakończenie hello uruchomionych zadań. Po zakończeniu są wykonywane zadania dla hello są zwalniane AUs toorun zadań w kolejce.

toochange hello liczba AUs dla Twojego konta usługi Data Lake Analytics:

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij pozycję **Właściwości**.
3. W obszarze **maksymalna AUs**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello. 
4. Kliknij pozycję **Zapisz**.

> [!NOTE]
> Jeśli użytkownik należy większej hello domyślne (250) AUs, w portalu powitania kliknij **pomoc + Obsługa** toosubmit żądania pomocy technicznej. można zwiększyć liczbę Hello AUs dostępne w ramach konta usługi Data Lake Analytics.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Maksymalna liczba zadań, które można uruchomić jednocześnie
Zasady regulują, jak wiele zadań można uruchomić na powitania tym samym czasie. Domyślnie ta wartość jest ustawiana too20. Jeśli usługi Data Lake Analytics ma AUs dostępne, nowe zadania są zaplanowane toorun do momentu hello całkowita liczba uruchomionych zadań osiągnie wartość hello niniejszych zasad. Po osiągnięciu hello maksymalna liczba zadań, które można uruchomić jednocześnie, kolejne zadania są umieszczane w kolejce w kolejności priorytetu do momentu ukończenia co najmniej jedno zadanie uruchomione (w zależności od dostępności Australia).

toochange hello liczba zadań, które można uruchomić jednocześnie:

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij pozycję **Właściwości**.
3. W obszarze **maksymalny numer z uruchomione zadania**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello. 
4. Kliknij pozycję **Zapisz**.

> [!NOTE]
> Jeśli potrzebujesz więcej niż hello domyślne (20) liczba zadań, w portalu powitania kliknij toorun **pomoc + Obsługa** toosubmit żądania pomocy technicznej. można zwiększyć Hello liczba zadań, które można uruchomić jednocześnie w ramach konta usługi Data Lake Analytics.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>Jak długo tookeep zadania metadanych i zasoby 
Po wykonaniu zadań U-SQL hello usługi Data Lake Analytics zachowuje wszystkie powiązane pliki. Powiązane pliki obejmują skrypt hello U-SQL, pliki DLL hello w skryptu U-SQL hello, skompilowanych zasobów i statystyki. pliki Hello znajdują się w folderze /system/ hello hello domyślnego konta usługi Azure Data Lake Storage. Ta zasada kontroluje, jak długo są przechowywane tych zasobów, zanim zostaną automatycznie usunięte (hello domyślny to 30 dni). Debugowanie i dostrajania wydajności zadań, które będzie ponownie w przyszłości hello można używać tych plików.

toochange jak długo tookeep zadania metadanych i zasoby:

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij pozycję **Właściwości**.
3. W obszarze **tooRetain dni zadanie odpytuje**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello.  
4. Kliknij pozycję **Zapisz**.

### <a name="job-level-policies"></a>Zasady na poziomie zadania
Z zasady na poziomie zadania, można kontrolować hello AUs maksymalna i maksymalny priorytet poszczególnych użytkowników (lub członków określonych grup zabezpieczeń), które można ustawić dla zadania, które przesyłają hello. To pozwala na kontrolowanie hello kosztów ponoszonych przez użytkowników. Umożliwia również kontroli hello wpływ, jaki zaplanowane zadania może być na wysoki priorytet zadania produkcji, które działają w hello tego samego konta usługi Data Lake Analytics.

Data Lake Analytics ma dwie zasady, które można ustawić na poziomie zadania hello:

* **Australia limit dla zadania**: użytkownicy, można kierować tylko zadania, które mają toothis liczby AUs. Domyślnie ten limit jest hello taki sam jak hello maksymalny limit Australia hello konta.
* **Priorytet**: użytkownicy, można kierować tylko zadania, które mają wartość priorytetu toothis mniejsze niż lub równe. Należy pamiętać, że większa liczba oznacza o niższym priorytecie. To jest domyślnie too1, która jest hello najwyższy możliwy priorytet.

Brak domyślnych zasad ustawić dla każdego konta. zasady domyślne Hello stosuje użytkowników tooall hello konta. Dodatkowe zasady można ustawić dla poszczególnych użytkowników i grup. 

> [!NOTE]
> Zasady na poziomie konta i zasad na poziomie zadania się jednocześnie.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Dodaj zasady dla określonego użytkownika lub grupy

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij pozycję **Właściwości**.
3. W obszarze **limitów przesyłanie zadań**, kliknij przycisk hello **Dodaj zasady** przycisku. Następnie wybierz lub wprowadź hello następujące ustawienia:
    1. **Obliczeniowe Nazwa zasady**: Wprowadź nazwę zasad, tooremind o celu hello hello zasad.
    2. **Wybierz użytkownika lub grupy**: Wybierz hello użytkownika lub grupy, które dotyczą te zasady.
    3. **Ustaw Limit Australia zadania hello**: hello Australia wyznaczonym stosowanym toohello wybrany użytkownik lub grupa.
    4. **Ustaw Limit priorytet hello**: Ustaw hello priorytet limit ma zastosowanie toohello wybrany użytkownik lub grupa.

4. Kliknij przycisk **OK**.

5. nowe zasady Hello ma na liście hello **domyślne** w sekcji tabela zasad **limitów przesyłanie zadań**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Usuń lub Edytuj istniejące zasady

1. W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.
2. Kliknij pozycję **Właściwości**.
3. W obszarze **limitów przesyłanie zadań**, Znajdź hello zasady tooedit.
4.  Witaj toosee **usunąć** i **Edytuj** kliknij przycisk Opcje w prawej kolumnie tabeli hello, hello **...** .

### <a name="additional-resources-for-job-policies"></a>Dodatkowe zasoby dotyczące zasad zadania
* [Omówienie zasad wpis w blogu](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Wpis w blogu zasad na poziomie konta](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Zasady na poziomie zadania wpis w blogu](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Następne kroki

* [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu hello portalu Azure](data-lake-analytics-get-started-portal.md)
* [Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-manage-use-powershell.md)

