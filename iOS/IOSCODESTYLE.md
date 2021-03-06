# QuickBlox iOS code style convention


##1. Основные принципы
###1.1 Организация кода

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}

```
###1.2 Четкость и ясность

Четкость и краткость, но ясность не должна страдать из-за краткости

**Хрошо:**

```objc
- (void)insertObject:(id)object atIndex:(NSInteger)index;
```

**Плохо:**

```objc
- (void)insert:(id)o at:(NSInteger)i;
```
Не использовать аббревиатуры какими бы не были длинными слова (есть некоторые сокращения, которыми можно пользоваться их список

**Хрошо:**

```objc
- (id)destinationSelection;
```

**Плохо:**

```objc
- (id)destSel;
```

###1.3 Согласованность
Методы, которые делают то же самое в разных классах должны иметь одинаковые названия.


```objc
- (NSInteger)tag; //реализованно в NSView, NSCell, NSControll.
```
###1.4 Без само-ссылок

**Хрошо:**

```objc
@property (nonatomic, copy) NSString *name;
@property (nonatomic, strong) NSArray *types;
```

**Плохо:**

```objc
@property (nonatomic, copy) NSString *nameString;
@property (nonatomic, strong) NSString *typeArray;
```
Если множество не **NSArray** или **NSSet**, то тогда указания типа имеет смысл:

```objc
@property (nonatomic, strong) NSDictionary *keyedAccountNames;
@property (nonatomic, strong) NSDictionary *messageDictionary;
@property (nonatomic, strong) NSIndexSet *selectedMailboxesIndexSet;
```
Исключением являются **UI** элементы:
 
```objc
@property (nonatomic, strong) UIButton *sendMessageButton;
@property (nonatomic, strong) UILabel *usernameLabel;
@property (nonatomic, strong) UIImageView *avatarImageView;
```
##2. Типографские обозначения
###2.1 Спец. символов
В именах не должно быть запятых, нижних подчеркиваний, каждое новое слово с большой буквы 

**Примeр:**.

```objc
@property (nonatomic, strong) UIButton *sendMessageButton;
- (void)runTheWordsTogether;
```
##3. Именование классов, файлов

**Хорошо:**

***QBChatMessage.h***

```objc
@interface QBChatMessage : NSObject
...
@end

```

**Плохо:**

***ChatMessage.h***

```objc
@interface ChatMessage : NSObject
...
@end

```

##4. Именование методов и @property
Имя метода начинается с маленькой буквы, каждое следующее слово с большой. Между -/+ и типом возвращаемого значения должен быть пробел.

**Пример:**

```objc
/**
 *	Message text
 */
@property (nonatomic, copy) NSString *text;

/**
 *	Message sender nick, use only for group Chat
 */
@property (nonatomic, copy) NSString *senderNick;

/**
 *  Unavailable for this class
 */
- (instancetype)init NS_UNAVAILABLE;

/**
 *  Unavailable for this class
 */
- (instancetype)new NS_UNAVAILABLE;

/**
 *  Designated initializer
 *
 *  @param sencerNick Sender nick
 *  @param text       Message text
 *
 *  @return QBChatMessage instance
 */
- (instancetype)initWithSenderNick:(NSString *)sencerNick text:(NSString *)text NS_DESIGNATED_INITIALIZER;

