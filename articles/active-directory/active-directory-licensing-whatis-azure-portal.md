---
title: "aaaWhat jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory? | Microsoft Docs"
description: "Opis usługi Azure Active Directory na podstawie grupy licencji, jak działa i najlepsze rozwiązania"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Na podstawie grupy podstawy licencjonowania w usłudze Azure Active Directory

Za pomocą płatnej usługi w chmurze, takich jak usługi Office 365, Enterprise Mobility + zabezpieczeń usługi Dynamics CRM i inne podobne produkty firmy Microsoft wymaga licencji. Te licencje są przypisane tooeach użytkownika, który wymaga usług toothese dostępu. licencje toomanage administratorzy za pomocą jednej hello portali zarządzania (Office lub Azure) i poleceń cmdlet programu PowerShell. Azure Active Directory (Azure AD) jest hello podstawowej infrastruktury, która obsługuje zarządzanie tożsamościami dla wszystkich usług chmurowych firmy Microsoft. Usługi Azure AD są przechowywane informacje o stanach przypisania licencji dla użytkowników.

Do tej pory licencje może zostać przypisana tylko na poziomie indywidualnego użytkownika hello, co może utrudnić zarządzania na dużą skalę. Na przykład tooadd lub usuń licencji użytkownika na podstawie organizacyjnego zmian, takich jak użytkownicy przyłączenie się lub opuszczenie hello organizacji lub działu, administrator często musi być zapisana złożonych skrypt programu PowerShell. Ten skrypt wykonuje poszczególnych wywołań toohello usługi w chmurze.

tooaddress tych będzie wymagał, usługi Azure AD teraz obejmuje oparte na grupach licencji. Można przypisać przynajmniej jednej grupy tooa licencji produktu. Usługi Azure AD zapewnia przypisanie licencji hello tooall członkami grupy hello. Nowe elementy członkowskie, które dołączyć do grupy hello są przypisywane hello odpowiednie licencje. Gdy opuszczą hello grupy te licencje zostaną usunięte. Eliminuje to potrzebę hello automatyzacji zarządzania licencji za pomocą programu PowerShell tooreflect zmiany hello i działów strukturę na poszczególnych użytkowników.

## <a name="features"></a>Funkcje

Oto główne funkcje hello na podstawie grupy licencji:

- Licencje można przypisywać tooany grupy zabezpieczeń w usłudze Azure AD. Grupy zabezpieczeń mogą być zsynchronizowanej lokalnej, za pomocą usługi Azure AD Connect. Bezpośrednio w usłudze Azure AD (nazywanych również grup tylko w chmurze), lub automatycznie za pomocą funkcji Dynamiczna grupa hello Azure AD, mogą także tworzyć grupy zabezpieczeń.

- Po przypisaniu tooa grupy licencji produktu, hello administrator może wyłączyć jeden lub więcej planów usług w produkcie hello. Zazwyczaj jest to realizowane przy hello organizacja nie jest jeszcze gotowa toostart przy użyciu usługi zawarta w produkcie. Na przykład hello administrator może przypisać działu tooa usługi Office 365, ale tymczasowe wyłączenie usługi Yammer hello.

- Obsługiwane są wszystkie usług chmurowych firmy Microsoft, które wymagają licencji na poziomie użytkownika. Obejmuje to wszystkie produkty, pakietu Enterprise Mobility + Security i Dynamics CRM usługi Office 365.

- Na podstawie grupy licencji jest obecnie dostępny tylko za pośrednictwem [hello portalu Azure](https://portal.azure.com). Jeśli przede wszystkim użyj innych portali zarządzania dla użytkowników i grupy zarządzania, takich jak portal hello usługi Office 365, możesz nadal toodo tak. Jednak należy używać hello Azure toomanage portalu licencji na poziomie grupy.

- Usługi Azure AD automatycznie zarządza licencji modyfikacje w wyniku zmiany członkostwa w grupie. Zazwyczaj modyfikacje licencji są efektywne w ciągu minut zmiany członkostwa.

- Użytkownik może należeć do zasad licencji określono wiele grup. Użytkownik ma także niektórych przypisane bezpośrednio, poza żadnych grup licencji. Hello wynikowa stan użytkownika jest kombinacją wszystkich przydzielonych produktu i licencji usługi.

- W niektórych przypadkach licencji nie można przypisać tooa użytkownika. Na przykład może nie być wystarczającej liczby dostępnych licencji w dzierżawie powitalnych lub usługi powodujące konflikt może zostać przypisane na powitania sam czas. Administratorzy mają dostęp tooinformation o użytkownikach, dla których usługi Azure AD nie można całkowicie przetworzyć grupy licencji. Następnie potencjalnie działań korygujących, na podstawie tych informacji.

- W publicznej wersji zapoznawczej płatną lub wersji próbnej subskrypcji dla wersji Azure AD podstawowa lub Premium jest wymagana w hello dzierżawy toouse licencji na podstawie grupy zarządzania.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat innych scenariuszy zarządzania licencji za pośrednictwem na podstawie grupy licencji, zobacz:

* [Rozpoczynanie pracy z licencjami w usłudze Azure Active Directory](active-directory-licensing-get-started-azure-portal.md)
* [Przypisywanie licencji tooa grupy w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identyfikowanie i rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Jak osoba toomigrate — licencjonowani użytkownicy toogroup na podstawie Licencjonowanie w usłudze Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Usługa Azure Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze](active-directory-licensing-group-advanced.md)
