---
title: "Przepływność aaaProvision dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset elastycznie przepływności containsers bazy danych Azure rozwiązania Cosmos, kolekcje, wykresów i tabel."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Ustaw przepustowość dla kontenerów bazy danych Azure rozwiązania Cosmos

Można określić przepustowość dla kontenerów bazy danych Azure rozwiązania Cosmos w hello portalu Azure lub za pomocą hello zestawy SDK klientów. 

Witaj w poniższej tabeli wymieniono hello przepustowości dostępnej dla kontenerów:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Kontener jednej partycji</strong></p></td>
            <td valign="top"><p><strong>Kontener podzielonym na partycje</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Przepustowość minimalna</p></td>
            <td valign="top"><p>400 jednostek żądań na sekundę</p></td>
            <td valign="top"><p>2500 jednostki żądania na sekundę</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Maksymalna przepustowość</p></td>
            <td valign="top"><p>10 000 jednostek żądań na sekundę</p></td>
            <td valign="top"><p>Nieograniczona liczba</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>Przepływność hello tooset przy użyciu hello portalu Azure

1. W nowym oknie, otwórz hello [portalu Azure](https://portal.azure.com).
2. Na pasku po lewej stronie powitania kliknij **bazy danych Azure rozwiązania Cosmos**, lub kliknij przycisk **więcej usług** u dołu hello następnie przewiń zbyt**baz danych**, a następnie kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.
3. Wybierz konto DB rozwiązania Cosmos.
4. W nowym oknie powitania kliknij **Eksploratora danych (wersja zapoznawcza)** w menu nawigacji hello.
5. W nowym oknie hello, rozwiń węzeł bazy danych i kontener, a następnie kliknij przycisk **& Ustawienia skalowania**.
6. W nowym oknie hello, wpisz nową wartość przepływności hello w hello **przepływności** , a następnie kliknij przycisk **zapisać**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>Przepływność hello tooset przy użyciu hello interfejsu API usługi DocumentDB dla platformy .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Przepływność — często zadawane pytania

**Można ustawić Mój tooless przepływności niż 400 RU/s?**

400 RU/s jest hello minimalną przepustowość na kolekcje z jedną partycją DB rozwiązania Cosmos (minimum dla kolekcji partycjonowanych hello jest 2500 RU/s). Żądanie jednostki są ustawiane w 100 RU/s odstępach czasu, ale przepływności nie można ustawić too100 RU/s lub dowolna wartość mniejszą niż 400 RU/s. Jeśli szukasz toodevelop ekonomiczne — metoda i przetestować rozwiązania Cosmos bazy danych, możesz użyć hello wolnego [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), które można wdrożyć lokalnie bez ponoszenia kosztów. 

**Jak ustawić througput przy użyciu hello bazy danych MongoDB interfejsu API?**

Nie ma żadnych przepływności tooset rozszerzenia interfejsu API bazy danych MongoDB. Witaj zalecane jest hello toouse interfejsu API usługi DocumentDB, jak pokazano w [tooset hello przepływność przy użyciu hello interfejsu API usługi DocumentDB dla platformy .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Następne kroki

Zobacz toolearn więcej informacji na temat udostępniania i skali planety będzie DB rozwiązania Cosmos [dzielenia na partycje i skalowania rozwiązania Cosmos DB](partition-data.md).
