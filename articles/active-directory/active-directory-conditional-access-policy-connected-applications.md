---
title: "zasady dostępu warunkowego opartego na urządzenia usługi Azure Active Directory aaaConfigure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zasady dostępu warunkowego opartego na urządzeniach usługi Azure Active Directory tooconfigure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory

Z [dostępu warunkowego w usłudze Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), można dostosować sposób autoryzowani użytkownicy mają dostęp do zasobów. Na przykład można ograniczyć hello toocertain zasobów tootrusted urządzeń. Zasady dostępu warunkowego, która wymaga zaufanego urządzenia jest nazywana zasad dostępu warunkowego opartego na urządzeniu.

Ten temat zawiera informacje o jak zasady dla aplikacji połączone AD Azure dostępu warunkowego opartego na urządzeniach tooconfigure. 


## <a name="before-you-begin"></a>Przed rozpoczęciem

Ties dostępu warunkowego opartego na urządzeniu **dostępu warunkowego dla usługi Azure AD** i **zarządzania urządzeniami usługi Azure AD razem**. Jeśli nie masz doświadczenia z jednym z tych obszarów jeszcze, należy przeczytać następujące tematy, najpierw hello:

- **[Dostęp warunkowy w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  — w tym temacie przedstawiono u omówienie warunkowego dostępu i hello terminologii pokrewne.

- **[Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory](device-management-introduction.md)**  — ten temat zawiera omówienie programu hello różne opcje masz tooconnect urządzeń z usługą Azure AD. 


## <a name="trusted-devices"></a>Zaufanych urządzeń

W świecie pierwszy mobile, najpierw chmury Azure Active Directory umożliwia toodevices rejestracji jednokrotnej, aplikacji i usług z dowolnego miejsca. Dla niektórych zasobów w danym środowisku, udzielanie dostępu wybranym użytkownikom toohello może nie być wystarczająca. Ponadto toohello odpowiednich użytkowników, użytkownik może wymagać toobe zaufanego urządzenia używane tooaccess zasobu. W danym środowisku, można zdefiniować, co to jest oparta na zaufanym urządzeniu hello następujące składniki:

- Witaj [platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) na urządzeniu
- Określa, czy urządzenie jest zgodne
- Określa, czy urządzenie jest przyłączony do domeny 

Witaj [platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) charakteryzuje się hello systemu operacyjnego, który działa na urządzeniu. W zasadach dostępu warunkowego opartego na urządzeniu można ograniczyć platform urządzeń toospecific dostępu toocertain zasobów.



W zasadach dostępu warunkowego opartego na urządzeniu można wymagać toobe zaufanych urządzeń oznaczone jako zgodne.

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Urządzenia może być oznaczony jako zgodne w katalogu hello przez:

- Usługi Intune 
- System zarządzania urządzeniami przenośnymi innej firmy, która integruje się z usługą Azure AD  

Tylko urządzenia, które są połączone tooAzure AD może być oznaczony jako zgodne. tooconnect tooAzure urządzenia usługi Active Directory, masz hello następujące opcje: 

- Azure AD w zarejestrowany
- Azure AD dołączony
- Hybrydowe przyłączonych do usługi Azure AD

    ![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Jeśli masz nakłady zasobów lokalnej usługi Active Directory (AD), można rozważyć urządzeń, które nie są połączone tooAzure AD, ale toobe sprzężonych tooyour AD zaufane.

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Następne kroki

Przed skonfigurowaniem zasad dostępu warunkowego opartego na urządzeniu w danym środowisku, należy podjąć przyjrzeć się hello [najlepszych rozwiązań dotyczących dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-best-practices.md).

