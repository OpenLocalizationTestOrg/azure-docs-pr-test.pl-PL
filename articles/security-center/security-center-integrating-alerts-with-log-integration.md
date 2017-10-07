---
title: "alerty Centrum zabezpieczeń Azure aaaIntegrating Azure dziennika integracji | Dokumentacja firmy Microsoft"
description: "Ten artykuł ułatwia szybkie wprowadzenie do integracji alerty Centrum zabezpieczeń z integracji dzienników Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Integrowanie z integracją dzienników Azure alerty Centrum zabezpieczeń Azure
Wiele operacji zabezpieczeń i odpowiedzi na zdarzenia zespołów zależne rozwiązania Security Information and Event Management (SIEM) jako hello punkt początkowy dla klasyfikowane i badanie alertów zabezpieczeń. W przypadku integracji dziennika Azure alerty Centrum zabezpieczeń Azure można zintegrować z rozwiązania SIEM.

Integracja dzienników Azure obsługuje obecnie HP ArcSight, Splunk i IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Jakie dzienniki można zintegrować?
Azure tworzy szczegółowe rejestrowanie dla każdej usługi. Te dzienniki są sklasyfikowane jako:

* **Dzienniki sterowania i zarządzania nimi** , które powodują widoczność hello operacje tworzenia Menedżera zasobów Azure, UPDATE i DELETE. Te zdarzenia płaszczyzny sterowania są udostępniane w hello Azure Dzienniki aktywności
* **Dzienniki płaszczyzna danych** , które powodują widoczność hello zdarzenia wywoływane, gdy przy użyciu zasobów platformy Azure. Przykładem jest dziennika zdarzeń systemu Windows hello, gdzie można uzyskać informacji o zabezpieczeniach zdarzenia z Podglądu zdarzeń hello kanału zabezpieczeń. Zdarzenia płaszczyzna danych (które są generowane przez maszynę wirtualną lub usługę Azure) są udostępniane przez dzienników diagnostycznych platformy Azure.

Integracja dzienników Azure obsługuje obecnie hello integracji:

* Dzienniki maszyny Wirtualnej platformy Azure
* Dzienniki inspekcji Azure
* Alerty Centrum zabezpieczeń Azure

## <a name="install-azure-log-integration"></a>Zainstaluj integracji dzienników Azure
Pobierz [integracji dzienników Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Witaj dzienników Azure Usługa integracji zbiera dane telemetryczne z hello maszyny, na którym jest zainstalowany.  Zbierane dane z telemetrii jest:

* Wyjątków występujących podczas wykonywania integracji dzienników Azure
* Metryki o liczbie hello zapytań i przetwarzania zdarzeń
* Statystyki, o które Azlog.exe są używane opcje wiersza polecenia

> [!NOTE]
> Zbieranie danych telemetrycznych można wyłączyć, usuwając zaznaczenie pola wyboru tej opcji.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integracja alerty Centrum zabezpieczeń i dzienników inspekcji platformy Azure
1. Witaj Otwórz wiersz polecenia i **cd** do **c:\Program Files\Microsoft Azure dziennika integracji**.
2. Uruchom hello **azlog createazureid** toocreate polecenia [Azure Active Directory — nazwy głównej usługi](../active-directory/active-directory-application-objects.md) w hello Azure Active Directory (AD) dzierżawcami, które obsługują hello subskrypcji platformy Azure.

    Zostanie wyświetlony monit o logowania do systemu Azure.

   > [!NOTE]
   > Musi być subskrypcji hello właściciela lub Współadministratorem subskrypcji hello.
   >
   >

    TooAzure uwierzytelnianie odbywa się za pośrednictwem usługi Azure AD.  Tworzenie nazwy głównej usługi integracji dzienników Azure tworzy hello tożsamości usługi Azure AD, która uzyskuje dostęp tooread z subskrypcji platformy Azure.
3. Uruchom hello **autoryzować azlog <SubscriptionID>**  polecenia tooassign czytnika dostępu na powitania subskrypcji toohello nazwy głównej usługi utworzony w kroku 2. Jeśli nie określisz **SubscriptionID**, a następnie nazwy głównej usługi hello jest przypisany hello czytnika roli tooall subskrypcje toowhich masz dostęp.

   > [!NOTE]
   > Ostrzeżenia mogą pojawić po uruchomieniu hello **autoryzować** polecenia natychmiast po hello **createazureid** polecenia. Brak niektórych opóźnienia między po utworzeniu konta hello Azure AD i kiedy konto hello jest dostępny do użytku. Jeśli Poczekaj około 10 sekund po uruchomieniu hello **createazureid** hello toorun polecenia **autoryzować** polecenia, a następnie nie powinna być widoczna te ostrzeżenia dotyczące.
   >
   >
4. Sprawdź, czy powitania po tooconfirm folderów, które hello JSON w plikach dziennika inspekcji są:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Sprawdź hello tooconfirm folderów, które alerty Centrum zabezpieczeń w nich następujące:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Skonfiguruj hello SIEM pliku usługi przesyłania dalej łącznika toohello odpowiedni folder. procedury Hello różni się zależnie od hello SIEM używasz.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji o Dzienniki aktywności platformy Azure i definicji właściwości, zobacz:

* [Operacje inspekcji w usłudze Resource Manager](../azure-resource-manager/resource-group-audit.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — hello najnowsze zabezpieczeń platformy Azure i informacji.
