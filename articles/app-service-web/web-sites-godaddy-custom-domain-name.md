---
title: "aaaConfigure niestandardowej nazwy domeny w usłudze Azure App Service (GoDaddy)"
description: "Dowiedz się, jak nazwa toouse domeny z GoDaddy z aplikacjami sieci Web Azure"
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Konfigurowanie nazwy domeny niestandardowej (kupionej bezpośrednio od firmy GoDaddy) w usłudze Azure App Service
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Jeśli została kupione domeny przy użyciu aplikacji sieci Web usługi aplikacji Azure można znaleźć toohello ostatniego kroku [kupić domenę dla aplikacji sieci Web](custom-dns-web-site-buydomains-web-app.md).

Ten artykuł zawiera instrukcje przy użyciu nazwy domeny niestandardowej, które zostało zakupione bezpośrednio z [GoDaddy](https://godaddy.com) z [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Opis rekordów DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Dodaj rekord DNS dla domeny niestandardowej
tooassociate domeny niestandardowej z aplikacją sieci web w usłudze App Service, należy dodać nowy wpis w tabeli DNS powitania dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez GoDaddy. Następujące kroki toolocate hello DNS hello użyj narzędzi dla GoDaddy.com

1. Logowanie na koncie tooyour z GoDaddy.com, a następnie wybierz **Moje konto** , a następnie **Zarządzanie domenami Mój**. Menu rozwijanego wybierz hello hello nazwy domeny ma toouse z aplikacją sieci web platformy Azure, a następnie wybierz **zarządzania DNS**.
   
    ![Domena niestandardowa strona GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Z hello **szczegóły domeny** przewiń toohello **pliku strefy DNS** kartę. Jest to sekcja hello używane do dodawania i modyfikowania rekordów DNS dla nazwy domeny.
   
    ![Karta pliku strefy DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Wybierz **Dodaj rekord** tooadd istniejącego rekordu.
   
    zbyt**Edytuj** istniejącego rekordu, wybierz hello pióro & papieru ikona obok hello rekordu.
   
   > [!NOTE]
   > Przed dodaniem nowych rekordów, należy zwrócić uwagę GoDaddy utworzył już rekordy DNS dla popularnych poddomen (o nazwie **hosta** w edytorze) takie jak **e-mail**, **pliki**, **poczty**i inne. Jeśli nazwa hello toouse ma już istnieje, zmodyfikuj istniejący rekord hello zamiast tworzenia nowej.
   > 
   > 
3. Podczas dodawania rekordu, musisz wybrać typ rekordu hello.
   
    ![Wybierz typ rekordu](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Następnie należy podać hello **hosta** (hello podrzędnej lub domeny niestandardowe) i jakie **wskazuje**.
   
    ![Dodaj rekord strefy](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Podczas dodawania **rekordu (hosta)** — należy ustawić hello **hosta** tooeither pola  **@**  (Ta pozycja reprezentuje nazwę domeny głównej, takich jak  **contoso.com**,) * (symbol wieloznaczny dopasowania wielu domen podrzędnych,) lub domenę podrzędną hello mają toouse (na przykład **www**.) Należy ustawić hello **wskazuje** pola adresu IP toohello aplikacji sieci web platformy Azure.
   * Podczas dodawania **rekord CNAME (alias)** — należy ustawić hello **hosta** domeny podrzędnej toohello pola mają toouse. Na przykład **www**. Należy ustawić hello **wskazuje** toohello pola **. azurewebsites.net** nazwy domeny aplikacji sieci web platformy Azure. Na przykład **contoso.azurewebsites.net**.
4. Kliknij przycisk **dodać kolejne**.
5. Wybierz **TXT** jako typ rekordu hello, następnie określ **hosta** wartość  **@**  i **wskazuje** wartość  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Ten rekord TXT jest używany przez Azure toovalidate własnej się, że domena hello opisanego przez hello rekordu lub hello pierwszy rekord TXT. Po hello domeny aplikacji sieci web toohello mapowane w hello portalu Azure, można usunąć tego wpisu rekordu TXT.
   > 
   > 
6. Po zakończeniu dodawania lub modyfikowania rekordów, kliknij przycisk **Zakończ** toosave zmiany.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Włącz nazwy domeny hello na aplikację sieci web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

