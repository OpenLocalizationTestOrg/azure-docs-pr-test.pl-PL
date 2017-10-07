---
title: "często zadawane pytania — aaa(deprecated) publikowania i korzystać z usługi Machine Learning aplikacji w portalu Azure Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Często zadawane pytania dotyczące publikowania aplikacji uczenia maszynowego w hello Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(przestarzałe) Publikowanie i za pomocą uczenia maszynowego aplikacji w portalu Azure Marketplace hello: często zadawane pytania

> [!NOTE]
> DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r. W związku z tym w tym artykule jest przestarzałe. 
> 
> Alternatywnie, można opublikować toohello eksperymentów z uczenia maszynowego [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) asysty hello hello danych nauki społeczności. Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Pytania dotyczące Korzystanie z portalu Marketplace
**1. Dlaczego pojawia się następujący komunikat o błędzie po wprowadzić dane wejściowe dla usługi sieci web hello hello:**

**Żądanie hello spowodowała zaplecza upłynął limit czasu lub błędu wewnętrznego. zespół Hello bada problem hello. Możemy Przepraszamy za niedogodności hello. (500)**

Twoje parametrów wejściowych może nie być zgodne toohello wymagany format hello internetowych specyficzne dla usługi. Można znaleźć toohello odpowiedniej dokumentacji łącze toofind hello poprawny format dla parametrów wejściowych i ograniczenia hello tej usługi sieci web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Jeśli skopiować łącza hello interfejsu API usługi sieci web hello, które są widoczne na hello strony "Eksploruj ten zestaw danych" i wklej go do innego okna przeglądarki, poświadczeniami, które powinny używać tooaccess hello wyników i jak widać je?**

Należy używać konta witryny Marketplace jako hello nazwy użytkownika i klucza podstawowego konta hello jako hello hasła. klucz podstawowy konta Hello znajduje się na powitania **Eksploruj ten zestaw danych** w obszarze hello opis usługi sieci web hello (kliknij hello **Pokaż** przycisk). wynik Hello może być wyświetlany w przeglądarce hello lub może on być dostępny za pobierania, w zależności od przeglądarki, którego używasz.

**3. Dlaczego uzyskać powitania po wprowadzić dane wejściowe hello usługi sieci web hello na stronie "Eksploruj ten zestaw danych" hello, następujący komunikat o błędzie:** 

**Wystąpił nieoczekiwany błąd podczas przetwarzania żądania. Spróbuj ponownie.**

Jeden lub więcej parametrów wejściowych usługi sieci web została przekroczona limit długości hello przypadku konsumowania usługi sieci web hello w witrynie marketplace hello **Eksploruj ten zestaw danych** strony. Witaj usługi może być wywołany z już długości danych wejściowych przy użyciu metody POST protokołu HTTP. Aby uzyskać przykłady, zobacz [przykładowe rozwiązania z wykorzystaniem R uczenia maszynowego i opublikowanych tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Dlaczego nie widzę żadnych czynności w hello "Interfejsu API EKSPLORATORA" kartę int hello magazynu w hello klasycznego portalu Azure?** 

Jest to znany problem dotyczący hello Azure Classic Portal Marketplace. Witaj zespołu działa tooresolve ten problem. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Pytania dotyczące publikowania z usługi Azure Machine Learning w witrynie Marketplace
**1. Dlaczego moja transakcji logo lub obrazów nie są odświeżanie Moje usługi sieci web?** 

Logo i obrazy są buforowane w portalu publikowania hello i może potrwać dni too10 hello nowe logo lub tooupdate obrazu na powitania portalu.

**2. Dlaczego jest karty "Szczegóły" hello z moją usługę sieci web w witrynie Marketplace przedstawiający komunikat o błędzie?**

Istnieje znany problem Marketplace, łącząc tooAzure uczenie maszynowe, aby uzyskać szczegółowe informacje o usłudze. Witaj zespołu działa tooresolve ten problem.

**3. Dlaczego hello R przykładowy kod w usługach sieci web Azure Machine Learning hello nie działa dla odbierającą hello usług sieci web w witrynie Marketplace?**

systemami uwierzytelniania Hello są różne, bezpośrednie połączenie usługi sieci web uczenie maszynowe tooAzure względem usługi sieci web toothese tooconnecting za pośrednictwem hello Marketplace. usługi Hello w witrynie Marketplace są usługi OData i może być wywołana za pomocą metod GET lub POST. 

**4. Dlaczego są łącza pomocy technicznej hello moją usługę sieci web oferuje nie zostaną zaktualizowane prawidłowo dla niektórych Moje oferty?**

łącza pomocy technicznej Hello są globalne na wydawcy, a nie na ofertę. 

**5. Jak opublikować usługi sieci web za pomocą tryb wprowadzania partii w witrynie Marketplace?**

tryb wprowadzania Hello partii nie jest obecnie obsługiwane w portalu Marketplace usługi sieci web.

**6. Kto I skontaktuj się z tooget pomocy w przypadku pytań dotyczących wydawca danych lub, jeśli mam problemy podczas publikowania?**

Skontaktuj się z zespołem portalu Azure Marketplace hello na < mailto:datamarketbd@microsoft.com > Aby uzyskać więcej informacji.

