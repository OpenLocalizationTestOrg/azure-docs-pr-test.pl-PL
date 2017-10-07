---
title: "aaaLogging usług sieci web usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak jest rejestrowanie tooenable uczenia maszynowego usługi sieci web. Rejestrowanie udostępnia dodatkowe informacje toohelp Rozwiązywanie problemów z hello interfejsów API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Włączanie rejestrowania usług sieci Web Machine Learning
Ten dokument zawiera informacje na powitania rejestrowania możliwości usługi sieci web usługi Machine Learning. Rejestrowanie udostępnia dodatkowe informacje, poza tylko liczbą błędów i komunikatów, które mogą pomóc w rozwiązaniu toohello Twojego wywołania Machine Learning API.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Sposób rejestrowania tooenable usługi sieci Web

Włączanie rejestrowania z hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu. 

1. Zaloguj się w portalu usługi sieci Web systemu Azure Machine Learning toohello [https://services.azureml.net](https://services.azureml.net). Usługi sieci web klasycznego portalu toohello można także uzyskać, klikając **nowego środowiska usług sieci Web** na stronie usługi sieci Web usługi Machine Learning hello w usłudze Machine Learning Studio.

   ![Nowe łącze środowisko usługi sieci Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Na pasku menu u góry hello kliknij **usług sieci Web** dla nowej usługi sieci web, lub kliknij przycisk **usług sieci Web klasycznego** dla klasyczny usługi sieci web.

   ![Wybierz nowy lub Classic usługi sieci web](media/machine-learning-web-services-logging/select-web-service.png)

3. Aby uzyskać nową usługę sieci web kliknij nazwę usługi sieci web hello. Usługi sieci web klasycznego kliknij nazwę usługi sieci web hello, a następnie na następnej stronie powitania kliknij przycisk hello odpowiedniego punktu końcowego.

4. Na pasku menu u góry hello kliknij **Konfiguruj**.

5. Zestaw hello **Włącz rejestrowanie** opcję zbyt*błąd* (toolog tylko błędy) lub *wszystkie* (Aby uzyskać pełne rejestrowanie).

   ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/enable-logging.png)

6. Kliknij pozycję **Zapisz**.

7. Dla usług sieci web klasycznego, należy utworzyć hello **diagnostyki ml** kontenera.

   Wszystkie dzienniki usługi sieci web są przechowywane w kontenerze obiektu blob o nazwie **diagnostyki ml** na koncie magazynu hello skojarzony z usługą sieci web hello. Dla nowej usługi sieci web ten kontener jest tworzony powitania po raz pierwszy uzyskać dostępu do usługi sieci web hello. Dla usług sieci web klasycznego należy toocreate hello kontenera Jeśli jeszcze nie istnieje. 

   1. W hello [portalu Azure](https://portal.azure.com), przejdź do pozycji toohello konta magazynu skojarzone z usługą sieci web hello.

   2. W obszarze **usługa Blob**, kliknij przycisk **kontenery**.

   3. Jeśli kontener hello **diagnostyki ml** nie istnieje, kliknij przycisk **+ kontener**, nadaj hello kontenera hello nazwy "ml Diagnostyka" i wybierz hello **dostęp typu** jako "Blob". Kliknij przycisk **OK**.

      ![Wybierz poziom rejestrowania](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Usługi sieci web klasycznego hello pulpitu nawigacyjnego usług sieci Web w usłudze Machine Learning Studio zawiera rejestrowania tooenable przełącznika. Ponieważ rejestrowanie jest teraz zarządzane za pośrednictwem hello usług sieci Web portalu, jednak tooenable rejestrowanie za pośrednictwem portalu hello zgodnie z opisem w tym artykule. Jeśli już włączone rejestrowanie w Studio, w hello Portal usługi sieci Web, należy wyłączyć rejestrowanie i włącz ją ponownie.


## <a name="hello-effects-of-enabling-logging"></a>efekty Hello Włączanie rejestrowania
Po włączeniu rejestrowania diagnostyki hello i błędów z punktem końcowym usługi sieci web hello są rejestrowane w hello **diagnostyki ml** kontenera obiektów blob w hello konta magazynu Azure połączone z obszarem roboczym hello użytkownika. Ten kontener zawiera wszystkie informacje diagnostyczne powitania dla wszystkich hello usługi punktów końcowych sieci web dla wszystkich hello obszary robocze skojarzone z tym kontem magazynu.

Hello dzienniki można wyświetlać przy użyciu dowolnego hello kilku dostępnych narzędzi tooexplore konta magazynu platformy Azure. Najprostszym Hello może być toonavigate toohello magazynu konta w portalu Azure hello, kliknij przycisk **kontenery**, a następnie kliknij przycisk kontenera hello **diagnostyki ml**.  

## <a name="log-blob-detail-information"></a>Dziennik blob szczegółowych informacji
Każdy obiekt blob w kontenerze hello przechowuje informacje diagnostyczne hello dokładnie jednego hello następujące akcje:

* Wykonywanie metody hello wykonywania wsadowego usługi  
* Wykonywanie metody hello żądań i odpowiedzi  
* Inicjowanie kontenera żądań i odpowiedzi

Nazwa Hello każdy obiekt blob ma prefiks hello następującej postaci: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Gdzie _typ dziennika_ jest jednym z hello następujące wartości:  

* Wsadowe  
* wynik/żądań  
* wynik/init  

