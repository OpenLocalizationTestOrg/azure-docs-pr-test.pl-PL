---
title: "Zarządzaj kontem bazy danych rozwiązania Cosmos Azure za pośrednictwem portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Zarządzanie kontem bazy danych Azure rozwiązania Cosmos w portalu Azure. Przewodnik na wyświetlanie, kopiowanie, usuwanie i dostęp do kont za pomocą portalu Azure."
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
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a>Jak zarządzać konta bazy danych Azure rozwiązania Cosmos
Dowiedz się, jak ustawić globalne spójności, pracy z kluczy oraz usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure.

## <a id="consistency"></a>Zarządzanie ustawieniami spójności bazy danych Azure rozwiązania Cosmos
Wybranie poziomu spójności prawo zależy od semantykę aplikacji. Należy zapoznać się z poziomu spójności dostępne w usłudze Azure DB rozwiązania Cosmos odczytując [za pomocą poziomów spójności w celu zwiększenia dostępności i wydajności w usłudze Azure DB rozwiązania Cosmos][consistency]. Azure DB rozwiązania Cosmos zapewnia spójność, dostępności i wydajności gwarancji, na każdym poziomie spójności niedostępna dla Twojego konta bazy danych. Konfigurowanie konta bazy danych z poziomu spójności silne wymaga danych zamkniętej do jednego regionu Azure i globalny nie jest dostępny. Z drugiej strony, poziomy swobodna spójności — spójność powiązanej nieaktualności, session lub Włącz ostatecznego można skojarzyć dowolną liczbę regiony platformy Azure przy użyciu konta bazy danych. Następujące prostych krokach pokazano, jak wybrać domyślny poziom spójności dla konta bazy danych. 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a>Aby określić domyślna spójność konta bazy danych Azure rozwiązania Cosmos
1. W [portalu Azure](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
2. W bloku konta kliknij **domyślna spójność**.
3. W **domyślna spójność** bloku, wybierz nowy poziom spójności i kliknij przycisk **zapisać**.
    ![Domyślna spójność sesji][5]

## <a id="keys"></a>Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu
Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do konta bazy danych Azure rozwiązania Cosmos. Zapewniając dwa klucze dostępu do bazy danych rozwiązania Cosmos Azure umożliwia ponowne generowanie kluczy nie przeszkód do swojego konta bazy danych Azure rozwiązania Cosmos. 

W [portalu Azure](https://portal.azure.com/), dostępu **klucze** bloku z menu zasobów na **konta bazy danych Azure rozwiązania Cosmos** bloku, aby wyświetlić, kopiowanie i ponowne generowanie kluczy dostępu, które są używane do dostęp do tego konta bazy danych Azure rozwiązania Cosmos.

![Azure Portal zrzut ekranu bloku klucze](./media/manage-account/keys.png)

> [!NOTE]
> **Klucze** bloku obejmuje również parametry połączenia podstawowych i pomocniczych, które mogą służyć do łączenia się z kontem z [narzędzia migracji danych](import-data.md).
> 
> 

Tylko do odczytu klucze są również dostępne w tym bloku. Odczyty i zapytań tworzy podczas operacji tylko do odczytu, usuwanie, i nie są zastępowane.

### <a name="copy-an-access-key-in-the-azure-portal"></a>Kopiowanie klucza dostępu w portalu Azure
Na **klucze** bloku, kliknij przycisk **kopiowania** przycisku z prawej strony klucz, który chcesz skopiować.

![Wyświetlanie i kopiowanie kluczy dostępu w portalu Azure, w bloku klucze](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Ponowne generowanie kluczy dostępu
Należy zmienić klucze dostępu do konta bazy danych Azure rozwiązania Cosmos okresowo, aby zabezpieczyć połączenia. Dwa klucze dostępu są przypisywane do utrzymania połączeń przy użyciu jednego klucza dostępu, jednocześnie ponownie generując drugi klucz dostępu konta bazy danych Azure rozwiązania Cosmos.

> [!WARNING]
> Trwa ponowne generowanie kluczy dostępu ma wpływ na wszystkie aplikacje, które są zależne od bieżącego klucza. Wszyscy klienci, którzy używają klucza dostępu do uzyskania dostępu do konta bazy danych Azure rozwiązania Cosmos trzeba zaktualizować do użycia nowego klucza.
> 
> 

Jeśli masz aplikacje lub usługi w chmurze przy użyciu konta bazy danych Azure rozwiązania Cosmos utracisz połączenia ponownego generowania kluczy, chyba że wdrożysz klucze. Poniższe kroki wchodzą w skład proces stopniowych kluczy.

1. Zaktualizuj klucz dostępu w kodzie aplikacji, aby odwołać pomocniczy klucz dostępu konta bazy danych Azure rozwiązania Cosmos.
2. Ponownie wygenerować podstawowy klucz dostępu dla konta bazy danych Azure rozwiązania Cosmos. W [Azure Portal](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
3. W **konto bazy danych Azure rozwiązania Cosmos** bloku, kliknij przycisk **klucze**.
4. Na **klucze** bloku, kliknij przycisk regenerate, a następnie kliknij przycisk **Ok** aby potwierdzić wygenerowanie nowego klucza.
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-keys.png)
5. Po upewnieniu się, że nowy klucz jest dostępny do użycia (około 5 minut od ponownego wygenerowania), należy zaktualizować klucz dostępu w kodzie aplikacji, aby odwołać nowego podstawowego klucza dostępu.
6. Wygeneruj ponownie pomocniczy klucz dostępu.
   
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Może upłynąć kilka minut przed wygenerowanym klucza może służyć do uzyskania dostępu do konta bazy danych Azure rozwiązania Cosmos.
> 
> 

## <a name="get-the--connection-string"></a>Pobierz ciąg połączenia
Aby pobrać parametrów połączenia, wykonaj następujące czynności: 

1. W [portalu Azure](https://portal.azure.com), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.
2. W menu zasobów kliknij **klucze**.
3. Kliknij przycisk **kopiowania** znajdujący się obok **parametry połączenia podstawowej** lub **parametry połączenia pomocniczej** pole. 

Jeśli używane są parametry połączenia w [narzędzia migracji bazy danych DB rozwiązania Cosmos Azure](import-data.md), Dodaj nazwę bazy danych do końca ciągu połączenia. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a>Usuń konto bazy danych Azure rozwiązania Cosmos
Aby usunąć konta bazy danych Azure rozwiązania Cosmos z portalu Azure, nie jest już używany, kliknij prawym przyciskiem myszy nazwę konta, a następnie kliknij przycisk **usunąć konto**.

![Jak usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure](./media/manage-account/deleteaccount.png)

1. W [portalu Azure](https://portal.azure.com/), uzyskać dostęp do konta bazy danych Azure rozwiązania Cosmos do usunięcia.
2. Na **konta bazy danych Azure rozwiązania Cosmos** bloku, kliknij prawym przyciskiem myszy konto, a następnie kliknij przycisk **usunąć konto**. 
3. W bloku wynikowy potwierdzenie wpisz nazwę konta Azure DB rozwiązania Cosmos aby upewnić się, że chcesz usunąć to konto.
4. Kliknij przycisk **usunąć** przycisku.

![Jak usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Następne kroki
Dowiedz się, jak [Rozpoczynanie pracy z Twoim kontem platformy Azure DB rozwiązania Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
