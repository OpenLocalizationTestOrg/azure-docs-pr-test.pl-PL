---
title: "Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service (GoDaddy)"
description: "Dowiedz się, jak użyć nazwy domeny z GoDaddy dla aplikacji sieci Web Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Konfigurowanie nazwy domeny niestandardowej (kupionej bezpośrednio od firmy GoDaddy) w usłudze Azure App Service
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Jeśli została kupione domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure odwoływać się do ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md).

Ten artykuł zawiera instrukcje przy użyciu nazwy domeny niestandardowej, które zostało zakupione bezpośrednio z [GoDaddy](https://godaddy.com) z [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Opis rekordów DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Dodaj rekord DNS dla domeny niestandardowej
Aby skojarzyć domeny niestandardowej z aplikacją sieci web w usłudze App Service, możesz należy dodać nowy wpis w tabeli DNS dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez GoDaddy. Wykonaj następujące kroki, aby zlokalizować narzędzia DNS dla GoDaddy.com

1. Zaloguj się na swoje konto w GoDaddy.com, a następnie wybierz **Moje konto** , a następnie **Zarządzanie domenami Mój**. Wybierz z menu rozwijanego dla nazwy domeny, które chcą korzystać z aplikacji sieci web platformy Azure i wybierz **zarządzania DNS**.
   
    ![Domena niestandardowa strona GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Z **szczegóły domeny** przewiń do **pliku strefy DNS** kartę. Jest to sekcja używane do dodawania i modyfikowania rekordów DNS dla nazwy domeny.
   
    ![Karta pliku strefy DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Wybierz **Dodaj rekord** można dodać istniejącego rekordu.
   
    Aby **Edytuj** istniejącego rekordu, wybierz pióro & Papier ikona obok rekordu.
   
   > [!NOTE]
   > Przed dodaniem nowych rekordów, należy zwrócić uwagę GoDaddy utworzył już rekordy DNS dla popularnych poddomen (o nazwie **hosta** w edytorze) takie jak **e-mail**, **pliki**, **poczty**i inne. Jeśli nazwa, którą chcesz utworzyć, już istnieje, zmodyfikuj istniejący rekord zamiast tworzenia nowej.
   > 
   > 
3. Podczas dodawania rekordu, musisz wybrać typ rekordu.
   
    ![Wybierz typ rekordu](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Następnie należy podać **hosta** (domenę niestandardową lub domenę podrzędną) i jakie **wskazuje**.
   
    ![Dodaj rekord strefy](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Podczas dodawania **rekordu (hosta)** — należy ustawić **hosta** pole jednej  **@**  (Ta pozycja reprezentuje nazwę domeny głównej, takich jak **contoso.com** ,) * (symbol wieloznaczny dopasowania wielu domen podrzędnych,) lub domenę podrzędną, o których chcesz użyć (na przykład **www**.) Należy ustawić **wskazuje** pole na adres IP, aplikacji sieci web platformy Azure.
   * Podczas dodawania **rekord CNAME (alias)** — należy ustawić **hosta** do domeny podrzędnej chcesz użyć. Na przykład **www**. Należy ustawić **wskazuje** do **. azurewebsites.net** nazwy domeny aplikacji sieci web platformy Azure. Na przykład **contoso.azurewebsites.net**.
4. Kliknij przycisk **dodać kolejne**.
5. Wybierz **TXT** jako typ rekordu, następnie określ **hosta** wartość  **@**  i **wskazuje** wartość  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Ten rekord TXT jest używany przez usługę Azure można sprawdzić poprawności własnej domeny opisanego przez rekord A lub pierwszy rekord TXT. Po zamapowaniu domeny aplikacji sieci web w portalu Azure można usunąć tego wpisu rekordu TXT.
   > 
   > 
6. Po zakończeniu dodawania lub modyfikowania rekordów, kliknij przycisk **Zakończ** można zapisać zmian.

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a>Włącz nazwy domeny w aplikacji sieci web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

