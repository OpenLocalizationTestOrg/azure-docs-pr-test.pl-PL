---
title: "Portalu Azure: tworzenie i zarządzanie puli elastycznej bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello portalu Azure i SQL Database toomanage wbudowane narzędzie analizy, monitor i odpowiedniego rozmiaru bazy danych wydajności toooptimize skalowalnej elastycznej puli i zarządzania nimi kosztów."
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
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Tworzenie i zarządzanie nimi pula elastyczna o hello portalu Azure
W tym temacie opisano sposób toocreate i zarządzanie nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) z hello portalu Azure. Można również utworzyć i zarządzać nimi Azure pula elastyczna o [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md). Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Tworzenie puli elastycznej 

Istnieją dwa sposoby tworzenia puli elastycznej. Możesz zrobić to od początku, jeśli znasz ustawienia puli hello, lub uruchomić zgodnie z zaleceniami hello usługi. SQL Database ma wbudowane narzędzie analizy zalecane ustawienia puli elastycznej, jeśli jest to bardziej ekonomiczne na podstawie hello poza danych telemetrii użycia baz danych.

Można utworzyć wiele pul na serwerze, ale nie można dodać bazy danych z różnych serwerów do hello tej samej puli. 

> [!NOTE]
> Pule elastyczne są ogólnodostępne we wszystkich regionach platformy Azure oprócz Indii Zachodnich, gdzie są obecnie dostępne w wersji zapoznawczej.  Pule elastyczne zostaną udostępnione ogólnie w tych regionach tak szybko, jak to możliwe.
>

### <a name="step-1-create-an-elastic-pool"></a>Krok 1: Tworzenie puli elastycznej

Tworzenie z istniejącej puli elastycznej **serwera** bloku w portalu hello jest hello Najprostszym sposobem toomove istniejących baz danych w puli elastycznej.

> [!NOTE]
> Można również utworzyć puli elastycznej, wyszukując **puli elastycznej SQL** w hello **Marketplace** lub klikając **+ Dodaj** w hello **pule elastyczne SQL**Przeglądaj bloku. Jesteś toospecify stanie nowego lub istniejącego serwera do obsługi przepływu pracy w tej puli.
>
>

