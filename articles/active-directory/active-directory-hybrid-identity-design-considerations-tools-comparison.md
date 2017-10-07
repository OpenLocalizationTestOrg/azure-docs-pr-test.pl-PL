---
title: "Tożsamość hybrydowa: porównanie narzędzi do integracji katalogów | Microsoft Docs"
description: "To jest strona zawiera kompleksowe tabelę, która porównuje hello różnych narzędzi integracji katalogów, których można użyć do integracji katalogów."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Tożsamość hybrydowa: porównanie narzędzi do integracji katalogów
Latach hello hello narzędzia do integracji katalogów były rozbudowywane i.  Ten dokument jest toohelp skonsolidowanego widoku tych narzędzi i porównanie funkcji hello, które są dostępne w każdym.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect obejmuje składniki hello i funkcje wcześniej wydane jako narzędzia Dirsync i AAD Sync. Te narzędzia nie są udostępniane oddzielnie, a wszystkie przyszłe ulepszenia będą uwzględniane w tooAzure aktualizacje AD Connect, aby zawsze wiedzieć, gdzie tooget hello najnowsze funkcje.
> 
> Narzędzia DirSync i Azure AD Sync są przestarzałe. Więcej informacji można znaleźć [tutaj](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Użyj powitania po klucz dla każdej z tabel hello.

● = dostępna teraz  
PW = w przyszłym wydaniu  
PZ = publiczna wersja zapoznawcza  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud lokalnymi synchronizacji
| Funkcja | Azure Active Directory Connect | Usługi synchronizacji usługi Azure Active Directory (AAD Sync) | Narzędzie do synchronizacji z usługą Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Połącz toosingle w lokalnym lesie usługi Active Directory |● |● |● |● |● |
| Połącz toomultiple lokalnych lasów usługi AD |● |● | |● |● |
| Połącz toomultiple lokalnej organizacjami Exchange |● | | | | |
| Połącz toosingle lokalnego katalogu LDAP |PW | | |● |● |
| Połącz toomultiple w lokalnych katalogach LDAP |PW | | |● |● |
| Połączenie lokalne tooon AD i lokalnymi katalogami LDAP |PW | | |● |● |
| Łączenie systemów toocustom (np. SQL, Oracle, MySQL itp.) |PW | | |● |● |
| Synchronizowanie atrybutów zdefiniowanych przez klienta (rozszerzenia katalogów) |● | | | | |
| Połączenie lokalne tooon HR (np. SAP, Oracle eBusiness, PeopleSoft) |PW | | |● |● |
| Inicjowanie obsługi systemów lokalnych tooon obsługuje reguły synchronizacji programu FIM i łączniki. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Synchronizacja lokalnych tooOn chmury
| Funkcja | Azure Active Directory Connect | Usługi synchronizacji usługi Azure Active Directory | Narzędzie do synchronizacji z usługą Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Zapisywanie zwrotne urządzeń |● | |● | | |
| Zapisywanie zwrotne atrybutów (dla wdrożenia hybrydowego programu Exchange) |● |● |● |● |● |
| Zapisywanie zwrotne obiektów grup |● | | | | |
| Zapisywanie zwrotne haseł (z funkcji samoobsługowego resetowania hasła i zmiany hasła) |● |● | | | |

## <a name="authentication-feature-support"></a>Obsługa funkcji uwierzytelniania
| Funkcja | Azure Active Directory Connect | Usługi synchronizacji usługi Azure Active Directory | Narzędzie do synchronizacji z usługą Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Synchronizacja haseł dla pojedynczego lokalnego lasu usługi AD |● |● |● | | |
| Synchronizacja haseł dla wielu lokalnych lasów usługi AD |● |● | | | |
| Logowanie jednokrotne z federacją |● |● |● |● |● |
| Zapisywanie zwrotne haseł (z funkcji samoobsługowego resetowania hasła i zmiany hasła) |● |● | | | |

## <a name="set-up-and-installation"></a>Konfiguracja i instalacja
| Funkcja | Azure Active Directory Connect | Usługi synchronizacji usługi Azure Active Directory | Narzędzie do synchronizacji z usługą Azure Active Directory (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Obsługuje instalację na kontrolerze domeny |● |● |● | |
| Obsługuje instalację przy użyciu programu SQL Express |● |● |● | |
| Łatwe uaktualnienie z narzędzia DirSync |● | | | |
| Lokalizacja środowiska użytkownika administratora tooWindows języków serwera |● |● |● | |
| Lokalizacja użytkownika końcowego UX tooWindows języków serwera | | | |● |
| Obsługa systemu Windows Server 2008 i Windows Server 2008 R2 |● dla synchronizacji, nie dla federacji |● |● |● |
| Obsługa systemu Windows Server 2012 i Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtrowanie i konfiguracja
| Funkcja | Azure Active Directory Connect | Usługi synchronizacji usługi Azure Active Directory | Narzędzie do synchronizacji z usługą Azure Active Directory (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtrowanie według domen i jednostek organizacyjnych |● |● |● |● |● |
| Filtrowanie według wartości atrybutów obiektów |● |● |● |● |● |
| Zezwalaj na minimalny zbiór synchronizowane toobe atrybutów (MinSync) |● |● | | | |
| Zezwalaj na inną usługę toobe szablony zostały zastosowane do przepływów atrybutów |● |● | | | |
| Umożliwia usuwanie atrybutów z przepływu z usługi AD tooAzure AD |● |● | | | |
| Umożliwia zaawansowane dostosowywanie przepływów atrybutów |● |● | |● |● |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

