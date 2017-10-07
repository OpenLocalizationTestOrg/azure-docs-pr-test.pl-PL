---
title: aaaRetrain modelu uczenia maszynowego | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak aktualizacja i tooretrain modelu hello sieci Web usługi toouse hello nowo uczonego modelu w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Ponownie ucz modelu uczenia maszynowego
W ramach procesu hello operationalization modeli uczenia maszyny w usłudze Azure Machine Learning modelu są uczone i zapisać. Następnie należy go toocreate predicative usługi sieci Web. Hello usługi sieci Web mogą być następnie używane w witrynach sieci web, pulpity nawigacyjne i aplikacji mobilnych. 

Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne. Wraz ze wzrostem dostępności nowych danych lub po hello konsumenta hello interfejsu API modelu hello własnych danych musi toobe retrained. 

Ponownego trenowania może występować często. Przy użyciu funkcji API ponownego trenowania programowe hello można programowo retrain hello modelu przy użyciu hello ponownego trenowania interfejsów API i aktualizacji hello usługi sieci Web z hello nowo trenowanego modelu. 

Niniejszy dokument opisuje hello ponownego trenowania procesu i pokazuje, jak toouse hello ponownego trenowania interfejsów API.

## <a name="why-retrain-defining-hello-problem"></a>Dlaczego ponownie ucz: Definiowanie hello problem
W ramach uczenia maszynowego hello szkolenia procesu model jest uczony przy użyciu zestawu danych. Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne. Wraz ze wzrostem dostępności nowych danych lub po hello konsumenta hello interfejsu API modelu hello własnych danych musi toobe retrained.

W tych scenariuszach programowe interfejsu API zapewnia tooallow wygodny sposób możesz lub powitania klienta toocreate Twojego interfejsów API klienta, który może na podstawie jednorazowe lub regularne retrain hello modelu, używając własnych danych. Następnie mogą ocenić wyniki hello ponownego trenowania i zaktualizować hello sieci Web usługi interfejsu API toouse hello nowo uczonego modelu.

> [!NOTE]
> Jeśli masz istniejące eksperyment uczenia i usługi sieci Web nowego można toocheck się ponownego próbkowania predykcyjnej istniejącej sieci Web usługi zamiast następujące wskazówki hello wspomnianego hello następujących sekcji.
> 
> 

## <a name="end-to-end-workflow"></a>Kompletny przepływ pracy
Witaj proces obejmuje następujące składniki hello: A eksperyment uczenia i eksperyment predykcyjny publikowane jako usługę sieci Web. tooenable ponownego trenowania uczonego modelu hello eksperyment uczenia musi zostać opublikowany jako usługę sieci Web, przy czym dane wyjściowe hello trenowanego modelu. Dzięki temu model toohello dostępu do interfejsu API do ponownego trenowania. 

Witaj następujące kroki, zastosuj tooboth nowy i klasycznego usługami sieci Web:

Tworzenie początkowej usługi sieci Web predykcyjnej hello:

* Tworzenie eksperymentu szkolenia
* Tworzenie eksperymentu predykcyjnej sieci web
* Wdrażanie usługi sieci web predykcyjnej

Ponownie ucz hello usługi sieci Web:

* Zaktualizuj tooallow eksperymentu uczenia do ponownego trenowania
* Wdrażanie hello ponownego trenowania usługi sieci web
* Użyj hello usługi wykonywania wsadowego kodu tooretrain hello modelu

Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Jeśli wdrożono klasycznym usługi sieci Web:

* Utwórz nowy punkt końcowy na powitania usługi sieci Web predykcyjnej
* Pobierz adres URL poprawki hello i kod
* Użyj hello poprawka adresu URL toopoint hello nowy punkt końcowy na powitania retrained modelu 

Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain usługi sieci Web klasycznego](machine-learning-retrain-a-classic-web-service.md).

Jeśli wystąpiły problemy podczas ponownego trenowania usługi sieci Web klasycznego, zobacz [Rozwiązywanie problemów z hello ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego](machine-learning-troubleshooting-retraining-models.md).

Jeśli wdrożono usługę sieci Web nowe:

* Zaloguj się tooyour konta usługi Azure Resource Manager
* Pobierz definicję usługi sieci Web hello
* Eksportuj hello definicji usługi sieci Web w formacie JSON
* Zaktualizuj toohello odwołanie hello `ilearner` obiektu blob w hello JSON
* Importowanie hello JSON do definicji usługi sieci Web
* Usługi sieci Web hello aktualizacji z nowej definicji usługi sieci Web

Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain usługi nowej sieci Web przy użyciu poleceń cmdlet programu PowerShell do zarządzania Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).

Witaj proces konfigurowania ponownego trenowania dla usługi sieci Web klasycznego obejmuje hello następujące kroki:

![Omówienie procesu ponownego trenowania][1]

Konfigurowanie ponownego trenowania dla usługi sieci Web nowy proces Hello obejmuje hello następujące kroki:

![Omówienie procesu ponownego trenowania][7]

## <a name="other-resources"></a>Inne zasoby
* [Modele ponownego trenowania i aktualizowania usługi Azure Machine Learning z fabryką danych Azure](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [Tworzenie wielu modeli uczenia maszynowego i sieci web punktów końcowych usługi z doświadczenia przy użyciu programu PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Witaj [AML ponownego trenowania modeli przy użyciu interfejsów API](https://www.youtube.com/watch?v=wwjglA8xllg) wideo pokazuje, jak modeli uczenia maszynowego tooretrain utworzone w usłudze Azure Machine Learning przy użyciu hello ponownego trenowania interfejsów API i programu PowerShell.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

