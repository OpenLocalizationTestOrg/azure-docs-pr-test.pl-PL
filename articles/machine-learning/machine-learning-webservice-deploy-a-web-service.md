---
title: "aaaDeploying nową usługę sieci web w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Usługa sieci web na podstawie Hello przepływ pracy wdrażania ARM"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Wdrażanie nowej usługi sieci Web
Microsoft Azure Machine learning teraz udostępnia usługi sieci web, które są oparte na [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) zezwala na nowe opcje planu rozliczeń i wdrażanie regionów toomultiple usługi sieci web.

Witaj toodeploy ogólny przepływ pracy z usługą sieci web przy użyciu usługi sieci Web Microsoft Azure Machine Learning to:

* Utworzyć eksperyment predykcyjny
* Wdróż go
* Konfigurowanie nazwy
* plan rozliczeniowy
* należy przeprowadzić test
* go używać.

powitania po ilustracja przedstawia przepływ pracy dotyczący hello.

![Przepływ pracy wdrożenia usługi sieci Web][1]

## <a name="deploy-web-service-from-studio"></a>Wdrażanie usługi sieci web w Studio
toodeploy eksperymentu jako nową usługę sieci web. Zaloguj się do hello Machine Learning Studio i utworzyć nową usługę sieci web predykcyjnej. 

**Uwaga**: Jeśli zostały już wdrożone eksperymentu jako usługę sieci web klasycznego nie można wdrożyć go jako nową usługę sieci web.

Kliknij przycisk **Uruchom** u dołu hello hello eksperymentu kanwy, a następnie kliknij przycisk **wdrażanie usługi sieci Web** i **wdrażanie usługi sieci Web [New]**. zostanie otwarta strona wdrożenia Hello hello Menedżera Usługa sieci Web usługi Machine Learning.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Strona eksperymentu wdrażanie Machine Learning Web Service Manager
Na stronie eksperymentu wdrażanie hello wprowadź nazwę usługi sieci web hello.
Wybrać planu cenowego. Jeśli masz istniejące planu cenowego, że zostanie ona wybrana, w przeciwnym razie należy utworzyć nowy plan cen hello usługi. 

1. W hello **planu cen** listy rozwijanej, wybierz istniejący plan lub hello **wybierz nowy plan** opcji.
2. W **Nazwa planu**, wpisz nazwę identyfikującą planu hello na rachunku.
3. Wybierz jedną z hello **miesięcznych poziomów Planowanie**. Zauważ, że warstw planu hello domyślne plany toohello w Twoim regionie domyślne i usługi sieci web jest wdrożone toothat regionu.

Kliknij przycisk **Wdróż** i otwiera hello strony Szybki Start dla usługi sieci web.

## <a name="quickstart-page"></a>Strona Szybki Start
strony Szybki Start usługi sieci web Hello zapewnia dostęp i wskazówki na powitania najbardziej typowych zadań, które ma zostać wykonane po utworzeniu nowej usługi sieci web. W tym miejscu można łatwo dostęp zarówno hello **testu** strony i **Consume** strony.

## <a name="testing-your-web-service"></a>Testowanie usługi sieci web
Ze strony szybkiego startu hello kliknij przycisk Test sieci web usługi w obszarze zadań.   

Usługa sieci web hello tootest jako usługa żądań i odpowiedzi (RR):

* Kliknij przycisk **testu** hello paska menu.
* Kliknij przycisk **żądań i odpowiedzi**.
* Wprowadź odpowiednie wartości dla kolumny wejściowe hello eksperymentu.
* Kliknij przycisk Testuj **żądań i odpowiedzi**.

Możesz wyniki będą wyświetlane na powitania po prawej stronie powitania strony.

tootest usługi sieci web usługi wykonywania wsadowego (BES), którego użyjesz pliku CSV:

* Kliknij przycisk **testu** hello paska menu.
* Kliknij przycisk **partii**.
* W obszarze dane wejściowe kliknij przycisk Przeglądaj i przejdź tooyour przykładowy plik danych.
* Kliknij przycisk **testu**.

Stan Hello testu jest wyświetlany w obszarze **Test zadań wsadowych**.

## <a name="consuming-your-web-service"></a>Korzystanie z usługi sieci Web
Po wdrożeniu jako usługę sieci web Azure Machine Learning eksperymenty Podaj interfejsu API REST, które mogą być używane przez szeroki zakres urządzeń i platform. Jest to spowodowane komunikatów w formacie hello prosty interfejs API REST akceptuje i odpowiada JSON. Witaj portalu usługi Azure Machine Learning zawiera kod, który może służyć usługi sieci web hello toocall R, C# i Python.

Na stronie Consuming hello można znaleźć:

* klucz interfejsu API Hello i URI służący do konsumowania usługi sieci web w aplikacjach.
* Tookick szablonów aplikacji sieci web i Excel uruchomić procesu zużycia.
* Przykładowy kod w języku C#, python i R tooget rozpoczęty.

Aby uzyskać więcej informacji dotyczących używania usług sieci web, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących używania usług sieci web zobacz:

[Jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md)

[Usługi sieci Web uczenie Azure maszyny: Wdrażanie i zużycia](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
