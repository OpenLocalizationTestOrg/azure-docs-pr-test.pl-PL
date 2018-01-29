---
title: "Formanty w usłudze Azure Active Directory dostępu warunkowego | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak działają kontroli dostępu warunkowego w usłudze Azure Active Directory."
services: active-directory
keywords: "dostęp warunkowy do aplikacji, dostęp warunkowy przy użyciu usługi Azure AD, bezpieczny dostęp do zasobów firmy, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/29/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4cb225266a45808e5fda271e901749bf03c636e2
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="controls-in-azure-active-directory-conditional-access"></a>Formanty w usłudze Azure Active Directory dostępu warunkowego 

Z [dostępu warunkowego w usłudze Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), można kontrolować sposób autoryzowanym użytkownikom dostępu aplikacji w chmurze. W zasad dostępu warunkowego można zdefiniować odpowiedzi ("tym") określony warunek, ("w takim przypadku"). W kontekście dostępu warunkowego 

- "**w takim przypadku**" jest wywoływana **warunku — instrukcja**

- "**To zrobić**" jest wywoływana **formantów**

![Formant](./media/active-directory-conditional-access-controls/11.png)

Kombinacja instrukcji warunku z formantów reprezentuje zasady dostępu warunkowego.

![Formant](./media/active-directory-conditional-access-controls/12.png)

Każdej kontrolki jest wymagania, które muszą być spełnione przez osobę lub system logowania lub ograniczenie użytkownika można zrobić po zalogowaniu się. 

Istnieją dwa typy formantów: 

- **Formanty GRANT** — aby brama dostępu

- **Formanty sesji** — w celu ograniczenia dostępu w ramach sesji

W tym temacie wyjaśniono różne formantów, które są dostępne w usłudze Azure AD dostęp warunkowy. 

## <a name="grant-controls"></a>Udziel formantów

Udziel kontroli możesz całkowicie blokowanie dostępu lub zezwolić na dostęp z dodatkowymi wymaganiami, wybierając żądane formanty. Wiele formantów można wymagać:

- Wszystkie wybrane formanty, które należy spełnić (*i*) 
- Jeden zaznaczony formant do spełnienia (*lub*)

![Formant](./media/active-directory-conditional-access-controls/17.png)



### <a name="multi-factor-authentication"></a>Uwierzytelnianie wieloskładnikowe

Aby wymusić uwierzytelnianie wieloskładnikowe na dostęp do aplikacji określonej chmury, można użyć tego formantu. Ten formant obsługuje następujących dostawców wieloskładnikowego: 

- Azure Multi-Factor Authentication 

- Dostawcy uwierzytelniania wieloskładnikowego lokalnymi łączyć się z usługi Active Directory Federation Services (AD FS).
 
Przy użyciu usługi Multi-Factor authentication pomaga chronić zasoby z uzyskiwany przez nieautoryzowanego użytkownika, który może mieć uzyskał dostęp do podstawowego poświadczenia prawidłowego użytkownika.



### <a name="compliant-device"></a>Zgodne urządzenie

Można skonfigurować zasady dostępu warunkowego, które są oparte na urządzeniu. Celem zasad dostępu warunkowego opartego na urządzeniu jest aby udzielić dostępu do zasobów skonfigurowany tylko z zaufanych urządzeń. Wymaganie zgodnego urządzenia jest jedną z opcji należy zdefiniować jest urządzenie zaufane. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

### <a name="domain-joined-device"></a>Urządzenia przyłączone do domeny

Wymaganie inną opcją jest urządzenia przyłączone do domeny należy skonfigurować zasady dostępu warunkowego opartego na urządzeniu. To wymaganie dotyczy komputerów stacjonarnych, laptopów i tabletów przedsiębiorstwa, które są częścią lokalnej usługi Active Directory systemu Windows. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).





### <a name="approved-client-app"></a>Aplikacja kliencka zatwierdzone

