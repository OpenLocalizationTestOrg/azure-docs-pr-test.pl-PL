---
title: "Krok 6: Dostęp do usługi Machine Learning Web hello | Dokumentacja firmy Microsoft"
description: "Krok 6 hello opracowanie wskazówki rozwiązanie predykcyjne: dostęp do usługi sieci Web Azure Machine Learning active."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Wskazówki krok 6: Hello dostępu do usługi sieci web uczenie maszynowe Azure

Jest to ostatni krok wskazówki hello hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Tworzenie obszaru roboczego usługi Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Nauczanie i Ewaluacja modeli hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Wdrażanie usługi sieci Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. **Witaj dostępu do usługi sieci Web**

- - -
Usługi sieci web, która używa modelu prognozowania ryzyko kredytowe wdrożyliśmy w poprzednim kroku hello w tym przewodniku. Teraz użytkownicy są w stanie toosend tooit danych i otrzymywać wyniki. 

Hello usługi sieci Web jest usługą sieci web platformy Azure, która umożliwia odbieranie i zwrócić dane przy użyciu interfejsów API REST w jeden z dwóch sposobów:  

* **Żądanie/odpowiedź** — hello użytkownik wysyła jeden lub więcej wierszy toohello danych środki usługi za pomocą protokołu HTTP i hello odpowiada usługi z jednego lub więcej zestawów wyników.
* **Wykonywanie wsadowe** — użytkownik hello przechowuje jednego lub większej liczby wierszy danych środki na platformie Azure blob, a następnie wysyła usługi toohello lokalizacji obiektu blob hello. wyniki Hello usługi, które hello wszystkich wierszy danych w hello blob danych wejściowych, magazyny hello wyniki w innym obiekcie blob i zwraca hello adres URL tego kontenera.  

Witaj tooaccess najszybszym i Najprostszym sposobem jest klasycznym usługi sieci web za pośrednictwem hello [aplikacji sieci Web usługi Azure ML żądanie-odpowiedź](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) lub [szablonu aplikacji sieci Web Azure ML partii wykonywania usługi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Te szablony aplikacji sieci web można utworzyć aplikacji sieci web niestandardowego, który zna usługi sieci web dane wejściowe i co zwróci. Toodo wystarczy zapewnienia usługi sieci web tooyour dostępu i danych, a szablon hello hello rest.

Aby uzyskać więcej informacji na temat używania szablonów aplikacji sieci web hello zobacz [korzystać z usługi Azure Machine Learning w sieci Web przy użyciu szablonu aplikacji sieci web](machine-learning-consume-web-service-with-web-app-template.md).

Można również zaprojektować niestandardową aplikację tooaccess hello usługi sieci web przy użyciu kodu starter dostarczany w R, C# i języków programowania Python.

Można znaleźć szczegółowe informacje w [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

