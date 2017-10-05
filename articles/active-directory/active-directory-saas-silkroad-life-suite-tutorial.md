---
title: "Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SilkRoad życia pakietu."
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
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="b7df4-103">Samouczek: Azure Active Directory integracji z pakietem życia SilkRoad</span><span class="sxs-lookup"><span data-stu-id="b7df4-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="b7df4-104">Celem tego samouczka jest pokazanie sposobu integracji SilkRoad Suite użytkowania z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7df4-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="b7df4-105">Integrowanie SilkRoad Suite użytkowania z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b7df4-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="b7df4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zestawu życia SilkRoad</span><span class="sxs-lookup"><span data-stu-id="b7df4-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="b7df4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SilkRoad życia pakiet rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7df4-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="b7df4-108">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7df4-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7df4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b7df4-109">Prerequisites</span></span>
<span data-ttu-id="b7df4-110">Aby skonfigurować integrację usługi Azure AD z pakietem życia SilkRoad, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b7df4-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="b7df4-111">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7df4-111">An Azure AD subscription</span></span>
* <span data-ttu-id="b7df4-112">Subskrypcja SilkRoad życia Suite logowanie Jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="b7df4-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="b7df4-113">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b7df4-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="b7df4-114">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b7df4-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b7df4-115">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b7df4-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b7df4-116">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7df4-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="b7df4-117">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b7df4-117">Scenario Description</span></span>
<span data-ttu-id="b7df4-118">Celem tego samouczka jest umożliwienie test rejestracji Jednokrotnej programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b7df4-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="b7df4-119">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b7df4-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7df4-120">Dodawanie pakietu życia SilkRoad z galerii</span><span class="sxs-lookup"><span data-stu-id="b7df4-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="b7df4-121">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7df4-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="b7df4-122">Dodawanie zestawu życia SilkRoad z galerii</span><span class="sxs-lookup"><span data-stu-id="b7df4-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="b7df4-123">Aby skonfigurować integrację usługi Azure AD SilkRoad życia pakietu, należy dodać pakiet życia SilkRoad z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b7df4-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7df4-124">**Aby dodać pakiet życia SilkRoad z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b7df4-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7df4-125">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="b7df4-127">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="b7df4-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b7df4-128">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="b7df4-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="b7df4-130">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="b7df4-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="b7df4-132">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="b7df4-134">W polu wyszukiwania wpisz **Suite życia SilkRoad**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="b7df4-136">W okienku wyników wybierz **Suite życia SilkRoad**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b7df4-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Aplikacje][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b7df4-138">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b7df4-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b7df4-139">Jest celem tej sekcji opisano, jak skonfigurować i przetestować Azure AD SSO z pakietem życia SilkRoad w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b7df4-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7df4-140">Dla logowania jednokrotnego do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi pakietu życia SilkRoad użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7df4-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="b7df4-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi pakietu życia SilkRoad musi określone.</span><span class="sxs-lookup"><span data-stu-id="b7df4-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="b7df4-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** SilkRoad życia pakietu.</span><span class="sxs-lookup"><span data-stu-id="b7df4-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="b7df4-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b7df4-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7df4-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b7df4-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7df4-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b7df4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7df4-146">**[Tworzenie użytkownika testowego zestawu życia SilkRoad](#creating-a-silkroad-life-suite-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SilkRoad życia pakiet, który jest połączony z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7df4-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b7df4-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b7df4-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7df4-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b7df4-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b7df4-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b7df4-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="b7df4-150">Celem tej sekcji jest do włączenia funkcji logowania jednokrotnego usługi Azure AD w klasycznym portalu Azure i konfigurowania rejestracji Jednokrotnej w SilkRoad życia pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7df4-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="b7df4-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z pakietem życia SilkRoad, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b7df4-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="b7df4-152">Logowanie do witryny firmy SilkRoad jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b7df4-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="b7df4-153">Aby uzyskać dostęp do aplikacji uwierzytelniania Suite życia SilkRoad Konfigurowanie Federacji przy użyciu usługi Microsoft Azure AD, skontaktuj się z SilkRoad pomocy technicznej lub Twoim przedstawicielem SilkRoad usług.</span><span class="sxs-lookup"><span data-stu-id="b7df4-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="b7df4-154">Przejdź do **usługodawcy**, a następnie kliknij przycisk **szczegóły federacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][10] 

3. <span data-ttu-id="b7df4-156">Kliknij przycisk **pobierania metadanych Federacji**, a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b7df4-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][11] 

4. <span data-ttu-id="b7df4-158">W klasycznym portalu Azure na **Suite życia SilkRoad** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b7df4-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 

5. <span data-ttu-id="b7df4-160">Na **jak chcesz użytkownikom zalogować się do zestawu życia SilkRoad** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][7] 

