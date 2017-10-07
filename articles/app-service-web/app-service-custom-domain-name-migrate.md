---
title: "aaaMigrate DNS usługi active nazwa tooAzure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate niestandardowej nazwy domeny DNS, który jest już przypisany tooa live tooAzure witryny usługi aplikacji bez żadnego przestoju."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Migrowanie active tooAzure nazwę DNS usługi aplikacji

W tym artykule opisano, jak nazwa toomigrate DNS usługi active zbyt[usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) bez żadnego przestoju.

Podczas migracji na żywo lokacji i jej tooApp nazwy domeny DNS usługi, tej nazwy DNS jest już obsługujące ruch na żywo. Można uniknąć przestoju w rozpoznawania nazw DNS podczas migracji hello przez powiązanie preemptively hello active DNS nazwy tooyour aplikacji usługi app Service.

Jeśli nie możesz Obawiamy o przestój w przypadku rozpoznawania nazw DNS, zobacz [mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacje sieci Web](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tym porad:

- [Upewnij się, że aplikację usługi aplikacji nie znajduje się w warstwie bezpłatna](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Powiąż preemptively hello nazwy domeny

Gdy powiąże preemptively niestandardową domenę, osiągnąć obu z następujących hello przed wprowadzeniem jakichkolwiek zmian w rekordach DNS:

- Zweryfikuj prawo własności do domeny
- Włącz hello nazwę domeny aplikacji

Podczas migracji na koniec nazwę DNS niestandardowych z hello starego lokacji toohello aplikacji usługi app Service, nie będzie bez przestojów w rozpoznawania nazw DNS.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Utwórz rekord weryfikacji domeny

rekord tooverify własność domeny, Dodaj TXT. mapuje Hello rekord TXT z _awverify.&lt; Poddomena >_ too_&lt;nazwa_aplikacji >. azurewebsites.net_. 

Hello rekord TXT, które są potrzebne, zależy od hello rekord DNS ma toomigrate. Przykłady można znaleźć w poniższej tabeli hello (`@` zazwyczaj reprezentuje hello domeny katalogu głównego):  

| Przykładowy rekord DNS | TXT Host | Wartość TXT |
| - | - | - |
| @ (root) | _awverify_ | _&lt;Nazwa aplikacji >. azurewebsites.net_ |
| WWW (sub) | _awverify.www_ | _&lt;Nazwa aplikacji >. azurewebsites.net_ |
| \*(symbol wieloznaczny) | _awverify.\*_ | _&lt;Nazwa aplikacji >. azurewebsites.net_ |

Na stronie rekordy DNS należy pamiętać, typ rekordu hello hello ma toomigrate nazwy DNS. Usługa aplikacji obsługuje mapowania z CNAME i.

### <a name="enable-hello-domain-for-your-app"></a>Włącz hello domeny aplikacji

W hello [portalu Azure](https://portal.azure.com), w lewym obszarze nawigacji strony aplikacji hello Witaj, wybierz **domen niestandardowych**. 

![Menu domeny niestandardowej](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

W hello **domen niestandardowych** strona, wybierz hello ** + ** ikona dalej zbyt**dodać nazwę hosta**.

![Dodaj nazwy hosta](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Typ hello pełną nazwę domeny dodaje rekord TXT hello, takich jak `www.contoso.com`. Dla domeny symbolu wieloznacznego (takich jak \*. contoso.com), można użyć dowolnej nazwy DNS, odpowiadający hello domenie symboli wieloznacznych. 

Wybierz **zweryfikować**.

Witaj **dodać nazwę hosta** przycisk jest aktywny. 

Upewnij się, że **typu rekordu Hostname** ustawiono typ rekordu DNS toohello ma toomigrate.

Wybierz **dodać nazwę hosta**.

![Dodaj aplikację toohello nazwy DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Może upłynąć trochę czasu, zanim hello nowe toobe hostname odzwierciedlone w aplikacji hello **domen niestandardowych** strony. Spróbuj odświeżyć dane hello tooupdate przeglądarki hello.

![Dodaje rekord CNAME](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Niestandardowe nazwę DNS jest teraz włączone w aplikacji Azure. 

## <a name="remap-hello-active-dns-name"></a>Ponowne mapowanie hello active nazwy DNS

Witaj tylko element toodo po lewej stronie jest ponowne mapowanie użytkownika active tooApp toopoint rekordów DNS usługi. Prawo teraz, nadal wskazuje tooyour starej lokacji.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Skopiuj adres IP aplikacji hello (rekord tylko)

Jeśli są ponowne mapowanie rekord CNAME, Pomiń tę sekcję. 

rekord A tooremap należy zewnętrznego adresu IP aplikacji usługi aplikacji hello, który jest wyświetlany w hello **domen niestandardowych** strony.

Zamknij hello **dodać nazwę hosta** strony, wybierając **X** w prawym górnym rogu hello. 

W hello **domen niestandardowych** pozycję Kopiuj aplikacji hello adres IP.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Zaktualizuj rekord DNS hello

Ponownie hello stronie rekordy DNS dostawcy domeny, wybierz tooremap rekordów DNS hello.

Dla hello `contoso.com` przykładowa domena główna, ponownie zamapować rekord A lub CNAME hello jak przykłady hello w hello w poniższej tabeli: 

| Przykład nazwy FQDN | Typ rekordu | Host | Wartość |
| - | - | - | - |
| contoso.com (root) | A | `@` | Adres IP z [aplikacji hello kopiowania adresu IP](#info) |
| www.contoso.com (sub) | CNAME | `www` | _&lt;Nazwa aplikacji >. azurewebsites.net_ |
| \*. contoso.com (symbol wieloznaczny) | CNAME | _\*_ | _&lt;Nazwa aplikacji >. azurewebsites.net_ |

Zapisz ustawienia.

Zapytania DNS należy zacząć rozwiązywanie tooyour aplikacji usługi app Service, natychmiast po sytuacji propagacji DNS.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toobind SSL niestandardowych certyfikatów tooApp usługi.

> [!div class="nextstepaction"]
> [Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-ssl.md)
