toocreate pamięć podręczną, najpierw zaloguj toohello [portalu Azure](https://portal.azure.com)i kliknij przycisk **nowy** > **baz danych** > **pamięci podręcznej Redis**.

> [!NOTE]
> Jeśli nie masz konta Azure, możesz w ciągu kliku minut [utworzyć je bezpłatnie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).
> 
> 

![Nowa pamięć podręczna](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> Ponadto toocreating buforuje w hello portalu Azure, można również utworzyć je za pomocą Menedżera zasobów szablony, programu PowerShell lub wiersza polecenia platformy Azure.
> 
> * toocreate w pamięci podręcznej przy użyciu szablonów usługi Resource Manager, zobacz [tworzenia pamięci podręcznej Redis przy użyciu szablonu](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate pamięci podręcznej przy użyciu programu Azure PowerShell, zobacz [zarządzania pamięcią podręczną Redis Azure przy użyciu programu Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate pamięci podręcznej przy użyciu wiersza polecenia platformy Azure, zobacz [jak toocreate i zarządzania pamięcią podręczną Redis Azure za pomocą interfejsu wiersza polecenia platformy Azure (Azure CLI) hello](../articles/redis-cache/cache-manage-cli.md).
> 
> 

W hello **nowa pamięć podręczna Redis** bloku, określ odpowiednią konfigurację pamięci podręcznej hello hello.

![Tworzenie pamięci podręcznej](media/redis-cache-create/redis-cache-cache-create.png) 

* W **nazwy Dns**, wprowadź dla punktu końcowego pamięci podręcznej hello toouse nazwę unikatową pamięci podręcznej. Nazwa pamięci podręcznej Hello musi być ciągiem o długości od 1 do 63 znaków i może zawierać tylko cyfry, litery i hello `-` znaków. Witaj pamięci podręcznej nazw nie może zaczynać się ani kończyć hello `-` znaku i następujących po sobie `-` znaki są nieprawidłowe.
* Aby uzyskać **subskrypcji**, wybierz hello mają toouse dla pamięci podręcznej hello subskrypcji platformy Azure. Jeśli konto ma tylko jedną subskrypcję, zostanie automatycznie wybrana i hello **subskrypcji** nie zostaną wyświetlone listy rozwijanej.
* W polu **Grupa zasobów** wybierz lub utwórz grupę zasobów dla pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [grupy zasobów przy użyciu toomanage zasobów platformy Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Użyj **lokalizacji** toospecify hello lokalizacji geograficznej, w którym jest hostowana pamięć podręczna. Aby uzyskać najlepszą wydajność hello, firma Microsoft zaleca tworzenie pamięci podręcznej hello w hello tym samym regionie co aplikacja klienta pamięci podręcznej hello.
* Użyj **warstwa cenowa** tooselect hello żądany rozmiar pamięci podręcznej i funkcje.
* **Klaster redis** pozwala toocreate pamięci podręcznych większych niż 53 GB i tooshard danych między wieloma węzłami Redis. Aby uzyskać więcej informacji, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Trwałość redis** oferuje hello możliwości toopersist tooan z pamięci podręcznej konta magazynu Azure. Aby uzyskać instrukcje na temat konfigurowania trwałości, zobacz [jak tooconfigure trwałości dla podręczna Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Sieć wirtualna** zapewnia większe bezpieczeństwo i izolację przez ograniczenie dostępu tooyour pamięci podręcznej tooonly tych klientów w ramach hello określonej sieci wirtualnej platformy Azure. Można używać wszystkich funkcji hello sieci wirtualnej, takie jak podsieci, zasady kontroli dostępu i inne funkcje toofurther ograniczyć tooRedis dostępu. Aby uzyskać więcej informacji, zobacz [jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Domyślnie dostęp inny niż za pomocą protokołu SSL jest zablokowany dla nowych pamięci podręcznych. port bez protokołu SSL tooenable hello wyboru **odblokować port 6379 (szyfrowane SSL)**.

Po skonfigurowaniu hello nowe opcje pamięci podręcznej kliknij **Utwórz**. Może upłynąć kilka minut, aż utworzony toobe pamięci podręcznej hello. Stan hello toocheck, możesz monitorować postęp hello na tablicy startowej hello. Po utworzeniu hello pamięci podręcznej nowa pamięć podręczna ma **systemem** stanu i jest gotowy do użycia z [ustawienia domyślne](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Utworzono pamięć podręczną](media/redis-cache-create/redis-cache-cache-created.png)

