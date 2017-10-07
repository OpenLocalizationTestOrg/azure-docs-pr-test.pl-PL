---
title: "aaaTroubleshooting członkostwo dynamiczne w grupach | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Rozwiązywanie problemów z członkostwem dynamicznym w grupach
**Po skonfigurowaniu reguły w grupie, ale aktualizowany nie członkostwa w grupie hello**<br/>Sprawdź, że hello **Włącz delegowane Zarządzanie grupami** ustawioną zbyt**tak** w hello **Konfiguruj** kartę. To ustawienie zostanie wyświetlony tylko wtedy, gdy użytkownik jest zalogowany jako użytkownik toowhom licencji usługi Azure Active Directory Premium jest przypisana. Sprawdź wartości atrybutów użytkownika w regule hello hello: istnieją użytkownicy, którzy spełniają zasady hello?

**Po skonfigurowaniu reguły, ale teraz hello istniejących członków hello reguły zostaną usunięte**<br/>Jest to oczekiwane zachowanie. Istniejących członków grupy hello są usuwane, gdy reguła jest włączona lub zmienione. Użytkownicy Hello zwrócił ewaluacyjną reguła hello są dodawane jako elementy członkowskie grupy toohello.     

**Nie widzę członkostwa zmian natychmiast po Dodawanie lub zmienianie reguły, dlaczego nie?**<br/>Ocenę członkostwa dedykowanych okresowo odbywa się w tle asynchronicznego. Jak długo trwa proces hello jest określana przez hello liczbę użytkowników w rozmiar katalogu i hello hello grupy utworzone w wyniku hello reguły. Zazwyczaj katalogi z małej liczby użytkowników zobaczą zmiany członkostwa w grupie hello mniej niż za kilka minut. Katalogi z dużą liczbą użytkowników może potrwać 30 minut lub dłużej toopopulate.

### <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
