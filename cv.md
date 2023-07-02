# Резюме 
*********
### Имя: Валерий Рябов 
### Контакты для связи: <img src="https://valeriyryabov.github.io/rsschool-cv/content/Logo.png" width="23" height="23"/> batuuu1337

*********
## Обо мне: 
Привет! Меня зовут Валерий. Я разрабатываю приложения на C# dotnet более десяти лет. Успел поработать в нескольких крупных софтверных компаниях и довести до внедрения более 10 проектов! Последние 6 лет занимаюсь только backend-разработкой, хотя до этого был fullstack-разработчиком. Имею опыт разработки на Pure Javascript, AngularJS, ExtJS 4. Хочу актуализировать свои знания современными и популярными фреймворками, например, такими как ReactJS и Vue. Также говорю на английском языке уровня B2.

*********
## Навыки: 
	Языки программирования:
		● C# / .NET
		● JavaScript
	СУБД:
		● MS SQL
		● PostgreSQL
		● OracleDB
	Операционные системы:
		● Windows
		● UNIX
	IDE:
		● Visual Studio
		● Rider
	Системы контроля версий:
		● SVN
		● GIT
		● TFS
	Backend, CMS:
		● ASP.NET MVC
		● ASP.NET MVC Web Api
		● ASP.NET Core
		● WCF
		● ASMX Services
		● Entity Framework
		● ADO.NET
	Frontend:
		● ExtJS
		● AngularJS
		● jQuery
		● HTML
		● CSS
		● Bootstrap
		● Ajax
		● TypeScript
		● Kendo UI
	Прочее:
		● LINQ
		● Ninject/Unity
		● XML
		● XSLT
		● WinForms
		● IIS
		● Elasticsearch
		● Castle Windsor
		
*********
## Пример кода из моего бота Telegram для контроля динамики своего веса:
```cs
private async Task BotOnMessageReceived(Message message, CancellationToken cancellationToken)
{
	_logger.LogInformation("Receive message type: {MessageType}", message.Type);

	if (message.From == null || message.From.IsBot)
	{
		_logger.LogWarning($"Unknown user or bot: MessageId={message.MessageId}");
		return;
	}

	if (string.IsNullOrEmpty(message.Text))
	{
		return;
	}

	string messageText = message.Text;

	var actions = new Dictionary<string, Func<Message, CancellationToken, Task<Message>>>
	{
		{ _actionPatterns[ActionType.MyWeight], MyWeightAsync },
		{ _actionPatterns[ActionType.SetMyWeight], SetMyWeightAsync },
		{ _actionPatterns[ActionType.ClearMealCount], ClearDailyMealCountAsync },
		{ _actionPatterns[ActionType.SetMealCount], SetDailyMealCountAsync },
		{ _actionPatterns[ActionType.GetMealCount], GetDailyMealCountAsync },
		{ _actionPatterns[ActionType.Usage], UsageAsync }
	};

	var action = actions
		.Where(x => Regex.IsMatch(messageText, x.Key))
		.Select(x => x.Value)
		.FirstOrDefault();

	if (action == null)
	{
		return;
	}

	Message sentMessage = await action(message, cancellationToken);

	_logger.LogInformation("The message was sent with id: {SentMessageId}", sentMessage.MessageId);
}
```
