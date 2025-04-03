
___
### Пакет: 
```C#
Microsoft.Extensions.DependencyInjection
```
### Базовая настройка
```C#
var services = new ServiceCollection();

// Регистрируем модели (обычно как Singleton, если хранят состояние)
services.AddSingleton<HomeModel>();
services.AddSingleton<SettingsModel>();

// Регистрируем контроллеры (как Transient, если они лёгкие)
services.AddTransient<HomeController>();
services.AddTransient<SettingsController>();

// Регистрируем формы (как Transient, чтобы каждый раз создавалась новая)
services.AddTransient<HomeForm>(); var services = new ServiceCollection();

// Регистрируем модели (обычно как Singleton, если хранят состояние)
services.AddSingleton<HomeModel>();
services.AddSingleton<SettingsModel>();

// Регистрируем контроллеры (как Transient, если они лёгкие)
services.AddTransient<HomeController>();
services.AddTransient<SettingsController>();

// Регистрируем формы (как Transient, чтобы каждый раз создавалась новая)
services.AddTransient<HomeForm>();
services.AddTransient<SettingsForm>();

// Регистрируем FormManager (как Singleton, он один на всё приложение)
services.AddSingleton<FormManager>();

// Строим провайдер
var provider = services.BuildServiceProvider();

// Запускаем приложение
var formManager = provider.GetRequiredService<FormManager>();
formManager.OpenForm<HomeForm>(); // Стартовая форма
Application.Run(provider.GetRequiredService<MainForm>());
```
### Автоматическое добавление:
```C#
// Program.cs
var assembly = Assembly.GetExecutingAssembly();

// Регистрируем модели (Singleton)
assembly.GetTypes()
    .Where(t => t.Name.EndsWith("Model") && !t.IsAbstract)
    .ToList()
    .ForEach(type => services.AddSingleton(type));

// Регистрируем контроллеры (Transient)
assembly.GetTypes()
    .Where(t => t.Name.EndsWith("Controller") && !t.IsAbstract)
    .ToList()
    .ForEach(type => services.AddTransient(type));

// Регистрируем формы (Transient)
assembly.GetTypes()
    .Where(t => t.IsSubclassOf(typeof(Form)) && !t.IsAbstract)
    .ToList()
    .ForEach(type => services.AddTransient(type));
```
### Менеджер форм:
```C#
public class FormManager
{
    private readonly IServiceProvider _serviceProvider;
    private Form _currentForm;

    public FormManager(IServiceProvider serviceProvider)
    {
        _serviceProvider = serviceProvider;
    }

    public void OpenForm<TForm>() where TForm : Form
    {
        _currentForm?.Close();
        _currentForm = _serviceProvider.GetRequiredService<TForm>();
        _currentForm.Show();
    }
}
```
### Пример:
```c#
Application.EnableVisualStyles();
Application.SetCompatibleTextRenderingDefault(false);

var services = new ServiceCollection();
var assembly = Assembly.GetExecutingAssembly();

assembly.GetTypes()
	.Where(t => t.Name.EndsWith("Model") && !t.IsAbstract)
	.ToList()
	.ForEach(type => services.AddSingleton(type));

assembly.GetTypes()
	.Where(t => t.Name.EndsWith("Controller") && !t.IsAbstract)
	.ToList()
	.ForEach(type => services.AddTransient(type));

assembly.GetTypes()
	.Where(t => t.IsSubclassOf(typeof(Form)) && !t.IsAbstract)
	.ToList()
	.ForEach(type => services.AddTransient(type));

services.AddSingleton<FormManager>();

var provider = services.BuildServiceProvider();

Application.Run(provider.GetRequiredService<HomeForm>());
```
### Пример открытия формы:
```C#
public class HomeController
{
    private readonly FormManager _formManager;

    // Внедряем FormManager через конструктор
    public HomeController(FormManager formManager)
    {
        _formManager = formManager;
    }

    public void DrugPanel(Panel panel, Form form)
    {
        AddDragControl.EnableDrag(panel, form);
    }

    public void OpenSignInForm(Panel childrenPanel)
    {
        // Теперь используем поле _formManager
        _formManager?.OpenChildrenForm<SignIn>(childrenPanel);
    }
} 
```