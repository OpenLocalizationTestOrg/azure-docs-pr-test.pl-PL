---
title: "Przegląd Roaming stanu aaaEnterprise | Dokumentacja firmy Microsoft"
description: "Zawiera informacje dotyczące ustawień roamingu stanu przedsiębiorstwa na urządzeniach z systemem Windows. Roamingu stanu przedsiębiorstwa udostępnia użytkownikom środowisko unified na ich urządzeniach z systemem Windows i skraca czas hello potrzebne do skonfigurowania nowego urządzenia."
services: active-directory
keywords: "Co to jest roamingu stanu przedsiębiorstwa, synchronizacji przedsiębiorstwa systemu windows w chmurze"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Omówienie roamingu stanu przedsiębiorstwa
Z systemem Windows 10 [usługi Azure Active Directory (Azure AD)](active-directory-whatis.md) użytkowników korzyści hello możliwości toosecurely zsynchronizować ich toohello danych ustawienia aplikacji w chmurze i ustawienia użytkownika. Roamingu stanu przedsiębiorstwa udostępnia użytkownikom środowisko unified na ich urządzeniach z systemem Windows i skraca czas hello potrzebne do skonfigurowania nowego urządzenia. Roamingu stanu przedsiębiorstwa działa podobnie standard toohello [konsumenta ustawienia synchronizacji](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) która została wprowadzona w systemie Windows 8. Ponadto roamingu stanu przedsiębiorstwa oferuje:

* **Rozdzielenie firmowych i konsumentów danych** — organizacje mają kontrolę nad ich danych i nie istnieje żadne mieszanie danych firmowych w konta użytkownika w chmurze lub danych konsumentów w konta chmury przedsiębiorstwa.
* **Ulepszone zabezpieczenia** — dane są automatycznie szyfrowane przed opuszczeniem urządzenia z systemem Windows 10 hello użytkownika za pomocą usługi Azure Rights Management (Azure RMS) i danych pozostaje zaszyfrowany magazynowanych w chmurze hello. Cała zawartość pozostaje zaszyfrowany magazynowanych w chmurze hello, z wyjątkiem hello przestrzeni nazw, takich jak ustawienia nazwy i nazwy aplikacji systemu Windows.  
* **Lepsze monitorowanie i zarządzanie** — zapewnia widoczność i kontroli za pośrednictwem, który przeprowadza synchronizację ustawień w Twojej organizacji i na których urządzeniach dzięki integracji portalu hello Azure AD. 

Roamingu stanu przedsiębiorstwa jest dostępne w wielu regionach platformy Azure. Hello zaktualizować listę dostępnych regionów na powitania można znaleźć [usługi Azure uporządkowane według regionów](https://azure.microsoft.com/regions/#services) strony w usłudze Azure Active Directory.

| Artykuł | Opis |
| --- | --- |
| [Włącz Roaming stanu przedsiębiorstwa w usłudze Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md) |Roamingu stanu przedsiębiorstwa jest dostępne tooany organizacji z subskrypcją Premium usługi Azure Active Directory (Azure AD). Aby uzyskać więcej informacji na temat tooget subskrypcji usługi Azure AD, zobacz hello [produktu usługi Azure AD](https://azure.microsoft.com/services/active-directory) strony. |
| [Ustawienia i dane mobilne — często zadawane pytania](active-directory-windows-enterprise-state-roaming-faqs.md) |W tym temacie odpowiedzi na pytania Administratorzy IT mogą mieć o ustawieniach i synchronizacji danych aplikacji. |
| [Zasady grupy i ustawienia zarządzania urządzeniami Przenośnymi dla ustawień synchronizacji](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 udostępnia zasady grupy i urządzeniami przenośnymi zarządzania urządzeniami Przenośnymi zasad ustawień toolimit ustawień synchronizacji. |
| [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |Witaj poniżej znajduje się pełna lista wszystkich ustawień hello, które będą przekazywane i/lub być zapasową w systemie Windows 10. |
| [Rozwiązywanie problemów](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |W tym temacie niektóre podstawowe kroki do rozwiązywania problemów i zawiera listę znanych problemów. |

