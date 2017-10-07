---
title: "aaaApplication integracja bramy z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera informacje dotyczące integracji brama aplikacji w Centrum zabezpieczeń Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Omówienie integracji między bramą aplikacji i Centrum zabezpieczeń Azure

Dowiedz się, jak bramy aplikacji i Centrum zabezpieczeń pomaga chronić zasobów aplikacji sieci web. Zapora aplikacji sieci web dla aplikacji bramy (WAF) integruje się z [Centrum zabezpieczeń](../security-center/security-center-intro.md) tooprovide tooprevent bezproblemowe widoku, wykrywanie i reagowanie aplikacji sieci web toounprotected toothreats w danym środowisku.

## <a name="overview"></a>Omówienie

Bramy aplikacji zapory aplikacji sieci Web jest zalecenia w Centrum zabezpieczeń do ochrony aplikacji sieci web z luki w zabezpieczeniach i luk w zabezpieczeniach. Zasoby sieci Web jest włączona, które nie są chronione przez zapory aplikacji sieci Web są wyświetlane w Centrum zabezpieczeń hello jako zalecenia o wysokim znaczeniu. Zalecenia dotyczące zapory aplikacji sieci web zostaną wyświetlone na powitania **omówienie** w obszarze **aplikacji**.

![Integracja z Centrum zabezpieczeń][1]

Kliknięcie żadnych zaleceń dotyczących zapory aplikacji sieci web zostanie otwarty nowy blok zawierającego szczegóły hello hello zalecenia.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Dodaj zasób sieci web aplikacji zapory tooan istniejących

Przejdź za**więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na powitania **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **aplikacji**. Na powitania **Centrum zabezpieczeń — aplikacje** bloku hello tabela zawiera listę aplikacji, wykrytych przez Centrum zabezpieczeń w ramach subskrypcji.

![aplikacje sieci Web][3]

Klikając aplikacji sieci web z krytyczny problem, możesz uzyskać hello **kondycja zabezpieczeń aplikacji** bloku. W poniższym obrazie hello hello aplikacji sieci web, która nie jest chroniona przez zapory aplikacji sieci web. 

![zasoby sieci Web, które nie są chronione][2]

Kliknij przycisk **Dodawanie zapory aplikacji sieci web** w obszarze **zalecenia** tooopen hello **Dodawanie zapory aplikacji sieci Web** bloku.

Jeśli nie masz istniejącą bramę aplikacji lub mają toocreate nowy, kliknij przycisk **Utwórz nowy** i na powitania **Tworzenie nowej zapory aplikacji sieci Web** bloku, a następnie kliknij przycisk **Microsoft - Brama aplikacji w**. Powoduje to przejście przez toocreate kroki hello bramy aplikacji. W tym momencie aplikacji sieci web jest dodawany jako zasobu chronionego, Centrum zabezpieczeń teraz śledzi, że ten zasób jest chroniony przez zapory aplikacji sieci web. To nie Dodaj jako członka puli wewnętrznej bazy danych.

Jeśli masz istniejącą bramę aplikacji, można go w **użyć istniejącego rozwiązania**

![Blok dodawania zapory aplikacji sieci Web][4]

Dodawanie bramę aplikacji tooan aplikacji sieci web za pomocą Centrum zabezpieczeń nie powoduje dodania hello zasobu jako członka puli wewnętrznej bazy danych, to należy wykonać w zasobu bramy aplikacji hello bezpośrednio.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Dodaj zasób tooan istniejących zapory aplikacji sieci web

Przejdź za**więcej usług** > **bezpieczeństwo i Obsługa tożsamości** > **Centrum zabezpieczeń** i na powitania **Centrum zabezpieczeń — omówienie**  bloku, kliknij przycisk **rozwiązania partnerskie**. Pokaż istniejącej bramy aplikacji obsługującej Centrum zabezpieczeń w hello **rozwiązań partnerskich** bloku.

![rozwiązania partnerskie][7]

Kliknij przycisk **Połącz aplikację** tooopen hello **łączenie aplikacji** bloku, w tym miejscu można skorzystać hello opcje tooselect istniejących aplikacji. Wybierz tooprotect aplikacji hello i kliknij przycisk **OK**. Nie dodaje hello puli zaplecza toohello aplikacji sieci web z bramy aplikacji hello. Ustawia to zasoby hello jako zasobu chronionego, Centrum zabezpieczeń można śledzić. zasób hello tooadd jako element członkowski puli wewnętrznej bazy danych, należy to zrobić na bramie aplikacji hello, w bieżącym bloku powitania kliknij **Konsola rozwiązań** toobe podjęte zasobu bramy aplikacji toohello umieszczane hello sieci web Pula zaplecza toohello aplikacji.

![aplikacje rozwiązania partnerskie][6]

## <a name="finalize-configuration"></a>Finalizowanie konfiguracji

Centrum zabezpieczeń ścieżki aplikacji dodany tooan bramy aplikacji jako chronionego zasobu.  Monitoruje kondycję hello tego zasobu i zapewnia, że jest chroniony przez bramę aplikacji. Witaj następnym krokiem jest tooadd hello prywatnego adresu IP, publiczny adres IP lub kartę interfejsu Sieciowego w puli zaplecza toohello maszyny wirtualnej bramy aplikacji hello. Dopóki nie jest to dodatkowe zalecenia **Finalizuj ochronę aplikacji** jest wyświetlany dopiero po dodaniu hello zasobów.

![Blok dodawania zapory aplikacji sieci Web][5]

## <a name="security-alerts"></a>Alerty zabezpieczeń

Centrum zabezpieczeń poruszanie się w obrębie zbyt**wykrywania** > **alerty zabezpieczeń**.  W tym miejscu możesz znaleźć alerty zapory aplikacji sieci Web z bramy aplikacji. Alerty są przerwane przez reguły zapory aplikacji sieci Web.

![alerty zabezpieczeń][8]

Kliknięcie reguła określi Lista alertów dla tej określonej reguły zapory aplikacji sieci Web. Każdy alert zawiera dodatkowe szczegóły znajdowanie hello. Szczegóły Hello udostępnienia bramy aplikacji toohello łącza.
 
![Szczegóły alertu][9]

## <a name="next-steps"></a>Następne kroki

jak Zapora aplikacji sieci web tooenable na istniejącą bramę aplikacji, odwiedź stronę toolearn [Tworzenie lub aktualizacja bramy aplikacji Azure z zapory aplikacji sieci web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png