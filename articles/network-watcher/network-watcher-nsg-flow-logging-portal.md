---
title: "Dzienniki przepływu grupy zabezpieczeń sieci aaaManage z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób rejestrowania toomanage przepływu sieciowej grupy zabezpieczeń w obserwatora sieciowego Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Zarządzanie dziennikami przepływu grupy zabezpieczeń sieci w portalu Azure hello

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [Interfejs API REST](network-watcher-nsg-flow-logging-rest.md)

Dzienniki przepływu grupy zabezpieczeń sieci są funkcją obserwatora sieciowego, umożliwiający tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci. Te dzienniki przepływu są zapisywane w formacie JSON i zawierają istotne informacje, w tym: 

- Wychodzące i przychodzące przepływem na podstawie reguł.
- dotyczy Hello hello przepływ karty interfejsu Sieciowego.
- 5-elementowej informacje o przepływu hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego, protokół).
- Informacja, czy dozwolony lub odrzucany ruchu.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć wystąpienia obserwatora sieciowego](network-watcher-create.md). Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną.

## <a name="register-insights-provider"></a>Zarejestruj dostawcę usługi Insights

Przepływ hello pomyślnie, rejestrowanie toowork **elemencie Microsoft.Insights** dostawcy musi być zarejestrowana. Dostawca hello tooregister, hello wykonaj następujące kroki: 

1. Przejdź za**subskrypcje**, a następnie wybierz hello subskrypcji, dla której ma zostać tooenable przepływu dzienników. 
2. Na powitania **subskrypcji** bloku, wybierz opcję **dostawców zasobów**. 
3. Spójrz na hello listy dostawców i sprawdź, że hello **elemencie microsoft.insights** dostawca został zarejestrowany. Jeśli nie, następnie wybierz **zarejestrować**.

![Widok dostawców][providers]

## <a name="enable-flow-logs"></a>Włączanie dzienników przepływu

Te kroki przejście hello proces włączania przepływu dzienniki w lokacji sieciowej grupy zabezpieczeń.

### <a name="step-1"></a>Krok 1

Przejdź do wystąpienia obserwatora sieciowego tooa, a następnie wybierz **przepływ NSG rejestruje**.

![Przegląd dzienników przepływu][1]

### <a name="step-2"></a>Krok 2

Wybierz grupy zabezpieczeń sieci z listy hello.

![Przegląd dzienników przepływu][2]

### <a name="step-3"></a>Krok 3 

Na powitania **ustawień dzienników przepływu** bloku, Ustaw stan hello zbyt**na**, a następnie skonfiguruj konto magazynu.  Gdy wszystko będzie gotowe, wybierz **OK**. Następnie wybierz **zapisać**.

![Przegląd dzienników przepływu][3]

## <a name="download-flow-logs"></a>Pobierz dzienniki przepływu

Przepływ dzienniki są zapisywane na koncie magazynu. Pobieranie Twojej tooview dzienniki przepływu je.

### <a name="step-1"></a>Krok 1

toodownload przepływ dzienników, wybierz **dzienniki przepływu można pobrać z kont magazynu skonfigurowanych**. Ten krok umożliwia przejście widoku konto magazynu tooa którego można określić, które toodownload dzienniki.

![Przepływ ustawień dzienników][4]

### <a name="step-2"></a>Krok 2

Przejdź do konta magazynu poprawne toohello. Następnie wybierz **kontenery** > **insights — dziennik networksecuritygroupflowevent**.

![Przepływ ustawień dzienników][5]

### <a name="step-3"></a>Krok 3

Przejdź do lokalizacji toohello hello przepływu dziennika, zaznacz go, a następnie wybierz **Pobierz**.

![Przepływ ustawień dzienników][6]

Informacji o strukturze hello hello dziennika można znaleźć [Omówienie dziennika przepływu grupy zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[wizualizacji dzienników przepływu grupy NSG z usługą Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
