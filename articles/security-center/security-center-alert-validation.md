---
title: "aaaAlerts weryfikacji w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia alerty zabezpieczeń hello toovalidate w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Walidacja alertów w usłudze Azure Security Center
Ten dokument ułatwia Dowiedz się, jak tooverify, jeśli system jest poprawnie skonfigurowany na potrzeby alerty Centrum zabezpieczeń Azure.

## <a name="what-are-security-alerts"></a>Czym są alerty zabezpieczeń?
Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci hello i połączonych rozwiązań partnerskich, takich jak zapory i punktu końcowego rozwiązań do ochrony, toodetect i alertów można toothreats. Odczyt [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) Aby uzyskać więcej informacji na temat alertów zabezpieczeń i Odczyt [opis alertów zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn więcej o różnych typach hello alertów.

## <a name="alert-validation"></a>Walidacja alertu
Po zainstalowaniu agenta Centrum zabezpieczeń na komputerze, wykonaj kroki hello poniżej z komputera hello miejscu zasobów atak powitania toobe hello alertu:

1. Skopiuj pulpitu toohello pliku wykonywalnego (na przykład calc.exe) lub innego katalogu wygody.
2. Zmień nazwę tego pliku zbyt**ASC_AlertTest_662jfi039N.exe**.
3. Otwórz wiersz polecenia hello i wykonywanie tego pliku z argumentem (po prostu fałszywych argument nazwy), takich jak: *ASC_AlertTest_662jfi039N.exe - foo*
4. Zaczekaj 5 minut too10 i otwórz alerty Centrum zabezpieczeń. Powinna być widoczna alertu toofollowing podobne, co:

    ![Walidacja alertu](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Podczas przeglądania ten alert, upewnij się, że pole hello włączyć inspekcję argumentów jest wyświetlany jako true. Zawiera ona wartość false, należy najpierw tooenable argumenty wiersza polecenia inspekcji. Można włączyć tę opcję, przy użyciu następującego wiersza polecenia hello:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Zobacz też
W tym artykule wprowadzono procesu weryfikacji toohello alertów. Teraz, kiedy znasz tej weryfikacji, spróbuj hello następujące artykuły:

* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Dowiedz się, jak toomanage alerty i zdarzenia toosecurity odpowiedź w Centrum zabezpieczeń.
* [Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md). Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Informacje o alertach zabezpieczeń w usłudze Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Dowiedz się więcej o różnych typach hello alertów zabezpieczeń.
* [Przewodnik rozwiązywania problemów z usługą Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Dowiedz się, jak tootroubleshoot typowe problemy w Centrum zabezpieczeń. 
* [Azure Security Center — często zadawane pytania](security-center-faq.md). Znajdź często zadawane pytania dotyczące korzystania z usługi hello.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

