---
title: aaaReference do nawigowania hello portalu Azure
description: "Dowiedz się hello możliwości różnych użytkowników dla aplikacji sieci Web usługi między hello portalu zarządzania i hello portalu Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Odwołanie do nawigowania hello portalu Azure
Witryn sieci Web Azure są teraz nazywane [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). Aktualizujemy wszystkie tooreflect naszej dokumentacji tej nazwy zmiany i tooprovide instrukcje hello portalu Azure. Dopóki ten proces odbywa się, można użyć tego dokumentu jako wskazówki dotyczące pracy z aplikacjami sieci Web w portalu Azure hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>przyszłość Hello hello klasycznego portalu Azure
Podczas zauważysz hello znakowania zmian na powitania klasycznego portalu Azure tego portalu jest proces hello zastępowane przez hello portalu Azure. Zgodnie z klasycznego portalu hello jest obecnie wycofywane, hello fokusu dla nowych aplikacji jest przesunięcie toohello portalu Azure. Wszystkie nowe funkcje nadchodzących dla aplikacji sieci Web będą dostępne w hello portalu Azure. Zacznij używać hello Azure Portal tootake zaletą hello najnowszej i najlepszej, że aplikacje sieci Web mają toooffer.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Układ różnice między hello klasycznego portalu Azure i portalu Azure
W portalu klasycznym hello wszystkie hello Azure usługi są wyświetlane na powitania lewą stronę. Nawigacja w portalu klasycznym hello następuje struktury drzewa, gdzie uruchomić z usługi hello i przejdź do każdego elementu. Ta struktura działa dobrze w przypadku, gdy zarządzanie składnikami niezależne. Jednak aplikacje utworzone na platformie Azure są kolekcja połączonych usług i ta struktura drzewa nie jest idealne rozwiązanie w przypadku pracy z kolekcji usług. 

Hello portalu Azure umożliwia łatwe toobuild aplikacji end-to-end ze składnikami z wielu usług. Hello portal jest zorganizowana jako *podróże*. A *podróży* jest szereg *bloków*, które są kontenerami dla hello różnych składników. Na przykład ustawienie automatyczne skalowanie aplikacji sieci web jest *podróży* który przejście kilku bloków pokazane na powitania poniższy przykład: hello **witryny sieci web** bloku (czy Tytuł bloku nie został jeszcze zaktualizowany toouse Witaj terminologii nowy), hello **ustawienia** bloku i hello **skalowanie w poziomie** bloku. W przykładzie hello automatyczne skalowanie jest konfigurowana toodepend na użycie procesora CPU, więc jest również **procent użycia procesora CPU** bloku. Witaj składniki w ramach hello *bloków* są nazywane *części*, który wygląda jak kafelki. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Przykład nawigacji: tworzenie aplikacji sieci web
Tworzenie nowej aplikacji sieci web jest nadal tak proste, jak 1, 2, 3. powitania po obraz pokazuje hello klasycznego portalu i hello portalu side-by-side toodemonstrate zmodyfikowaną nie znacznie hello liczbę czynności potrzebne tooget aplikacji sieci web w górę i uruchomiona. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

W portalu hello są dostępne z hello najbardziej typowych aplikacji sieci web, w tym galerii popularnych aplikacji, takich jak WordPress. Aby uzyskać pełną listę dostępnych aplikacji, odwiedź stronę hello [portalu Azure Marketplace].

Podczas tworzenia aplikacji sieci web, określ adres URL, plan usługi aplikacji i lokalizację w portalu hello tak samo jak to zrobić w klasycznym portalu hello. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Ponadto hello portal pozwala zdefiniować inne typowe ustawienia. Na przykład [grup zasobów](../azure-resource-manager/resource-group-overview.md) on toosee proste i zarządzanie nimi powiązanych zasobów systemu Azure. 

## <a name="navigation-example-settings-and-features"></a>Przykład nawigacji: ustawienia i funkcje
Witaj wszystkie ustawienia i funkcje teraz są logicznie pogrupowane w jednej bloku, w którym można nawigować.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Na przykład można utworzyć domeny niestandardowe, klikając **domen niestandardowych i SSL** w hello **ustawienia** bloku.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset się alert monitorowania, kliknij przycisk **żądań i błędów** , a następnie **dodać Alert**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Diagnostyka tooenable, kliknij przycisk **dzienników diagnostycznych** w hello **ustawienia** bloku.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Ustawienia aplikacji tooconfigure, kliknij przycisk **ustawienia aplikacji** w hello **ustawienia** bloku. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Inna niż nazwa marki hello, kilka czynności w portalu hello został przeniesiony lub pogrupowane inaczej toomake go toofind łatwiej je. Na przykład poniżej przedstawiono zrzut ekranu hello strony odpowiednie dla ustawienia aplikacji (**Konfiguruj**) w portalu klasycznym hello.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Więcej zasobów
[Azure Portal]: https://portal.azure.com
[portalu Azure Marketplace]: /marketplace/

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

