---
title: "Konfigurowanie SSL odciążania — brama aplikacji w usłudze Azure - Azure Portal | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje, aby utworzyć bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu portalu"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a>Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu portalu

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Usługę Azure Application Gateway można skonfigurować tak, aby przerywała sesję protokołu SSL (Secure Sockets Layer) na poziomie bramy, co pozwoli na uniknięcie wykonywania kosztownych zadań szyfrowania protokołu SSL w kolektywie serwerów sieci Web. Odciążanie protokołu SSL upraszcza również konfigurowanie serwerów frontonu i zarządzanie aplikacją sieci Web.

## <a name="scenario"></a>Scenariusz

Poniższy scenariusz przechodzi przez konfigurowanie SSL odciążenia na istniejącą bramę aplikacji. Scenariusz przyjęto założenie, że już zostały wykonane kroki, aby [Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Przed rozpoczęciem

Aby skonfigurować odciążanie protokołu SSL z bramy aplikacji, wymagany jest certyfikat. Ten certyfikat jest załadowany na bramie aplikacji i używany do szyfrowania i odszyfrowywania ruchu wysyłane za pośrednictwem protokołu SSL. Ten certyfikat musi mieć format wymiana informacji osobistych (pfx). Ten format pliku umożliwia klucz prywatny można wyeksportować co jest wymagane przez bramę aplikacji do szyfrowania i deszyfrowania ruchu.

## <a name="add-an-https-listener"></a>Dodaj odbiornika protokołu HTTPS

Odbiornik HTTPS jest szuka ruchu na podstawie konfiguracji i pomaga kierowania ruchu do pul zaplecza.

### <a name="step-1"></a>Krok 1

Przejdź do portalu Azure i wybierz istniejącą bramę aplikacji

### <a name="step-2"></a>Krok 2

Kliknij odbiorników i kliknij przycisk Dodaj, aby dodać odbiornik.

![Blok omówienie bramy aplikacji][1]

### <a name="step-3"></a>Krok 3

Wprowadź wymagane informacje dla odbiornika i przekazywanie certyfikatu PFX, po zakończeniu kliknij przycisk OK.

**Nazwa** — ta wartość jest przyjazną nazwę odbiornika.

**Konfiguracja adresu IP frontonu** — ta wartość jest konfiguracja adresu IP frontonu, która jest używana dla odbiornika.

**Portu frontonu (nazwa/Port)** — użyć przyjazną nazwę dla portu na frontonie bramy aplikacji i rzeczywistym portem.

**Protokół** — przełącznika do określania, jeśli http lub https jest używane dla frontonu.

**Certyfikat (nazwa/hasło)** — odciążania Jeśli protokół SSL jest używany, certyfikatu PFX jest wymagane dla tego ustawienia i przyjazną nazwę i hasło są wymagane.

![Dodawanie bloku odbiornika][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a>Utwórz regułę i powiązać ją do odbiornika

Odbiornik został utworzony. Nadszedł czas, aby utworzyć zasadę, aby obsługiwać ruch z odbiornika. Zasady definiują sposób ruch jest kierowany do pul zaplecza, na podstawie wielu ustawień konfiguracji, w tym, czy koligacji na podstawie plików cookie sesji jest używana, protokół, port i sondy kondycji.

### <a name="step-1"></a>Krok 1

Kliknij przycisk **reguły** bramy aplikacji, a następnie kliknij przycisk Dodaj.

![Blok zasady bramy aplikacji][3]

### <a name="step-2"></a>Krok 2

Na **Dodaj podstawowe reguły** bloku, wpisz przyjazną nazwę reguły i wybierz polecenie odbiornika utworzony w poprzednim kroku. Wybierz pulę zaplecza odpowiednie i ustawienia protokołu http, a następnie kliknij przycisk **OK**

![Okno ustawień protokołu HTTPS][4]

Ustawienia są teraz zapisywane na bramie aplikacji. Proces zapisywania dla tych ustawień może potrwać pewien czas, zanim staną się dostępne do wyświetlenia za pośrednictwem portalu lub przy użyciu programu PowerShell. Po zapisaniu bramy aplikacji obsługuje szyfrowania i odszyfrowywania ruchu. Cały ruch między bramą aplikacji i serwerów sieci web zaplecza będą obsługiwane za pośrednictwem protokołu http. Każdy komunikat do klienta, jeśli inicjowane przy użyciu protokołu https zostaną zwrócone do klienta szyfrowane.

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się, jak skonfigurować sondy kondycji niestandardowych z bramy aplikacji Azure, zobacz [utworzyć sondy kondycji niestandardowych](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
