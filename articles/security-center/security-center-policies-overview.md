---
title: "Wprowadzenie do zasad zabezpieczeń Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad zabezpieczeń Centrum zabezpieczeń Azure i kluczowych możliwości."
services: security-center
documentationcenter: na
author: YuriDio
manager: MBaldwin
editor: 
ms.assetid: f24b1e4a-cc36-4542-b21e-041453cdfcd8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/13/2017
ms.author: yurid
ms.openlocfilehash: 7a4d056fa71f211dea5e7be649c39034eabc9395
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2017
---
# <a name="security-policies-overview"></a>Omówienie zasad zabezpieczeń
Ten artykuł zawiera omówienie zasad zabezpieczeń w Centrum zabezpieczeń.

## <a name="what-are-security-policies"></a>Czym są zasady zabezpieczeń?
Zasady zabezpieczeń definiują pożądaną konfigurację Twoich obciążeń oraz pomagają zapewnić zgodność z wymaganiami dotyczącymi zabezpieczeń określonymi przez firmę lub przepisy. W Centrum zabezpieczeń Azure można zdefiniować zasady dla subskrypcji platformy Azure i dostosować je do danego typu obciążenia i wrażliwość danych. Na przykład aplikacje korzystające z danymi podlegającymi ochronie, takich jak dane osobowe, mogą wymagać wyższego poziomu zabezpieczeń niż innych obciążeń. 

Zasady usługi Security Center zawierają następujące składniki:

- **Zbieranie danych**: Określa agenta inicjowania obsługi administracyjnej i [zbierania danych](https://docs.microsoft.com/azure/security-center/security-center-enable-data-collection) ustawienia.
- **Zasady zabezpieczeń**: Określa, który kontroluje monitorów Centrum zabezpieczeń i zaleca. Można edytować [zasady zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-policies) w Centrum zabezpieczeń. Można również użyć [zasadami Azure](security-center-azure-policy.md) (w wersji zapoznawczej ograniczone) do tworzenia nowych definicji, zdefiniuj dodatkowe zasady, a przypisanie zasad w grupach zarządzania.
- **Wiadomości e-mail z powiadomieniami**: Określa kontaktów zabezpieczeń i [powiadomień e-mail](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details) ustawienia.
- **Warstwa cenowa**: definiuje wolnego lub standard [cennik wybór](https://docs.microsoft.com/azure/security-center/security-center-pricing). Wybranej warstwie określa funkcji Centrum zabezpieczeń, które są dostępne dla zasobów w zakresie. Można określić warstwy dla subskrypcji, grupy zasobów i obszarów roboczych. 


## <a name="who-can-edit-security-policies"></a>Kto może edytować zasady zabezpieczeń?
Centrum zabezpieczeń używa opartej na rolach kontroli dostępu (RBAC), który zawiera wbudowane role, które można przypisać do użytkowników, grup i usług Azure. Po otwarciu Centrum zabezpieczeń, zostanie wyświetlona tylko informacje związane z zasobami, które mają dostęp do. Co oznacza, że użytkownicy są przypisane roli *właściciela*, *współautora*, lub *czytnika* do zasobu należącego do grupy zasobów lub subskrypcji. Oprócz tych ról istnieją dwie określone role usługi Security Center:

- **Czytnik zabezpieczeń**: ma widoku praw do Centrum zabezpieczeń, który zawiera zalecenia, alertów, zasad i kondycji, ale ich nie można wprowadzić zmian.
- **Administrator zabezpieczeń**: mają te same prawa widoku jako *czytnika zabezpieczeń*, i może również zaktualizować zasady zabezpieczeń i odrzucić zalecenia i alerty.


## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono informacje dotyczące zasad zabezpieczeń w Centrum zabezpieczeń Azure. Aby dowiedzieć się więcej na temat Centrum zabezpieczeń Azure, zobacz następujące artykuły:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md): informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md): Dowiedz się, w jaki sposób zalecenia Centrum zabezpieczeń ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md) — informacje na temat monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w usłudze Azure Security Center](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
- [Bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md): Dowiedz się, jak zarządza i zabezpiecza dane w Centrum zabezpieczeń.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/): Pobierz najnowsze zabezpieczeń platformy Azure i informacje.


