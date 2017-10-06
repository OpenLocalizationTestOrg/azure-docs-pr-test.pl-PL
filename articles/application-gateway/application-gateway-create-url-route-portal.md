---
title: "aaaCreate na podstawie ścieżki reguły — brama aplikacji w usłudze Azure - Portal Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate reguły na podstawie ścieżki dla bramy aplikacji przy użyciu hello portalu"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Tworzenie reguły na podstawie ścieżki dla bramy aplikacji przy użyciu portalu hello

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-url-route-cli.md)

Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http. Sprawdza, czy jest skonfigurowane dla adresu URL hello na liście hello brama aplikacji w puli zaplecza tooa trasy, a wysyła toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza. Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.

Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły. Brama aplikacji ma dwa typy zasad: zasady podstawowe i na podstawie ścieżki. Witaj typu podstawowe reguły, zapewnia usługi okrężnego dla zaplecza hello pul podczas reguły ścieżki dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania puli zaplecza odpowiednie hello.

## <a name="scenario"></a>Scenariusz

Witaj następujący scenariusz przechodzi przez utworzenie w istniejącą bramę aplikacji na podstawie ścieżki reguły.
Witaj scenariuszu przyjęto założenie, że już zostały wykonane kroki hello zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).

![trasy adresu URL][scenario]

## <a name="createrule"></a>Tworzenie reguły na podstawie ścieżki hello

Reguły na podstawie ścieżki wymaga własnego odbiornika, przed utworzeniem reguły hello można tooverify się, że masz toouse dostępne odbiornika.

### <a name="step-1"></a>Krok 1

Przejdź toohello [portalu Azure](http://portal.azure.com) i wybierz istniejącą bramę aplikacji. Kliknij przycisk **reguły**

![Application Gateway — omówienie][1]

### <a name="step-2"></a>Krok 2

Kliknij przycisk **na podstawie ścieżki** tooadd przycisk nowej reguły na podstawie ścieżki.

### <a name="step-3"></a>Krok 3

Witaj **reguły na podstawie ścieżki Dodaj** bloku ma dwie sekcje. Pierwsza sekcja Hello jest, gdzie są zdefiniowane hello odbiornika, nazwa hello hello reguły i ustawienia ścieżki domyślnej hello. ustawienia ścieżki domyślna Hello są dla tras, które nie są objęte hello niestandardowej ścieżki na podstawie trasy. Witaj drugiej sekcji hello **reguły na podstawie ścieżki Dodaj** bloku jest, gdzie został zdefiniowany hello ścieżki reguły oparte na siebie.

**Ustawienia podstawowe**

* **Nazwa** — ta wartość jest regułą toohello przyjazną nazwę dostępnej w portalu hello.
* **Odbiornik** — ta wartość jest hello odbiornik, który jest używany dla hello reguły.
* **Domyślna pula zaplecza** — to ustawienie jest ustawieniem hello, definiujący toobe zaplecza hello używany dla reguły domyślnej hello
* **Domyślne ustawienia HTTP** — to ustawienie jest ustawienie hello, który definiuje toobe ustawienia HTTP hello używany dla reguły domyślnej hello.

**Reguły ścieżki**

* **Nazwa** — ta wartość jest przyjazną nazwę reguły na podstawie toopath.
* **Ścieżki** — to ustawienie określa hello ścieżki hello reguły szuka podczas przesyłania ruchu
* **Puli zaplecza** — to ustawienie jest ustawieniem hello, definiujący hello toobe zaplecza dla reguły hello używane
* **Ustawienie HTTP** — to ustawienie jest ustawieniem hello, definiujący toobe ustawienia HTTP hello używany dla reguły hello.

> [!IMPORTANT]
> Ścieżki: Lista hello ścieżka toomatch wzorców. Każdy musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolona znajduje się na końcu hello. Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *.  

![Dodawanie bloku reguły na podstawie ścieżki z informacjami o wypełnione][2]

Dodawanie tooan reguły na podstawie ścieżki istniejącą bramę aplikacji jest łatwy za pośrednictwem portalu hello. Po utworzeniu reguły na podstawie ścieżki, może być edytowany tooadd dodatkowe reguły. 

![Dodawanie dodatkowych reguły ścieżki][3]

Ten krok obejmuje skonfigurowanie trasę na podstawie ścieżki. Jest ważne toounderstand, że żądania są nie ulegną, jak żądania są dostępne w bramy aplikacji sprawdza żądania hello oraz basic na powitania adresu url wzorca Wysyła hello żądania toohello odpowiednie zaplecza.

## <a name="next-steps"></a>Następne kroki

toolearn tooconfigure odciążanie protokołu SSL z bramy aplikacji Azure, zobacz temat [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
