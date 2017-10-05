---
title: "Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zalogować się do systemu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla IntelliJ."
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ

Zestaw narzędzi platformy Azure dla IntelliJ udostępnia dwie metody logowania do konta platformy Azure:

  * **Interakcyjne**: należy wprowadzić poświadczenia platformy Azure za każdym razem, zaloguj się do konta platformy Azure.
  * **Automatyczne**: Tworzenie pliku poświadczeń, który służy do automatycznego logowania do konta platformy Azure.

W poniższych sekcjach opisano sposób używania każdej metody.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a>Zaloguj się interaktywnie do konta platformy Azure

Aby zalogować się do platformy Azure ręcznie wprowadzić poświadczenia platformy Azure, wykonaj następujące czynności:

1. Otwórz projekt z IntelliJ IDEA.

2. Kliknij przycisk **narzędzia**, wskaż polecenie **Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Polecenie IntelliJ Azure logowania][I01]

3. W **Azure logowania** wybierz **Interactive**, a następnie kliknij przycisk **Zaloguj**.

   ![Okno Azure logowania z Interactive wybrane][I02]

4. W **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.

   ![W oknie dialogowym logowania do platformy Azure][I03]

5. W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Okno dialogowe Wybieranie subskrypcji][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Wylogować się z konta platformy Azure, po zarejestrowaniu trybie interakcyjnym

Po skonfigurowaniu konta przy użyciu powyższych kroków możesz spowoduje automatyczne wylogowanie z konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA. Jednak jeśli chcesz wylogować się z konta platformy Azure *bez* ponowne uruchomienie IntelliJ IDEA, wykonaj następujące czynności.

1. W IntelliJ IDEA na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure Wyloguj**.

   ![Polecenie IntelliJ Azure Wyloguj][L01]

2. W **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.

   ![Okno potwierdzenia Azure Wyloguj][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a>Zaloguj się do konta platformy Azure automatycznie

Ta sekcja przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi. Po zakończeniu tego procesu Eclipse używa pliku poświadczeń do automatycznie Cię logować do usługi Azure każdym otwarciu projektu.

1. Otwórz projekt z IntelliJ IDEA.

2. Na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Polecenie IntelliJ Azure logowania][A01]

3. W **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.

   ![Okno Azure logowania z automatycznego wybrane][A02]

4. W **dialogowym logowania do usługi Azure** okna, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.

   ![W oknie dialogowym logowania do platformy Azure][A03]

5. W **tworzenia plików uwierzytelniania** okna, wybierz subskrypcje, które chcesz użyć, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.

   ![Tworzenie plików uwierzytelniania okna][A04]

6. W **stan tworzenia nazwy głównej usługi** okno dialogowe po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.

   ![Okno dialogowe Stan tworzenia nazwy głównej usługi][A05]

7. W **Azure logowania** okna, kliknij przycisk **Zaloguj**.

   ![Okno dialogowe logowania do platformy Azure][A06]

8. W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Okno dialogowe Wybieranie subskrypcji][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Wylogować się z konta platformy Azure po zalogowaniu się automatycznie

Po skonfigurowaniu konta przy użyciu powyższych kroków Azure Toolkit automatycznie loguje się użytkownik do konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA. Jednak aby wylogować się z konta platformy Azure i uniemożliwić automatycznego rejestrowania w zestawie narzędzi programu Azure, wykonaj następujące czynności:

1. W IntelliJ IDEA na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure Wyloguj**.

   ![Polecenie IntelliJ Azure Wyloguj][L01]

2. W **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.

   ![Okno potwierdzenia Azure Wyloguj][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Zaloguj się do konta platformy Azure automatycznie przy użyciu istniejącego pliku poświadczeń

Jeśli możesz wylogować się z konta platformy Azure, korzystając z IntelliJ IDEA, możesz korzystać istniejący plik poświadczeń do automatycznie zalogować się do konta. Aby skonfigurować zestaw narzędzi platformy Azure dla programu Eclipse wykorzystywała istniejący plik poświadczeń, wykonaj następujące czynności:

1. Otwórz projekt z IntelliJ IDEA.

2. Na **narzędzia** menu wskaż **Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Polecenie IntelliJ Azure logowania][A01]

3. W **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.

   ![Okno Azure logowania z automatycznego wybrane][A02]

4. W **wybierz plik Authentication** okno dialogowe, wybierz plik utworzonej wcześniej poświadczenia, a następnie kliknij **wybierz**.

   ![Wybierz plik Authentication — okno dialogowe][A08]

5. W **Azure logowania** okna, kliknij przycisk **Zaloguj**.

   ![Okno Azure logowania z automatycznego wybrane][A06]

6. W **Wybierz subskrypcje** okno dialogowe, subskrypcje, które chcesz użyć, a następnie kliknij przycisk **OK**.

   ![Okno dialogowe Wybieranie subskrypcji][A07]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Nowości w zestawie narzędzi programu Azure dla programu Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * [Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Nowości w zestawie narzędzi programu Azure for IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * *Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ* (w tym artykule)
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
