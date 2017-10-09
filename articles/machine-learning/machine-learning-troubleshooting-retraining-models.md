---
title: "Usługa sieci web aaaTroubleshoot ponownego trenowania klasycznego Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Zidentyfikować i rozwiązać typowe problemy napotkano, gdy są ponownego trenowania hello modelu dla usługi sieci Web Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Rozwiązywanie problemów z hello ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego
## <a name="retraining-overview"></a>Ponownego trenowania — omówienie
Podczas wdrażania eksperyment predykcyjny jako usługę sieci web oceniania jest statyczny modelu. Wraz ze wzrostem dostępności nowych danych lub w przypadku hello konsumenta hello interfejsu API ma własne dane modelu hello musi toobe retrained. 

Aby uzyskać pełny przewodnik hello ponownego trenowania procesu usługi sieci Web klasycznego, zobacz [Retrain Machine Learning modeli programowo](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Proces ponownego trenowania
Jeśli potrzebujesz hello tooretrain usługi sieci Web, należy dodać niektóre dodatkowe elementy:

* Wdrożone z hello eksperyment uczenia usługi sieci Web. musi mieć eksperymentu Hello **wyjście usługi sieci Web** toohello dane wyjściowe hello podłączony moduł **Train Model** modułu.  
  
    ![Dołącz modelu train toohello dane wyjściowe hello usług sieci web.][image1]
* Nowy punkt końcowy dodać tooyour oceniania usługi sieci Web.  Można dodać punktu końcowego hello programowo przy użyciu hello przykładowego kodu, do którego odwołuje się hello Retrain Machine Learning modeli tematu lub za pośrednictwem hello klasycznego portalu Azure.

Następnie można użyć hello próbki kodu C# z modelu tooretrain strony pomocy interfejsu API usługi hello szkolenia sieci Web. Po zostały obliczone wyniki hello i uzyskaniu je, należy zaktualizować hello uczonego modelu oceniania usługi sieci web przy użyciu hello nowy punkt końcowy, który został dodany.

Z wszystkich elementów hello w miejscu hello główne kroki należy wykonać tooretrain hello modelu są następujące:

1. Wywołanie usługi sieci Web szkolenia hello: wywołanie hello jest toohello usługi wykonywania wsadowego (BES), nie hello żądanie odpowiedzi usługi (RR). Można użyć hello próbki C# kodu na powitania interfejsu API pomocy strony toomake hello wywołania. 
2. Znajdź hello wartości dla hello *BaseLocation*, *RelativeLocation*, i *SasBlobToken*: te wartości są zwracane w danych wyjściowych hello z toohello Twojego wywołania szkoleń w sieci Web Usługa. 
   ![Wyświetlanie danych wyjściowych hello hello ponownego trenowania próbki i hello BaseLocation, RelativeLocation i SasBlobToken wartości.][image6]
3. Hello aktualizacji dodano punkt końcowy z hello nowych oceniania usługi sieci web z hello uczenia modelu: przy użyciu hello przykładowy kod podany w hello Retrain Machine Learning modeli programowo, zaktualizuj nowy punkt końcowy hello dodane toohello nowo oceniania modelu z hello uczonego modelu z hello usługi sieci Web szkolenia.

## <a name="common-obstacles"></a>Typowych wąskich gardeł
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Sprawdź toosee, jeśli masz hello Popraw poprawki
Hello poprawka używasz adres URL musi być hello, co skojarzony z hello nowego punktu końcowego oceniania dodaniu toohello oceniania usługi sieci Web. Istnieje wiele sposobów tooobtain hello poprawka adresu URL:

**Opcja 1: programowo**

Witaj tooget Popraw poprawki:

1. Uruchom hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.
2. Z danych wyjściowych hello AddEndpoint, Znajdź hello *HelpLocation* wartość i skopiuj adres URL hello.
   
   ![HelpLocation w danych wyjściowych hello hello addEndpoint próbki.][image2]
3. Wklej adres URL hello na stronę tooa toonavigate przeglądarki łącza pomocy hello usługi sieci Web.
4. Kliknij przycisk hello **aktualizacji zasobów** strona pomocy poprawki hello tooopen łącza.

**Opcja 2: Hello Użyj klasycznego portalu Azure**

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Hello Otwórz kartę uczenia maszynowego. ![Karta oparcie maszyny.][image4]
3. Następnie kliknij nazwę obszaru roboczego **usług sieci Web**.
4. Kliknij przycisk hello oceniania usługi sieci Web, którą użytkownik pracuje z. (Jeśli nie jest zmodyfikowała hello domyślnej nazwy usługi sieci web hello, będą kończyć się [Exp oceniania.]).
5. Kliknij przycisk **dodać punkt końcowy**.
6. Po dodaniu punktu końcowego powitania kliknij nazwę punktu końcowego hello. Następnie kliknij przycisk **aktualizacji zasobów** tooopen hello stosowania poprawek strony pomocy.

> [!NOTE]
> Jeśli dodano hello toohello punkt końcowy usługi sieci Web szkolenia zamiast hello predykcyjnej usługi sieci Web, zostanie wyświetlony następujący błąd, po kliknięciu hello hello **aktualizacji zasobów** łącza: Niestety, ale ta funkcja nie jest obsługiwana lub niedostępne w tym kontekście. Ta usługa sieci Web ma nie nadaje się do aktualizacji zasobów. Firma Microsoft Przepraszamy za niedogodności hello i działają na ułatwieniu ten przepływ pracy.
> 
> 

![Nowy punkt końcowy pulpitu nawigacyjnego.][image3]

Strona pomocy poprawki Hello zawiera hello PATCH musi używać adresu URL i udostępnia przykładowy kod, można użyć toocall go.

![Adres URL poprawki.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Aktualizacja punktu końcowego oceniania poprawne hello toosee wyboru
* Nie poprawka hello usługi sieci Web szkolenia: hello poprawki operacja musi zostać wykonana na powitania oceniania usługi sieci Web.
* Nie poprawka hello domyślny punkt końcowy usługi sieci Web: hello poprawki operacja musi zostać wykonana na powitania oceniania nowy punkt końcowy usługi sieci Web, który został dodany.

Możesz sprawdzić, które hello końcowy usługi sieci Web jest włączone zaproszonych hello klasycznego portalu Azure. 

> [!NOTE]
> Upewnij się, że w przypadku dodawania hello toohello punkt końcowy usługi sieci Web predykcyjnych, hello usługi sieci Web szkolenia. Jeśli zostały poprawnie wdrożone zarówno szkolenia, jak i usługi sieci Web predykcyjnej, powinny pojawić się dwa oddzielne usług sieci Web na liście. Hello predykcyjnej usługi sieci Web powinien kończyć się "[exp predykcyjnych.]".
> 
> 

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Hello Otwórz kartę uczenia maszynowego. ![Obszaru roboczego uczenia maszyny interfejsu użytkownika.][image4]
3. Wybierz obszar roboczy.
4. Kliknij przycisk **usług sieci Web**.
5. Wybierz usługę sieci Web predykcyjnej.
6. Sprawdź, czy nowy punkt końcowy został dodany toohello usługi sieci Web.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Sprawdź hello roboczy usługi sieci web w tooensure jest poprawny region hello
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Wybierz hello menu uczenia maszynowego.
   ![Machine learning region interfejsu użytkownika.][image4]
3. Sprawdź lokalizację hello obszaru roboczego.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
