---
title: "aaaAzure dziennika integracji z dzienników inspekcji usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello Usługa integracji dziennika Azure oraz integrowanie dzienniki z dzienników inspekcji platformy Azure"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integracja dzienników inspekcji usługi Azure Active Directory

Zdarzenia inspekcji w usłudze Azure Active Directory (Azure AD) pomaga zidentyfikować uprzywilejowanych akcji, które wystąpiły w usłudze Azure Active Directory. Widać hello typy zdarzeń, które można śledzić, przeglądając [zdarzenia raportów inspekcji usługi Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Przed rozpoczęciem powitalne opisanych w tym artykule, należy przejrzeć hello [wprowadzenie](security-azure-log-integration-get-started.md) artykułu i wykonaj kroki hello istnieje.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Dzienniki inspekcji w usłudze Azure Active directory toointegrate kroki

1. Otwórz wiersz polecenia hello i uruchom to polecenie:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Uruchom następujące polecenie: 
 
   ``azlog createazureid``

   To polecenie wyświetla monit o podanie logowania do systemu Azure. Witaj polecenie następnie tworzy usługi Azure Active Directory nazwy głównej usługi w dzierżawcy usługi Azure AD hello hostujących hello subskrypcji platformy Azure, w których hello zalogowanego użytkownika jest administratora, administratora współpracującego lub właściciela. polecenie Hello zakończy się niepowodzeniem, jeśli tylko użytkownik-Gość w dzierżawie usługi Azure AD hello jest hello zalogowanego użytkownika. TooAzure uwierzytelnianie odbywa się za pośrednictwem usługi Azure AD. Tworzenie nazwy głównej usługi integracji dziennika Azure tworzy hello tożsamości usługi Azure AD, która uzyskuje dostęp tooread z subskrypcji platformy Azure.

3. Uruchom następujące polecenie tooprovide hello swojego identyfikatora dzierżawcy. Należy toobe członkiem hello dzierżawy admin roli toorun hello polecenia.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Przykład:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Sprawdź, czy powitania po tooconfirm folderów, które hello JSON dziennik inspekcji usługi Azure Active Directory są tworzone w nich:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Witaj poniżej film wideo przedstawia kroki hello omówione w tym artykule:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Aby uzyskać szczegółowe instrukcje dotyczące przełączania hello informacji w plikach JSON hello do informacji o zabezpieczeniach i zdarzeń systemu zarządzania (SIEM) skontaktuj się z dostawcą SIEM.

Społeczność pomoc jest dostępna za pośrednictwem hello [Forum MSDN integracji dziennika Azure](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Tym forum umożliwia pracownikom hello Azure dziennika integracji społeczności toosupport siebie z pytania, odpowiedzi, porady i wskazówki. Ponadto hello Azure dziennika integracji zespołu monitoruje tym forum i pomaga zawsze, gdy mogą go.

Można również otworzyć [żądania obsługi](../azure-supportability/how-to-create-azure-support-request.md). Wybierz **integracji dziennika** jako usługa hello żądania pomocy technicznej.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat integracji dziennika Azure, zobacz:

* [Microsoft Azure dziennika integracji Azure dzienników](https://www.microsoft.com/download/details.aspx?id=53324): strony Centrum pobierania ten zapewnia szczegółowe informacje, wymagania systemowe i instrukcje dotyczące instalacji integracji dziennika Azure.
* [Wprowadzenie tooAzure integracji dziennika](security-azure-log-integration-overview.md): w tym artykule przedstawiono tooAzure integracji dziennika, jego kluczowych możliwości i sposobu działania.
* [Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): ten wpis w blogu pokazuje, jak rozwiązania Splunk, HP ArcSight i IBM QRadar partnerskie tooconfigure toowork Azure dziennika integracji z.
* [Często zadawane pytania Azure dziennika integracji](security-azure-log-integration-faq.md): w tym artykule odpowiedzi na pytania dotyczące integracji dziennika Azure.
* [Integrowanie alerty Centrum zabezpieczeń Azure dziennika w przypadku integracji](../security-center/security-center-integrating-alerts-with-log-integration.md): w tym artykule opisano, jak alerty Centrum zabezpieczeń toosync, wraz z zebranych przez diagnostyki Azure i dzienników inspekcji platformy Azure, z Twojego analizy dzienników zdarzeń zabezpieczeń maszyny wirtualnej lub Rozwiązania SIEM.
* [Nowe funkcje diagnostyki Azure i Azure dzienniki inspekcji](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): ten wpis w blogu wprowadza tooAzure dzienniki inspekcji i inne funkcje, które ułatwiają uzyskać wgląd w działania hello zasobów platformy Azure.
