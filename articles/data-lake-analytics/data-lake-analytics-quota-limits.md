---
title: "Limity przydziału Analytics Lake danych aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ogranicza tooadjust i zwiększ limit przydziału konta usługi Azure Data Lake Analytics (ADLA)."
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Limity przydziału usługi Azure Data Lake Analytics

Dowiedz się, jak ogranicza tooadjust i zwiększ limit przydziału konta usługi Azure Data Lake Analytics (ADLA). Znajomość tych limitów mogą ułatwić zrozumienie zachowania zadania z języka U-SQL. Wszystkie limity przydziału są miękkie, więc może zwiększyć maksymalną wartością hello dotarcie do toous.

## <a name="azure-subscriptions-limits"></a>Limity subskrypcji platformy Azure

**Maksymalna liczba ADLA konta dla subskrypcji:** 5

 Jest to hello maksymalną liczbę kont ADLA, które można utworzyć na subskrypcję. Jeśli spróbujesz konta ADLA toocreate szóstego, wystąpi błąd "Osiągnięto maksymalną liczbę kont usługi Data Lake Analytics może (5) hello w regionie, w obszarze Nazwa subskrypcji". W takim przypadku Usuń wszystkie nieużywane konta ADLA albo dotrzeć toous przez [otwarcie biletu pomocy technicznej](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Limity konta ADLA

**Maksymalna liczba jednostek Analytics (AUs) dla konta:** 250

Jest to hello maksymalną liczbę AUs, które można uruchomić jednocześnie w ramach Twojego konta. Jeśli Twoja Suma uruchamianie AUs we wszystkich zadań przekracza ten limit, automatycznie są kolejkowane zadania nowsza. Na przykład:

* Jeśli masz tylko jedno zadanie uruchomione z 250 AUs, podczas przesyłania drugiej zadania go będzie czekać w kolejce zadań hello przed zakończeniem hello pierwszego zadania.
* Jeśli masz pięć zadania uruchomione i każdego używa 50 AUs, podczas przesyłania szóstego zadanie, które wymaga 20 AUs oczekuje w kolejce zadań hello, dopóki istnieją 20 AUs dostępne.

**Maksymalna liczba jednoczesnych zadań U-SQL dla danego konta:** 20

Jest to hello maksymalna liczba zadań, które można uruchomić jednocześnie w ramach Twojego konta. Powyżej tej wartości automatycznie są kolejkowane zadania nowsza.

## <a name="adjust-adla-quota-limits-per-account"></a>Dostosuj ADLA limity przydziału dla konta

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Wybierz istniejące konto ADLA.
3. Kliknij pozycję **Właściwości**.
4. Dostosuj **równoległości** i **równoczesnych zadań** toosuit potrzeb.

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Zwiększ limit przydziału maksymalnej

1. W portalu Azure, otwórz żądanie pomocy technicznej.

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Wybierz typ problemu hello **przydziału**.
3. Wybierz użytkownika **subskrypcji** (Upewnij się, nie jest "wersję próbną").
4. Wybierz typ przydziału **usługi Data Lake Analytics**.

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. W bloku hello problem opisano żądanego Zwiększ limit z **szczegóły** z czego potrzebujesz tej dodatkowej pojemności.

    ![Blok portalu usługi Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Sprawdź informacje kontaktowe i Utwórz żądanie obsługi hello.

Firma Microsoft sprawdza żądania i próbuje tooaccommodate jak najszybciej potrzeb firmy.

## <a name="next-steps"></a>Następne kroki

* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
