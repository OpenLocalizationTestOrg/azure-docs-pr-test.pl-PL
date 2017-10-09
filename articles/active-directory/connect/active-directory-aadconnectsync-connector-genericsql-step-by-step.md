---
title: "krok aaaGeneric krok przez łącznik usług SQL | Dokumentacja firmy Microsoft"
description: "W tym artykule jest przedstawienie za pomocą prostego systemu HR krok po kroku przy użyciu hello ogólny Łącznik usług SQL."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Instrukcja krok po kroku dotycząca ogólnego łącznika SQL
Ten temat jest przewodnik krok po kroku. Tworzy HR proste przykładową bazę danych i używać go do importowania niektórym użytkownikom i ich członkostwa w grupie.

## <a name="prepare-hello-sample-database"></a>Przygotowanie hello przykładowej bazy danych
Na serwerze z uruchomionym programem SQL Server, uruchom skrypt SQL hello w [dodatek a.](#appendix-a). Ten skrypt tworzy przykładowa baza danych o nazwie hello GSQLDEMO. Witaj model obiektów dla hello utworzone bazy danych prawdopodobnie tego obrazu:  
![Model obiektu](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Utwórz również użytkownika ma toouse tooconnect toohello w bazie danych. W tym przewodniku hello użytkownik o nazwie FABRIKAM\SQLUser i znajduje się w domenie hello.

## <a name="create-hello-odbc-connection-file"></a>Tworzenie pliku połączenia ODBC hello
Hello ogólny Łącznik usług SQL korzysta z serwera zdalnego toohello tooconnect ODBC. Najpierw musimy toocreate plik o hello informacje dotyczące połączenia ODBC.

1. Uruchom narzędzie do zarządzania ODBC hello na serwerze:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Witaj wybierz kartę **pliku DSN**. Kliknij przycisk **Dodaj...** .  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Witaj działa sterownik out-of-box drobne, więc zaznacz go i kliknij **Dalej >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Określ plik hello nazwę, takich jak **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Kliknij przycisk **Zakończ**.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Połączenia hello tooconfigure czasu. Nadaj hello źródła danych czytelny opis, a następnie podaj nazwę hello powitania serwera z uruchomionym programem SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Wybierz jak tooauthenticate z SQL. W takim przypadku stosujemy uwierzytelniania systemu Windows.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Podaj nazwę hello hello przykładowej bazy danych, **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Zachowaj domyślne wszystko na tym ekranie. Kliknij przycisk **Zakończ**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify wszystko działa zgodnie z oczekiwaniami, kliknij przycisk **Testuj źródło danych**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Upewnij się, że hello test zakończy się pomyślnie.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. plik konfiguracji ODBC Hello teraz powinny być widoczne w pliku DSN.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Mamy teraz plik hello możemy muszą i może rozpocząć tworzenie hello łącznika.

## <a name="create-hello-generic-sql-connector"></a>Utwórz hello ogólny Łącznik usług SQL
1. Hello interfejsu użytkownika Menedżera usługi synchronizacji, wybierz **łączniki** i **Utwórz**. Wybierz **ogólnego SQL (Microsoft)** i nadaj mu nazwę opisową.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Znajdź plik DSN hello, który został utworzony w poprzedniej sekcji hello i przekaż go toohello serwera. Podaj hello poświadczenia tooconnect toohello w bazie danych.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. W tym przewodniku, to aby ułatwić firmie Microsoft firma Microsoft i powiedzieć, że istnieją dwa typy obiektów, **użytkownika** i **grupy**.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. atrybuty hello toofind, chcemy hello toodetect łącznika te atrybuty analizując hello samej tabeli. Ponieważ **użytkowników** jest słowem zastrzeżonym SQL, potrzebujemy tooprovide w kwadratowe nawiasy kwadratowe [].  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Czas toodefine hello zakotwiczenia atrybut i atrybut DN hello. Aby uzyskać **użytkowników**, możemy użyć kombinacji hello hello dwa atrybuty username i identyfikator pracownika. Dla **grupy**, używamy, Nazwa_grupy (nie realistyczne w rzeczywistych, ale w ramach tego przewodnika działa).
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Nie wszystkie typy atrybutów, można wykryć w bazie danych SQL. w szczególności nie Hello odwołanie do atrybutu typu. Typ obiektu grupy hello potrzebujemy toochange hello OwnerID i MemberID tooreference.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. atrybuty Hello Wybraliśmy atrybuty odwołania w poprzednim kroku hello wymagać hello typ obiektu, który te wartości są odwołania do. W tym przypadku hello typ obiektu użytkownika.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Na stronie powitania parametry globalne zaznacz **znaku wodnego** jako hello strategii delta. Także wpisać w formacie daty/godziny hello **RRRR MM-dd gg**.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Na powitania **Konfiguruj partycje i hierarchie** wybierz oba typy obiektów.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Na powitania **wybierz typy obiektów** i **wybierz atrybuty**, zaznacz typy obiektów i wszystkich atrybutów. Na powitania **Konfiguruj zakotwiczenia** kliknij przycisk **Zakończ**.

## <a name="create-run-profiles"></a>Tworzenie profilów uruchamiania
1. Hello interfejsu użytkownika Menedżera usługi synchronizacji, wybierz **łączniki**, i **Konfigurowanie profilów uruchamiania**. Kliknij przycisk **nowy profil**. Możemy zaczynać **pełny Import**.  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Wybierz typ hello **pełny Import (tylko etap)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Wybierz partycję hello **obiektu = użytkownik**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Wybierz **tabeli** i typ **[użytkownicy]**. Przewiń w dół toohello wielowartościowe obiektu typu sekcji, a następnie wprowadź dane hello tak jak na poniższej ilustracji hello. Wybierz **Zakończ** toosave hello kroku.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Wybierz **nowy krok**. Teraz, wybierz opcję **obiektu = grupy**. Na ostatniej stronie powitania Użyj konfiguracji hello jak hello poniższej ilustracji. Kliknij przycisk **Zakończ**.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Opcjonalnie: Jeśli chcesz, można skonfigurować dodatkowe profile uruchamiania. W ramach tego przewodnika hello pełny Import jest używany.
7. Kliknij przycisk **OK** toofinish zmienianie profilów uruchamiania.

## <a name="add-some-test-data-and-test-hello-import"></a>Dodać niektóre importu hello testu, jak dane i testu
Wprowadź dane testowe w przykładowej bazie danych. Gdy wszystko będzie gotowe, wybierz **Uruchom** i **pełny import**.

Oto użytkownika z dwóch numery telefonów i grupy z niektóre elementy członkowskie.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Dodatek A
**Skrypt toocreate hello przykładowa baza danych SQL**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