```

Методы, которые обозначают какое-либо действие, начинаются с глагола(кроме do, does)

**Хорошо:**

```objc
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
```
**Плохо:**

```objc
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
```
Ставьте слово описывающее аргумент перед аргументом

**Хорошо:**

```objc
- (id)viewWithTag:(NSInteger)aTag;
```
**Плохо:**

```objc
- (id)taggedView:(int)aTag;
```
Добавляйте новые ключевые слова в конце, при перегрузке метода в наследнике

**NSView, UIView:**

```objc
- (id)initWithFrame:(CGRect)frameRect;
```

**NSMatrix субкласс от NSView:**

```objc
- (id)initWithFrame:(NSRect)frameRect mode:(int)aMode cellClass:(Class)factoryId numberOfRows:(int)rowsHigh numberOfColumns:(int)colsWide;
```
Не используйте “and” для связи между аргументами

**Хорошо:**

```objc
- (NSInteger)runModalForDirectory:(NSString *)path file:(NSString *)name;
```
**Плохо:**

```objc
- (NSInteger)runModalForDirectory:(NSString *)path andFile:(NSString *)name;
```
Если метод реализует несколько действий, то используйте для связи “and”

**Пример:**

```objc
- (BOOL)openFile:(NSString *)fullPath withApplication:(NSString *)appName andDeactivate:(BOOL)flag;
```

###4.2 Методы доступа

Если свойство - существительное, то формат такой:

```objc
- (type)noun;
- (void)setNoun:(type)aNoun;
```
Если свойство - прилагательное, то формат такой:

```objc
- (BOOL)isAllowed;
- (void)setAllowed:(BOOL)flag;
```

###4.3 Методы делегата

Первое слово в названии метода должно быть название класса отправителя:

```objc
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath;
```
Используйте "did" или "will" для методов, которые вызываются уведомить делегатов, что что-то произошло или вот-вот произойдет.

```objc
- (void)scrollViewDidScroll:(UIScrollView *)scrollView;
```
Хотя вы можете использовать "did" или "will" для методов, которые вызываются чтобы обратиться к делегату что-то сделать от имени другого объекта, "should", является предпочтительным.


```objc
- (BOOL)windowShouldClose:(id)sender;
```

###4.4 Методы коллекций

Для объектов, которые управляют коллекциями, методы должны соответствовать форме:

```objc
- (void)addElement:(elementType)anObj;
- (void)removeElement:(elementType)anObj;
- (NSArray *)elements;
- (void)insertElement:(elementType)anObj atIndex:(NSInteger)index;
- (void)removeElementAtIndex:(NSInteger)index;
```

###4.5 Аргументы методов

Имя аргумента начинается с маленькой буквы, каждое следующее слово с большой. Не использовать “pointer” или “ptr”. Избегайте одно- или двух-буквенных названий. Избегайте аббревиатуры. В методах доступа и конструкторах добавлять a/an перед именем аргумента.

**Пример:**

```objc
- (id)objectAtIndex:(NSUInteger)index;
- (void)setFont:(NSFont *)aFont;
- (instance)initWithFrame:(NSRect)aRect;
```
###4.6 Вызов методов

Использование ***point style*** допускается только для property.

**Хорошо:**

```objc
//name - @property
self.object.name = @"Andrey";
```
**Плохо:**

```objc
//count - метод класса
if (self.objects.count) {
	...
}
```

При вызове методов не допускается более 2 пар квадратных скобок в строке:

**Хорошо:**

```objc
NSInteger count = [self.objects count];
```
**Плохо:**

```objc
NSString *collectionID = [((Collection *)[[[self gamesource] gameParts] lastObject]) collectionID];
```

Пример объявления метода

```objc
- (void)addTarget:(id)target action:(SEL)action forControlEvents:(UIControlEvents)controlEvents
```

##5. Именование функций

###5.1 Основные правила
Именование функций использует те же правила, что и именование методов за исключением:

- Название функций начинается с префикса
- Первое слово после префикса начинается с большой буквы

Большинство названий функций начинается с глагола:

```objc
void NSHighlightRect(NSRect rect);
void NSDeallocateObject(id object);
```
Если функция возвращает свой ​​первый аргумент, то надо опустить глагол 

```objc
unsigned int NSEventMaskFromType(NSEventType type)
```

Если возвращаемое значение - ссылка, то надо использовать `Get`

```objc
const char *NSGetSizeAndAlignment(const char *typePtr, unsigned int *sizep, unsigned int *alignp)
```

Если значение возвращается `BOOL`, функция должна начинаться с флективных глаголов (*Флекти́вный - устройство языка синтетического типа, при котором доминирует словоизменение при помощи флексий — формантов, сочетающих сразу несколько значений.*):

```objc
BOOL NSDecimalIsNotANumber(const NSDecimal *decimal)
```

##6. Именование уведомлений (notifications)

Именование уведомлений происходит по шаблону:

`[Name of associated class]` + `[Did | Will]` + `[UniquePartOfName]` + `Notification`

**Пример:**

```objc
// Key in userInfo. Value is a dictionary of NSExtensionItems and associated NSError instances.
FOUNDATION_EXTERN NSString * const NSExtensionItemsAndErrorsKey;

