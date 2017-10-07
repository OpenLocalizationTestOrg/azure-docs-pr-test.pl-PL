---
title: "zachowanie aaaOverride HTTP przy użyciu aparatu reguł hello Azure CDN | Dokumentacja firmy Microsoft"
description: "aparat reguł Hello umożliwia toocustomize sposób obsługi żądań HTTP przez usługi Azure CDN, takich jak blokowanie hello dostarczania niektórych typów zawartości, definiowania zasad buforowania i modyfikować nagłówki HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Zastąpienie zachowania HTTP przy użyciu aparatu reguł hello Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Omówienie
aparat reguł Hello umożliwia toocustomize sposób obsługi żądań HTTP, takich jak blokowanie hello dostarczania niektórych typów zawartości, definiowania zasad buforowania i modyfikowanie nagłówków HTTP.  W tym samouczku zostanie pokazują, że tworzenia reguły, która zmieni hello buforowanie zasobów w sieci CDN.  Również jest dostępna w hello zawartości wideo "[Zobacz też](#see-also)" sekcji.

   > [!TIP] 
   > Odwołanie składni toohello szczegółowo, zobacz [odwołanie do aparatu reguł](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Samouczek
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Polecenie hello **HTTP dużych** kartę, a następnie **aparatu reguł**.
   
    Opcje dla nowej reguły są wyświetlane.
   
    ![Nowe opcje reguły CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > kolejność Hello, w którym są wyświetlane wiele reguł ma wpływ na sposób obsługi. Kolejne reguły mogą zastąpić akcje hello określone przez poprzednie reguły.
   > 
   > 
3. Wprowadź nazwę w hello **nazwę / opis** pola tekstowego.
4. Określ typ hello żądań, które hello reguła będzie dotyczyć.  Domyślnie program hello **zawsze** wybrano warunek dopasowania.  Użyjesz **zawsze** w tym samouczku, dlatego pozostaw wybrany.
   
   ![Warunek dopasowania CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Istnieje wiele typów dopasowania dostępne w listy rozwijanej hello warunki.  Kliknięcie toohello informacyjną ikona hello niebieski lewej warunku dopasowania hello objaśnia hello aktualnie wybrany warunek szczegółowo.
   > 
   >  Witaj pełną listę wyrażeń warunkowych szczegółowo, zobacz [wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Witaj pełną listę warunków dopasowania szczegółowo, zobacz [warunki odpowiada aparatu reguł](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Kliknij przycisk hello  **+**  obok przycisku zbyt**funkcje** tooadd nowej funkcji.  Z listy rozwijanej hello powitania po lewej stronie, wybierz **życie wewnętrzny Max-Age**.  W polu tekstowym hello, która jest wyświetlana, wprowadź **300**.  Pozostaw hello pozostałe wartości domyślne.
   
   ![Funkcja CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Zgodnie z warunkami dopasowania, klikając toohello informacyjną ikona hello blue lewej strony hello nowe funkcji wyświetli szczegółowe informacje na temat tej funkcji.  W przypadku hello **życie wewnętrzny Max-Age**, możemy są zastępowanie zasobów hello **Cache-Control** i **Expires** toocontrol nagłówków, gdy węzeł brzegowy CDN hello odświeży hello zasobów z hello źródła.  Naszym przykładzie 300 sekund oznacza, że węzeł brzegowy CDN hello będą buforowane hello zasobów przez 5 minut przed odświeżeniem zawartości hello ze swoją witryną źródłową.
   > 
   > Witaj pełną listę funkcji, które szczegółowo, zobacz [Szczegóły funkcji aparatu reguł](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Kliknij przycisk hello **Dodaj** przycisk toosave hello nowej reguły.  Nowa reguła Hello teraz oczekuje na zatwierdzenie. Po jej zatwierdzeniu hello stan zmieni się z **oczekujące XML** za**Active XML**.
   
   > [!IMPORTANT]
   > Zmiany zasad może trwać too90 toopropagate minut za pośrednictwem hello CDN.
   > 
   > 

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure CDN](cdn-overview.md)
* [Odwołanie do aparatu reguł](cdn-rules-engine-reference.md)
* [Warunki uzgadniania aparatu reguł](cdn-rules-engine-reference-match-conditions.md)
* [Wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-conditional-expressions.md)
* [Funkcje aparatu reguł](cdn-rules-engine-reference-features.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
* [Azure piątki: Usługi Azure CDN zaawansowanych nowych funkcji Premium](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (klip wideo)