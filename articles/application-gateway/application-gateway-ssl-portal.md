---
title: "aaaConfigure SSL odciążania — brama aplikacji w usłudze Azure - Portal Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu portalu hello"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu portalu hello

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web. Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.

## <a name="scenario"></a>Scenariusz

powitania po scenariusz przechodzi przez konfigurowanie SSL odciążenia na istniejącą bramę aplikacji. Witaj scenariuszu przyjęto założenie, że już zostały wykonane kroki hello zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Przed rozpoczęciem

tooconfigure odciążanie protokołu SSL z bramy aplikacji, wymagany jest certyfikat. Ten certyfikat jest ładowany w bramie aplikacji hello i używany tooencrypt i odszyfrowywania ruchu hello wysyłane za pośrednictwem protokołu SSL. certyfikat Hello musi toobe Format Wymiana informacji osobistych (pfx). Tego formatu pliku umożliwia dla hello prywatnego klucza toobe wyeksportowane wymaganych przez hello aplikacji bramy tooperform hello szyfrowania i odszyfrowywania ruchu.

## <a name="add-an-https-listener"></a>Dodaj odbiornika protokołu HTTPS

odbiornik HTTPS Hello szuka ruchu na podstawie konfiguracji i pomaga pul zaplecza toohello ruchu hello trasy.

### <a name="step-1"></a>Krok 1

Przejdź toohello portalu Azure i wybierz istniejącą bramę aplikacji

### <a name="step-2"></a>Krok 2

Obiekty nasłuchujące i kliknij tooadd przycisku Dodaj hello odbiornik.

![Blok omówienie bramy aplikacji][1]

### <a name="step-3"></a>Krok 3

Wprowadź wymagane informacje dla odbiornika hello hello i przekazywania hello PFX certyfikatu, po zakończeniu kliknij przycisk OK.

**Nazwa** — ta wartość jest przyjazna nazwa odbiorników hello.

**Konfiguracja adresu IP frontonu** — ta wartość jest hello konfiguracji adresu IP frontonu, służący do hello odbiornika.

**Portu frontonu (nazwa/Port)** -przyjazną nazwę dla hello port używany na powitania frontonu bramy aplikacji hello i port rzeczywiste hello używany.

**Protokół** — toodetermine przełącznika, jeśli frontonu hello jest używany http lub https.

**Certyfikat (nazwa/hasło)** — odciążania Jeśli protokół SSL jest używany, certyfikatu PFX jest wymagane dla tego ustawienia i przyjazną nazwę i hasło są wymagane.

![Dodawanie bloku odbiornika][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Utwórz regułę i powiązać ją odbiornika toohello

odbiornik Hello został utworzony. Jest toocreate czasu reguły toohandle hello ruch z hello odbiornika. Zasady definiują sposób ruch jest kierowany toohello pul zaplecza na podstawie wielu ustawień konfiguracji, w tym, czy koligacji na podstawie plików cookie sesji jest używana, protokół, port i sondy kondycji.

### <a name="step-1"></a>Krok 1

Kliknij przycisk hello **reguły** bramy aplikacji hello, a następnie kliknij przycisk Dodaj.

![Blok zasady bramy aplikacji][3]

### <a name="step-2"></a>Krok 2

Na powitania **Dodaj podstawowe reguły** bloku, wpisz przyjazną nazwę reguły hello hello i wybierz utworzony w poprzednim kroku hello odbiornika hello. Wybierz pulę zaplecza odpowiednie hello i ustawienia protokołu http, a następnie kliknij przycisk **OK**

![Okno ustawień protokołu HTTPS][4]

Ustawienia Hello są teraz zapisywane toohello bramy aplikacji. Hello Zapisz proces dla tych ustawień może trochę potrwać, zanim staną się dostępne tooview za pośrednictwem portalu hello lub za pomocą programu PowerShell. Brama aplikacji hello raz zapisane obsługuje hello szyfrowania i odszyfrowywania ruchu. Cały ruch między bramą aplikacji hello i serwerów sieci web zaplecza hello będą obsługiwane za pośrednictwem protokołu http. Dowolnego klienta do tyłu toohello komunikacji Jeśli inicjowane przy użyciu protokołu https, zostanie zwrócony klienta toohello szyfrowane.

## <a name="next-steps"></a>Następne kroki

toolearn tooconfigure niestandardowych kondycji sondowania z bramy aplikacji Azure, zobacz [utworzyć sondy kondycji niestandardowych](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