// The host process will enter the foreground
FOUNDATION_EXTERN NSString *const NSExtensionHostWillEnterForegroundNotification;

// The host process did enter the background
FOUNDATION_EXTERN NSString *const NSExtensionHostDidEnterBackgroundNotification;

// The host process will resign active status (stop receiving events), the extension may be suspended
FOUNDATION_EXTERN NSString *const NSExtensionHostWillResignActiveNotification;

// The host process did become active (begin receiving events)
FOUNDATION_EXTERN NSString *const NSExtensionHostDidBecomeActiveNotification;
```

##7. Синтаксис написания конструкций if, for, switch

После оператора идет пробел, далее следует условие, далее пробел и открывающаяся фигурная скобка

**Пример:**

```objc
if ([user.login isEqualToString:login]) {

	return user;         
} 
else {

	NSLog(@”User login not equal to login”);
}
```

`if` в одну строку тоже оборачивается в `{ }`

**Плохо:**

```objc
if ([user.login isEqualToString:login]) 
	return user;  
```

##8. Именование ресурсов
Ресурсами в проекте считаются файлы изображений, звуковые и видео файлы, текстовые файлы. Имена ресурсов должны выглядеть таким образом:

`project`-`resource`-`namespace`-`asset-name`-`state`.png

Q-municate project: 

`qm`-`ic`-`login`-`top-user`.png<br>
`qm`-`bg`-`chat`-`attachement-left`-`normal`.png<br>
`qm`-`bg`-`chat`-`attachement-left`-`pressed`.png<br>

##9. Работа с Storyboards/Xibs

Xib контроллера должен называться аналогично имени его UIViewController
Внутренние View необходимо именовать соответственно назначению
##10. 3rd party библиотеки
Используем `CocoaPods` для всех сторонних библиотек

##11. Константы
Все константные значения необходимо выносить в consts:

```objc
NSString *const kQMAuthorizationKey = @"WzrAY7vrGmbgFfP";
NSString *const kQMAuthorizationSecret = @"xS2uerEveGHmEun";
NSString *const kQMAccountKey = @"6Qyiz3pZfNsex1Enqnp7";
```
##12. Рекомендации

###12.1 Использование литералов.
Для сокращения времени написания используйте литералы:

**Хорошо:**

```objc
NSString *title = @"New Title";
NSNumber *fontSize = @42;
NSArray *chars = @[@"a", @"b"];
NSDictionary *dictionary = @{@"one" : @"1", @"two" : @"2", @"three" : @"3"};


```
**Плохо:**

```objc
NSString *title = [NSString stringWithString:@"New Title"];
NSNumber *fontSize = [NSNumber numberWithInt:42];
NSArray *chars = [NSArray arrayWIthObjects:@"a", @"b",nil]
NSDictionary *dictionary = [NSDictionary dictionaryWithObjects:@"1", @"2", @"3", nil forKeys:@"one", @"two", @"three", nil]];
```

## 13. Deprecation rules

Аттрибут:

```
DEPRECATED_MSG_ATTRIBUTE("Deprecated in projectVersion. Use 'newMethodName' instead.");

```

Warning в инлайн доку вставляется между `@param` и `@return`: 

**Пример:**

``` objc
/**
 *  Get image by attachment
 *
 *  @param attachment      QBChatAttachment instance
 *  @param completion      Fetch image result
 *
 *  @warning *Deprecated in QMServices 0.3.2:* Use 'getImageForAttachmentMessage:completion:' instead.
 */
- (void)getImageForChatAttachment:(QBChatAttachment *)attachment completion:(void (^)(NSError *error, UIImage *image))completion DEPRECATED_MSG_ATTRIBUTE("Deprecated in 0.3.2. Use 'getImageForAttachmentMessage:completion:' instead.");
```