1. W hello [portalu Azure](http://portal.azure.com/), kliknij przycisk **więcej usług**  **>**  **serwerów SQL**, a następnie kliknij przycisk powitania serwera, który zawiera hello ma tooadd tooan elastycznej puli baz danych.
2. Kliknij przycisk **Nowa pula**.

    ![Dodaj serwer tooa puli](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **— Lub —**

    Może zostać wyświetlony komunikat z informacją, że są zalecane elastyczne pule powitania serwera. Kliknij hello toosee wiadomość hello zalecane zależności telemetrycznych użycia baz danych historycznych, a następnie kliknąć toosee warstwy hello więcej szczegółów i dostosować hello puli. Zobacz [omówienie zaleceń puli](#understand-elastic-pool-recommendations) dalszej części tego tematu dla jak hello tworzone są zalecenia.

    ![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Witaj **puli elastycznej** zostanie wyświetlony blok, czyli gdzie Określ ustawienia hello z puli. Jeśli kliknięto **nowej puli** w poprzednim kroku hello jest hello warstwy cenowej **standardowe** jest wybrany domyślnie i nie baz danych. Tworzenie puli pustych lub określ zestaw istniejących baz danych z tej toomove serwera na powitania puli. W przypadku tworzenia puli zalecana hello zalecane cenowym ustawienia wydajności i listy baz danych są wstępnie, ale nadal można je zmienić.

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Określ nazwę puli elastycznej hello, lub pozostaw domyślne hello.

### <a name="step-2-choose-a-pricing-tier"></a>Krok 2. Wybieranie warstwy cenowej

Witaj warstwa cenowa puli określa hello funkcji elastics toohello dostępne w puli hello i hello maksymalną liczbę jednostek Edtu (maks. wartość eDTU) i bazy danych dostępności tooeach magazynu (GB). Aby uzyskać szczegółowe informacje, zobacz Warstwy usługi.

Kliknij toochange hello warstwę cenową dla puli hello **warstwa cenowa**, kliknij hello cenowym, a następnie kliknij przycisk **wybierz**.

> [!IMPORTANT]
> Po wybraniu hello warstwy cenowej i zatwierdź zmiany, klikając **OK** w ostatnim kroku hello, nie będzie hello stanie toochange cenowym hello puli. toochange hello warstwę cenową istniejącej puli elastycznej, tworzenie elastycznej puli w hello żądanej warstwy cenowej i Migrowanie hello baz danych toothis nową pulę.
>

![Wybór warstwy cenowej](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Krok 3: Konfigurowanie puli hello

Po ustawieniu warstwy cenowej hello, kliknij przycisk Konfiguruj pulę, którego można dodać bazy danych, ustawić jednostki Edtu i magazyn (GB puli) oraz ustawić hello min i max jednostek Edtu dla hello elastics hello puli.

1. Kliknij przycisk **Konfiguruj pulę**.
2. Zaznacz hello bazy danych ma tooadd toohello puli. Ten krok jest opcjonalny podczas tworzenia puli hello. Po utworzeniu puli hello można dodać bazy danych.
    tooadd baz danych, kliknij przycisk **Dodaj bazę danych**, kliknij przycisk hello baz danych, że mają tooadd, a następnie kliknij przycisk hello **wybierz** przycisku.

    ![Dodawanie baz danych](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Jeśli hello baz danych, z którymi pracujesz ma za mało danych telemetrii historycznych danych użycia, hello **szacowane eDTU i GB użycia** wykresu i hello **rzeczywiste użycie jednostek eDTU** toohelp aktualizacji wykresu słupkowego wprowadzeniu konfiguracji decyzji. Ponadto hello usługi może spowodować toohelp komunikat zalecenie hello możesz odpowiedniego rozmiaru puli. Patrz sekcja [Zalecenia dynamiczne](#understand-elastic-pool-recommendations).

3. Używanie formantów hello na powitania **Konfigurowanie puli** tooexplore ustawienia strony i skonfigurować pulę. Zobacz [elastyczne pule limity](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) uzyskać więcej szczegółów na temat limitów dla każdej warstwy usług i zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md) Aby uzyskać szczegółowe wskazówki dotyczące doboru wielkości puli elastycznej. Aby uzyskać więcej informacji na temat ustawień puli, zobacz [właściwości puli elastycznej](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Kliknij przycisk **wybierz** w hello **Konfigurowanie puli** blok po zmianie ustawień.
5. Kliknij przycisk **OK** toocreate hello puli.

## <a name="understand-elastic-pool-recommendations"></a>Omówienie zaleceń puli elastycznej

Hello usługi SQL Database ocenia historyczne dane użycia i zaleca jednej lub kilku pul, gdy jest bardziej ekonomiczne rozwiązanie niż używanie pojedynczych baz danych. Każde zalecenie jest konfigurowane z unikatowym podzbiorem powitania serwera baz danych, które najlepiej odpowiadają hello puli.

![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Witaj zalecenie puli obejmuje:

- Warstwę cenową dla puli hello (Basic, Standard, Premium lub Premium RS)
- Odpowiednie **Jednostki eDTU PULI** (określane również jako Maks. wartość eDTU na pulę)
- Witaj **maks. wartość eDTU** i **min. wartość eDTU** na bazę danych
- Witaj listę zalecanych baz danych dla puli hello

> [!IMPORTANT]
> Usługa Hello uwzględnia hello ostatnich 30 dni telemetrii podczas rekomendowania pul. Dla toobe bazy danych, traktowane jako kandydatem do puli elastycznej musi istnieć co najmniej 7 dni. Bazy, które znajdują się już w puli elastycznej, nie są brane pod uwagę podczas tworzenia zaleceń dla puli elastycznej.
>

Hello usługa oblicza zapotrzebowanie na zasoby oraz opłacalność przenoszenia hello jednej bazy danych w poszczególnych warstwach usług w pulach hello sam warstwy. Na przykład wszystkie bazy danych w warstwie Standardowej na serwerze są oceniane pod względem dopasowania do Standardowej puli elastycznej. Oznacza to, że usługa hello nie tworzy zalecenia dotyczące warstwy między takich jak przeniesienie standardowe bazy danych do puli Premium.

Po dodaniu puli toohello baz danych, zalecenia są generowane dynamicznie na podstawie hello historycznych danych użycia hello baz danych, wybrana przez Ciebie. Te zalecenia są wyświetlane w hello jednostek eDTU i GB wykres użycia i transparent zalecenie u góry hello hello **Konfigurowanie puli** bloku. Te zalecenia są zamierzone tooassist można utworzyć puli elastycznej zoptymalizowane pod kątem konkretnych baz danych.

![zalecenia dynamiczne](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Zarządzanie i monitorowanie puli elastycznej

Można użyć hello toomonitor portalu Azure i zarządzać puli elastycznej i hello hello puli baz danych. Z portalu hello można monitorować użycie hello puli elastycznej i baz danych hello w tej puli. Można również utworzyć zestaw zmian tooyour puli elastycznej i Prześlij wszystkie zmiany na powitania sam czas. Te zmiany obejmują dodawanie lub usuwanie baz danych, zmiana ustawień puli elastycznej lub zmiany ustawień bazy danych.

powitania po grafika przedstawia przykład puli elastycznej. Widok Hello zawiera:

*  Wykresy do monitorowania użycia zasobów, zarówno hello puli elastycznej i hello zawartych baz danych w puli hello.
*  Witaj **Konfiguruj** puli toomake przycisku zmienia toohello puli elastycznej.
*  Witaj **Utwórz bazę danych** przycisku, który tworzy bazę danych i dodaje go toohello bieżącej puli elastycznej.
*  Zadania elastyczne, które ułatwiają zarządzanie dużej liczby baz danych, uruchamiając skrypty Transact SQL wszystkich baz danych na liście.

![Widok puli][2]

Możesz toosee określonej puli tooa jego wykorzystania zasobów. Domyślnie pula hello jest użycie magazynu i eDTU tooshow skonfigurowanych hello ostatniej godziny. Wykres Hello może być skonfigurowany tooshow różnych metryk za pośrednictwem różnych czas systemu windows.

1. Wybierz pulę elastyczną toowork z.
2. W obszarze **monitorowania puli elastycznej** jest wykres z etykietą **wykorzystania zasobów**. Kliknij przycisk hello wykresu.

    ![Monitorowanie puli elastycznej][3]

    Witaj **Metryka** zostanie otwarty blok, wyświetlanie szczegółowego widoku hello określonej metryki za pośrednictwem hello określone okno czasu.   

    ![Blok metryki][9]

### <a name="toocustomize-hello-chart-display"></a>Wyświetl wykres hello toocustomize

Można edytować hello wykres i toodisplay bloku metryki hello innych metryk, takich jak procent, procent we/wy danych i dziennika we/wy procent wykorzystania procesora CPU.

1. W bloku metryki hello, kliknij **Edytuj**.

    ![Kliknij przycisk Edytuj][6]

2. W hello **Edytuj wykres** bloku, wybierz zakres czasu (Ostatnia godzina dzisiaj, lub ostatni tydzień), lub kliknij przycisk **niestandardowych** tooselect data zakresu w hello ostatnich dwóch tygodni. Wybierz typ wykresu hello (paska lub linii), a następnie wybierz hello toomonitor zasobów.

   > [!Note]
   > Tylko metryki z tej samej jednostki miary można wyświetlić w hello hello pod adresem hello sam czas. Na przykład w przypadku wybrania "procent liczby jednostek eDTU" następnie możesz wybrać tylko innych metryk odsetku hello jednostką miary.
   >

    ![Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Następnie kliknij przycisk **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Zarządzanie i monitorowanie baz danych w puli elastycznej

Można również monitorować pojedyncze bazy danych dla potencjalne problemy.

1. W obszarze **elastycznej bazy danych monitorowania**, jest wykres przedstawia metryki pięć baz danych. Domyślnie program hello wykres Wyświetla hello top 5 baz danych w puli hello przez użycie średnią liczbę jednostek eDTU w hello ostatniej godziny. Kliknij przycisk hello wykresu.

    ![Monitorowanie puli elastycznej][4]

2. Witaj **wykorzystania zasobów bazy danych** zostanie wyświetlony blok. Zapewnia to szczegółowy widok hello użycia bazy danych w puli hello. Przy użyciu siatki hello w dolnej części bloku hello hello, można wybrać żadnych baz danych w toodisplay puli hello jej użycie w hello wykresu (w górę too5 baz danych). Można również dostosować hello metryki i przedziału czasowego wyświetlane na wykresie hello klikając **Edytuj wykres**.

    ![Blok wykorzystanie zasobów bazy danych][8]

### <a name="toocustomize-hello-view"></a>Widok hello toocustomize

1. W hello **bazy danych wykorzystania zasobów** bloku, kliknij przycisk **Edytuj wykres**.

    ![Kliknij pozycję Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. W hello **Edytuj** wykresu bloku, wybierz zakres czasu (Ostatnia godzina lub po 24 godzinach) lub kliknij przycisk **niestandardowych** tooselect różnych dziennie w hello poza toodisplay 2 tygodnie.

    ![Kliknij przycisk niestandardowe](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Kliknij przycisk hello **porównania baz danych przez** tooselect listy rozwijanej różne metryki toouse podczas porównywania baz danych.

    ![Edytuj wykres hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor baz danych

Na liście bazy danych hello w hello **wykorzystania zasobów bazy danych** bloku można znaleźć określonej bazy danych przez wyszukiwanie stronach hello liście hello lub wpisując hello nazwę bazy danych. Użyj hello wyboru tooselect hello bazy danych.

![Wyszukaj toomonitor baz danych][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Dodaj zasób puli elastycznej tooan alertu

Można dodać reguły tooan elastycznej puli, która Wyślij wiadomość e-mail punkty końcowe tooURL ciągów toopeople lub alert, kiedy puli elastycznej hello trafienia ustawiony próg użycia.

**tooadd zasobów tooany alertu:**

1. Kliknij hello **wykorzystania zasobów** hello tooopen wykresu **Metryka** bloku, kliknij przycisk **Dodaj alert**, a następnie wprowadź informacje hello w hello **Dodawanie alertu Reguła** bloku (**zasobów** są automatycznie konfigurowane pracy z puli hello toobe).
2. Wpisz **nazwa** i **opis** , które identyfikują hello tooyou alertów oraz odbiorców hello.
3. Wybierz **Metryka** , które mają tooalert z listy hello.

    Wykres Hello dynamicznie pokazuje wykorzystania zasobów dla tego toohelp metryki, wybierz próg.

4. Wybierz **warunku** (większe niż poniżej, itd.) i **próg**.
5. Wybierz **okres** hello metryki czasu reguły muszą zostać spełnione przed hello wyzwalaczy alertu.
6. Kliknij przycisk **OK**.

Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Przenoszenie bazy danych w puli elastycznej

Można dodać lub usunąć bazy danych z istniejącej puli. Witaj baz danych może być w innych pulach. Jednak można dodawać tylko baz danych, które są na hello sam serwer logiczny.

1. W bloku hello hello puli w obszarze **elastycznych baz danych** kliknij **Konfigurowanie puli**.

    ![Kliknij przycisk Konfiguruj pulę][1]

2. W hello **Konfigurowanie puli** bloku, kliknij przycisk **dodać toopool**.

    ![Kliknij przycisk Dodaj toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. W hello **dodać bazy danych** bloku, wybierz hello bazy danych lub puli toohello tooadd baz danych. Następnie kliknij przycisk **wybierz**.

    ![Wybierz tooadd baz danych](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Witaj **Konfigurowanie puli** bloku teraz list hello wybranej toobe dodane o jej stanie ustawić także bazy danych**oczekujące**.

    ![Dodawanie puli oczekujące](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. W hello **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Przenoszenie bazy danych z puli elastycznej

1. W hello **Konfigurowanie puli** bloku, wybierz hello bazy danych lub tooremove baz danych.

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Kliknij przycisk **usunąć z puli**.

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Hello **Konfigurowanie puli** bloku teraz list hello bazy danych wybrane toobe usuwane z jego stan zbyt**oczekujące**.

    ![Podgląd bazy danych Dodawanie i usuwanie](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. W hello **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Zmień ustawienia wydajności puli elastycznej

Podczas monitorowania wykorzystania zasobów hello elastycznej puli może stwierdzić, że pewnych zmian są potrzebne. Może być pula hello wymaga zmiany hello limity wydajność lub pamięć masową. Prawdopodobnie ma toochange hello ustawienia do bazy danych w puli hello. Można zmienić ustawienia hello puli hello w dowolnym czasie tooget hello równowagę wydajności i kosztów. Zobacz [kiedy należy puli elastycznej użyć?](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.

toochange hello jednostek Edtu i Magazyn limity dla każdej puli i jednostek Edtu na bazę danych:

1. Otwórz hello **Konfigurowanie puli** bloku.

    W obszarze **ustawienia puli elastycznej**, użyj albo ustawienia puli hello toochange suwaka.

    ![Użycie zasobów w puli elastycznej](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Po zmianie ustawienia hello wyświetlania hello pokazuje hello szacowany miesięczny koszt hello zmiany.

    ![Aktualizacja puli elastycznej i nowych miesięczny koszt](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Czas oczekiwania operacji puli elastycznej
* Zmiana hello minimalna liczba jednostek Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.
* Zmiana hello Edtu na pulę, zależy od hello łączną ilość miejsca używanego przez wszystkie bazy danych w puli hello. Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB. Na przykład jeśli całkowita ilość miejsca hello jest używany przez wszystkie bazy danych w puli hello jest 200 GB, a następnie hello oczekuje się, że czas oczekiwania na zmianę hello puli eDTU na pulę wynosi 3 godziny lub mniej.

## <a name="next-steps"></a>Następne kroki

- toounderstand jakie puli elastycznej zobacz [puli elastycznej bazy danych SQL](sql-database-elastic-pool.md).
- Aby uzyskać wskazówki dotyczące wykorzystujących pule elastyczne, zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md).
- toouse zadania elastyczne toorun języka Transact-SQL skryptów na dowolnej liczbie baz danych w puli hello, zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).
- Zobacz tooquery na dowolnej liczbie baz danych w puli hello [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
- Dla transakcji Zobacz dowolnej liczbie baz danych w puli hello [transakcji elastycznej](sql-database-elastic-transactions-overview.md).


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
