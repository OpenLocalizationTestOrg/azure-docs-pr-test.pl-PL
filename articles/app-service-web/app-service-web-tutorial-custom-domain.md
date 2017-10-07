---
title: "aaaMap istniejących niestandardowe DNS nazwa aplikacji sieci Web tooAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd istniejącą domenę DNS niestandardowej nazwy aplikacji sieci web (domena niestandardowych) tooa, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web

Usługa [Azure Web Apps](app-service-web-overview.md) oferuje wysoce skalowalną i samonaprawialną usługę hostowaną w Internecie. Ten samouczek pokazuje, jak toomap istniejących DNS niestandardowej nazwy tooAzure aplikacji sieci Web.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Mapowanie poddomeny (na przykład `www.contoso.com`) przy użyciu rekordu CNAME
> * Mapowanie domeny katalogu głównego (na przykład `contoso.com`) przy użyciu rekord a.
> * Zamapować domenę symboli wieloznacznych (na przykład `*.contoso.com`) przy użyciu rekordu CNAME
> * Mapowanie domeny przy użyciu skryptów automatyzacji

Możesz użyć dowolnej **rekord CNAME** lub **rekordu** toomap DNS niestandardowej nazwy tooApp usługi. 

> [!NOTE]
> Zalecane jest użycie rekord CNAME dla wszystkich niestandardowych nazw DNS z wyjątkiem domeny katalogu głównego (na przykład `contoso.com`).

