---
title: "Przykładowe wyrażenia filtru jest możliwe za pomocą usługi Azure Machine Learning Przygotowanie danych | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera zestaw przykładów wyrażeń filtru przy użyciu usługi Azure Machine Learning Przygotowanie danych"
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/11/2017
ms.openlocfilehash: ae70f5981c7ca533740968e0eea1b0b83df414fa
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="sample-of-filter-expressions-python"></a>Przykładowe wyrażenia filtru (Python) 
Przed przeczytaniem tego dodatku odczytu [Przegląd rozszerzalności języka Python](data-prep-python-extensibility-overview.md).

## <a name="filter-with-equivalence-test"></a>Filtrowanie za pomocą równoważność testu
Filtruj tylko w wierszach których wartość Col2 (numeryczną) jest większa niż 4. 

```python
    row["Col2"] > 4
```

## <a name="filter-with-multiple-columns"></a>Filtruj z wieloma kolumnami 
Filtruj tylko w wierszach gdzie Col1 zawiera wartość **dobrej** i Col2 zawiera wartość 1 (numeryczną). 
```python
    row["Col1"] == 'Good' and row["Col2"] == 1
```

## <a name="test-filter-against-null"></a>Filtr testu względem wartości null
Filtruj tylko w wierszach gdzie Col1 ma wartość null. 
```python
    pd.isnull(row["Col1"])
```
