---
title: "aaaHandling alerty zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia przypadki naruszenia zabezpieczeń toohandle toouse Centrum zabezpieczeń Azure możliwości."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center
Klasyfikowane i badanie alertów zabezpieczeń może zająć dużo czasu na powitania nawet najbardziej doświadczona analityków zabezpieczeń i dla wielu jest tooeven twardym wiedzieć, gdzie toobegin. Za pomocą [analytics](security-center-detection-capabilities.md) tooconnect hello informacji między różne [alerty zabezpieczeń](security-center-managing-and-responding-alerts.md), Centrum zabezpieczeń zapewnia jednolity obraz kampanii ataku i wszystkich hello powiązanych alertów — możesz szybko poznać trwało atakująca hello jakie akcje i jakie zasoby został zmieniony.

W tym dokumencie omówiono sposób zabezpieczeń toouse ostrzec możliwości w Centrum zabezpieczeń tooassist obsługi zdarzeń zabezpieczeń.

## <a name="what-is-a-security-incident"></a>Co to jest zdarzenie naruszenia zabezpieczeń?
W usłudze Security Center zdarzenie naruszenia zabezpieczeń to agregacja wszystkich alertów zasobu, które są zgodne ze wzorcami [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/), tzw. „zabójczego łańcucha”. Zdarzenia są wyświetlane w hello [alerty zabezpieczeń](security-center-managing-and-responding-alerts.md) kafelków i bloku. Zdarzenie będzie ujawnić hello listę powiązanych alertów, dzięki czemu możesz tooobtain więcej informacji na temat każdego wystąpienia.

## <a name="managing-security-incidents"></a>Zarządzanie zdarzeniami naruszenia zabezpieczeń
Patrząc na kafelku alerty zabezpieczeń hello można przejrzeć bieżącego przypadki naruszenia zabezpieczeń. Dostęp do portalu Azure hello i wykonaj kroki hello poniżej toosee więcej szczegółów na temat każdego zdarzenia zabezpieczeń:

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, zobaczysz hello **alerty zabezpieczeń** kafelka.

    ![Kafelek Alerty zabezpieczeń w usłudze Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. Kliknięcie tego kafelka tooexpand go i jeśli zostanie wykryty zdarzenia zabezpieczeń, zostanie wyświetlony w obszarze hello wykres alerty zabezpieczeń w sposób przedstawiony poniżej:

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig2.png)

3. Powiadomienie, że opis zdarzenia zabezpieczeń hello ma inną ikonę porównywany tooother alertów. Kliknij go tooview bardziej szczegółowe informacje dotyczące tego zdarzenia.

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig3.png)

4. Na powitania **zdarzenia** bloku pojawi się bardziej szczegółowych informacji o tego zdarzenia zabezpieczeń obejmuje pełny opis, jego ważności (czyli w tym przypadku wysokiej), jego bieżący stan (w tym przypadku jest nadal *aktywny*, które sugeruje hello użytkownika nie podjęte tooit działania — można to zrobić, klikając prawym przyciskiem myszy na powitania zdarzenia w programie hello **alerty zabezpieczeń** blok), zasobu atak powitania (w tym przypadku *VM1*), hello czynności korygujące dla zdarzenia hello i w hello dolne okienko masz hello alertów, które wchodzą w skład tego zdarzenia. Więcej informacji o każdym alercie ma tooobtain zostanie otwarty po prostu kliknij go, a kolejny blok, jak pokazano poniżej:

    ![Zdarzenie naruszenia zabezpieczeń](./media/security-center-incident/security-center-incident-fig4.png)

Hello informacji na temat tego bloku różnią się zgodnie z toohello alertu. Odczyt [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) Aby uzyskać więcej informacji na temat toomanage te alerty. Pewne istotne kwestie dotyczące tej funkcji:

* Nowy filtr umożliwia toocustomize, który tooIncident z widoku tylko alerty tylko, lub obie.
* powitalne tego samego alertu może istnieć w ramach zdarzenia (jeśli dotyczy), a także toobe widoczne jako alert autonomicznych.

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono sposób toouse hello możliwości zdarzenia zabezpieczeń w Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md)
* [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md)
* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md)
* [Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md)
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
