---
title: 'Synchronizacja programu Azure AD Connect: zagadnienia techniczne | Dokumentacja firmy Microsoft'
description: "Zawiera wyjaśnienie założeń techniczne hello synchronizacja programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Synchronizacja programu Azure AD Connect: zagadnienia techniczne
W tym artykule przedstawiono podsumowanie tematu hello [opis architektury](active-directory-aadconnectsync-technical-concepts.md).

Synchronizacja programu Azure AD Connect, bazując na platformie stałe metakatalogowego synchronizacji.
Witaj następujące sekcje wprowadzenie pojęcia hello metakatalogowego synchronizacji.
Kompilowanie od serwera MIIS, ILM i FIM, usług hello Azure do synchronizacji usługi Active Directory zapewnia hello dalej platformę łączącego toodata źródeł, synchronizowania danych między źródłami danych, a także hello alokowania i anulowania alokowania tożsamości.

![Zagadnienia techniczne](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Witaj następujące sekcje zawierają więcej szczegółowych informacji o następujące aspekty hello usługę synchronizacji programu FIM hello:

* Łącznik
* Przepływ atrybutów
* Obszar łączników
* Metaverse
* Inicjowanie obsługi

## <a name="connector"></a>Łącznik
Witaj modułów kodu, które są używane toocommunicate z połączonego katalogu są nazywane łączników (wcześniej znane jako agenci zarządzania (MAs)).

Te pliki zostaną zainstalowane na komputerze hello systemem synchronizacja programu Azure AD Connect. Witaj łączników udostępnia hello tooconverse możliwości bez wykorzystania agentów przy użyciu protokołów systemu zdalnego zamiast polegania na powitania wdrażania agentów specjalne. Oznacza to zmniejszyć ryzyko i czas wdrażania, szczególnie w przypadku zajmujących się kluczowych aplikacji i systemów.

Hello ilustracji powyżej łącznika hello jest synonimem hello przestrzeni łącznika, ale obejmuje całą komunikację z systemu zewnętrznego hello.

Witaj łącznika jest odpowiedzialny wszystkie importowanie i eksportowanie funkcji toohello systemu i zwalnia deweloperzy z konieczności toounderstand jak tooconnect tooeach systemu natywnie używając deklaratywne przekształcenia danych toocustomize inicjowania obsługi administracyjnej.

Importu i eksportu tylko wówczas, gdy zaplanowane, co pozwala na dalsze izolacji od zmian w ramach systemu hello, ponieważ zmiany automatycznie nie propagować toohello połączonego źródła danych. Ponadto deweloperzy mogą również utworzyć własne łączniki do łączenia toovirtually dowolnego źródła danych.

## <a name="attribute-flow"></a>Przepływ atrybutów
Hello metaverse jest widokiem hello skonsolidowane wszystkich tożsamości dołączonego do sąsiadujących — obszary łączników. W powyższym rysunku hello przedstawiono przepływ atrybutów liniami z strzałek dla przepływu ruchu przychodzącego i wychodzącego. Przepływ atrybutów jest hello proces kopiowania lub Przekształcanie danych z jednego systemu tooanother i wszystkich atrybutów przepływów (przychodzący lub wychodzący).

Przepływ atrybutu odbywa się między hello obszar łączników i hello metaverse dwukierunkowo po toorun zaplanowane operacje synchronizacji (pełna lub różnicowa).

Przepływ atrybutów jest używane tylko w przypadku tych synchronizacje są uruchamiane. Przepływy atrybutów są definiowane w reguły synchronizacji. Mogą to być przychodzącego (ISR hello ilustracji powyżej) lub wychodzący (OSR hello ilustracji powyżej).

## <a name="connected-system"></a>System połączony
System połączony (alias połączonego katalogu) odwołuje się do systemu zdalnego toohello Azure AD Connect synchronizacji został podłączony tooand odczytu i zapisu tooand danych tożsamości z.

## <a name="connector-space"></a>Obszar łączników
Każdego połączonego źródła danych jest reprezentowany jako podzbiór filtrowane hello obiektów i atrybutów w hello przestrzeni łącznika.
Umożliwia toooperate usługi synchronizacji hello lokalnie bez hello potrzeby toocontact hello zdalnego systemu podczas synchronizowania obiektów hello i ogranicza tooimports interakcji i eksportuje tylko.

Jeśli źródło danych hello i hello łącznika tooprovide możliwości hello listę zmian (import zmian), następnie zwiększa wydajność operacyjną hello znacznie jako cykl jedynie zmian wprowadzonych od czasu ostatniego sondowania hello są wymieniane. Obszar łączników Hello powoduje hello połączonego źródła danych z propagowanie automatycznie wymagające tego harmonogramu łącznika hello importuje i eksportuje zmiany. Dodano ubezpieczenia przyznaje spokój umysłu podczas testowania, przeglądania i potwierdzenie hello następną aktualizację.

## <a name="metaverse"></a>Metaverse
Hello metaverse jest widokiem hello skonsolidowane wszystkich tożsamości dołączonego do sąsiadujących — obszary łączników.

Tożsamości są połączone ze sobą i uprawnienia przypisano dla różnych atrybutów w mapowaniach przepływu importu, obiektu metaverse centralnej hello rozpoczyna tooaggregate informacji z wielu systemów. Z tego przepływu atrybutu obiektu mapowania przenoszenia systemów toooutbound informacji.

Obiekty są tworzone podczas autorytatywne systemu projektów je do środowiska metaverse hello. Jak najszybciej po usunięciu wszystkich połączeń obiektu metaverse hello jest usuwany.

Nie można bezpośrednio edytować obiektów w magazynie metaverse hello. Wszystkie dane w obiekcie hello musi się odbywać za pośrednictwem przepływ atrybutów. Hello metaverse obsługuje trwałe łączniki z każdego miejsca łącznika. Te łączniki nie wymagają ponownej oceny dla każdej synchronizacji, uruchom. Oznacza to, że synchronizacja programu Azure AD Connect nie ma zgodnego obiektu zdalnego hello toolocate zawsze. Dzięki temu można uniknąć hello potrzebę tooattributes zmiany tooprevent kosztowne agentów, które zazwyczaj będzie odpowiedzialny za korelowanie hello obiektów.

Gdy odnajdywanie nowych źródeł danych, które mogą mieć istniejących obiektów, które wymagają toobe zarządzane, używa synchronizacji Azure AD Connect procesu wywoływana sprzężenia reguły tooevaluate potencjalnych kandydatów z których tooestablish łącze.
Po utworzeniu połączenia hello ocena powtarzał i przepływu normalnego atrybutów może wystąpić między hello zdalnego połączonego źródła danych i hello metaverse.

## <a name="provisioning"></a>Inicjowanie obsługi
Gdy projekty wiarygodne źródło w innym łącznikiem reprezentującą podrzędne połączonego źródła danych można tworzyć nowy obiekt do metaverse hello nowy obiekt przestrzeni łącznika.

To z założenia stanowi połączenie, a przepływ atrybutów można kontynuować dwukierunkowo.

Zawsze, gdy reguła określa wymagane toobe utworzone przez nowy obiekt przestrzeni łącznika, jest on nazywany inicjowania obsługi administracyjnej. Jednak ponieważ tej operacji tylko odbywa się w przestrzeni łącznika hello, go nie jest przenoszone do hello połączonego źródła danych do momentu eksportu jest wykonywane.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Azure AD Connect Sync: Dostosowywanie opcji synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
