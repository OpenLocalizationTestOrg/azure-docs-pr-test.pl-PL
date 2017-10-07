---
title: "aaaControlling ruchu aplikacji sieci web platformy Azure z usługą Azure Traffic Manager"
description: "Ten artykuł zawiera informacje podsumowania dla usługi Azure Traffic Manager pod kątem tooAzure aplikacji sieci web."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Kontrolowanie aplikacji sieci Web platformy Azure przy użyciu usługi Azure Traffic Manager
> [!NOTE]
> Ten artykuł zawiera informacje podsumowania dla Menedżera ruchu Microsoft Azure, co wiąże tooAzure aplikacji usługi sieci Web aplikacji. Więcej informacji na temat usługi Azure Traffic Manager sam można znaleźć, przechodząc na stronę hello łącza na końcu hello w tym artykule.
> 
> 

## <a name="introduction"></a>Wprowadzenie
Można użyć usługi Azure Traffic Manager toocontrol jak żądania od klientów sieci web są rozproszone tooweb aplikacji w usłudze Azure App Service. Po dodaniu profilu Menedżera ruchu Azure tooa punktów końcowych aplikacji sieci web, usługi Azure Traffic Manager przechowuje informacje o hello stanu aplikacji sieci web (uruchomionej, zatrzymanej lub usunięte), dzięki czemu można zdecydować, które z tych punktów końcowych powinny odbierać dane.

## <a name="load-balancing-methods"></a>Metody równoważenia obciążenia
Trzy metody równoważenia obciążenia różnych korzysta z usługi Azure Traffic Manager. Te ustawienia zostały opisane w powitania po liście zgodnie z tagami tooAzure aplikacji sieci web.

* **Tryb failover**: Jeśli masz klony aplikacji sieci web w różnych regionach, można użyć tej metody tooconfigure jedną witrynę sieci web aplikacji tooservice cały ruch klienta sieci web i skonfigurować innej aplikacji sieci web w tooservice inny region, który ruchu w przypadku hello pierwszej aplikacji sieci web staje się niedostępna.
* **Działanie okrężne**: Jeśli klony aplikacji sieci web znajdują się w różnych regionach, możesz użyć tego ruchu toodistribute — metoda jednakowo w aplikacjach sieci web hello w różnych regionach.
* **Wydajność**: hello metody wydajności dystrybuuje ruch oparte na powitania najkrótszy tooclients czas obiegu. Hello metody wydajności może służyć do aplikacji sieci web w obrębie hello tym samym regionie lub w różnych regionach.

## <a name="web-apps-and-traffic-manager-profiles"></a>Aplikacje sieci Web i profilów usługi Traffic Manager
tooconfigure hello kontroli ruchu w aplikacji sieci web, możesz utworzyć profil w usłudze Azure Traffic Manager korzystającą z metod opisanych powyżej równoważenia obciążenia hello trzy, a następnie dodaj punkty końcowe hello (w tym przypadku aplikacji sieci web) dla których ma zostać toocontrol toohello ruchu profil. Stan aplikacji sieci web (uruchomionej, zatrzymanej lub usunięto) jest regularnie przekazanych toohello profilu, aby usługi Azure Traffic Manager można kierować ruch odpowiednio.

Korzystając z usługi Azure Traffic Manager przy użyciu platformy Azure, należy pamiętać hello następujące punkty:

* W przypadku tylko wdrożenia aplikacji sieci web w obrębie hello tego samego regionu, aplikacje sieci Web już zapewnia funkcje trybu failover i okrężnego bez względu tooweb aplikacji trybu.
* Dla wdrożeń w hello tym samym regionie, który korzystać z aplikacji sieci Web w połączeniu z innej usługi w chmurze Azure, można połączyć oba rodzaje scenariuszy hybrydowych tooenable punktów końcowych.
* Można określić tylko jeden punkt końcowy aplikacji sieci web dla regionu w profilu. Po wybraniu aplikacji sieci web jako punktu końcowego dla regionu co hello pozostałe aplikacje sieci web, w tym regionie staną się niedostępne do wybrania dla tego profilu.
* Witaj aplikacji punktów końcowych sieci web przez użytkownika w profilu Menedżera ruchu Azure zostanie wyświetlony w obszarze hello **nazw domen** sekcji na powitania strony konfiguracji dla aplikacji sieci web hello hello profilu, ale nie będzie można skonfigurować istnieje.
* Po dodaniu profilu tooa aplikacji sieci web hello **adres URL witryny** na powitania pulpitu nawigacyjnego sieci Web hello strony portalu aplikacji wyświetli hello domeny niestandardowej adres URL aplikacji sieci web hello, jeśli zdefiniowano jeden. W przeciwnym razie zostanie wyświetlony adres URL profilu usługi Traffic Manager hello (na przykład `contoso.trafficmgr.com`). Witaj zarówno nazwa domeny bezpośredniego hello aplikacji sieci web i hello adres URL usługi Traffic Manager będą widoczne na stronie Konfigurowanie aplikacji sieci web hello w obszarze hello **nazwy domen** sekcji.
* Niestandardowa nazwa domeny będzie działać zgodnie z oczekiwaniami, ale w tooadding dodanie ich tooyour aplikacji sieci web, musisz również skonfigurować sieci toohello toopoint mapy DNS adresu URL Menedżera ruchu. Aby uzyskać informacje na temat tooset niestandardową domenę dla aplikacji sieci web platformy Azure, zobacz [Konfigurowanie niestandardowej nazwy domeny dla usługi Azure witryny sieci web](app-service-web-tutorial-custom-domain.md).
* Można dodawać tylko aplikacje sieci web, które znajdują się w tryb standardowy lub premium tooa profilu Menedżera ruchu Azure.

## <a name="next-steps"></a>Następne kroki
Koncepcyjna i techniczne omówienie usługi Azure Traffic Manager, zobacz [Omówienie Menedżera ruchu](../traffic-manager/traffic-manager-overview.md).

Aby uzyskać więcej informacji dotyczących korzystania z Menedżera ruchu z aplikacjami sieci Web, zobacz hello blogach [przy użyciu usługi Azure Traffic Manager z witryn sieci Web Azure](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) i [usługi Azure Traffic Manager teraz można zintegrować z witryn sieci Web Azure](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

