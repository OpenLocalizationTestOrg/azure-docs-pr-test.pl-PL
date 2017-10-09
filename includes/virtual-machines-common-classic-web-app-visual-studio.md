

Po utworzeniu projektu aplikacji sieci web dla platformy Azure można udostępnić maszynę wirtualną na platformie Azure. Można następnie skonfigurować maszyny wirtualnej hello dodatkowego oprogramowania lub użyć hello maszyny wirtualnej do celów diagnostycznych lub debugowania.

toocreate maszynę wirtualną podczas tworzenia aplikacji sieci web, wykonaj następujące kroki:

1. W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu** > **Web**, a następnie wybierz pozycję **Aplikacji sieci Web ASP.NET** (w obszarze hello **Visual C#** lub **Visual Basic** węzłach).
2. W hello **nowy projekt ASP.NET** okno dialogowe, wybierz opcję hello typu aplikacji sieci web, a w hello Azure sekcji okna dialogowego hello (w hello prawym dolnym rogu), upewnij się, że hello **Host w chmurze hello**jest zaznaczone pole wyboru (to pole wyboru jest oznaczony **Utwórz zasoby zdalne** w niektórych instalacji).
   
    ![][0]
3. Na przykład na liście rozwijanej hello w Microsoft Azure, wybierz **maszyny wirtualnej (wersja 1)**, a następnie kliknij przycisk hello **OK** przycisku.
4. Zaloguj się w tooAzure, jeśli zostanie wyświetlony monit. Witaj **Utwórz maszynę wirtualną** zostanie wyświetlone okno dialogowe.
   
    ![][2]
5. W hello **nazwy DNS** wprowadź nazwę hello maszyny wirtualnej. Nazwa DNS Hello musi być unikatowa na platformie Azure. Jeśli wprowadzona nazwa hello jest niedostępna, zostanie wyświetlony czerwony wykrzyknik.
6. W hello **obrazu** wybierz hello obraz maszyny wirtualnej hello toobase na. Można wybrać hello obrazy standardowe maszyny wirtualnej platformy Azure lub przekazywanego tooAzure obrazu.
7. Pozostaw hello **Włącz usługi IIS i Web Deploy** pole wyboru jest zaznaczone, jeśli nie planujesz tooinstall różnych serwerów sieci web. Wyłączenie narzędzia Web Deploy, nie będzie możliwe toopublish z programu Visual Studio. Możesz dodać usług IIS i Web Deploy tooany obrazów systemu Windows Server hello spakowane, w tym obrazów niestandardowych.
8. W hello **rozmiar** wybierz rozmiar hello hello maszyny wirtualnej.
9. Określ hello poświadczenia logowania dla tej maszyny wirtualnej. Zanotuj je, ponieważ konieczne będzie ich tooaccess hello komputera przy użyciu pulpitu zdalnego.
10. W hello **lokalizacji** wybierz maszynę wirtualną hello hello region toohost.
11. Kliknij przycisk hello **OK** toostart przycisk tworzenia hello maszyny wirtualnej. Możesz wykonać hello postęp operacji hello w hello **dane wyjściowe** okna.
    
    ![][3]
12. Po zainicjowaniu obsługi maszyny wirtualnej hello, opublikowanych skrypty są tworzone w **PublishScripts** węzła w rozwiązaniu. Witaj opublikowana skrypt będzie uruchamiany i przepisy maszynę wirtualną na platformie Azure. Witaj **dane wyjściowe** okno wyświetla stan hello. skrypt Hello wykonuje następujące akcje tooset maszyny wirtualnej hello hello:
    
    * Tworzy hello maszyny wirtualnej, jeśli jeszcze nie istnieje.
    * Tworzy konto magazynu, którego nazwa zaczyna się od `devtest`, ale tylko wtedy, gdy nie ma już konto magazynu w wybranym regionie hello.
    * Tworzy usługi w chmurze jako kontener dla maszyny wirtualnej hello i tworzy rolę sieci web dla aplikacji sieci web hello.
    * Konfiguruje narzędzie Web Deploy na powitania maszyny wirtualnej.
    * Umożliwia skonfigurowanie usług IIS i platformy ASP.NET na powitania maszyny wirtualnej.
    
    ![][4]
13. (Opcjonalnie) Możesz połączyć toohello nowej maszyny wirtualnej. W **Eksploratora serwera**, rozwiń węzeł hello **maszyn wirtualnych** węzła, wybieranie węzła hello hello maszyny wirtualnej został utworzony, a jego menu skrótów, **Połącz przy użyciu pulpitu zdalnego**. Alternatywnie w **Eksplorator chmury** można **Otwórz w portalu** hello menu skrótów i połączyć toohello maszyny wirtualnej.
    
    ![][5]

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz toocustomize hello opublikowanych skrypty, które zostały utworzone, przeczytaj więcej szczegółowych informacji na [tooDev tooPublish przy użyciu skrypty programu Windows PowerShell i środowisk testowych](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
