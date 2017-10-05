---
title: "Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** Zainstaluj program Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca się, zainstaluj program endpoint protection na maszynach wirtualnych Azure (maszyny wirtualne), jeśli program endpoint protection nie jest już włączona. To zalecenie dotyczy tylko maszyn wirtualnych systemu Windows.

> [!NOTE]
> To Przykładowe wdrożenie używa Antimalware firmy Microsoft. Zobacz [integracji partnerskich w Centrum zabezpieczeń Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) lista partnerów zintegrowana z Centrum zabezpieczeń.  
>
>

## <a name="implement-the-recommendation"></a>Wykonania zalecenia

> [!NOTE]
> Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

1. W **zalecenia** bloku, wybierz opcję **Zainstaluj program Endpoint Protection**.
   ![Wybierz Zainstaluj program Endpoint Protection][1]
2. **Zainstaluj program Endpoint Protection** zostanie otwarty blok zawierający listę maszyn wirtualnych bez ochrony punktu końcowego. Wybierz z listy maszyn wirtualnych, które chcesz zainstalować program endpoint protection na, a następnie kliknij przycisk **zainstalować na maszynach wirtualnych**.
   ![Wybierz maszyny wirtualne, aby zainstalować program Endpoint Protection na][2]
3. **Wybierz program Endpoint Protection** zostanie otwarty blok, aby umożliwić wybranie funkcji ochrony punktów końcowych, którego chcesz użyć. W tym przykładzie załóżmy wybierz **Microsoft Antimalware**.
   ![Wybierz program Endpoint Protection][3]
4. Dodatkowe informacje dotyczące funkcji ochrony punktów końcowych są wyświetlane. Wybierz pozycję **Utwórz**.
   ![Tworzenie rozwiązania do ochrony przed złośliwym oprogramowaniem][4]
5. Wprowadź ustawienia konfiguracji na **dodać rozszerzenie** bloku, a następnie wybierz **OK**. Aby dowiedzieć się więcej o ustawieniach konfiguracji, zobacz [domyślnej i niestandardowej konfiguracji ochrony przed złośliwym kodem](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) jest teraz aktywny na wybranych maszyn wirtualnych.

## <a name="see-also"></a>Zobacz też
W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń "Zainstaluj program Endpoint Protection". Aby dowiedzieć się więcej na temat włączania Antimalware firmy Microsoft na platformie Azure, zobacz następujący dokument:

* [Antimalware firmy Microsoft dla usługi w chmurze i maszyn wirtualnych](../security/azure-security-antimalware.md) — Dowiedz się, jak wdrożyć Antimalware firmy Microsoft.

Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, można znaleźć w następujących dokumentach:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
