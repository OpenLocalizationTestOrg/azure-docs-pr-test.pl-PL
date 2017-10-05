---
title: "Rozwiązywanie problemów z członkostwo dynamiczne w grupach | Dokumentacja firmy Microsoft"
description: "Porady dotyczące rozwiązywania problemów dynamicznego zarządzania członkostwem w grupach w usłudze Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Rozwiązywanie problemów z członkostwem dynamicznym w grupach
**Po skonfigurowaniu reguły w grupie, ale aktualizowany nie członkostwa w grupie**<br/>Sprawdź, czy **Włącz delegowane Zarządzanie grupami** mają ustawioną wartość **tak** w **Konfiguruj** kartę. To ustawienie zostanie wyświetlony tylko wtedy, gdy użytkownik jest zalogowany jako użytkownik, któremu przypisano licencji usługi Azure Active Directory Premium. Sprawdź wartości atrybutów użytkownika dla reguły: istnieją użytkownicy, którzy spełniają zasady?

**Po skonfigurowaniu reguły, ale teraz istniejących członków reguły zostaną usunięte**<br/>Jest to oczekiwane zachowanie. Istniejących członków grupy są usuwane, gdy reguła jest włączona lub zmienione. Użytkownicy zwrócił ewaluacyjną reguła są dodawane jako członków do grupy.     

**Nie widzę członkostwa zmian natychmiast po Dodawanie lub zmienianie reguły, dlaczego nie?**<br/>Ocenę członkostwa dedykowanych okresowo odbywa się w tle asynchronicznego. Jak długo trwa proces jest określana przez liczbę użytkowników w katalogu i rozmiar grupy utworzone w wyniku reguły. Zazwyczaj katalogi z małej liczby użytkowników zobaczą zmiany członkostwa w grupie w mniej niż kilka minut. Katalogi z dużą liczbą użytkowników może potrwać 30 minut lub dłużej, aby wypełnić.

### <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
