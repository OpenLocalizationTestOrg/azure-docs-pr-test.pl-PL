---
title: "aaaCreating punktów końcowych usługi sieci Web w uczeniu maszynowym | Dokumentacja firmy Microsoft"
description: "Tworzenie punktów końcowych usługi sieci Web w usłudze Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Tworzenie punktów końcowych
> [!NOTE]
>  W tym temacie opisano techniki stosowane tooa **klasycznego** usługi Machine Learning w sieci Web.
> 
> 

Podczas tworzenia usług sieci Web, które sprzedawać klientów do przodu tooyour należy tooprovide przeszkolone modele tooeach klienta, który jest nadal połączony toohello eksperymentu, za pomocą których hello sieci Web została utworzona usługa. Ponadto wszelkie aktualizacje, które eksperymentu toohello powinny być stosowane selektywnie tooan punktu końcowego bez zastępowania hello dostosowania.

tooaccomplish, uczenie maszynowe Azure umożliwia toocreate wiele punktów końcowych dla wdrożonej usługi sieci Web. Każdy punkt końcowy w hello usługi sieci Web jest niezależnie skierowana, ograniczenie i zarządzany. Każdy punkt końcowy jest unikatowy klucz adresu URL i autoryzacji rozpowszechniania tooyour klientów.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Dodawanie usługi sieci Web tooa punkty końcowe
Istnieją trzy sposoby tooadd tooa punkt końcowy usługi sieci Web.

* Programistycznie
* Za pomocą portalu usługi sieci Web systemu Azure Machine Learning hello
* Mimo że hello klasycznego portalu Azure

Po utworzeniu punktu końcowego hello, możesz pobrać go za pośrednictwem interfejsów API synchroniczne, partii interfejsów API i arkusze programu excel. Ponadto punkty końcowe tooadding za pośrednictwem tego interfejsu użytkownika, umożliwia także tooprogrammatically interfejsów API Management punktu końcowego hello Dodawanie punktów końcowych.

> [!NOTE]
> Jeśli dodano toohello dodatkowe punkty końcowe usługi sieci Web, nie można usunąć hello domyślnego punktu końcowego.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Programowe Dodawanie punktu końcowego
Można dodać punkt końcowy usługi sieci Web tooyour programowo przy użyciu hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) przykładowy kod.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Dodawanie punktu końcowego za pomocą portalu usługi sieci Web systemu Azure Machine Learning hello
1. W usłudze Machine Learning Studio kolumny nawigacji po lewej stronie powitania kliknij usług sieci Web.
2. U dołu hello hello pulpit nawigacyjny z usługi sieci Web, kliknij przycisk **zarządzanie punktami końcowymi**. portal usługi sieci Web systemu Azure Machine Learning Hello otwiera stronę punkty końcowe toohello hello usługi sieci Web.
3. Kliknij przycisk **Nowy**.
4. Wpisz nazwę i opis dla nowego punktu końcowego hello. Nazwy punktu końcowego musi być 24 znaków lub mniej długości i musi składać się z małych małych liter i cyfr. Wybierz poziom rejestrowania hello i czy jest włączone przykładowych danych. Aby uzyskać więcej informacji, zobacz [należy włączyć rejestrowanie dla usługi Machine Learning Web](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Dodawanie punktu końcowego za pomocą hello klasycznego portalu Azure
1. Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com), kliknij przycisk **uczenia maszynowego** w lewej kolumnie hello. Kliknij obszar roboczy hello, który zawiera hello usługi sieci Web, w której jesteś zainteresowany.
   
    ![Przejdź tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Kliknij przycisk **usług sieci Web**.
   
    ![Przejdź do usługi tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. Kliknij usługę sieci Web hello interesują Cię toosee hello listę dostępnych punktów końcowych.
   
    ![Przejdź tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. U dołu hello hello strony, kliknij przycisk **Dodawanie punktu końcowego**. Wpisz nazwę i opis, upewnij się, że nie ma żadnych innych punktów końcowych z hello takie same nazwy tej usługi sieci Web. Pozostaw hello ograniczania poziom jego wartość domyślna w przypadku braku specjalnych wymagań. Zobacz toolearn więcej informacji na temat ograniczania [skalowanie punkty końcowe interfejsu API](machine-learning-scaling-webservice.md).
   
    ![Tworzenie punktu końcowego](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Następne kroki
[Jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

