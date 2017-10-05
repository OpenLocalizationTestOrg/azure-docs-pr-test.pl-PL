---
title: "Krok 1: Tworzenie obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Krok 1 opracowanie wskazówki rozwiązanie predykcyjne: Dowiedz się, jak skonfigurować nowy obszar roboczy usługi Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a>Przewodnik, krok 1. Tworzenie obszaru roboczego usługi Machine Learning
Jest to pierwsze tego przewodnika, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

1. **Tworzenie obszaru roboczego usługi Machine Learning**
2. [Przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)
3. [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Nauczanie i ocena modeli](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Wdrażanie usługi sieci Web](machine-learning-walkthrough-5-publish-web-service.md)
6. [Dostęp do usługi sieci Web](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

Aby korzystać z usługi Machine Learning Studio, należy mieć obszaru roboczego programu Microsoft Azure Machine Learning. Ten obszar roboczy zawiera narzędzia potrzebne do tworzenia, zarządzania i opublikować eksperymentów.  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

Administrator dla subskrypcji platformy Azure musi utworzyć obszaru roboczego, a następnie dodać możesz jako właściciela lub współautora. Aby uzyskać więcej informacji, zobacz [tworzenie i udostępnianie obszaru roboczego uczenia maszynowego Azure](machine-learning-create-workspace.md).

Po utworzeniu obszaru roboczego usługi Machine Learning Studio Otwórz ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)). Jeśli masz więcej niż jeden obszar roboczy, można wybrać obszar roboczy na pasku narzędzi w prawym górnym rogu okna.

![Wybierz obszar roboczy w Studio][2]

> [!TIP]
> Jeśli wprowadzono właściciela obszaru roboczego, można udostępniać eksperymentów, nad którymi pracuje przez zapraszanie innych osób do obszaru roboczego. Można to zrobić w usłudze Machine Learning Studio na **ustawienia** strony. Wystarczy konta Microsoft lub konta organizacyjnego dla każdego użytkownika.
> 
> Na **ustawienia** kliknij przycisk **użytkowników**, następnie kliknij przycisk **ZAPROSIĆ użytkowników więcej** w dolnej części okna.
> 
> 

- - -
**Następnie: [przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)**

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
