---
title: "Portalu Azure: tworzenie i zarządzanie puli elastycznej bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać portalu Azure i SQL Database wbudowane narzędzie analizy do zarządzania, monitorowania i skalowalnej elastycznej puli w celu zoptymalizowania wydajności bazy danych i zarządzanie nimi kosztów odpowiedniego rozmiaru."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a>Tworzenie i zarządzanie nimi puli elastycznej z portalu Azure
W tym temacie przedstawiono sposób tworzenia i zarządzania nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) z portalu Azure. Można również utworzyć i zarządzać nimi Azure pula elastyczna o [PowerShell](sql-database-elastic-pool-manage-powershell.md), interfejsu API REST lub [C#](sql-database-elastic-pool-manage-csharp.md). Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Tworzenie puli elastycznej 

Istnieją dwa sposoby tworzenia puli elastycznej. Można utworzyć ją od podstaw, znając wymagane ustawienia puli, lub uruchomić zgodnie z zaleceniami usługi. SQL Database ma wbudowane narzędzie analizy zalecane ustawienia puli elastycznej, jeśli jest to bardziej ekonomiczne na podstawie ostatnich danych telemetrii użycia baz danych.

Można utworzyć wiele pul na serwerze, ale nie można dodać bazy danych z różnych serwerów do tej samej puli. 

> [!NOTE]
> Pule elastyczne są ogólnodostępne we wszystkich regionach platformy Azure oprócz Indii Zachodnich, gdzie są obecnie dostępne w wersji zapoznawczej.  Pule elastyczne zostaną udostępnione ogólnie w tych regionach tak szybko, jak to możliwe.
>

### <a name="step-1-create-an-elastic-pool"></a>Krok 1: Tworzenie puli elastycznej

Tworzenie z istniejącej puli elastycznej **serwera** bloku w portalu jest najprostszym sposobem, aby przenieść istniejące bazy danych w puli elastycznej.

> [!NOTE]
> Można również utworzyć puli elastycznej, wyszukując **puli elastycznej SQL** w **Marketplace** lub klikając **+ Dodaj** w **puli elastycznej SQL** Przeglądaj bloku. Jesteś w stanie umożliwia określenie nowego lub istniejącego serwera do obsługi przepływu pracy w tej puli.
>
>

1. W [portalu Azure](http://portal.azure.com/), kliknij przycisk **więcej usług**  **>**  **serwerów SQL**, a następnie kliknij serwer, który zawiera bazy danych, które chcesz dodać do puli elastycznej.
2. Kliknij przycisk **Nowa pula**.

    ![Dodawanie puli na serwerze](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **— Lub —**

    Może zostać wyświetlony komunikat z informacją, że są zalecane elastyczne pule serwera. Kliknij komunikat, aby wyświetlić pule zalecane na podstawie historycznych danych telemetrycznych użycia baz danych, a następnie kliknij przycisk warstwy, aby zobaczyć więcej szczegółów i dostosować pulę. Zobacz sekcję [Pojęcie zaleceń puli](#understand-elastic-pool-recommendations) w dalszej części tego artykułu, aby dowiedzieć się, w jaki sposób tworzone są zalecenia.

    ![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. **Puli elastycznej** zostanie wyświetlony blok, czyli gdzie Określ ustawienia dla użytkownika. Jeśli kliknięto **nowej puli** w poprzednim kroku, warstwa cenowa jest **standardowe** jest wybrany domyślnie i nie baz danych. Możesz utworzyć pustą pulę lub określić zestaw istniejących baz danych z tego serwera w celu przeniesienia ich do puli. Jeśli tworzysz zalecanej puli zalecana warstwa cenowa, ustawienia wydajności i listy baz danych są wstępnie, ale nadal można je zmienić.

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Określ nazwę puli elastycznej lub pozostaw wartość domyślną.

### <a name="step-2-choose-a-pricing-tier"></a>Krok 2. Wybieranie warstwy cenowej

Warstwa cenowa puli Określa funkcje dostępne dla elastics w puli, a maksymalna liczba jednostek Edtu (maks. wartość eDTU) i dostępne dla każdej bazy danych magazynu (GB). Aby uzyskać szczegółowe informacje, zobacz Warstwy usługi.

Aby zmienić warstwę cenową dla puli, kliknij przycisk **Warstwa cenowa**, kliknij wybraną warstwę cenową, a następnie kliknij przycisk **Wybierz**.

> [!IMPORTANT]
> Po wybraniu warstwy cenowej i kliknięciu przycisku **OK** w ostatnim kroku w celu zatwierdzenia wprowadzonych zmian nie można już zmienić warstwy cenowej puli. Aby zmienić warstwę cenową istniejącej puli elastycznej, tworzenie elastycznej puli w ramach żądanej warstwy cenowej i przeprowadzić migrację bazy danych do nowej puli.
>

![Wybór warstwy cenowej](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a>Krok 3. Konfigurowanie puli

Po ustawieniu warstwy cenowej, kliknij przycisk Konfiguruj pulę, którego można dodać bazy danych, ustawić jednostki Edtu i magazyn (GB puli), a wartość minimalna i maksymalna liczba jednostek Edtu dla elastics w puli.

1. Kliknij przycisk **Konfiguruj pulę**.
2. Wybierz bazy danych, które chcesz dodać do puli. Ten krok jest opcjonalny podczas tworzenia puli. Bazy danych można dodać po jej utworzeniu.
    Aby dodać bazy danych, kliknij przycisk **Dodaj bazę danych**, kliknij bazy danych, które chcesz dodać, a następnie kliknij przycisk **Wybierz**.

    ![Dodawanie baz danych](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Jeśli bazy danych, z którymi pracujesz, mają wystarczającą ilość historycznych danych telemetrycznych dotyczących użycia, aktualizacje wykresu **Szacowany poziom użycia jednostek eDTU i GB** oraz wykresu słupkowego **Rzeczywiste użycie jednostek eDTU** ułatwiają podejmowanie decyzji związanych z konfiguracją. Ponadto usługa może ułatwić wybranie odpowiedniego rozmiaru puli, wyświetlając komunikat z zaleceniami. Patrz sekcja [Zalecenia dynamiczne](#understand-elastic-pool-recommendations).

3. Użyj elementów sterujących na stronie **Konfigurowanie puli**, aby eksplorować ustawienia i skonfigurować pulę. Zobacz [elastyczne pule limity](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) uzyskać więcej szczegółów na temat limitów dla każdej warstwy usług i zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md) Aby uzyskać szczegółowe wskazówki dotyczące doboru wielkości puli elastycznej. Aby uzyskać więcej informacji na temat ustawień puli, zobacz [właściwości puli elastycznej](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Po wprowadzeniu zmian w ustawieniach kliknij przycisk **Wybierz** w bloku **Konfigurowanie puli**.
5. Kliknij przycisk **OK**, aby utworzyć pulę.

## <a name="understand-elastic-pool-recommendations"></a>Omówienie zaleceń puli elastycznej

Usługa SQL Database ocenia historyczne dane użycia bazy danych i zaleca zastosowanie co najmniej jednej puli baz danych, jeśli okaże się, że jest to bardziej ekonomiczne rozwiązanie niż używanie pojedynczych baz danych. Każde zalecenie jest konfigurowane z unikatowym podzbiorem baz danych serwera, które są najlepiej dopasowane do puli.

![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Zalecenie puli obejmuje:

- Warstwę cenową dla puli (podstawowa, standardowa, Premium lub Premium RS)
- Odpowiednie **Jednostki eDTU PULI** (określane również jako Maks. wartość eDTU na pulę)
- **Maks. wartość eDTU** i **Min. wartość eDTU** na bazę danych
- Listę zalecanych baz danych dla puli

> [!IMPORTANT]
> Podczas rekomendowania pul usługa uwzględnia dane telemetryczne z ostatnich 30 dni. Dla bazy danych wziąć pod uwagę jako potencjalny puli elastycznej musi istnieć co najmniej 7 dni. Bazy, które znajdują się już w puli elastycznej, nie są brane pod uwagę podczas tworzenia zaleceń dla puli elastycznej.
>

Usługa oblicza zapotrzebowanie na zasoby oraz opłacalność przenoszenia pojedynczych baz danych w każdej warstwie usług do pul w tej samej warstwie. Na przykład wszystkie bazy danych w warstwie Standardowej na serwerze są oceniane pod względem dopasowania do Standardowej puli elastycznej. Oznacza to, że usługa nie tworzy zaleceń międzywarstwowych, takich jak przeniesienie bazy danych z warstwy Standardowej do puli Premium.

Po dodaniu bazy danych do puli, zalecenia są generowane dynamicznie na podstawie historycznych danych użycia wybranych baz danych. Te zalecenia są wyświetlane w jednostek eDTU i GB wykres użycia i transparent zalecenia w górnej części **Konfigurowanie puli** bloku. Zalecenia te mają na celu ułatwić tworzenie puli elastycznej zoptymalizowane pod kątem konkretnych baz danych.

![zalecenia dynamiczne](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Zarządzanie i monitorowanie puli elastycznej

Azure portal umożliwia monitorowanie i zarządzanie elastycznej puli baz danych w puli. W portalu można monitorować użycie puli elastycznej i baz danych w tej puli. Można również utworzyć zestaw zmian do puli elastycznej i Prześlij wszystkie zmiany w tym samym czasie. Te zmiany obejmują dodawanie lub usuwanie baz danych, zmiana ustawień puli elastycznej lub zmiany ustawień bazy danych.

Na poniższym rysunku przedstawiono przykład puli elastycznej. Widok zawiera:

*  Wykresy do monitorowania użycia zasobów w puli elastycznej i baz danych zawartych w puli.
*  **Konfiguruj** puli przycisk, aby wprowadzić zmiany w puli elastycznej.
*  **Utwórz bazę danych** przycisku, który tworzy bazę danych i dodaje go do bieżącej puli elastycznej.
*  Zadania elastyczne, które ułatwiają zarządzanie dużej liczby baz danych, uruchamiając skrypty Transact SQL wszystkich baz danych na liście.

![Widok puli][2]

Można przejść do określonej puli, aby wyświetlić jego wykorzystania zasobów. Domyślnie skonfigurowano puli pokazanie użycia magazynu i liczby jednostek eDTU w ciągu ostatniej godziny. Wykres można skonfigurować do wyświetlenia różnych metryk za pośrednictwem różnych okna czasowe.

1. Wybierz do pracy z puli elastycznej.
2. W obszarze **monitorowania puli elastycznej** jest wykres z etykietą **wykorzystania zasobów**. Kliknij wykres.

    ![Monitorowanie puli elastycznej][3]

    **Metryka** zostanie otwarty blok, przedstawiając wyświetlenia szczegółowych informacji o określonej metryki w określone okno czasu.   

    ![Blok metryki][9]

### <a name="to-customize-the-chart-display"></a>Aby dostosować wyświetlanie wykresu

Wykres i metryki bloku, aby wyświetlić innych metryk, takich jak procent, procent we/wy danych i dziennika we/wy procent wykorzystania procesora CPU można edytować.

1. W bloku metryki, kliknij **Edytuj**.

    ![Kliknij przycisk Edytuj][6]

2. W **Edytuj wykres** bloku, wybierz zakres czasu (Ostatnia godzina dzisiaj, lub ostatni tydzień), lub kliknij przycisk **niestandardowych** aby wybrać wszystkie zakres dat w ciągu ostatnich dwóch tygodni. Wybierz typ wykresu (paska lub linii), a następnie wybierz zasoby do monitorowania.

   > [!Note]
   > Tylko metryki z tej samej jednostki miary mogą być wyświetlane na wykresie, w tym samym czasie. Na przykład w przypadku wybrania "procent liczby jednostek eDTU" następnie można wybrać tylko innych metryk odsetku jako jednostka miary.
   >

    ![Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Następnie kliknij przycisk **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Zarządzanie i monitorowanie baz danych w puli elastycznej

Można również monitorować pojedyncze bazy danych dla potencjalne problemy.

1. W obszarze **elastycznej bazy danych monitorowania**, jest wykres przedstawia metryki pięć baz danych. Domyślnie wykresu wyświetla top 5 baz danych w puli przez użycie w jednostkach eDTU średni w ostatniej godziny. Kliknij wykres.

    ![Monitorowanie puli elastycznej][4]

2. **Wykorzystania zasobów bazy danych** zostanie wyświetlony blok. Zapewnia to szczegółowy widok użycia bazy danych w puli. Przy użyciu siatki w dolnej części bloku, można wybrać żadnych baz danych w puli, aby wyświetlić jego użycia na wykresie (maksymalnie 5 bazy danych). Można również dostosować metryki i przedziału czasowego wyświetlane na wykresie, klikając **Edytuj wykres**.

    ![Blok wykorzystanie zasobów bazy danych][8]

### <a name="to-customize-the-view"></a>Aby dostosować widok

1. W **bazy danych wykorzystania zasobów** bloku, kliknij przycisk **Edytuj wykres**.

    ![Kliknij pozycję Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. W **Edytuj** wykresu bloku, wybierz zakres czasu (Ostatnia godzina lub po 24 godzinach) lub kliknij przycisk **niestandardowych** wybierz inny dzień w ciągu ostatnich 2 tygodni do wyświetlenia.

    ![Kliknij przycisk niestandardowe](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Kliknij przycisk **porównania baz danych przez** listy rozwijanej, aby wybrać inną metrykę do używania przy porównywaniu baz danych.

    ![Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a>Aby wybrać baz danych do monitorowania

Na liście bazy danych w **wykorzystania zasobów bazy danych** bloku można znaleźć określonej bazy danych przez wyszukiwanie na stronach na liście lub wpisując nazwy bazy danych. Użyj pola wyboru, aby wybrać bazę danych.

![Wyszukaj baz danych do monitorowania][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a>Dodawanie alertu do zasobu puli elastycznej

Reguły można dodać do puli elastycznej puli elastycznej trafienia ustawiony próg użycia wysyłania wiadomości e-mail do osób lub alertu ciągów do adresu URL punktów końcowych.

**Aby dodać alert do dowolnego zasobu:**

1. Kliknij przycisk **wykorzystania zasobów** wykresu, aby otworzyć **Metryka** bloku, kliknij przycisk **Dodaj alert**, a następnie wypełnij informacje w **dodać regułę alertu** bloku (**zasobów** jest automatycznie ustawiony do pracy z puli).
2. Wpisz **nazwa** i **opis** , które identyfikują alert i adresaci.
3. Wybierz **Metryka** przewidzianą do alertów z listy.

    Wykres przedstawia dynamicznie wykorzystania zasobów dla tej metryki, pomaga wybrać progu.

4. Wybierz **warunku** (większe niż poniżej, itd.) i **próg**.
5. Wybierz **okres** czas, przez który metryki reguły muszą zostać spełnione przed wyzwalaczy alertu.
6. Kliknij przycisk **OK**.

Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Przenoszenie bazy danych w puli elastycznej

Można dodać lub usunąć bazy danych z istniejącej puli. Bazy danych może być w innych pulach. Jednak można dodawać tylko baz danych, które znajdują się na tym samym serwerze logicznym.

1. W bloku dla puli w obszarze **elastycznych baz danych** kliknij **Konfigurowanie puli**.

    ![Kliknij przycisk Konfiguruj pulę][1]

2. W **Konfigurowanie puli** bloku, kliknij przycisk **dodać do puli**.

    ![Kliknij przycisk Dodaj do puli](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. W **dodać bazy danych** bloku, wybierz bazę danych lub baz danych do dodania do puli. Następnie kliknij przycisk **wybierz**.

    ![Wybierz bazy danych do dodania](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    **Konfigurowanie puli** blok zawiera teraz bazy danych wybrane do dodania z jego stan **oczekujące**.

    ![Dodawanie puli oczekujące](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. W **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Przenoszenie bazy danych z puli elastycznej

1. W **Konfigurowanie puli** bloku, wybierz bazę danych lub baz danych do usunięcia.

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Kliknij przycisk **usunąć z puli**.

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    **Konfigurowanie puli** blok zawiera teraz bazy danych wybrane do usunięcia z jego stan **oczekujące**.

    ![Podgląd bazy danych Dodawanie i usuwanie](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. W **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Zmień ustawienia wydajności puli elastycznej

Podczas monitorowania wykorzystania zasobów w puli elastycznej może stwierdzić, że pewnych zmian są potrzebne. Może być puli wymaga zmian w granicach wydajność lub pamięć masową. Prawdopodobnie chcesz zmienić ustawienia bazy danych w puli. Ustawienia puli można zmienić w dowolnym momencie można uzyskać równowagę wydajności i kosztów. Zobacz [kiedy należy puli elastycznej użyć?](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.

Aby zmienić limitów jednostek Edtu i magazynu dla każdej puli i jednostek Edtu na bazę danych:

1. Otwórz **Konfigurowanie puli** bloku.

    W obszarze **ustawienia puli elastycznej**, za pomocą suwaka albo wprowadzenia zmian ustawień puli.

    ![Użycie zasobów w puli elastycznej](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Po zmianie ustawienia pokazuje szacowany koszt miesięczne zmiany.

    ![Aktualizacja puli elastycznej i nowych miesięczny koszt](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Czas oczekiwania operacji puli elastycznej
* Zmiana wartości min Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.
* Zmiana jednostek Edtu na pulę zależy od całkowitej ilości miejsca używanego przez wszystkie bazy danych w puli. Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB. Na przykład jeśli całkowita ilość miejsca, używany przez wszystkie bazy danych w puli jest 200 GB, oczekiwany czas oczekiwania do zmiany puli liczbę jednostek eDTU na pulę wynosi 3 godziny, a następnie lub mniej.

## <a name="next-steps"></a>Następne kroki

- Aby zrozumieć, co puli elastycznej zobacz [puli elastycznej bazy danych SQL](sql-database-elastic-pool.md).
- Aby uzyskać wskazówki dotyczące wykorzystujących pule elastyczne, zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md).
- Aby użyć zadania elastyczne umożliwiają uruchamianie skryptów języka Transact-SQL na dowolnej liczbie baz danych w puli, zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).
- Aby zapytania na dowolnej liczbie baz danych w puli, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
- Dla transakcji dowolnej liczbie baz danych w puli, zobacz [transakcji elastycznej](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
