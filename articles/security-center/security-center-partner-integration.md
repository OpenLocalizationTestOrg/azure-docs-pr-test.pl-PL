---
title: "Integracja aaaPartner w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu Centrum zabezpieczeń Azure integruje się z partnerami tooenhance ogólnej zabezpieczeń zasobów platformy Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Integracja z partnerami w usłudze Azure Security Center

W tym artykule opisano sposób Centrum zabezpieczeń Azure integruje się z partnerami toohelp zwiększyć ogólne bezpieczeństwo. Centrum zabezpieczeń zapewnia zintegrowane środowisko na platformie Azure i wykorzystuje hello Azure Marketplace partnera certyfikacji i rozliczeń.

> [!NOTE] 
> Począwszy od czerwca 2017 Centrum zabezpieczeń używa programu Microsoft Monitoring Agent hello toocollect i magazynu danych. Aby uzyskać więcej informacji, zobacz artykuł [Migracja platformy usługi Azure Security Center](security-center-platform-migration.md). Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Dlaczego warto wdrażać rozwiązania partnerskie z usługi Security Center

Są cztery główne przyczyny tooleverage partnera integracji w Centrum zabezpieczeń:

- **Łatwość wdrażania**. Wdrażanie rozwiązania partnerów przy hello następujące zalecenia Centrum zabezpieczeń jest znacznie prostsze. proces wdrażania Hello można całkowicie zautomatyzować przy użyciu topologii sieci i ustawienia domyślne. Alternatywnie klienci mogą wybrać opcję częściowej automatyzacji, dającą większą elastyczność i możliwość dostosowania.
- **Zintegrowane wykrycia**. Zdarzenia zabezpieczeń z rozwiązań partnerskich są automatycznie zbierane, agregowane i wyświetlane w ramach zdarzeń i alertów usługi Security Center. Te zdarzenia są również zespolone z wykrycia z tooprovide źródeł, inne zaawansowane funkcje wykrywania zagrożeń.
- **Ujednolicone monitorowanie i zarządzanie**. Klienci mogą użyć toomonitor zdarzenia zintegrowane kondycji wszystkich rozwiązań partnerskich jeden rzut oka. Podstawowe możliwości zarządzania jest dostępny, instalację tooadvanced łatwy dostęp przy użyciu hello rozwiązaniem partnerskim.
- **Eksportuj tooSIEM**. Klientów można wyeksportować wszystkie Centrum zabezpieczeń i partnera wspólnych alerty systemów lokalnych tooon Format zdarzenia (CEF) Security Information and Event Management (SIEM) przy użyciu integracji dzienników Azure (wersja zapoznawcza).


## <a name="partners-that-integrate-with-security-center"></a>Partnerzy, którzy integrują się z usługą Security Center

Obecnie usługę Security Center można zintegrować z następującymi rozwiązaniami:

- Ochrona punktów końcowych ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec i [usługa firmy Microsoft chroniąca przed złośliwym kodem dla usług Azure Cloud Services i maszyn wirtualnych](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Zapora aplikacji sieci Web ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) i [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Zapora nowej generacji ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) i [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Ocena luk w zabezpieczeniach ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Wraz z upływem czasu Centrum zabezpieczeń będzie rozwiń hello liczby partnerów w ramach tych kategorii i dodać nowe kategorie. 

## <a name="deploy-a-partner-solution"></a>Wdrażanie rozwiązania partnerów

Na podstawie konfiguracji hello środowiska platformy Azure i zasady zabezpieczeń hello zdefiniowanych Centrum zabezpieczeń może zalecić, aby wdrożyć rozwiązanie partnerskie. Witaj zalecenia Centrum zabezpieczeń prowadzi użytkownika przez proces hello wyboru i zainstalowaniu rozwiązanie partnerskie. Witaj cały proces wdrażania może się różnić, w zależności od typu hello rozwiązania i partnera, którego używasz. Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [Instalowanie ochrony punktu końcowego](security-center-install-endpoint-protection.md)
- [Dodawanie zapory aplikacji sieci Web](security-center-add-web-application-firewall.md)
- [Dodawanie zapory nowej generacji](security-center-add-next-generation-firewall.md)
- [Funkcja oceny luk w zabezpieczeniach nie jest zainstalowana](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Zarządzanie rozwiązaniami partnerskimi

Po wdrożeniu tooview informacje o kondycji rozwiązania hello hello i wykonywać zadania zarządzania podstawowego, na powitania **Centrum zabezpieczeń** bloku, wybierz hello **rozwiązania partnerskie** opcji. Aby uzyskać więcej informacji na temat zarządzania rozwiązaniami partnerskimi w usłudze Security Center, zobacz artykuł [Monitor partner solutions with Azure Security Center](security-center-partner-solutions.md) (Monitorowanie rozwiązań partnerskich w usłudze Azure Security Center).

![Integracja z partnerami](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Obsługa ochrony punktu końcowego firmy Symantec jest ograniczona toodiscovery. Nie są dostępne żadne alerty dotyczące kondycji.
>

## <a name="see-also"></a>Zobacz też

W tym artykule przedstawiono sposób toointegrate partnera rozwiązań w Centrum zabezpieczeń Azure. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące artykuły hello:

* [Przewodnik planowania i obsługi usługi Security Center](security-center-planning-and-operations-guide.md)
* [Zarządzanie i reagowanie na alerty toosecurity w Centrum zabezpieczeń](security-center-managing-and-responding-alerts.md)
* [Alerty zabezpieczeń według typu w usłudze Security Center](security-center-alerts-type.md)
* [Monitorowanie kondycji zabezpieczeń w usłudze Security Center](security-center-monitoring.md). Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Monitorowanie rozwiązań partnerskich w usłudze Security Center](security-center-partner-solutions.md). Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md). Pobierz zadawane pytania dotyczące korzystania z usługi hello toofrequently odpowiedzi.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
