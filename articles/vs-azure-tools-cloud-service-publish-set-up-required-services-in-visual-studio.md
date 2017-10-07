---
title: "aaaPrepare toopublish lub wdrożyć aplikację Azure w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooset procedury hello chmury i przechowywania konta usług i konfigurowania aplikacji platformy Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Przygotowanie tooPublish lub wdrożyć aplikację Azure w programie Visual Studio
## <a name="overview"></a>Omówienie
Zanim będzie można opublikować projekt usługi w chmurze, możesz skonfigurować hello następujące usługi:

* A **usługi w chmurze** toorun ról w hello środowiska platformy Azure
* A **konta magazynu** zapewniający dostęp do usług obiektów Blob, kolejki i tabeli toohello.

Użyj hello następujące procedury tooset tych usług i konfigurowania aplikacji

## <a name="create-a-cloud-service"></a>Tworzenie usługi w chmurze
toopublish tooAzure usługi chmury, należy najpierw utworzyć usługi w chmurze, uruchamianego ról w hello środowiska platformy Azure. Usługi w chmurze można tworzyć w hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), zgodnie z opisem w sekcji hello **toocreate usługi w chmurze przy użyciu hello klasycznego portalu Azure**w dalszej części tego tematu. Usługi w chmurze można również utworzyć w programie Visual Studio, używając Kreatora publikacji hello.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate usługi w chmurze przy użyciu programu Visual Studio
1. Otwórz menu skrótów hello hello Azure projektu i wybierz polecenie **publikowania**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Jeśli masz konta, zaloguj się przy użyciu nazwy użytkownika i hasła dla konta Microsoft hello lub konta organizacyjnego, który został skojarzony z subskrypcją platformy Azure.
3. Wybierz hello **dalej** toohello tooadvance przycisk **ustawienia** strony.

    ![Typowe ustawienia publikowania Kreatora](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. W hello **usługi w chmurze** wybierz **Utwórz nowy**. Witaj **tworzenie usług Azure** zostanie wyświetlone okno dialogowe.
5. Wprowadź nazwę hello usługi w chmurze. Nazwa Hello stanowi część adresu URL hello usługi i dlatego musi być globalnie unikatowa. Nazwa Hello nie jest rozróżniana wielkość liter.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>usługi w chmurze przy użyciu klasycznego portalu Azure hello toocreate
1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkId=253103) w witrynie internetowej firmy Microsoft hello.
2. (opcjonalnie) toodisplay listę usługi w chmurze, które zostały już utworzone, wybierz link usługi w chmurze powitania po lewej stronie powitania hello strony.
3. Wybierz hello  **+**  ikonę w hello lewym dolnym rogu, a następnie wybierz pozycję **usługi w chmurze** w wyświetlonym menu hello. Inny ekran z dwóch opcji **szybkie tworzenie** i **Utwórz niestandardowy**, zostanie wyświetlone. Jeśli wybierzesz **szybkie tworzenie**, można utworzyć usługi w chmurze tak, podając jego adres URL i hello regionu, gdzie będzie fizycznie obsługiwana. Jeśli wybierzesz **Utwórz niestandardowy**, natychmiast można opublikować usługi w chmurze, określając pakietu (pliku cspkg), plik konfiguracji (cscfg), a certyfikat. Tworzenie niestandardowych nie jest wymagane, jeśli planujesz toopublish usługi w chmurze przy użyciu hello **publikowania** polecenia w projekcie platformy Azure. Witaj **publikowania** polecenie jest dostępne w menu skrótów hello projektu platformy Azure.
4. Wybierz **szybkie tworzenie** toolater opublikować usługi w chmurze za pomocą programu Visual Studio.
5. Określ nazwę usługi w chmurze. pełny adres URL Hello pojawi się nazwa toohello dalej.
6. Na liście hello wybierz region hello, w której większość użytkowników znajdują się.
7. U dołu okna hello hello, wybierz hello **Tworzenie usługi w chmurze** łącza.

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu
Konto magazynu zapewnia dostęp toohello usług obiektów Blob, kolejki i tabeli. Konto magazynu można utworzyć za pomocą programu Visual Studio lub hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate konto magazynu przy użyciu programu Visual Studio
1. W **Eksploratora rozwiązań**, otwórz menu skrótów hello hello **magazynu** węzeł, a następnie wybierz pozycję **Utwórz konto magazynu**.

    ![Utwórz nowe konto magazynu Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Wybierz lub wprowadź następujące informacje dotyczące hello nowe konto magazynu w hello hello **Utwórz konto magazynu** okno dialogowe.

   * Witaj ma konto magazynu hello tooadd toowhich subskrypcji platformy Azure.
   * Nazwa Hello ma toouse hello nowe konto magazynu.
   * Witaj region lub grupę koligacji, (na przykład zachodnie stany USA lub Azja Wschodnia).
   * Witaj typ replikacji ma toouse dla konta magazynu hello, takich jak geograficznie nadmiarowy.
3. Gdy wszystko będzie gotowe, wybierz pozycję **Utwórz**.hello nowe konto magazynu jest wyświetlana w hello **magazynu** na liście **Eksploratora serwera**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate konto magazynu przy użyciu hello klasycznego portalu Azure
1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkId=253103) w witrynie internetowej firmy Microsoft hello.
2. (Opcjonalnie) tooview kont magazynu, wybierz hello **magazynu** łącze w panelu hello na powitania po lewej stronie powitania strony.
3. Witaj lewym dolnym rogu strony hello, wybierz hello  **+**  ikony.
4. W wyświetlonym menu hello wybierz **magazynu**, a następnie wybierz pozycję **szybkie tworzenie**.
5. Nadaj nazwę, która spowoduje unikatowy adres url hello konta magazynu.
6. Nadaj nazwę usługi w chmurze. pełny adres URL Hello pojawi się nazwa toohello dalej.
7. W wykazie hello regionów wybierz region, w którym znajdują się większość użytkowników.
8. Określ, czy replikacja geograficzna tooenable. Jeśli możesz włączyć replikację geograficzną, dane zostaną zapisane w wielu lokalizacjach fizycznych tooreduce hello ryzyko utraty. Ta funkcja umożliwia bardziej kosztownego magazynowania, ale może zmniejszyć koszt hello przez włączenie lokalizacji geograficznej, podczas tworzenia konta magazynu hello zamiast opcji dodawania funkcji hello później. Aby uzyskać więcej informacji, zobacz [— replikacja geograficzna](http://go.microsoft.com/fwlink/?LinkId=253108).
9. U dołu okna hello hello, wybierz hello **Utwórz konto magazynu** łącza.

Po utworzeniu konta magazynu zobaczysz hello adresów URL, użyj tooaccess zasobów w każdej z usług Azure storage hello, a także hello klucze podstawowe i pomocnicze dostępu dla konta. Użyj tych żądań tooauthenticate przed hello usług magazynu kluczy.

> [!NOTE]
> Witaj pomocniczy klucz dostępu zawiera hello sam dostęp do konta magazynu tooyour jako hello podstawowy klucz dostępu i jest generowany na nazwę kopii zapasowej klucza podstawowego dostępu zagrożenia bezpieczeństwa. Ponadto zaleca się ponowne generowanie kluczy dostępu na bieżąco. Ciąg ustawienie toouse hello dodatkowej klucz połączenia można modyfikować podczas ponownego generowania klucza podstawowego hello, umożliwi zmodyfikowanie go toouse hello ponownie wygenerować podstawowy klucz podczas ponownego generowania klucza pomocniczego hello.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Konfigurowanie aplikacji usługi toouse podał hello konta magazynu
Należy skonfigurować dowolnej roli, który uzyskuje dostęp do magazynu usług toouse hello usług magazynu platformy Azure utworzonych przez użytkownika. toodo, można użyć wielu konfiguracji usługi Azure projektu. Domyślnie dwa są tworzone w projekcie platformy Azure. Za pomocą wielu konfiguracji usługi, można użyć hello tego samego połączenia parametrów w kodzie, ale ma inną wartość parametrów połączenia w każdej konfiguracji usługi. Na przykład można użyć jednego toorun konfiguracji usługi i debugowania aplikacji lokalnie przy użyciu emulatora magazynu Azure hello i toopublish konfiguracji innej usługi tooAzure Twojej aplikacji. Aby uzyskać więcej informacji dotyczących konfiguracji usługi, zobacz [Konfigurowanie Your Azure projektu przy użyciu usługi konfiguracji z wieloma](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>udostępnia usługi toouse Twojej aplikacji, które hello konta magazynu tooconfigure
1. W programie Visual Studio Otwórz rozwiązania Azure. W Eksploratorze rozwiązań Otwórz menu skrótów powitania dla każdej roli w projekcie platformy Azure, który uzyskuje dostęp do usług magazynu hello i wybierz polecenie **właściwości**. W edytorze programu Visual Studio hello zostanie wyświetlona strona o nazwie hello hello roli. pola hello hello zostanie wyświetlona strona Hello **konfiguracji** kartę.
2. Strony właściwości hello hello roli, wybierz **ustawienia**.
3. W hello **konfiguracji usługi** listy, wybierz nazwę hello hello usługi konfiguracji, które mają tooedit. Jeśli chcesz tooall zmiany toomake hello konfiguracji usługi dla tej roli, można wybrać **wszystkie konfiguracje**.  Aby uzyskać więcej informacji o sposobie tooupdate usługi konfiguracji, zobacz sekcję hello **Zarządzanie parametry połączenia dla konta magazynu** w temacie hello [konfigurowania hello ról dla usługi w chmurze platformy Azure z programem Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify żadnych ustawień parametrów połączenia wybierz hello **...** przycisk Następne ustawienie toohello. Witaj **utworzyć parametry połączenia magazynu** zostanie wyświetlone okno dialogowe.
5. W obszarze **łączyć się przy użyciu**, wybierz hello **subskrypcji** opcji.
6. W hello **subskrypcji** Wybierz subskrypcję. Jeśli hello subskrypcji nie zawierają hello ma, wybierz hello **pobieranie ustawień publikowania** łącza.
7. W hello **nazwa konta** listy, wybierz nazwę konta magazynu. Narzędzia Azure automatycznie uzyskuje poświadczeń konta magazynu przy użyciu pliku .publishsettings hello. toospecify Twojego konta magazynu poświadczeń ręcznie, wybierz hello **ręcznie wprowadzić poświadczenia** opcji, a następnie kontynuuj tej procedury. Nazwa konta magazynu i klucza podstawowego można uzyskać z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885). Jeśli nie chcesz toospecify ustawienia konta magazynu ręcznie, wybierz hello **OK** okno dialogowe hello tooclose przycisku.
8. Wybierz hello **wprowadź konto magazynu** łącze poświadczeń.
9. W hello **nazwa konta** wprowadź hello nazwę konta magazynu.

   > [!NOTE]
   > Zaloguj się do hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), a następnie wybierz pozycję hello **magazynu** przycisku. Hello portal pokazuje listę kont magazynu. Jeśli wybierzesz konto otwiera stronę dla niego. Możesz skopiować hello nazwę konta magazynu hello na tej stronie. Jeśli używasz poprzedniej wersji hello klasyczny portal hello nazwa konta magazynu jest wyświetlana w hello **kont magazynu** widoku. toocopy to nazwa, zaznacz ją w hello **właściwości** okna tego wyświetlić, a następnie wybierz klucze hello Ctrl-C. Nazwa hello toopaste do programu Visual Studio, wybierz hello **nazwa konta** tekst pola, a następnie wybierz hello klawiszy Ctrl + V.
   >
   >
10. W hello **klucz konta** polu, wprowadź klucz podstawowy lub skopiuj i wklej go z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
     toocopy tego klucza:

    1. U dołu hello hello strony dla konta magazynu odpowiednie hello, wybierz hello **zarządzanie kluczami** przycisku.
    2. Na powitania **zarządzanie kluczami dostępu** strony, zaznacz tekst hello hello podstawowy klucz dostępu, a następnie wybierz hello klawiszy Ctrl + C.
    3. W menu Narzędzia Azure, wkleić klucz hello hello **klucz konta** pole.
    4. Należy wybrać jedną z hello następujące opcje toodetermine jak hello usługi będą uzyskiwać dostęp do konta magazynu hello:

       * **Korzystanie z protokołu HTTP**. Jest opcja Standardowa hello. Na przykład `http://<account name>.blob.core.windows.net`.
       * **Użycie protokołu HTTPS** bezpiecznego połączenia. Na przykład `https://<accountname>.blob.core.windows.net`.
       * **Określ niestandardowe punkty końcowe** dla każdego z trzech hello usług. Możesz wpisać tymi punktami końcowymi do pola powitania dla hello określonej usługi.

         > [!NOTE]
         > Tworząc niestandardowe punkty końcowe, można utworzyć bardziej złożoną parametry połączenia. Korzystając z tego formatu ciągu, można określić punktów końcowych usługi magazynu zawierające nazwę domeny niestandardowej zarejestrowany dla konta magazynu z hello usługi Blob. Ponadto można przyznać dostęp tylko tooblob zasobów w jeden kontener za pomocą sygnatury dostępu współdzielonego. Aby uzyskać więcej informacji o tym, jak niestandardowe punkty końcowe toocreate, zobacz [skonfigurować parametry połączenia magazynu Azure](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave te zmiany ciąg połączenia wybierz hello **OK** przycisk, a następnie wybierz pozycję hello **zapisać** przycisk na powitania narzędzi. Po zapisaniu zmian można pobrać wartości hello tego ciągu połączenia w kodzie, za pomocą [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Podczas publikowania tooAzure Twojej aplikacji, wybierz konfigurację usługi hello zawierającej konto magazynu Azure hello hello ciągu połączenia. Po opublikowaniu aplikacji, sprawdź, czy aplikacja hello działa zgodnie z oczekiwaniami przed hello usług Azure storage

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat publikowania tooAzure aplikacji z programu Visual Studio, zobacz [publikowania usługi w chmurze przy użyciu narzędzia Azure hello](vs-azure-tools-publishing-a-cloud-service.md).