Pracownicy używają urządzeń przenośnych dla obu osobiste i zadań, możesz mieć możliwość ochrony danych firmowych dostęp za pomocą urządzeń, nawet w przypadku, gdy nie są zarządzane przez użytkownika.
Można użyć [zasad ochrony aplikacji usługi Intune](https://docs.microsoft.com/intune/app-protection-policy) w celu ochrony danych firmowych, niezależnie od wszelkich rozwiązań do zarządzania urządzeniami przenośnymi (MDM).


W aplikacjach klienckich zatwierdzone może wymagać aplikację klienta, który próbuje uzyskać dostęp do obsługi aplikacji w chmurze [zasad ochrony aplikacji usługi Intune](https://docs.microsoft.com/intune/app-protection-policy). Na przykład można ograniczyć dostęp do usługi Exchange Online do aplikacji Outlook. Zasady dostępu warunkowego, która wymaga aplikacji klienta zatwierdzonych jest także znana jako [zasad dostępu warunkowego opartego na aplikacji](active-directory-conditional-access-mam.md). Aby uzyskać listę obsługiwanych klientów zatwierdzonych aplikacji, zobacz [zatwierdzone wymagania aplikacji klienta](active-directory-conditional-access-technical-reference.md#approved-client-app-requirement).


### <a name="terms-of-use"></a>Warunki użytkowania

Użytkownik może być wymagane w dzierżawie, aby wyrazić zgodę na warunki użytkowania, zanim zostanie im przyznany dostęp do zasobu. Administrator może skonfigurować i dostosować warunki użytkowania przekazując dokumentu PDF. Jeśli użytkownik znajduje się w zakresie tej kontroli dostępu do aplikacji jest przyznane tylko jeśli zostały Akceptuję warunki użytkowania. 


### <a name="custom-controls"></a>Formanty niestandardowe 

Formanty niestandardowe można tworzyć w dostępu warunkowego, które przekierować użytkowników do usługi zgodne w celu dalszego spełniają wymagania poza usługą Azure Active Directory. Dzięki temu można używać niektórych zewnętrznych uwierzytelnianie wieloskładnikowe i dostawców weryfikacji do wymuszania zasad dostępu warunkowego lub tworzenie niestandardowych usługi. W celu spełnienia tego formantu, przeglądarka użytkownika jest przekierowywany do zewnętrznej usługi, wykonuje wszelkie wymagane uwierzytelnianie lub sprawdzania poprawności działania i jest następnie przekierowany z powrotem do usługi Azure Active Directory. Jeśli użytkownik został pomyślnie uwierzytelniony lub sprawdzić poprawności, użytkownik nadal w przepływ dostępu warunkowego. 

## <a name="custom-controls"></a>Formanty niestandardowe

Kontrolki niestandardowe są możliwości wersji usługi Azure Active Directory Premium P2. Podczas korzystania z niestandardowych formantów, użytkownicy są przekierowywani do zgodne usługi by spełnić dodatkowe wymagania poza usługą Azure Active Directory. W celu spełnienia tego formantu, przeglądarka użytkownika jest przekierowywany do zewnętrznej usługi, wykonuje wszelkie wymagane uwierzytelnianie lub sprawdzania poprawności działania i jest następnie przekierowany z powrotem do usługi Azure Active Directory. Azure Active Directory sprawdza odpowiedź i, jeśli użytkownik został pomyślnie uwierzytelniony lub sprawdzić poprawności, użytkownik będzie nadal występował w przepływ dostępu warunkowego.

Tych kontrolek Zezwalaj na korzystanie z niektórych usług zewnętrznych lub niestandardowych jako kontroli dostępu warunkowego, a rozszerzenie możliwości dostępu warunkowego.

Obecnie oferty usługi zgodne dostawców obejmują:

- Duo zabezpieczeń

- RSA

- [Trusona](https://www.trusona.com/docs/azure-ad-integration-guide)

Aby uzyskać więcej informacji dotyczących tych usług skontaktuj się bezpośrednio z dostawców.

### <a name="creating-custom-controls"></a>Tworzenie niestandardowych formantów

Aby utworzyć niestandardowego formantu, najpierw należy skontaktować się dostawcę, który chcesz wykorzystać. Każdy dostawca firmy Microsoft ma swoją własną procesu i wymagania dotyczące Załóż, subskrypcji lub w przeciwnym razie staną się częścią usługi i wskazywać, że chcesz zintegrować z dostępu warunkowego. W tym momencie dostawcy zapewnia bloku danych w formacie JSON. Te dane dostawcy i dostępu warunkowego współdziałają ze sobą dzierżawy, tworzy nowego formantu i określa, jak dostęp warunkowy można stwierdzić, czy użytkownicy wykonali pomyślnie weryfikacji z dostawcy.

Skopiuj dane JSON, a następnie wkleić ją w polu tekstowym powiązane. Nie wprowadzaj żadnych zmian do formatu JSON bez jawnie zrozumienia podczas wprowadzania zmian. Wprowadzania zmian może przerwać połączenie między dostawcą a firmą Microsoft i potencjalnie Zablokuj użytkownicy spoza konta.

Można utworzyć niestandardowego formantu jest **Zarządzaj** sekcji **dostępu warunkowego** strony.

![Formant](./media/active-directory-conditional-access-controls/82.png)

Kliknięcie przycisku **nowej kontrolki niestandardowej**, powoduje otwarcie bloku z pola tekstowego danych JSON formantu.  


![Formant](./media/active-directory-conditional-access-controls/81.png)


### <a name="deleting-custom-controls"></a>Usuwanie kontrolek niestandardowych

Aby usunąć kontrolkę niestandardową, należy najpierw upewnić, że nie jest używany w żadnych zasad dostępu warunkowego. Po jego zakończeniu:

1. Przejdź do listy formanty niestandardowe

2. Kliknij przycisk...  

3. Wybierz pozycję **Usuń**.

### <a name="editing-custom-controls"></a>Niestandardowe formanty edycji

Aby edytować kontrolkę niestandardową, należy usunąć bieżącego formantu i Utwórz nowy formant zaktualizowanych informacji.




## <a name="session-controls"></a>Formanty sesji

Formanty sesji włączyć ograniczone doświadczenie w aplikacji w chmurze. Formanty sesji są wymuszane przez aplikacje w chmurze i polegać na dodatkowe informacje dostarczane przez usługę Azure AD do aplikacji o sesji.

![Formant](./media/active-directory-conditional-access-controls/31.png)

### <a name="use-app-enforced-restrictions"></a>Użyj aplikacji wymuszane ograniczeń

Aby wymagać usługi Azure AD do przekazywania informacji o urządzeniu do aplikacji w chmurze, można użyć tego formantu. Dzięki temu można sprawdzić, czy użytkownik jest pochodzi z zgodne urządzenie lub urządzenia przyłączone do domeny aplikacji w chmurze. Ten formant jest obecnie obsługiwana tylko z programem SharePoint jako aplikacji w chmurze. SharePoint używa informacji o urządzeniu umożliwia wyświetlanie użytkownikom bardziej ograniczony lub pełne środowisko w zależności od stanu urządzenia.
Aby dowiedzieć się więcej na temat sposobu wymagać ograniczony dostęp z programem SharePoint, zobacz [kontroli dostępu z urządzeń niezarządzanych](https://aka.ms/spolimitedaccessdocs).



## <a name="next-steps"></a>Następne kroki

- Jeśli chcesz wiedzieć, jak skonfigurować zasady dostępu warunkowego, zobacz [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

- Jeśli wszystko jest gotowe do skonfigurowania zasad dostępu warunkowego dla danego środowiska, zobacz [najlepszych rozwiązań dotyczących dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-best-practices.md). 
