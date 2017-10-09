---
title: dokumentacji pomocy geograficznie aaaMulti | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obszaru roboczego i opublikować usługi sieci web w regionie Azure, inny niż hello Południowa centralnej Stanów Zjednoczonych (SCUS) region platformy Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Dokumentacja pomocy dotyczącej wielu regionów geograficznych
W tym artykule opisano, jak można utworzyć obszaru roboczego i opublikować usługi sieci web w różnych regionach platformy Azure.  Witaj [produkty Azure według regionu strony](https://azure.microsoft.com/en-us/regions/services/) zawiera listę regionów, gdzie dostępna jest usługa Azure Machine Learning.

## <a name="create-a-workspace"></a>Tworzenie obszaru roboczego
1. Zaloguj się toohello klasycznego portalu Azure.
2. Kliknij przycisk **+ nowy** > **usług danych** > **UCZENIA MASZYNOWEGO** > **szybkie tworzenie**.  W obszarze **lokalizacji** wybrać inny region, takich jak **Azja południowo-wschodnia**.
   ![Obraz pomocy Multi-geograficznie 1][1]
3. Wybierz obszar roboczy hello, a następnie kliknij przycisk **logowania tooML Studio**.
   ![Pomoc geograficznie wielu obraz 2][2]
4. Obszar roboczy jest teraz dostępna w innym regionie, w których można używać tak samo jak inne obszaru roboczego. tooswitch między obszarów roboczych, zobacz toohello górnym rogu ekranu. Kliknij przycisk hello listy rozwijanej, wybierz hello regionu i hello następnie wybierz obszar roboczy. Wszystko to toohello lokalnego obszaru roboczego region.  Na przykład będzie wszystkich usług sieci web utworzony z obszaru roboczego w hello, w tym samym regionie hello w obszarze roboczym w której znajduje się.
   ![Pomoc geograficznie wielu obrazu 3][3]

## <a name="open-an-experiment-from-gallery"></a>Otworzyć eksperyment z galerii
Po otwarciu doświadczenia z galerii można również wybrać regionu, którego chcesz doświadczenia hello toocopy.

![Pomoc geograficznie wielu obrazu 4][4a]

## <a name="web-service-management"></a>Zarządzanie usługami sieci Web
tooprogrammatically zarządzania usługami sieci web, takich jak do ponownego trenowania, użyj adresu określonego regionu hello:

* https://asiasoutheast.Management.azureml.NET
* https://europewest.Management.azureml.NET

### <a name="things-toonote"></a>Toonote rzeczy
1. Możesz skopiować tylko eksperymenty między obszarami roboczymi, które należą toohello tego samego regionu w ten sposób. Jeśli potrzebujesz toocopy eksperymentu w obszary robocze w różnych regionach, można użyć hello [PowerShell](http://aka.ms/amlps) polecenie commandlet [ *AmlExperiment kopii* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish który. Inne obejście jest toopublish hello eksperymentu w galerii w trybie nieznajdujące się na liście, a następnie otwórz go w obszarze roboczym hello z hello inny region.
2. Selektor region Hello Pokaż tylko obszarów roboczych do jednego regionu w czasie.  
3. Obszar roboczy wolne lub obszar roboczy (anonimowe) dostępu dla gości zostanie utworzona i hostowanych w centralnej Południowe stany USA  
4. Usługi sieci Web wdrożone z obszaru roboczego w Azji Południowo-Wschodnia będą również obsługiwane w Azji Południowo-Wschodnia.  

## <a name="more-information"></a>Więcej informacji
Zadaj pytanie na powitania [forum usługi Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