toomigrate witryny na żywo i jego tooApp nazwy domeny DNS usługi, zobacz [migracji active tooAzure nazwę DNS usługi aplikacji](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

* [Utwórz aplikację usługi aplikacji](/azure/app-service/), lub użyć utworzonego w samouczku innej aplikacji.
* Kup nazwę domeny i upewnij się, że masz dostęp toohello DNS rejestru dla dostawcy domeny (na przykład GoDaddy).

  Na przykład tooadd wpisów DNS dla `contoso.com` i `www.contoso.com`, musi być możliwe tooconfigure hello ustawień DNS na potrzeby hello `contoso.com` domeny głównej.

  > [!NOTE]
  > Jeśli nie masz istniejącej domeny nazwa, należy wziąć pod uwagę [zakupu domeny przy użyciu hello portalu Azure](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Przygotowywanie aplikacji hello

toomap niestandardowe DNS nazwy tooa aplikacji sieci web, aplikacji sieci web hello [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być płatną warstwy (**Shared**, **podstawowe**, **standardowe**, lub  **Premium**). W tym kroku, możesz upewnij się, że tej aplikacji usługi aplikacji znajduje się w hello hello obsługiwane warstwy cenowej.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Przejdź do aplikacji toohello w hello portalu Azure

Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji hello.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/select-app.png)

Zostanie wyświetlona strona zarządzania hello z hello aplikacji usługi app Service.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Sprawdź hello warstwy cenowej

Lewy pasek nawigacyjny strony aplikacji hello hello, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

Warstwa bieżąca aplikacja Hello zostanie wyróżniona niebieskim obramowaniem. Sprawdź toomake się, że aplikacja hello nie jest hello **wolne** warstwy. Niestandardowe DNS nie jest obsługiwany w hello **wolne** warstwy. 

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Jeśli hello planu usługi aplikacji nie jest **wolne**, zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[mapy rekord CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Skalowanie w górę hello planu usługi aplikacji

Wybierz jedno z warstw — wolne hello (**Shared**, **podstawowe**, **standardowe**, lub **Premium**). 

Kliknij pozycję **Wybierz**.

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.

![Potwierdzenie operacji skalowania](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Mapa rekord CNAME

W samouczku przykład Witaj, Dodaj rekord CNAME dla hello `www` domeny podrzędnej (na przykład `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Utwórz rekord CNAME hello

Dodaj toomap rekordów CNAME hostname domyślnej aplikacji toohello domeny podrzędnej (`<app_name>.azurewebsites.net`).

Dla hello `www.contoso.com` przykład domeny, Dodaj rekord CNAME, który mapuje nazwę hello `www` zbyt`<app_name>.azurewebsites.net`.

Po dodaniu hello CNAME strony rekordy DNS hello wygląda hello poniższy przykład:

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Włącz mapowanie rekordu CNAME hello na platformie Azure

Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**. 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

W hello **domen niestandardowych** strony aplikacji hello, Dodaj hello w pełni kwalifikowana nazwa DNS niestandardowe (`www.contoso.com`) toohello listy.

Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Typ hello pełną nazwę domeny dodaje rekord CNAME, takich jak `www.contoso.com`. 

Wybierz **zweryfikować**.

Witaj **dodać nazwę hosta** przycisk jest aktywny. 

Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**CNAME (www.example.com lub wszystkie poddomeny)**.

Wybierz **dodać nazwę hosta**.

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony. Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, u dołu hello hello strony.

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Mapa rekord a.

W przykładzie samouczek hello dodaniu rekordu A dla domeny głównej hello (na przykład `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Skopiuj adres IP aplikacji hello

rekord A toomap należy aplikacji hello zewnętrzny adres IP. Ten adres IP można znaleźć w aplikacji hello **domen niestandardowych** strony w hello portalu Azure.

Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**. 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

W hello **domen niestandardowych** pozycję Kopiuj aplikacji hello adres IP.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Utwórz rekord A hello

wymaga usługi aplikacji toomap A tooan rekordów aplikacji, **dwóch** rekordy DNS:

- **A** rejestrowany adres IP toomap toohello aplikacji.
- A **TXT** zarejestrować nazwę hosta domyślnego toomap toohello aplikacji `<app_name>.azurewebsites.net`. Usługa aplikacji używa tego rekordu tylko podczas konfiguracji, czy jesteś właścicielem domeny niestandardowej hello tooverify. Po domeny niestandardowej jest weryfikowane i skonfigurowaniu w usłudze App Service, można usunąć tego rekordu TXT. 

Dla hello `contoso.com` przykład domeny utworzyć rekordy A i TXT hello zgodnie z poniższej tabeli toohello (`@` zazwyczaj reprezentuje hello domeny głównej). 

| Typ rekordu | Host | Wartość |
| - | - | - |
| A | `@` | Adres IP z [aplikacji hello kopiowania adresu IP](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Dodanie rekordów hello hello strony rekordy DNS wygląda hello poniższy przykład:

![Strona rekordów DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Włącz hello mapowanie rekordu w aplikacji hello

W aplikacji hello **domen niestandardowych** strony hello portalu Azure, należy dodać hello w pełni kwalifikowana nazwa DNS niestandardowe (na przykład `contoso.com`) toohello listy.

Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Typ hello pełną nazwę domeny skonfigurować rekord hello A, takich jak `contoso.com`.

Wybierz **zweryfikować**.

Witaj **dodać nazwę hosta** przycisk jest aktywny. 

Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**rekordu (example.com)**.

Wybierz **dodać nazwę hosta**.

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony. Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.

![Dodaje rekord](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Możesz pominąć krok lub wkradła się Literówka gdzieś wcześniej, zostanie wyświetlony błąd weryfikacji, u dołu hello hello strony.

![Błąd weryfikacji](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Zamapować domenę symboli wieloznacznych

W przykładzie samouczek hello mapy [nazwa DNS z symbolem wieloznacznym](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (na przykład `*.contoso.com`) toohello aplikacji usługi app Service przez dodanie rekordu CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Utwórz rekord CNAME hello

Dodaj nazwę hosta domyślnego symbolu wieloznacznego nazwa toohello aplikacji toomap rekordów CNAME (`<app_name>.azurewebsites.net`).

Dla hello `*.contoso.com` przykład domeny hello rekord CNAME przypisze nazwę hello `*` zbyt`<app_name>.azurewebsites.net`.

Po dodaniu hello CNAME hello strony rekordy DNS wygląda hello poniższy przykład:

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Włącz mapowanie rekordu CNAME hello w aplikacji hello

Można teraz dodawać żadnych poddomeny odpowiadający hello symbolu wieloznacznego nazwa toohello aplikacji (na przykład `sub1.contoso.com` i `sub2.contoso.com` odpowiada `*.contoso.com`). 

Hello wywołało nawigacji strony aplikacji hello hello portalu Azure, wybierz **domen niestandardowych**. 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Wybierz hello  **+**  ikona dalej zbyt**dodać nazwę hosta**.

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Wpisz w pełni kwalifikowaną nazwą domeny odpowiadający hello domenie symbolu wieloznacznego (na przykład `sub1.contoso.com`), a następnie wybierz **weryfikacji**.

Witaj **dodać nazwę hosta** przycisk jest aktywny. 

Upewnij się, że **typu rekordu Hostname** ustawiono zbyt**rekord CNAME (www.example.com lub wszystkie poddomeny)**.

Wybierz **dodać nazwę hosta**.

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony. Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.

Wybierz hello  **+**  ikonę ponownie tooadd innej nazwy hosta odpowiadający hello domenie symboli wieloznacznych. Na przykład dodać `sub2.contoso.com`.

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Testowanie w przeglądarce

Przeglądaj toohello nazwy DNS, który został wcześniej skonfigurowany (na przykład `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, i `sub2.contoso.com`).

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Zautomatyzować za pomocą skryptów

Można zautomatyzować zarządzanie domenami niestandardowymi za pomocą skryptów, za pomocą hello [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure 

Witaj następujące polecenie dodaje skonfigurowane niestandardowe DNS nazwy tooan aplikacji usługi app Service. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Aby uzyskać więcej informacji, zobacz [mapy domeny niestandardowej aplikacji sieci web tooa](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Witaj następujące polecenie dodaje skonfigurowane niestandardowe DNS nazwy tooan aplikacji usługi app Service. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Aby uzyskać więcej informacji, zobacz [przypisać domeny niestandardowej aplikacji sieci web tooa](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Mapa poddomeny przy użyciu rekordu CNAME
> * Mapa domeny głównej, przy użyciu rekord a.
> * Zamapować domenę symboli wieloznacznych przy użyciu rekordu CNAME
> * Mapowanie domeny przy użyciu skryptów automatyzacji

Przejść dalej toolearn samouczka toohello jak toobind SSL niestandardowych certyfikatów tooa aplikacji sieci web.

> [!div class="nextstepaction"]
> [Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-ssl.md)
