---
title: "aaaAdding usługi Azure Active Directory przy użyciu usług połączonych w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dodawanie usługi Azure Active Directory za pomocą programu Visual Studio Dodaj połączone usługi hello — okno dialogowe"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Dodawanie usługi Azure Active Directory przy użyciu usług połączonych w programie Visual Studio
Za pomocą usługi Azure Active Directory (Azure AD), może obsługiwać pojedynczego logowania jednokrotnego (SSO) dla aplikacji sieci web platformy ASP.NET MVC ani uwierzytelnianie usługi Active Directory w usługach interfejsu API sieci Web. Azure Active Directory Authentication użytkowników można za pomocą ich kont z aplikacji sieci web tooyour tooconnect usługi Azure Active Directory. Zalety Hello Azure uwierzytelnianie usługi Active Directory z interfejsu API sieci Web obejmują zwiększone bezpieczeństwo danych podczas udostępnianie interfejsu API z aplikacji sieci web. Z usługą Azure AD nie ma toomanage system oddzielne z zarządzaniem konta i użytkownika.

## <a name="prerequisites"></a>Wymagania wstępne
- Konto platformy Azure — Jeśli nie masz konta platformy Azure, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Połącz tooAzure Active Directory przy użyciu usług połączonych hello okna dialogowego
1. W programie Visual Studio Utwórz lub Otwórz projekt platformy ASP.NET MVC lub projekt interfejsu API sieci Web platformy ASP.NET.

1. Z hello Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **usług połączonych** węzeł i wybierz z menu kontekstowego hello **dodać usług połączonych**.

1. Na powitania **usług połączonych** wybierz pozycję **uwierzytelniania w usłudze Azure Active Directory**.
   
    ![Strona usług połączonych](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. Na powitania **wprowadzenie** strony hello **Konfigurowanie usługi Azure AD Authentication** kreatora wybierz **dalej**.
   
    ![Strona wprowadzenia](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. Na powitania **jednokrotnego na** strony hello **Konfigurowanie usługi Azure AD Authentication** kreatora, wybierz domenę z hello **domeny** listy rozwijanej. Witaj listy domen zawiera wszystkie domeny jest dostępny przez konta hello wymienione w oknie dialogowym Ustawienia konta hello. Alternatywnie, można wprowadzić nazwę domeny, jeśli nie znajdziesz hello szukasz, takich jak `mydomain.onmicrosoft.com`. Można wybrać toocreate opcji hello aplikację usługi Azure Active Directory lub użyć ustawień hello z istniejącej aplikacji usługi Azure Active Directory. Wybierz **dalej** po zakończeniu.
   
    ![Jednokrotnego na stronie](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Na powitania **dostęp do katalogu** strony hello **Konfigurowanie usługi Azure AD Authentication** kreatora upewnij się, że hello **odczytuj dane katalogu** zaznaczenia pola wyboru. 
   
    ![Strona dostępu do katalogu](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Wybierz **Zakończ** tooadd hello niezbędną konfigurację tooenable kodu i odwołania projektu do uwierzytelniania usługi Azure AD. Witaj domeny usługi Active Directory można wyświetlić na powitania [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio spowoduje wyświetlenie [co się stało](#how-your-project-is-modified) tooshow artykułu możesz jak projekt został zmodyfikowany. Toocheck, że wszystko działało, otwórz je hello zmodyfikowane pliki konfiguracji i sprawdź, czy ustawienia hello wymienione w artykule hello są dostępne. 

## <a name="how-your-project-is-modified"></a>Jak zmienić jest projektu
Po uruchomieniu kreatora hello Visual Studio dodaje Azure Active Directory i skojarzone odwołania tooyour projektu. Pliki konfiguracji i plików kodu w projekcie są również zmodyfikowanych tooadd obsługę usługi Azure AD. Hello modyfikacje określonych przez Visual Studio, które są zależne od typu projektu hello. Aby uzyskać szczegółowe informacje dotyczące sposobu zostaną zmodyfikowane projekty składnika ASP.NET MVC, zobacz [jakie projektów MVC — happened](http://go.microsoft.com/fwlink/p/?LinkID=513809). Dla projektów interfejsu API sieci Web, zobacz [co się stało — projekty interfejsu API sieci Web](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Następne kroki
* [Forum MSDN dotyczące usługi Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Dokumentacja usługi Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Wpis w blogu: TooAzure wprowadzenie do usługi Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

