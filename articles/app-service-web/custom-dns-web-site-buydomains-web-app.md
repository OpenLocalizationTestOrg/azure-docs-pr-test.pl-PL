---
title: aaaBuy niestandardowej nazwy domeny dla aplikacji sieci Web Azure
description: "Dowiedz się, jak nazwa toobuy domeny niestandardowej z aplikacją sieci web w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Kup niestandardowej nazwy domeny dla aplikacji sieci Web Azure

Domeny aplikacji usługi (wersja zapoznawcza) są domeny najwyższego poziomu, które są zarządzane bezpośrednio na platformie Azure. One był łatwy toomanage domen niestandardowych dla [Azure Web Apps](app-service-web-overview.md). Ten samouczek pokazuje, jak toobuy domeny usługi aplikacji i przypisz DNS nazwy tooAzure aplikacji sieci Web.

Ten artykuł dotyczy usługi Azure App Service (aplikacje sieci Web, aplikacje API Apps, Mobile Apps, Logic Apps). Dla maszyny Wirtualnej platformy Azure lub usługi Azure Storage, zobacz [tooAzure domeny przypisać usługi aplikacji maszyny Wirtualnej lub usługi Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Dla usług w chmurze, zobacz [Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

* [Utwórz aplikację usługi aplikacji](/azure/app-service/), lub użyć utworzonego w samouczku innej aplikacji.

## <a name="prepare-hello-app"></a>Przygotowywanie aplikacji hello

domen niestandardowych toouse w aplikacji sieci Web Azure, aplikacji sieci web firmy [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być płatną warstwy (**współużytkowane**, **podstawowe**, **standardowe**, lub **Premium**). W tym kroku, możesz upewnij się, że tej aplikacji sieci web hello jest w hello obsługiwane warstwy cenowej.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure

Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Przejdź do aplikacji toohello w hello portalu Azure

Wybierz z menu po lewej stronie powitania **usługi aplikacji**, a następnie wybierz nazwę hello aplikacji hello.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-domain/select-app.png)

Zostanie wyświetlona strona zarządzania hello z hello aplikacji usługi app Service.  

### <a name="check-hello-pricing-tier"></a>Sprawdź hello warstwy cenowej

Lewy pasek nawigacyjny strony aplikacji hello hello, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

Warstwa bieżąca aplikacja Hello zostanie wyróżniona niebieskim obramowaniem. Sprawdź toomake się, że aplikacja hello nie jest hello **wolne** warstwy. Niestandardowe DNS nie jest obsługiwany w hello **wolne** warstwy. 

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Jeśli hello planu usługi aplikacji nie jest **wolne**, zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[domeny hello Kup](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Skalowanie w górę hello planu usługi aplikacji

Wybierz jedno z warstw — wolne hello (**Shared**, **podstawowe**, **standardowe**, lub **Premium**). 

Kliknij pozycję **Wybierz**.

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.

![Potwierdzenie operacji skalowania](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Kup hello domeny

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure
Otwórz hello [portalu Azure](https://portal.azure.com/) i zaloguj się przy użyciu konta platformy Azure.

### <a name="launch-buy-domains"></a>Uruchamianie Kup domen
W hello **aplikacje sieci Web** , kliknij pozycję hello nazwę aplikacji sieci web, wybierz opcję **ustawienia**, a następnie wybierz **domen niestandardowych**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

W hello **domen niestandardowych** kliknij przycisk **kupić domen**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Skonfiguruj hello domeny zakupu

W hello **aplikacji usługi domeny** strony w hello **wyszukiwania dla domeny** okno, nazwa domeny hello typu toobuy i typ `Enter`. Witaj sugerowane dostępnych domen są wyświetlane poniżej pola tekstowego hello. Wybierz co najmniej jedna domena ma toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Kliknij przycisk hello **informacje kontaktowe** i wypełnij formularz informacji kontaktowych hello domeny. Gdy skończysz, kliknij przycisk **OK** tooreturn toohello aplikacji usługi domeny strony.
   
Należy wypełnić wszystkie wymagane pola z dokładnością tak jak to możliwe. Nieprawidłowe dane, aby uzyskać więcej informacji może spowodować niepowodzenie toopurchase domen. 

Następnie wybierz opcje hello potrzebne dla danej domeny. Zobacz hello w poniższej tabeli objaśnienia:

| Ustawienie | Sugerowana wartość | Opis |
|-|-|-|
|Automatycznego odnawiania | **Włączanie** | Odnawia domenę usługi App automatycznie co roku. Karty kredytowej jest rozliczana hello tej samej cenie zakupu w czasie hello odnawiania. |
|Ochrona prywatności | Włączanie | Zgódź się zbyt "Ochrona prywatności", który jest dostępny w hello zapłaconej kwoty _bezpłatnie_ (z wyjątkiem domen najwyższego poziomu, którego rejestr nie obsługują ochrony prywatności, takich jak _. co.in_, _. co.uk_i tak dalej). |
| Przypisz domyślne nazwy hostów | **www** i**@** | Wybierz hello żądana powiązań z nazwami hostów, w razie potrzeby. Po zakończeniu operacji zakupu domeny hello aplikacji sieci web są dostępne na powitania wybrane nazwy hostów. Jeśli aplikacja sieci web hello jest za [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), nie widzisz domeny głównej hello hello opcja tooassign (@), ponieważ Menedżera ruchu jest nie rekordów A pomocy technicznej. Należy wprowadzić zmiany przypisania hostname toohello po zakończeniu zakupu domeny hello. |

### <a name="accept-terms-and-purchase"></a>Zaakceptuj postanowienia i zakupu

Kliknij przycisk **postanowienia prawne** tooreview hello warunków i opłat hello, następnie kliknij przycisk **kupić**.

> [!NOTE]
> Domeny aplikacji usługi użyj domeny hello toohost usługi Azure DNS. Ponadto toohello opłata rejestracja domeny, użycia dla usługi Azure DNS opłaty. Aby uzyskać informacje, zobacz [cennik usługi Azure DNS](https://azure.microsoft.com/pricing/details/dns/).
>
>

Po powrocie do hello **aplikacji usługi domeny** kliknij przycisk **OK**. Gdy trwa operacja hello, zostanie wyświetlony hello następujące powiadomienia:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Nazwy hostów hello testu

Jeśli zostały przypisane domyślne nazwy hostów tooyour sieci web aplikacji, również wyświetlane jest powiadomienie Powodzenie dla każdej wybranej nazwy hosta. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Umożliwia wyświetlenie nazwy hostów hello wybrane w hello **domen niestandardowych** strony w hello **Hostnames** sekcji. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

nazwy hostów hello tootest, przejdź toohello wymienione nazwy hostów, w przeglądarce hello. W przykładzie hello hello poprzedzających zrzut ekranu, spróbuj nawigowanie po too_kontoso.net_ i _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Przypisanie nazwy hostów tooweb aplikacji

Jeśli wybierzesz nie tooassign, jeden lub więcej domyślnej nazwy hostów tooyour aplikacji sieci web podczas hello proces zakupu lub jeśli nie potrzebujesz tooassign nazwy hosta na liście, można przypisać nazwy hosta w dowolnym momencie.

Można również przypisywać nazwy hostów w tooany domena usługi aplikacji hello innych aplikacji sieci web. Witaj kroki zależą od czy hello domeny aplikacji usługi i aplikacji sieci web hello należą toohello tej samej subskrypcji.

- Inną subskrypcję: Mapowanie niestandardowych rekordów DNS z aplikacji sieci web toohello domena usługi aplikacji hello jak zewnętrznie zakupionych domeny. Aby uzyskać informacji na temat dodawania DNS niestandardowej nazwy tooan domena usługi aplikacji, zobacz [Zarządzanie niestandardowych rekordów DNS](#custom). toomap aplikacji sieci web tooa zakupionych domen zewnętrznych, zobacz [mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacje sieci Web](app-service-web-tutorial-custom-domain.md). 
- Tej samej subskrypcji: hello Użyj następujące kroki.

### <a name="launch-add-hostname"></a>Uruchom dodać nazwy hosta
W hello **usługi aplikacji** strony, hello wybierz nazwę aplikacji sieci web przewidzianych tooassign nazwy hostów, aby wybrać **ustawienia**, a następnie wybierz **domen niestandardowych**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Upewnij się, że zakupione domeny jest wymieniony w hello **domenami usługi aplikacji** sekcji, ale nie wybierz go. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Wszystkich domen usługi aplikacji w tej samej subskrypcji są wyświetlane w aplikacji sieci web hello hello **domen niestandardowych** strony. Jeśli Twoja domena to w aplikacji sieci web hello subskrypcji, ale niewidoczna w aplikacji sieci web hello **domen niestandardowych** strony, spróbuj otworzyć hello **domen niestandardowych** strony lub odświeżanie hello strony sieci Web. Sprawdź również, dzwonka powiadomień hello u góry hello hello portalu Azure niepowodzeń postępu lub utworzenia.
>
>

Wybierz **dodać nazwę hosta**.

### <a name="configure-hostname"></a>Konfigurowanie nazwy hosta
W hello **dodać nazwę hosta** okno dialogowe, nazwy FQDN hello typu domenę usługi aplikacji lub dowolnej domeny podrzędnej. Na przykład:

- kontoso.NET
- www.kontoso.NET
- ABC.kontoso.NET

Po zakończeniu wybierz **weryfikacji**. Typ rekordu hostname Hello jest automatycznie wybrana.

Wybierz **dodać nazwę hosta**.

Po zakończeniu operacji hello jest wyświetlone powiadomienie Powodzenie dla hello przypisane nazwy hosta.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Zamknij dodać nazwy hosta
W hello **dodać nazwę hosta** Przypisz żadnych innych hostname tooyour aplikacji sieci web, zgodnie z potrzebami. Po zakończeniu zamknij hello **dodać nazwę hosta** strony.

Powinien zostać wyświetlony hostname(s) hello przydzielone w Twojej aplikacji **domen niestandardowych** strony.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Nazwy hostów hello testu

Przejdź toohello wymienione nazwy hostów, w przeglądarce hello. W przykładzie hello hello zrzut ekranu poprzedzającym spróbuj nawigowanie po too_abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Zarządzanie niestandardowych rekordów DNS

Na platformie Azure rekordy DNS dla domeny usługi aplikacji są zarządzane przy użyciu [usługi Azure DNS](https://azure.microsoft.com/services/dns/). Można dodać, usunąć i Aktualizuj rekordy DNS, podobnie jak zewnętrznie zakupionych domeny.

### <a name="open-app-service-domain"></a>Domena Otwórz usługi aplikacji

W portalu Azure, w menu po lewej stronie powitania hello wybierz **więcej usług** > **domenami usługi aplikacji**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Wybierz hello toomanage domeny. 

### <a name="access-dns-zone"></a>Dostęp do strefy DNS

W menu po lewej stronie powitania domeny wybierz **strefy DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Ta akcja powoduje otwarcie hello [strefy DNS](../dns/dns-zones-records.md) strony domenę usługi aplikacji w usłudze Azure DNS. Aby uzyskać informacje na temat tooedit rekordy DNS, zobacz [jak toomanage strefy DNS w hello portalu Azure](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Anuluj zakupu (usuwania domeny)

Po zakupie hello domena usługi aplikacji masz pięć dni toocancel zakupu dla pełny zwrot kosztów. Po pięć dni można usunąć hello domena usługi aplikacji, ale nie można otrzymać zwrot kosztów.

### <a name="open-app-service-domain"></a>Domena Otwórz usługi aplikacji

W portalu Azure, w menu po lewej stronie powitania hello wybierz **więcej usług** > **domenami usługi aplikacji**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Wybierz hello domeny tooyou chcesz toocancel lub usunąć. 

### <a name="delete-hostname-bindings"></a>Usuń powiązań z nazwami hostów

W menu po lewej stronie powitania domeny wybierz **powiązań z nazwami hostów**. Poniżej przedstawiono Hello powiązań z nazwami hostów ze wszystkich usług platformy Azure.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

Nie można usunąć hello domena usługi aplikacji, dopóki nie zostaną usunięte wszystkie powiązań z nazwami hostów.

Usuń powiązanie każdej nazwy hosta, wybierając **... **  >  **Usunąć**. Po usunięciu wszystkich powiązań hello wybierz **zapisać**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Anuluj lub delete

W menu po lewej stronie powitania domeny wybierz **omówienie**. 

Czy nie upłynął termin anulowania hello na powitania zakupionych domeny, wybierz **anulować zakup**. W przeciwnym razie zobacz **usunąć** zamiast tego przycisku. toodelete hello domeny bez zwrotu kosztów, wybierz opcję **usunąć**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Wybierz **OK** tooconfirm hello operacji. Jeśli nie chcesz tooproceed, kliknij w dowolnym miejscu poza powitalne okno dialogowe potwierdzenia.

Po zakończeniu operacji hello domeny hello jest zwolnione z subskrypcji i wszyscy toopurchase ponownie. 
