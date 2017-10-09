---
title: "aaaImport danych z pliku do usługi Azure Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak plik tooupload dane szkoleniowe tooAzure Twojego dysku twardego Machine Learning Studio. Spowoduje to utworzenie modułu zestawu danych w obszarze roboczym hello."
keywords: "Importowanie danych, formatu danych, typy danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importowanie danych szkoleniowych z pliku na dysku twardym w usłudze Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Dowiedz się, jak tooupload danych plików z toouse Twojego dysku twardego jako danych szkoleniowych w usłudze Azure Machine Learning Studio. Importując plik danych hello masz modułu zestawu danych gotowe do użycia w obszarze roboczym.

## <a name="steps-tooimport-data-from-a-local-file"></a>Kroki tooimport danych z pliku lokalnego
tooimport danych z lokalnego dysku twardego hello następujące:

1. Kliknij przycisk **+ nowy** u dołu okna Machine Learning Studio hello hello.
2. Wybierz **DATASET** i **z pliku lokalnego**.
3. W hello **przekazać nowy zestaw danych** okna dialogowego, przeglądania toohello pliku, który chcesz tooupload
4. Wprowadź nazwę, identyfikowanie hello typu danych i opcjonalnie wprowadź opis. Opis jest zalecane — umożliwia toorecord żadnych właściwości hello dane mają tooremember, korzystając z danych hello w przyszłości hello informacje.
5. Witaj wyboru **jest nowa wersja istniejący zestaw danych hello** pozwala tooupdate istniejący zestaw danych z nowych danych. Kliknij to pole wyboru, a następnie wprowadź nazwę hello istniejący zestaw danych.

![Przekaż nowy zestaw danych](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Podczas przekazywania zobaczysz komunikat jest przekazywanego pliku. Przekaż czas zależy od rozmiaru hello szybkości danych i hello usługi toohello połączenia. Jeśli wiesz, że plik hello potrwa długo, można wykonać inne czynności w usłudze Machine Learning Studio, podczas oczekiwania. Powoduje zamknięcie przeglądarki hello jednak toofail przekazywania danych hello.

## <a name="dataset-module-is-ready-for-use"></a>Moduł zestawu danych jest gotowy do użycia
Po przekazaniu plików dane są przechowywane w module zestawu danych i jest dostępne tooany eksperymentu w obszarze roboczym.

Podczas edycji eksperyment, można znaleźć hello zestawy danych po utworzeniu hello **Moje zestawów danych** liście hello **zapisane zestawów danych** listy hello modułu palety. Możesz przeciągać i upuszczać dataset hello na kanwie eksperymentu hello należy toouse hello dataset do dalszej analizy i uczenia maszynowego.
