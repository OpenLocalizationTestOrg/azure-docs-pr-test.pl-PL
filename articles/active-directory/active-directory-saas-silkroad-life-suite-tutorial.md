---
title: "Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SilkRoad życia pakietu."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="9fa6e-103">Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad</span><span class="sxs-lookup"><span data-stu-id="9fa6e-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="9fa6e-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate SilkRoad Suite użytkowania z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="9fa6e-105">Integrowanie SilkRoad Suite użytkowania z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="9fa6e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSilkRoad Suite życia</span><span class="sxs-lookup"><span data-stu-id="9fa6e-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="9fa6e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSilkRoad życia pakiet rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa6e-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="9fa6e-108">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fa6e-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9fa6e-109">Prerequisites</span></span>
<span data-ttu-id="9fa6e-110">tooconfigure integracji usługi Azure AD z pakietem życia SilkRoad należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="9fa6e-111">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa6e-111">An Azure AD subscription</span></span>
* <span data-ttu-id="9fa6e-112">Subskrypcja SilkRoad życia Suite logowanie Jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="9fa6e-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="9fa6e-113">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="9fa6e-114">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9fa6e-115">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9fa6e-116">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="9fa6e-117">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9fa6e-117">Scenario Description</span></span>
<span data-ttu-id="9fa6e-118">Celem Hello tego samouczka jest tooenable możesz tootest logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="9fa6e-119">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9fa6e-120">Dodawanie pakietu życia SilkRoad z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9fa6e-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="9fa6e-121">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa6e-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="9fa6e-122">Dodawanie zestawu życia SilkRoad z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9fa6e-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="9fa6e-123">tooconfigure hello integracji pakietu życia SilkRoad do usługi Azure AD, należy tooadd SilkRoad życia pakietu z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9fa6e-124">**tooadd SilkRoad życia pakietu z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fa6e-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa6e-125">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="9fa6e-127">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="9fa6e-128">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="9fa6e-130">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="9fa6e-132">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="9fa6e-134">W polu wyszukiwania hello wpisz **Suite życia SilkRoad**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="9fa6e-136">W okienku wyników hello, wybierz **Suite życia SilkRoad**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplikacje][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9fa6e-138">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9fa6e-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9fa6e-139">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i Azure AD SSO z pakietem życia SilkRoad testu na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9fa6e-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9fa6e-140">Dla toowork logowania jednokrotnego usługi Azure AD musi tooknow jest użytkownika odpowiednikiem hello w SilkRoad życia Suite tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="9fa6e-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu życia SilkRoad musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="9fa6e-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** SilkRoad życia pakietu.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="9fa6e-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9fa6e-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9fa6e-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9fa6e-146">**[Tworzenie użytkownika testowego zestawu życia SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave odpowiednikiem Simona Britta życia pakietu SilkRoad, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9fa6e-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9fa6e-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9fa6e-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9fa6e-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="9fa6e-150">Celem Hello w tej sekcji jest tooenable logowania jednokrotnego programu Azure AD w hello klasycznego portalu Azure i tooconfigure logowania jednokrotnego w SilkRoad życia pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="9fa6e-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fa6e-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa6e-152">Logowania jednokrotnego tooyour SilkRoad witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="9fa6e-153">tooobtain dostępu toohello SilkRoad życia Suite uwierzytelniania aplikacji dla Konfigurowanie Federacji przy użyciu usługi Microsoft Azure AD, skontaktuj się z SilkRoad pomocy technicznej lub Twoim przedstawicielem SilkRoad usług.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="9fa6e-154">Przejdź za**dostawcy usług**, a następnie kliknij przycisk **szczegóły federacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][10] 

3. <span data-ttu-id="9fa6e-156">Kliknij przycisk **pobierania metadanych Federacji**, a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][11] 

4. <span data-ttu-id="9fa6e-158">W hello klasycznego portalu Azure na powitania **Suite życia SilkRoad** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 

5. <span data-ttu-id="9fa6e-160">Na powitania **jak ma toosign użytkowników na tooSilkRoad Suite życia** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][7] 

6. <span data-ttu-id="9fa6e-162">Na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][8]   
 1. <span data-ttu-id="9fa6e-164">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używanej przez Twoją witrynę Suite życia SilkRoad toosign na tooyour użytkowników (np.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="9fa6e-165">Otwórz hello pobrane **Silkroad** pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="9fa6e-166">Zlokalizuj hello **AssertionConsumerService** tag, a następnie hello kopiowania **lokalizacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Azure AD rejestracji jednokrotnej][21] 
 4. <span data-ttu-id="9fa6e-168">Wklej wartość hello do hello **adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="9fa6e-169">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-169">Click **Next**.</span></span>

