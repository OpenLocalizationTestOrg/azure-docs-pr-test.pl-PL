---
title: Obraz maszyny wirtualnej w portalu Azure Marketplace hello aaaManaging | Dokumentacja firmy Microsoft
description: "Szczegółowy przewodnik na jak toomanage maszyny wirtualnej obrazu w portalu Azure Marketplace powitania po opublikowaniu początkowej"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Przewodnik po produkcji dla maszyny wirtualnej zapewnia w hello Azure Marketplace
W tym artykule opisano sposób aktualizowania maszyny wirtualnej na żywo z tej oferty w hello Azure Marketplace. Go prowadzi użytkownika przez proces dodawania jednego lub więcej nowe jednostki SKU tooan istniejących oferta hello. On również prowadzi użytkownika przez proces hello usuwania oferty na żywo maszyny wirtualnej lub wersji z hello Marketplace.

Po oferta/jednostka SKU jest umieszczane w hello [portalu Azure](http://portal.azure.com), nie można zmienić hello następujące pola tekstowe:

* **Identyfikator oferty**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** i wybierz ofertę. Następnie kliknij przycisk **obrazów maszyn wirtualnych** > **identyfikator oferty**.
* **Identyfikator jednostki SKU**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** i wybierz ofertę. Następnie kliknij przycisk **jednostki SKU** > **Dodaj jednostki SKU**.
* **Namespace wydawcy**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** > **wskazówki** > **Powiedz nam o Twoja firma** (znajdujący się w obszarze "Krok 2 zarejestrować Twoja firma") > **Namespace wydawcy** > **Namespace**.

Po hello oferta/SKU ma na liście hello [Marketplace](http://azure.microsoft.com/marketplace), nie można zmienić hello następujące pola tekstowe:

* **Identyfikator oferty**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** i wybierz ofertę. Następnie kliknij przycisk **obrazów maszyn wirtualnych** > **identyfikator oferty**.
* **Identyfikator jednostki SKU**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** i wybierz ofertę. Następnie kliknij przycisk **jednostki SKU** > **Dodaj jednostki SKU**.
* **Namespace wydawcy**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** > **wskazówki** > **Powiedz nam o Twoja firma** (znajdujący się w obszarze "Krok 2 Register") **Namespace wydawcy** > **Namespace**.
* **Porty**: hello publikowania portalu, przejdź zbyt**maszyn wirtualnych** i wybierz ofertę. Następnie kliknij przycisk **obrazów maszyn wirtualnych** > **Otwieranie portów**.
* **Zmiany listy SKU(s) cennika**
* **Zmiana modelu rozliczeń wymienionych SKU(s)**
* **Usuwanie rozliczeń regionów wymienionych SKU(s)**
* **Dane zmiany hello liczba SKU(s) wymienionych na dysku**

## <a name="update-hello-technical-details-of-a-sku"></a>Zaktualizuj hello szczegóły techniczne dotyczące jednostki SKU
tooadd nowe toohello wersji jednostki SKU na liście i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **obrazów maszyn wirtualnych** kartę.
4. W hello **jednostki SKU** sekcji, Znajdź hello, które mają tooupdate jednostki SKU.
5. Dodaj nowy numer wersji jednostki SKU hello, a następnie kliknij przycisk hello  **+**  przycisku. Nowa wersja Hello powinna mieć format X.Y.Z, gdzie X, Y i Z są liczbami całkowitymi. Powinien mieć tylko przyrostowe zmiany wersji.
6. W hello **adres URL dysku VHD systemu operacyjnego** , wprowadź identyfikator URI utworzony dla systemu operacyjnego hello wirtualnego dysku twardego sygnatury dostępu współdzielonego hello i Zapisz zmiany hello.

   > [!IMPORTANT]
   > Użytkownik nie może przyrostu/dekrementacja hello liczba dysków danych z wymienionych wersji. W takim przypadku należy toocreate nowe jednostki SKU. Szczegółowe wskazówki można znaleźć w sekcji toohello [Dodaj nowe jednostki SKU w ramach wymienionych oferty](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Obrazy maszyn wirtualnych](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Aktualizuj szczegóły nietechnicznym hello oferty lub wersji
Można aktualizować hello nietechnicznym (marketing, prawnych, pomocy technicznej, kategorie) szczegółowe informacje na żywo oferty lub wersji w hello Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Opis oferty hello aktualizacji i logo
Witaj tooupdate szczegóły oferty i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **MARKETING** kartę.
4. Kliknij przycisk **angielski (USA)**.
5. Kliknij przycisk hello **szczegóły** kartę. W hello **opis** , oferty hello Aktualizacja sekcji **tytuł**, **Podsumowanie**, i **długie Podsumowanie** i Zapisz zmiany hello.

   > [!NOTE]
   > Po zaktualizowaniu szczegóły jednostki SKU hello należy pamiętać o tych ograniczeń: 
   * Nie należy wprowadzać tekst zduplikowany opis oferty hello i opis jednostki SKU hello.
   * Nie należy wprowadzać zduplikowane tekst hello SKU tytuł i oferty hello długie podsumowanie. 
   * Nie należy wprowadzać zduplikowane tekst hello SKU tytuł i hello Podsumowanie oferty.
   >
   >

    ![Szczegóły](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. W hello **logo** sekcji hello **szczegóły** pozycję Aktualizuj hello logo. Upewnij się, że logo hello wykonaj hello [wskazówki dotyczące portalu Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > Ikona bohater jest opcjonalna. Można wybrać ikonę bohater nie tooupload. Po przekazaniu ikona bohater nie ma jednak toodelete nie należy go z hello publikowania portalu. Wykonaj hello [bohater ikony wskazówki](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Logo](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Opis jednostki SKU hello aktualizacji
Witaj tooupdate SKU szczegółowe informacje i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **MARKETING** kartę.
4. Kliknij przycisk **angielski (USA)**.
5. Kliknij przycisk hello **plany** kartę. W hello **jednostki SKU** sekcji, zaktualizuj hello SKU **tytuł**, **Podsumowanie**, i **opis** i Zapisz zmiany hello.

   > [!NOTE]
   > Po zaktualizowaniu szczegóły jednostki SKU hello należy pamiętać o tych ograniczeń: 
   * Nie należy wprowadzać tekst zduplikowany opis oferty hello i opis jednostki SKU hello. 
   * Nie należy wprowadzać zduplikowane tekst hello SKU tytuł i oferty hello długie podsumowanie. 
   * Nie należy wprowadzać zduplikowane tekst hello SKU tytuł i hello Podsumowanie oferty.
   >
   >
6. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Plany](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Zmień istniejące linki lub Dodaj nowe łącza
istniejące linki toochange lub dodać nowe łącza, a następnie ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **MARKETING** kartę.
4. Kliknij przycisk **angielski (USA)**.
5. Kliknij przycisk hello **łącza** kartę.
6. nowe łącze w hello tooadd **łącza** kliknij **+ Dodaj łącze**. W hello **Dodaj łącze** okna dialogowego wprowadź łącze hello **tytuł** i **adres URL** i Zapisz zmiany hello. Można wprowadzić każde łącze, które zawierają informacje, które mogą ułatwić klientom.
7. tooupdate lub usuń istniejące łącze, wybierz łącze hello i kliknij przycisk hello **Edytuj** przycisku lub hello **usunąć** przycisku.

   > [!NOTE]
   > Upewnij się, że hello łącza, które zostały wprowadzone w tej sekcji działają poprawnie, ponieważ te linki uzyskać weryfikowane podczas procesu żądania produkcji.
   >
   >
8. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Linki](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Dodaj łącze](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Zmień istniejący obraz przykładowej lub Dodaj nowy obraz próbki
toochange istniejący przykład obrazu lub Dodaj nowe próbki obrazy i ponownie opublikować ofertę, wykonaj następujące kroki:

> [!NOTE]
> Obraz tylko jeden przykład jest wyświetlany w hello [portalu Azure](https://portal.azure.com).
>
>

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **MARKETING** kartę.
4. Kliknij przycisk **angielski (USA)**.
5. Kliknij przycisk hello **przykładowe obrazy** kartę.
6. tooadd nowy obraz przykładowej w hello **przykładowe obrazy** kliknij **PRZEKAŻ nowy obraz** i Zapisz zmiany hello.

   > [!NOTE]
   > Łącznie z obrazem próbki jest opcjonalna.
   >
7. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Przykładowe obrazy](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Aktualizacja zawartości prawne hello
tooupdate hello treści i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **MARKETING** kartę.
4. Kliknij przycisk **angielski (USA)**.
5. Kliknij przycisk hello **prawne** kartę. W hello **prawne** sekcji, aktualizacja Twojego zasad/warunki użytkowania. Wpisz lub Wklej hello zasad/warunków w hello **warunki użytkowania** i Zapisz zmiany hello.
6. limit znaków Hello hello prawne warunki użytkowania wynosi 1 milion znaków.
7. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Informacje prawne](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Zaktualizuj informacje pomocy technicznej hello
Witaj tooupdate informacje pomocy technicznej i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **Obsługa** kartę.
4. W hello **Engineering skontaktuj się z** sekcji aktualizacji hello engineering szczegóły dotyczące kontaktu. Te informacje są używane do wewnętrznej komunikacji między partnerami hello i Microsoft tylko.
5. W hello **pomocy technicznej** sekcji, zaktualizuj informacje kontaktowe pomocy technicznej hello i hello **OBSŁUGUJE adres URL**. Te informacje są używane do wewnętrznej komunikacji między partnerami hello i Microsoft tylko.

   > [!NOTE]
   > Jeśli chcesz tooprovide tylko obsługa poczty e-mail, wprowadź numer telefonu zastępczego w hello **pomocy technicznej** sekcji. W takim przypadku hello poczty e-mail, pod warunkiem, zamiast niego jest używana.
   >
   >
6. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Pomoc techniczna](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Kategorie hello aktualizacji
Witaj tooupdate kategorii sekcji dla danej oferty i ponownie opublikować ofertę, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **kategorii** kartę.
4. W hello **kategorii** sekcji, zaktualizuj hello kategorie dla danej oferty i Zapisz zmiany hello. Możesz się toofive kategorii dla galerii Azure Marketplace hello.
5. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Kategorie](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Dodaj nowe jednostki SKU w ramach wymienionych oferty
tooadd nowe jednostki SKU w ramach Twojej oferty na żywo, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **jednostki SKU** kartę. Następnie kliknij przycisk **Dodaj jednostki SKU**. 
4. W oknie dialogowym hello, wprowadź **identyfikator jednostki SKU** pisane małymi literami. Wybierz hello **Przełącz własnej licencji (BYOL) modelu rozliczeń** pole wyboru, jeśli chcesz, aby toopublish hello nowe jednostki SKU z modelu BYOL rozliczeń. W przeciwnym razie wyczyść pole wyboru hello. Kliknij przycisk hello znaczników znacznik toocreate nowe jednostki SKU. Jeśli nie wybierzesz modelu rozliczeń BYOL hello, modelu rozliczeń hello jest ustawiany automatycznie toohourly. Jeśli chcesz hello 30-dniowej bezpłatnej wersji próbnej dla modelu rozliczenia godzinowe hello, wybierz opcję **jeden miesiąc** dla **jest dostępna bezpłatna wersja próbna?** W przeciwnym razie wybierz **wersji próbnej nie**. (**Jest dostępna bezpłatna wersja próbna?**  jest wyświetlana tylko wtedy, gdy nie wybrano BYOL, podczas tworzenia hello nowej wersji.)

   > [!IMPORTANT]
   > **Ukryj tej jednostki SKU z hello Marketplace, ponieważ zawsze powinna zostać zakupione za pośrednictwem szablon rozwiązania** powinien być **tak** *tylko* Jeśli zatwierdzeniu publikowania szablon rozwiązania. W przeciwnym razie ta opcja powinna być zawsze **nr**.
   >
   >
4. W menu powitania po lewej stronie powitania kliknij hello **obrazów maszyn wirtualnych** kartę i sprawdź hello nowe jednostki SKU, które zostały utworzone.
5. tooset maksymalnie hello nowej wersji, zobacz [uzyskać certyfikacji dla obrazu maszyny Wirtualnej](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) orientacji.
6. tooadd materiałów dla marketingowych hello nowej wersji, zobacz [Marketplace Podaj marketingu zawartości](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. informacje o cenach tooadd hello nowej wersji, zobacz [ustawić cenach](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

    ![Jednostki SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Dodaj jednostki SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Zmień liczba dysków danych hello wymienionych jednostki SKU
Użytkownik nie może przyrostu/dekrementacja hello liczba dysków danych z wymienionych wersji. W takim przypadku należy toocreate nowe jednostki SKU. Szczegółowe wskazówki można znaleźć w sekcji toohello [Dodaj nowe jednostki SKU w ramach wymienionych oferty](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Usuń to wymienione oferta z hello Marketplace
Różne aspekty muszą toobe obsługę podjąć w przypadku hello tooremove żądanie na żywo oferty. wskazówki tooget z tooremove zespołu pomocy technicznej hello to wymienione oferta z hello Marketplace, wykonaj następujące kroki:

1. Zgłoś biletu pomocy technicznej na powitania [utworzenia zdarzenia](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) strony.

2. Wybierz **typ problemu** jako **Zarządzanie oferty**i wybierz **kategorii** jako **modyfikowanie oferty i/lub jednostki SKU już w środowisku produkcyjnym**.
3. Przesyłanie żądania hello.

zespołem pomocy technicznej Hello przeprowadzi Cię przez proces usuwania hello oferty lub jednostki SKU.

> [!NOTE]
> Oferta hello można usunąć zawsze, gdy jest on w stanie projektu (ale nie tymczasowym czy produkcyjnym). Na powitania **HISTORII** , kliknij pozycję **Odrzuć wersję ROBOCZĄ**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Usuń wymienionych jednostki SKU z hello Marketplace
toodelete wymienionych SKU z hello Marketplace, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).

2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W okienku powitania po lewej stronie powitania kliknij hello **jednostki SKU** kartę.
4. Wybierz hello SKU mają toodelete i kliknij przycisk hello **usunąć** przycisku.
5. Przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish hello oferty w hello Marketplace.
6. Po opublikowaniu hello oferty w portalu Marketplace hello, hello SKU jest usuwane z hello Marketplace i hello portalu Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Usuń hello bieżącej wersji listy jednostki SKU z hello Marketplace
toodelete hello bieżącej wersji listy SKU z hello Marketplace, wykonaj następujące kroki: 

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).

2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **obrazów maszyn wirtualnych** kartę.
4. Wybierz hello SKU których bieżąca wersja toodelete i kliknij hello **usunąć** przycisku.
5. Przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish hello oferty w hello Marketplace.
6. Po oferta hello pobiera ponownie opublikować w hello Marketplace, hello bieżącej wersji hello SKU wymienione są usuwane z hello Marketplace i hello portalu Azure. Witaj SKU następnie przywróceniu tooits poprzedniej wersji.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Przywróć hello listę wartości tooproduction cen
wartości tooproduction toorevert hello listę cen, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).
2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **CENNIK** kartę.
4. Wybierz region, w których ceny ma tooreset.

    ![Cennik regionów](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Dla jednostki SKU o modelu rozliczenia godzinowe Zresetuj hello ceny dla wszystkich rdzeni hello są one w środowisku produkcyjnym hello wybranego regionu. Dla jednostki SKU z modelu rozliczeń BYOL, upewnij się, hello SKU dostępna w regionie hello, zaznaczając pole wyboru hello na powitania jednostki SKU w hello **dostępności jednostki SKU EXTERNALLY-LICENSED (BYOL)** sekcji.

    ![Modelami cenowymi](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Kliknij przycisk **AUTOPRICE innymi rynkach na podstawie cen w Stanach Zjednoczonych**.

   > [!NOTE]
   > Etykieta przycisku Hello mogą się różnić w zależności od regionu hello, którą wybierzesz. Ponieważ wybrano Stanów Zjednoczonych, przycisk hello etykietą **AUTOPRICE inne rynkach oparte na cen w UNITED STATES**.
   >
   >

    ![Autoprice](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Na 1 hello Autoprice kreatora, wybierz hello rynku podstawowej i kliknij przycisk hello **strzałka** przycisku.

    ![Podstawowy rynku](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Na stronie 2, wybierz planów usług i liczników (rdzenie) i kliknij hello **strzałka** przycisku.

    ![Plany usługi i liczników](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. Na stronie 3 kliknij **Przełącz wszystkie** tooselect wszystkich regionach. Lub użytkownik może ręcznie wybrać pola wyboru dla konkretnych regionów. Kliknij przycisk hello **strzałka** przycisku.

    ![Wybierz rynkach](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Na 4, przejrzyj kursy wymiany hello i kliknij przycisk **Zakończ**. Kreator Hello resetuje hello cennik zgodnie z opcji tooyour.

11. Na powitania **CENNIK** , kliknij pozycję **WIDOKU podsumowanie zmian**.
    Dla **wyświetlanie wersji**, wybierz pozycję **projekt**oraz **porównania z**, wybierz pozycję **produkcji**. Jeśli widzisz różnic cenową cennik hello wartości produkcji toohello pomyślnie przywrócone.

    ![Wyświetl podsumowanie i zmiany](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Przywróć hello wartości tooproduction modelu rozliczeń
toorevert hello rozliczeń tooproduction wartości modelu, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).

2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **jednostki SKU** kartę.
4. Kliknij przycisk hello **Edytuj** modelu rozliczeń hello toorevert przycisku. W wyświetlonym oknie hello zaznaczyć lub wyczyścić hello **rozliczeń i licencjonowania odbywa się zewnętrznie z platformy Azure (alias Bring Your Own License)** pole wyboru.

    ![Edytuj rozliczeń](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Wykonaj kroki powitania "Hello Przywróć wyświetlanie wartości cen tooproduction" w tym artykule.
6. Przejdź toohello **publikowania** , a następnie kliknij pozycję **tooSTAGING WYPYCHANIA**. Testowanie w środowisku przemieszczania hello ofertę szczegółowe instrukcje, zobacz [Test ofertę maszyny Wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Po przetestowaniu ofertę tymczasowych, przejdź toohello **publikowania** kartę w hello publikowania portalu. Kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Przywróć ustawienie widoczności hello listy wartości produkcji toohello jednostki SKU
Ustawienie widoczności hello toorevert listy wartości produkcji toohello jednostka SKU, wykonaj następujące kroki:

1. Zaloguj się toohello [publikowania portal](https://publish.windowsazure.com).

2. Przejdź toohello **maszyn wirtualnych** , a następnie wybierz ofertę.
3. W menu powitania po lewej stronie powitania kliknij hello **jednostki SKU** kartę.
4. Wybierz użytkownika jednostki SKU, a następnie Przywróć ustawienie widoczności hello hello wartość produkcji toohello jednostki SKU.

    ![Widoczność](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Po zakończeniu hello zmiany, kliknij przycisk **tooPRODUCTION tooPUSH zatwierdzenie ŻĄDANIA** toorepublish ofertę w hello Marketplace.

## <a name="see-also"></a>Zobacz też
* [Get Started: Publikowanie oferty toohello portalu Azure Marketplace](marketplace-publishing-getting-started.md)
* [Zrozumienie wypłaty raportowania](marketplace-publishing-report-payout.md)
* [Zmień programu incentive odsprzedawcy Cloud Solution Provider](marketplace-publishing-csp-incentive.md)
* [Rozwiązywanie typowych problemów publikowania w hello Marketplace](marketplace-publishing-support-common-issues.md)
* [Uzyskaj pomoc techniczną jako wydawca](marketplace-publishing-get-publisher-support.md)
* [Utwórz lokalną obrazu maszyny Wirtualnej](marketplace-publishing-vm-image-creation-on-premise.md)
* [Utwórz maszynę wirtualną z systemem Windows w portalu Azure w wersji zapoznawczej hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
