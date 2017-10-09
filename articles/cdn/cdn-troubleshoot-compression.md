---
title: "aaaTroubleshooting kompresji plików w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z kompresji plików Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Rozwiązywanie problemów związanych z kompresją pliku CDN
Ten artykuł ułatwia rozwiązywanie problemów z [kompresji plików CDN](cdn-improve-performance.md).

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i kliknij przycisk **Get Support**.

## <a name="symptom"></a>Objaw
Kompresja dla punktu końcowego jest włączona, ale pliki są zwracane nieskompresowane.

> [!TIP]
> toocheck czy pliki zostały zwrócone skompresowany, potrzebujesz toouse, takich jak narzędzie [Fiddler](http://www.telerik.com/fiddler) lub przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Nagłówki odpowiedzi hello HTTP wyboru zwrócone z sieci CDN pamięci podręcznej zawartości.  Jeśli istnieje nagłówek o nazwie `Content-Encoding` o wartości **gzip**, **bzip2**, lub **deflate**, jest skompresowana zawartość.
> 
> ![Kodowanie zawartości nagłówka](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Przyczyna
Istnieje kilka możliwych przyczyn, w tym:

* Witaj zażądał zawartości nie jest uprawniony do kompresji.
* Nie włączono kompresję hello żądany typ pliku.
* Hello żądania HTTP nie zawiera nagłówka zażądał typu prawidłowy kompresji.

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów
> [!TIP]
> Podobnie jak w przypadku wdrażania nowych punktów końcowych, zmiany w konfiguracji sieci CDN zająć niektórych toopropagate czas za pośrednictwem sieci hello.  Zwykle zmiany zostaną zastosowane w ciągu 90 minut.  Jeśli jest to powitania po skonfigurowaniu kompresji dla punktu końcowego CDN po raz pierwszy, należy rozważyć oczekuje się, że ustawienia kompresji hello zostaną rozpropagowane POP toohello toobe 1 – 2 godz. 
> 
> 

### <a name="verify-hello-request"></a>Sprawdź hello żądania
Najpierw należy wykonać związane z poprawnością szybkie sprawdzenie hello żądania.  Można użyć przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello żądań wysyłanych.

* Sprawdź wysyłanie żądania hello tooyour adres URL punktu końcowego, `<endpointname>.azureedge.net`, a nie źródła.
* Sprawdź Żądanie hello zawiera **Accept-Encoding** nagłówka i hello wartość dla nagłówka zawiera **gzip**, **deflate**, lub **bzip2** .

> [!NOTE]
> **Azure CDN from Akamai** profile obsługują tylko **gzip** kodowania.
> 
> 

![Nagłówki żądania CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie standardowa)
> [!NOTE]
> Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Standard from Verizon** lub **Azure CDN Standard from Akamai** profilu. 
> 
> 

Przejdź do punktu końcowego tooyour w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk hello **Konfiguruj** przycisku.

* Sprawdź, czy kompresja jest włączona.
* Sprawdź hello typ MIME dla zawartości toobe skompresowane jest uwzględniona w hello listy formatów skompresowany hello.

![Ustawienia kompresji CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie Premium)
> [!NOTE]
> Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Premium from Verizon** profilu.
> 
> 

Przejdź do punktu końcowego tooyour w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk hello **Zarządzaj** przycisku.  zostanie otwarta Hello portalu dodatkowym.  Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.  Kliknij przycisk **kompresji**. 

* Sprawdź, czy kompresja jest włączona.
* Sprawdź hello **typów plików** lista zawiera listę rozdzielanych przecinkami (bez spacji) typów MIME.
* Sprawdź hello typ MIME dla zawartości toobe skompresowane jest uwzględniona w hello listy formatów skompresowany hello.

![Ustawienia kompresji sieci CDN w warstwie premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Sprawdź, czy hello zawartość jest buforowana
> [!NOTE]
> Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).
> 
> 

Przy użyciu narzędzia dla deweloperów w przeglądarce, sprawdź, czy hello odpowiedzi nagłówki tooensure hello plików jest buforowana w regionie hello, w którym jest on wymagany.

* Sprawdź hello **serwera** nagłówka odpowiedzi.  Nagłówek Hello musi mieć hello format **platformy (serwer protokołu POP/ID)**, jak pokazano w hello poniższy przykład.
* Sprawdź hello **pamięci podręcznej X** nagłówka odpowiedzi.  należy odczytać nagłówka Hello **TRAFIEŃ**.  

![Nagłówki odpowiedzi CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Sprawdź, czy plik hello spełnia wymagania dotyczące rozmiaru hello
> [!NOTE]
> Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).
> 
> 

toobe kwalifikuje się do kompresji, plik musi spełniać następujące wymagania dotyczące rozmiaru hello:

* Większe niż 128 bajtów.
* Mniejszy niż 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Sprawdzanie hello żądania na serwerze pochodzenia hello **za pośrednictwem** nagłówka
Witaj **za pośrednictwem** wskazuje nagłówka HTTP serwera sieci web toohello hello żądania jest przekazywany przez serwer proxy.  Serwery sieci web Microsoft IIS domyślnie nie Kompresuj odpowiedzi, gdy Żądanie hello zawiera **za pośrednictwem** nagłówka.  toooverride to zachowanie, wykonaj następujące hello:

* **IIS 6**: [ustawić HcNoCompressionForProxies = "FALSE" hello właściwości metabazy usług IIS](https://msdn.microsoft.com/library/ms525390.aspx)
* **Usługi IIS 7 i nowsze**: [wartość **noCompressionForHttp10** i **noCompressionForProxies** tooFalse w konfiguracji serwera hello](http://www.iis.net/configreference/system.webserver/httpcompression)

