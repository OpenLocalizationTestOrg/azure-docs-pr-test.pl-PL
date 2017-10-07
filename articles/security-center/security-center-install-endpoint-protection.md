---
title: "aaaInstall Endpoint Protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** Zainstaluj program Endpoint Protection **."
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
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca się, zainstaluj program endpoint protection na maszynach wirtualnych Azure (maszyny wirtualne), jeśli program endpoint protection nie jest już włączona. To zalecenie odnosi się tylko tooWindows maszyn wirtualnych.

> [!NOTE]
> To Przykładowe wdrożenie używa Antimalware firmy Microsoft. Zobacz [integracji partnerskich w Centrum zabezpieczeń Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) lista partnerów zintegrowana z Centrum zabezpieczeń.  
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

1. W hello **zalecenia** bloku, wybierz opcję **Zainstaluj program Endpoint Protection**.
   ![Wybierz Zainstaluj program Endpoint Protection][1]
2. Witaj **Zainstaluj program Endpoint Protection** zostanie otwarty blok zawierający listę maszyn wirtualnych bez ochrony punktu końcowego. Wybierz jedną z hello hello listy maszyn wirtualnych, które mają tooinstall programu endpoint protection na i kliknij przycisk **zainstalować na maszynach wirtualnych**.
   ![Wybierz maszyny wirtualne tooinstall Endpoint Protection na][2]
3. Witaj **wybierz program Endpoint Protection** tooallow zostanie otwarty blok możesz tooselect hello ochrony punktów końcowych ma toouse. W tym przykładzie załóżmy wybierz **Microsoft Antimalware**.
   ![Wybierz program Endpoint Protection][3]
4. Dodatkowe informacje na temat ochrony punktów końcowych hello jest wyświetlany. Wybierz pozycję **Utwórz**.
   ![Tworzenie rozwiązania do ochrony przed złośliwym oprogramowaniem][4]
5. Wprowadź ustawienia konfiguracji hello wymagane na powitania **dodać rozszerzenie** bloku, a następnie wybierz **OK**. toolearn więcej informacji na temat ustawień konfiguracji hello, zobacz [domyślnej i niestandardowej konfiguracji ochrony przed złośliwym kodem](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) jest teraz aktywny na powitania wybrane maszyny wirtualne.

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Zainstaluj program Endpoint Protection". toolearn więcej informacji na temat włączania Antimalware firmy Microsoft na platformie Azure, zobacz następujące dokumentu hello:

* [Antimalware firmy Microsoft dla usługi w chmurze i maszyn wirtualnych](../security/azure-security-antimalware.md) — Dowiedz się, jak toodeploy Antimalware firmy Microsoft.

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz hello w następujących dokumentach:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