6. <span data-ttu-id="9fa6e-170">Na powitania **skonfigurować logowanie jednokrotne w SilkRoad życia Suite** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]  
 1. <span data-ttu-id="9fa6e-172">Kliknij przycisk Pobierz certyfikat, a następnie zapisz plik hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="9fa6e-173">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-173">Click **Next**.</span></span>

7. <span data-ttu-id="9fa6e-174">W Twojej **SilkRoad** aplikacji, kliknij przycisk **źródeł uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][12] 

8. <span data-ttu-id="9fa6e-176">Kliknij przycisk **Dodawanie uwierzytelniania źródła**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][13] 

9. <span data-ttu-id="9fa6e-178">W hello **Dodaj źródło uwierzytelniania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][14]  
 1. <span data-ttu-id="9fa6e-180">W obszarze **opcja 2 — plik metadanych**, kliknij przycisk **Przeglądaj** tooupload hello pobrany plik metadanych.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="9fa6e-181">Kliknij przycisk **dostawcy tożsamości utworzyć przy użyciu danych pliku**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="9fa6e-182">W hello **źródeł uwierzytelniania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][15] 

11. <span data-ttu-id="9fa6e-184">Na powitania **Edytuj źródło uwierzytelniania** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][16] 
 1. <span data-ttu-id="9fa6e-186">Jako **włączone**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="9fa6e-187">W hello **opis IdP** tekstowym, wpisz opis dla danej konfiguracji (np.: *logowania jednokrotnego programu Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="9fa6e-188">W hello **nazwa IdP** tekstowym, wpisz nazwę, która jest tooyour określonej konfiguracji (np.: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="9fa6e-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-189">Click **Save**.</span></span>

12. <span data-ttu-id="9fa6e-190">Wyłącz wszystkie źródła uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][17]

13. <span data-ttu-id="9fa6e-192">W hello klasycznego portalu Azure na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD rejestracji jednokrotnej][18]

14. <span data-ttu-id="9fa6e-194">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD rejestracji jednokrotnej][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9fa6e-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa6e-196">Create an Azure AD test user</span></span>
<span data-ttu-id="9fa6e-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="9fa6e-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9fa6e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa6e-200">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="9fa6e-202">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="9fa6e-203">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9fa6e-205">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="9fa6e-207">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="9fa6e-209">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="9fa6e-210">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="9fa6e-211">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-211">Click **Next**.</span></span>

6. <span data-ttu-id="9fa6e-212">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="9fa6e-214">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="9fa6e-215">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="9fa6e-216">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="9fa6e-217">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="9fa6e-218">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-218">Click **Next**.</span></span>

7. <span data-ttu-id="9fa6e-219">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="9fa6e-221">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9fa6e-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="9fa6e-223">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="9fa6e-224">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="9fa6e-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="9fa6e-225">Tworzenie użytkownika testowego SilkRoad życia pakietu</span><span class="sxs-lookup"><span data-stu-id="9fa6e-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="9fa6e-226">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta SilkRoad życia pakietu.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="9fa6e-227">Britta firmy musi mieć identyfikator logowania jednokrotnego (czasem określana tooas *AuthParam*), które odpowiadają na Britta **emailaddress** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="9fa6e-228">**toocreate użytkownika o nazwie Simona Britta SilkRoad życia pakietu, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fa6e-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="9fa6e-229">Pytaj użytkownika toocreate zespołu pomocy technicznej SilkRoad życia pakietu użytkownika, takiej jak **identyfikator logowania jednokrotnego** hello atrybutu samą wartość jak hello **emailaddress** z Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9fa6e-230">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fa6e-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="9fa6e-231">Celem Hello w tej sekcji jest tooenable toouse Simona Britta Azure logowania jednokrotnego, przyznając jej tooSilkRoad dostępu Suite życia.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9fa6e-233">**tooassign tooSilkRoad Simona Britta Suite życia wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9fa6e-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="9fa6e-234">Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9fa6e-236">Z listy aplikacji hello wybierz **Suite życia SilkRoad**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Przypisz użytkownika][202] 

3. <span data-ttu-id="9fa6e-238">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 

4. <span data-ttu-id="9fa6e-240">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="9fa6e-241">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="9fa6e-243">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9fa6e-243">Test single sign-on</span></span>
<span data-ttu-id="9fa6e-244">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="9fa6e-245">Po kliknięciu kafelka Suite życia SilkRoad hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SilkRoad życia pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9fa6e-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fa6e-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9fa6e-246">Additional Resources</span></span>
* [<span data-ttu-id="9fa6e-247">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fa6e-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9fa6e-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9fa6e-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