6. <span data-ttu-id="b7df4-162">Na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][8]   
 1. <span data-ttu-id="b7df4-164">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania do witryny SilkRoad życia pakietu (np.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="b7df4-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="b7df4-165">Otwórz pobrany **Silkroad** pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="b7df4-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="b7df4-166">Zlokalizuj **AssertionConsumerService** tag, a następnie skopiuj **lokalizacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="b7df4-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD rejestracji jednokrotnej][21] 
 4. <span data-ttu-id="b7df4-168">Wklej wartości do **adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b7df4-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="b7df4-169">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-169">Click **Next**.</span></span>

6. <span data-ttu-id="b7df4-170">Na **skonfigurować logowanie jednokrotne w SilkRoad życia Suite** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]  
 1. <span data-ttu-id="b7df4-172">Kliknij przycisk Pobierz certyfikat, a następnie zapisz plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="b7df4-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="b7df4-173">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-173">Click **Next**.</span></span>

7. <span data-ttu-id="b7df4-174">W Twojej **SilkRoad** aplikacji, kliknij przycisk **źródeł uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][12] 

8. <span data-ttu-id="b7df4-176">Kliknij przycisk **Dodawanie uwierzytelniania źródła**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][13] 

9. <span data-ttu-id="b7df4-178">W **Dodaj źródło uwierzytelniania** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][14]  
 1. <span data-ttu-id="b7df4-180">W obszarze **opcja 2 — plik metadanych**, kliknij przycisk **Przeglądaj** można przekazać pliku pobranego metadanych.</span><span class="sxs-lookup"><span data-stu-id="b7df4-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="b7df4-181">Kliknij przycisk **dostawcy tożsamości utworzyć przy użyciu danych pliku**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="b7df4-182">W **źródeł uwierzytelniania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][15] 

11. <span data-ttu-id="b7df4-184">Na **Edytuj źródło uwierzytelniania** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][16] 
 1. <span data-ttu-id="b7df4-186">Jako **włączone**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="b7df4-187">W **opis IdP** tekstowym, wpisz opis dla danej konfiguracji (np.: *logowania jednokrotnego programu Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="b7df4-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="b7df4-188">W **nazwa IdP** tekstowym, wpisz nazwę, która jest specyficzna dla konfiguracji (np.: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="b7df4-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="b7df4-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-189">Click **Save**.</span></span>

12. <span data-ttu-id="b7df4-190">Wyłącz wszystkie źródła uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b7df4-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD rejestracji jednokrotnej][17]

13. <span data-ttu-id="b7df4-192">W klasycznym portalu Azure na **pojedynczy znak na potwierdzenie** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD rejestracji jednokrotnej][18]

14. <span data-ttu-id="b7df4-194">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD rejestracji jednokrotnej][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b7df4-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7df4-196">Create an Azure AD test user</span></span>
<span data-ttu-id="b7df4-197">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b7df4-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="b7df4-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b7df4-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7df4-200">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="b7df4-202">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="b7df4-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b7df4-203">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7df4-205">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="b7df4-207">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="b7df4-209">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b7df4-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="b7df4-210">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="b7df4-211">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-211">Click **Next**.</span></span>

6. <span data-ttu-id="b7df4-212">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="b7df4-214">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="b7df4-215">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="b7df4-216">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="b7df4-217">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="b7df4-218">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-218">Click **Next**.</span></span>

7. <span data-ttu-id="b7df4-219">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="b7df4-221">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b7df4-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="b7df4-223">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="b7df4-224">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="b7df4-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="b7df4-225">Tworzenie użytkownika testowego SilkRoad życia pakietu</span><span class="sxs-lookup"><span data-stu-id="b7df4-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="b7df4-226">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta SilkRoad życia pakietu.</span><span class="sxs-lookup"><span data-stu-id="b7df4-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="b7df4-227">Britta firmy musi mieć identyfikator logowania jednokrotnego (czasami określane jako *AuthParam*), które odpowiadają na Britta **emailaddress** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7df4-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="b7df4-228">**Aby utworzyć użytkownika o nazwie Simona Britta SilkRoad życia pakietu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b7df4-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="b7df4-229">Skontaktuj się z zespołem pomocy technicznej SilkRoad życia pakietu można utworzyć użytkownika, takiej jak **identyfikator logowania jednokrotnego** atrybutu taką samą wartość jak **emailaddress** z Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7df4-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b7df4-230">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7df4-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="b7df4-231">Celem tej sekcji jest umożliwienie Simona Britta się za pomocą logowania jednokrotnego Azure przez udostępnienie jej SilkRoad życia pakietu.</span><span class="sxs-lookup"><span data-stu-id="b7df4-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b7df4-233">**Aby przypisać Simona Britta SilkRoad życia pakietu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b7df4-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="b7df4-234">W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="b7df4-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b7df4-236">Na liście aplikacji zaznacz **Suite życia SilkRoad**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Przypisz użytkownika][202] 

3. <span data-ttu-id="b7df4-238">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-238">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 

4. <span data-ttu-id="b7df4-240">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="b7df4-241">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="b7df4-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b7df4-243">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b7df4-243">Test single sign-on</span></span>
<span data-ttu-id="b7df4-244">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b7df4-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="b7df4-245">Po kliknięciu kafelka SilkRoad życia pakietu w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane SilkRoad życia pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7df4-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7df4-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b7df4-246">Additional Resources</span></span>
* [<span data-ttu-id="b7df4-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7df4-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7df4-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7df4-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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





