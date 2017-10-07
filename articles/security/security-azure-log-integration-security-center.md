---
title: "aaaAzure dziennika integracji z Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooget zabezpieczeń Azure Centrum Praca z integracji dziennika alertów"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Jak tooget Twojego Centrum zabezpieczeń alerty integracji dzienników Azure
Ten artykuł zawiera hello kroki wymagane tooenable hello Azure dziennika integracji usługi toopull zabezpieczeń informacji o alertach generowanych przez Centrum zabezpieczeń Azure. Należy pomyślnie ukończono kroki hello hello [wprowadzenie](security-azure-log-integration-get-started.md) artykuł przed wykonaniem kroków hello w tym artykule.

## <a name="detailed-steps"></a>Szczegółowe procedury
Witaj kroków spowoduje utworzenie hello wymagane usługi Azure Active Directory — nazwy głównej usługi i przypisz hello zasady usługi subskrypcji toohello uprawnienia do odczytu:
1. Otwórz wiersz polecenia hello i przejdź zbyt**c:\Program Files\Microsoft Azure dziennika integracji**
2. Uruchom polecenie hello``azlog createazureid``

    To polecenie wyświetla monit o podanie logowania do systemu Azure. polecenie Hello następnie tworzy [Azure Active Directory — nazwy głównej usługi](../active-directory/develop/active-directory-application-objects.md) w hello dzierżaw usługi Azure AD, obsługujące hello subskrypcji platformy Azure, w których hello zalogowanego użytkownika jest administratora, administratora współpracującego lub właściciela. polecenie Hello zakończy się niepowodzeniem, jeśli tylko użytkownik-Gość w hello dzierżawy Azure AD jest hello zalogowanego użytkownika. TooAzure uwierzytelnianie odbywa się za pośrednictwem usługi Azure Active Directory (AD). Tworzenie nazwy głównej usługi integracji Azlog tworzy hello tożsamości usługi Azure AD, które będzie mieć dostęp tooread z subskrypcji platformy Azure.

2. Obok należy uruchomić polecenie, które przypisuje dostęp czytelnika na powitania subskrypcji toohello nazwy głównej usługi utworzony w kroku 2. Jeśli nie określisz SubscriptionID polecenia hello podejmie tooassign hello usługi czytnika głównej roli tooall subskrypcje toowhich masz dostęp. </br></br>
``azlog authorize <SubscriptionID>`` </br> na przykład </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Ostrzeżenia mogą pojawić po uruchomieniu hello autoryzować polecenie natychmiast po poleceniu createazureid hello. Brak niektórych opóźnienia między po utworzeniu konta hello Azure AD i kiedy konto hello jest dostępny do użytku. Jeśli poczekać około 60 sekund po uruchomieniu hello createazureid polecenia toorun hello autoryzacji polecenia, a następnie nie powinna być widoczna tych ostrzeżeń.

4. Sprawdź, czy powitania po tooconfirm folderów, które hello JSON w plikach dziennika inspekcji są:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Sprawdź hello tooconfirm folderów, które alerty Centrum zabezpieczeń w nich następujące:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Jeśli wystąpiły problemy podczas hello instalacji i konfiguracji, otwórz [żądania obsługi](/azure-supportability/how-to-create-azure-support-request.md), wybierz pozycję **integracji dziennika** jako usługa hello żądania pomocy technicznej.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat integracji Azure dziennika Zobacz hello w następujących dokumentach:

* [Microsoft Azure dziennika integracji Azure dzienników](https://www.microsoft.com/download/details.aspx?id=53324) — Centrum pobierania, aby uzyskać szczegółowe informacje, wymagania systemowe i zainstalować instrukcje dotyczące integracji dzienników Azure.
* [Wprowadzenie tooAzure dziennika integracji](security-azure-log-integration-overview.md) — tym dokumencie przedstawiono tooAzure dziennika integracji, jego kluczowych możliwości i jak działa.
* [Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — ten wpis w blogu pokazuje, jak tooconfigure Azure dziennika toowork integracji z rozwiązań partnerskich Splunk HP ArcSight i IBM QRadar.
* [Dzienników Azure — często zadawane pytania (FAQ) integracji](security-azure-log-integration-faq.md) — to często zadawane pytania dotyczące odpowiedzi na pytania dotyczące integracji dzienników Azure.
* [Integrowanie Centrum zabezpieczeń alertów z usługi Azure dziennika integracji](../security-center/security-center-integrating-alerts-with-log-integration.md) — tym dokumencie przedstawiono, jak alerty Centrum zabezpieczeń toosync, wraz z zebrane przez diagnostyki Azure i dzienników inspekcji platformy Azure, z Twojego analizy dzienników zdarzeń zabezpieczeń maszyny wirtualnej lub Rozwiązania SIEM.
* [Nowe funkcje diagnostyki Azure i dzienników inspekcji platformy Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) — ten wpis w blogu wprowadza tooAzure dzienniki inspekcji i inne funkcje, które ułatwiają uzyskać wgląd w działania hello zasobów platformy Azure.
