---
title: "Jak skonfigurować alerty zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować alerty zabezpieczeń dla rozszerzenia Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: e057120e31eeebc3da274536c09d6d9972854338
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-security-alerts-in-azure-ad-privileged-identity-management"></a>Jak skonfigurować alerty zabezpieczeń w usłudze Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Alerty zabezpieczeń
Azure Privileged Identity zarządzania (PIM) generuje alerty w przypadku podejrzanej lub niebezpieczna działania w danym środowisku. Po wyzwoleniu alertu jest wyświetlane na pulpicie nawigacyjnym usługi PIM. Wybierz alert, aby wyświetlić raport zawierający listę użytkowników lub ról, które wyzwoliła alert.

![Alerty zabezpieczeń pulpitu nawigacyjnego PIM — zrzut ekranu][1]

| Alerty | Wyzwalacz | Zalecenie |
| --- | --- | --- |
| **Role są przypisywane poza usługą PIM** |Administrator trwale został przypisany do roli, poza interfejsu usługi PIM. |Przejrzyj nowe przypisanie roli. Ponieważ inne usługi można przypisać tylko administratorami trwałymi, zmień ją na kwalifikujące się przypisania w razie potrzeby. |
| **Role są aktywowane zbyt często** |Znaleziono zbyt wiele reaktywacje z tego samego elementu role w określonym terminie w ustawieniach. |Skontaktuj się z użytkownika, aby zobaczyć, dlaczego ich uaktywniono rolę tak wiele razy. Być może limit czasu jest zbyt krótka dla ich do wykonywania swoich zadań lub może być one używane skrypty do automatycznie aktywować rolę. |
| **Role nie wymagają uwierzytelniania wieloskładnikowego w celu aktywacji** |Dostępne są role bez włączone w ustawieniach usługi MFA. |Firma Microsoft uwierzytelniania MFA można wymagać dla ról najbardziej wysoko uprzywilejowane, ale zdecydowanie zaleca się włączenie usługi MFA do aktywacji wszystkich ról. |
| **Administratorzy nie są używane role uprzywilejowane** |Brak kwalifikujących się Administratorzy, które nie zostały ostatnio aktywowane ich ról. |Uruchom Przegląd dostępu, aby określić użytkowników, którzy nie potrzebują już dostępu. |
| **Istnieje zbyt wiele administratorów globalnych** |Brak administratorów globalnych niż zalecane. |Jeśli masz dużą liczbę administratorów globalnych, istnieje prawdopodobieństwo, że użytkownicy uzyskują więcej uprawnień niż jest to wymagane. Przenieść użytkowników do ról uprzywilejowanych mniej lub upewnij niektóre z nich kwalifikuje się do roli zamiast trwale przypisana. |

## <a name="configure-security-alert-settings"></a>Konfigurowanie ustawień alertów zabezpieczeń
Niektóre alerty zabezpieczeń w PIM do pracy z własnego środowiska i cele zabezpieczeń można dostosować. Wykonaj następujące kroki, aby osiągnąć bloku ustawienia:

1. Zaloguj się do [portalu Azure](https://portal.azure.com/) i wybierz **Azure AD Privileged Identity Management** kafelka na pulpicie nawigacyjnym.
2. Wybierz **zarządzane ról uprzywilejowanych** > **ustawienia** > **alerty ustawienia**.
   
    ![Przejdź do ustawień alertów zabezpieczeń][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Alert "Role są aktywowane zbyt często"
Ten alert jest wyzwalane, gdy użytkownik aktywuje tej samej roli uprzywilejowanej wiele razy w danym okresie. Możesz skonfigurować zarówno okres czasu, jak i liczbę aktywacji.

* **Okres odnawiania aktywacji**: Określ w dni, godziny, minuty, a w drugim okresie chcesz użyć do śledzenia podejrzanych odnowienia.
* **Liczba odnowień aktywacji**: Określ liczbę aktywacji od 2 do 100, które należy wziąć pod uwagę warta alertu, w ramach czasowych została wybrana opcja. Możesz zmienić to ustawienie za pomocą suwaka, lub wpisz liczbę w polu tekstowym.

### <a name="there-are-too-many-global-administrators-alert"></a>Alert "są zbyt wielu administratorów globalnych"
PIM wyzwala ten alert, jeśli są spełnione dwa różne kryteria, a obie z nich można skonfigurować. Najpierw należy nawiązać pewnej wartości progowej administratorów globalnych. Po drugie określonego procentu przypisania roli całkowita musi być administratorów globalnych. Jeśli tylko spełnia jednego z tych wskaźników, nie powoduje wyświetlenia alertu.  

* **Minimalna liczba administratorów globalnych**: Określ liczbę administratorów globalnych od 2 do 100, należy rozważyć kwotę niebezpieczne.
* **Procent administratorów globalnych**: Określanie wartości procentowej Administratorzy, którzy administratorów globalnych, od 0 do 100%, która jest niebezpieczne w danym środowisku.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Alert "Administratorzy nie są używane role uprzywilejowane"
Ten alert wyzwala, jeśli użytkownik przejdzie do pewnego czasu bez uaktywniania roli.

* **Liczba dni**: Określ liczbę dni z zakresu od 0 do 100, które użytkownik może przejść bez uaktywniania roli.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
