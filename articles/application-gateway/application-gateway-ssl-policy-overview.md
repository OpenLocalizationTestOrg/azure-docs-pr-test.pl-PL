---
title: "Omówienie zasad aaaSSL bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat bramy aplikacji Azure umożliwia tooconfigure zasady SSL"
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>Omówienie zasad SSL bramy aplikacji

Brama aplikacji umożliwia zarządzanie certyfikatami SSL toocentralize i zmniejszyć koszty szyfrowania i odszyfrowywania z farmy serwerów wewnętrznej bazy danych. Ten SSL scentralizowane Obsługa również umożliwia toospecify SSL centralnej zasady odpowiednie wymagania dotyczące zabezpieczeń organizacji tooyour. To ułatwia spełnia zarówno wymagania zgodności, a także wskazówki dotyczące zabezpieczeń i zalecane rozwiązania.

Zasady protokołu SSL zawierają kontroli wersji protokołu SSL, a także mechanizmów szyfrowania i kolejność hello szyfry są używane podczas uzgadniania protokołu SSL. Do tej bramy aplikacji oferuje dwa mechanizmy tooallow klientów toocontrol SSL zasad, wstępnie zdefiniowanych lub niestandardowych zasad.

## <a name="predefined-ssl-policy"></a>Wstępnie zdefiniowane zasady SSL

Brama aplikacji ma trzy wstępnie zdefiniowane zasady. Za pomocą dowolnego z tych zasad tooget hello odpowiedni poziom zabezpieczeń, można skonfigurować bramy. nazwy zasad Hello są przypisane przez hello rok i miesiąc, w którym zostały skonfigurowane. Każdej zasady oferty różnych wersji protokołu SSL i mechanizmów szyfrowania. Zalecane jest toouse hello najnowsze zasady tooensure hello najlepsze SSL zabezpieczeń SSL. Brama aplikacji w obecnie umożliwia toochoose użytkowników z jednej z poniższych hello wstępnie zdefiniowane.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|Właściwość  |Wartość  |
|---|---|
|Nazwa     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|Domyślne| Wartość true (jeśli został określony nie wstępnie zdefiniowanych zasad) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|Właściwość  |Wartość  |
|   ---      |  ---       |
|Nazwa     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|Domyślne| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|Właściwość  |Wartość  |
|---|---|
|Nazwa     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|Domyślne| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>Niestandardowe zasady SSL

Jeśli wstępnie zdefiniowane zasady SSL musi toobe skonfigurowany dla wymagań, masz musi definiować własne niestandardowe zasady SSL. W takim przypadku możesz mieć pełną kontrolę nad toosupport wersji protokołu SSL hello minimalna jak również obsługiwanych mechanizmów szyfrowania i ich kolejność priorytetów.
 
Wersji protokołu SSL:

* Protokoły SSL 2.0 i 3.0 są domyślnie wyłączane dla wszystkich bram aplikacji. Te wersje protokołu nie są konfigurowalne.
* Niestandardowe SSL zasad definicji zapewnia opcję tooselect jedno hello następujące trzy protokoły jako hello minimalna SSL protokołu wersja bramy TLSv1_0, TLSv1_1, TLSv1_2.
* Jeśli nie SSL zdefiniowano zasad wszystkie trzy (TLSv1_0, TLSv1_1, TLSv1_2) są włączone.

Mechanizmy szyfrowania:

Brama aplikacji w obsługuje hello następujące mechanizmy szyfrowania, z których można wybrać zasadami niestandardowymi. Hello kolejności mechanizmów szyfrowania hello określa kolejność priorytetów hello podczas negocjacji w protokole SSL.

Mechanizmy szyfrowania dostępne:

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>Następne kroki

[Skonfiguruj zasady SSL na bramy aplikacji](application-gateway-configure-ssl-policy-powershell.md)
