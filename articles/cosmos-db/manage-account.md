---
title: "konto bazy danych rozwiązania Cosmos Azure za pośrednictwem portalu Azure hello aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage Twojego Azure DB rozwiązania Cosmos konta za pośrednictwem hello portalu Azure. Przewodnik na temat używania hello tooview portalu Azure, kopiowania, usuwania i dostępu do konta."
keywords: Portal Azure documentdb, azure, platformy Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Jak toomanage konta bazy danych Azure rozwiązania Cosmos
Dowiedz się, jak pracować z kluczami tooset globalne spójności i usunąć konta bazy danych Azure rozwiązania Cosmos w hello portalu Azure.

## <a id="consistency"></a>Zarządzanie ustawieniami spójności bazy danych Azure rozwiązania Cosmos
Wybieranie poziomu spójności prawo hello zależy od semantyki hello aplikacji. Należy zapoznać się z hello poziomy spójności dostępne w usłudze Azure DB rozwiązania Cosmos odczytując [przy użyciu spójności poziomy toomaximize dostępności i wydajności w usłudze Azure DB rozwiązania Cosmos][consistency]. Azure DB rozwiązania Cosmos zapewnia spójność, dostępności i wydajności gwarancji, na każdym poziomie spójności niedostępna dla Twojego konta bazy danych. Konfigurowanie konta bazy danych z poziomu spójności silne wymaga danych zamkniętej tooa pojedynczy region platformy Azure i niedostępne globalnie. Na drugiej Witaj, hello poziomy swobodna spójności — spójność powiązanej nieaktualności, session lub Włącz ostatecznego tooassociate można dowolną liczbę regiony platformy Azure przy użyciu konta bazy danych. Hello następujące proste kroki pokazują, jak tooselect hello domyślny poziom spójności dla konta bazy danych. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>toospecify hello domyślna spójność konta bazy danych Azure rozwiązania Cosmos
1. W hello [portalu Azure](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
2. W bloku konta usługi powitania kliknij **domyślna spójność**.
3. W hello **domyślna spójność** bloku, wybierz hello nowy poziom spójności i kliknij przycisk **zapisać**.
    ![Domyślna spójność sesji][5]

## <a id="keys"></a>Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu
Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi hello generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do hello konta bazy danych Azure rozwiązania Cosmos. Zapewniając dwa klucze dostępu do bazy danych Azure rozwiązania Cosmos umożliwia tooregenerate hello klucze z nie przeszkód tooyour konta bazy danych Azure rozwiązania Cosmos. 

W hello [portalu Azure](https://portal.azure.com/), hello dostępu **klucze** bloku z menu zasobów hello na powitania **konta bazy danych Azure rozwiązania Cosmos** tooview bloku, kopiowania i regenerate hello kluczy dostępu są używane tooaccess konta bazy danych Azure rozwiązania Cosmos.

![Azure Portal zrzut ekranu bloku klucze](./media/manage-account/keys.png)

> [!NOTE]
> Witaj **klucze** blok zawiera również podstawowe i parametry połączenia pomocniczej, które mogą być używane tooconnect tooyour konta z hello [narzędzia migracji danych](import-data.md).
> 
> 

Tylko do odczytu klucze są również dostępne w tym bloku. Odczyty i zapytań tworzy podczas operacji tylko do odczytu, usuwanie, i nie są zastępowane.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Skopiuj klucz dostępu w hello portalu Azure
Na powitania **klucze** bloku, kliknij hello **kopiowania** toohello przycisk rogu hello klucz ma toocopy.

![Wyświetlanie i kopiowanie kluczy dostępu w portalu Azure, bloku klucze hello](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Ponowne generowanie kluczy dostępu
Należy zmienić hello dostępu do kluczy tooyour bazy danych Azure rozwiązania Cosmos konta okresowo toohelp zabezpieczania połączeń. Dwa klucze dostępu są przypisane tooenable możesz toomaintain połączeń toohello konta bazy danych Azure rozwiązania Cosmos przy użyciu jednego klucza dostępu, jednocześnie ponownie generując hello drugi klucz dostępu.

> [!WARNING]
> Trwa ponowne generowanie kluczy dostępu ma wpływ na wszystkie aplikacje, które są zależne od hello bieżącego klucza. Wszystkich klientów, którzy używają hello dostępu do klucza tooaccess hello Azure DB rozwiązania Cosmos konta musi być zaktualizowany toouse hello nowego klucza.
> 
> 

Jeśli masz aplikacje lub usługi w chmurze przy użyciu konta bazy danych Azure rozwiązania Cosmos hello utracisz połączenia hello ponownego generowania kluczy, chyba że wdrożysz klucze. Hello poniższe kroki wchodzą w skład procesu hello objętego stopniowych klucze.

1. Zaktualizuj klucz dostępu hello w Twojej aplikacji kod tooreference hello pomocniczy klucz dostępu z hello konta bazy danych Azure rozwiązania Cosmos.
2. Wygeneruj ponownie hello podstawowy klucz dostępu dla konta bazy danych Azure rozwiązania Cosmos. W hello [Azure Portal](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
3. W hello **konto bazy danych Azure rozwiązania Cosmos** bloku, kliknij przycisk **klucze**.
4. Na powitania **klucze** bloku, kliknij przycisk regenerate hello, a następnie kliknij przycisk **Ok** tooconfirm, które mają toogenerate nowy klucz.
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-keys.png)
5. Po upewnieniu się, się, że ten nowy klucz hello jest dostępny do użytku (około 5 minut od ponownego wygenerowania), zaktualizować klucza dostępu hello w Twojej aplikacji kod tooreference hello nowego podstawowego klucza dostępu.
6. Wygeneruj ponownie hello pomocniczy klucz dostępu.
   
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Może upłynąć kilka minut, zanim nowo wygenerowany klucz może być używane tooaccess konta bazy danych Azure rozwiązania Cosmos.
> 
> 

## <a name="get-hello--connection-string"></a>Pobierz ciąg połączenia hello
tooretrieve połączenie string, hello następujące: 

1. W hello [portalu Azure](https://portal.azure.com), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
2. W menu zasobów hello, kliknij przycisk **klucze**.
3. Kliknij hello **kopiowania** przycisku Dalej toohello **parametry połączenia podstawowej** lub **parametry połączenia pomocniczej** pole. 

Jeśli używane są parametry połączenia hello w hello [narzędzia migracji bazy danych DB rozwiązania Cosmos Azure](import-data.md), Dołącz hello bazy danych nazwa toohello koniec hello parametry połączenia. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a>Usuń konto bazy danych Azure rozwiązania Cosmos
tooremove bazy danych Azure rozwiązania Cosmos konta z hello Portal Azure nie jest już używany, kliknij prawym przyciskiem myszy nazwę konta hello i kliknij przycisk **usunąć konto**.

![Jak konto toodelete bazy danych Azure rozwiązania Cosmos hello portalu Azure](./media/manage-account/deleteaccount.png)

1. W hello [portalu Azure](https://portal.azure.com/), uzyskać dostęp do konta bazy danych Azure rozwiązania Cosmos hello mają toodelete.
2. Na powitania **konta bazy danych Azure rozwiązania Cosmos** bloku, kliknij prawym przyciskiem myszy konto hello, a następnie kliknij przycisk **usunąć konto**. 
3. Na powitania wynikowy bloku potwierdzenie wpisz hello Azure DB rozwiązania Cosmos konta, które mają konta hello toodelete nazwa tooconfirm.
4. Kliknij przycisk hello **usunąć** przycisku.

![Jak konto toodelete bazy danych Azure rozwiązania Cosmos hello portalu Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Następne kroki
Dowiedz się, jak za[Rozpoczynanie pracy z Twoim kontem platformy Azure DB rozwiązania Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
