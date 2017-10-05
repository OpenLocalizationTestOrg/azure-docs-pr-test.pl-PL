---
title: "Zaloguj się instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zalogować się do programu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Azure logowania instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse

Zestaw narzędzi platformy Azure dla programu Eclipse udostępnia dwie metody logowanie do konta platformy Azure:

  * **Interakcyjne** — gdy używana jest ta metoda będzie wprowadź swoje poświadczenia usługi Azure każdym logowaniu się do konta platformy Azure.
  * **Automatyczne** — w przypadku korzystania z tej metody spowoduje utworzenie pliku poświadczeń, który zawiera dane główne usługi, po upływie którego służy plik poświadczeń do automatycznego logowania się do konta platformy Azure.

Kroki opisane w poniższych sekcjach opisano sposób używania każdej metody.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Interakcyjne logowanie do konta platformy Azure

Poniższe kroki przedstawiają sposób logowania się do usługi Azure ręcznie wprowadzić poświadczenia platformy Azure.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][I01]

1. Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **Interactive**, a następnie kliknij przycisk **logowania**.

   ![Zaloguj się okno dialogowe][I02]

1. Gdy **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][I03]

1. Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Podpisywanie poza konta platformy Azure po zalogowaniu trybie interakcyjnym

Po skonfigurowaniu kroki opisane w poprzedniej sekcji, zostaną automatycznie wylogowani z konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse. Jednak jeśli chcesz wylogować się z konta platformy Azure bez ponownego uruchamiania Eclipse, należy użyć następujące kroki.

1. W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.

   ![Menu Eclipse Azure wylogowaniu][L01]

1. Gdy **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.

   ![Wyloguj się okno dialogowe][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Automatyczne logowanie do konta platformy Azure i utworzeniu pliku poświadczenia do użycia w przyszłości

Poniższe kroki przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi. Po wykonaniu tych kroków, Eclipse będą automatycznie używać pliku poświadczeń do automatycznego rejestrowania użytkownika na platformie Azure każdym otwarciu projektu.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][A01]

1. Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.

   ![Zaloguj się okno dialogowe][A02]

1. Gdy **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A03]

1. Gdy **tworzenia plików uwierzytelniania** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.

   ![Okno dialogowe logowania do platformy Azure][A04]

1. **Stan Creatation nazwy głównej usługi** zostanie wyświetlone okno dialogowe i po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.

   ![Okno dialogowe Stan Creatation nazwy głównej usługi][A05]

1. Gdy **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A06]

1. Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Podpisywanie poza konta platformy Azure po zalogowaniu automatycznie

Po skonfigurowaniu kroki opisane w poprzedniej sekcji, Azure Toolkit spowoduje automatyczne zalogowanie na konto platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse. Jednak aby wylogować się z konta platformy Azure i uniemożliwić automatycznego rejestrowania w zestawie narzędzi programu Azure, należy użyć następujących kroków.

1. W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.

   ![Menu Eclipse Azure wylogowaniu][L01]

1. Gdy **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.

   ![Wyloguj się okno dialogowe][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Logowanie do konta platformy Azure automatycznie przy użyciu pliku poświadczeń, które zostały już utworzone

Jeśli możesz wylogować się z platformy Azure, korzystając z programu Eclipse, należy ponownie skonfigurować zestaw narzędzi platformy Azure dla programu Eclipse użyć pliku poświadczeń, które zostały utworzone, aby automatycznie mógł zalogować się na konto platformy Azure. Poniższe kroki objaśniają Konfigurowanie narzędzi Azure, aby wykorzystywała istniejący plik poświadczeń.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][A01]

1. Podczas **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.

   ![Zaloguj się okno dialogowe][A02]

1. Gdy **wybierz plik uwierzytelniony** zostanie wyświetlone okno dialogowe, wybierz plik poświadczeń, który został utworzony wcześniej, a następnie kliknij przycisk **wybierz**.

   ![Zaloguj się okno dialogowe][A08]

1. Gdy **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A06]

1. Gdy **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * *Zaloguj się instrukcje dotyczące zestawu narzędzi platformy Azure dla programu Eclipse (w tym artykule)*
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
