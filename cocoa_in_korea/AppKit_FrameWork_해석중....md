framework
[주소](https://developer.apple.com/reference/appkit)
#APPKit

  - 당신의 macOS 어플리케이션의 **user interface** 를 설계하고 관리하세요. 
  - 사용자 **상호 작용 및 시스템 이벤트에 대해 대응**하고, **접근성을 활성화** 하며, **문서**, **텍스트**, **이미지 처리**를 합니다.

##Overview

AppKit은 시각적이고, 이벤트 중심의 UI 에 대한 모든 객체를 포함하는 프레임워크입니다. (windows, panels, buttons, menus, scrollers, and text fields 같은것들 말이죠.)
AppKit은 효율적으로 화면을 렌더링하고, 하드웨어 장치와 스크린 버퍼 사이에서  의사소통하고, 화면을 그리기전에 그 영역을 치우고, 뷰를 클립하기 와 같은 모든 세부 사항을 처리합니다.
처음 사용하는 사람들은 AppKit 클래스 수가 많아 상당히 벅찰 수도 있습니다. 하지만 대부분의 AppKit 클래스는 우리가 사용하지 않고 간접적으로 사용하는 지원 클래스 입니다. 당신이 AppKit을 사용하는 수준에 따라 어떻게 사용할지 선택할 수 있습니다 :


 - **Interface Builder를 사용하여 사용자 인터페이스 객체에서 응용 프로그램 개체에 대한 연결을 만듭니다:**
이 경우에는 **응용 프로그램 클래스** 와 **델리케이트 메소드**만 구현 하면 됩니다.
예를 들어, 사용자가 메뉴항목을 쓰게 하려면 메뉴 항목을 선택할 때 호출되는 메소드를 구현 하기만 하면 됩니다.


 - **사용자 인터페이스를 프로그램 적으로 제어하고 싶다면**, **AppKit 클래스**와 **프로토콜**에 익숙해야합니다. 예를 들자면 창에서 다른 창에 아이콘을 드래그 할 수 있도록 하려면 프로그래밍과 NSDragging과 같은 프로토콜을 사용해야하고 이를 사용하는데 익숙해야 합니다.


 - **NSView 또는 다른 클래스를 상속하여 자신의 객체를 구현합니다:** NSView을 서브 클래싱할때 에는 그래픽 함수를 사용하여 자신의 드로잉 메서드를 만듭니다. 서브 클래스를 작성하려면 **AppKit의 구조를보다 깊이 이해할 필요**가 있습니다.

AppKit을 더 배우고 싶으면, NSApplication, NSWindow 및 NSView 클래스들의 설명을 검토하고, 델리게이트 메소드에 좀더 주위를 기울이시면 됩니다. 더 깊고 자세한  AppKit에 대한 이해를 원한다면, NSResponder와 RunLoop (NSRunLoop은 Foundation 프레임워크에 있습니다)의 설명을 참조하세요.


##AppKit Classes and Protocols
**AppKit 은 큽니다!** AppKit은 125개 이상의 클래스와 프로토콜로 구성됩니다.이 클래스 모두 Foundation 프레임 워크의 NSObject 클래스에서 파생 되었습니다. 다음 섹션에서는 AppKit클래스와 프로토콜을 통해 다루는 주제 중 일부에 대해 간단하게 설명하겠습니다.


##Encapsulating an Application
모든 어플리케이션은 메인이벤트 루프를 조종하기위해, 어플리케이션의 창과 메뉴들을 추적하기위해, 이벤트에 적합한 객체들(즉, 자신이나 창들중 하나)을 분배하기 위해, 그리고 응용프로그램 수준(application-level)이벤트를 notification을 받기 위해 NSApplication의 단일 인스턴스를 사용합니다. NSApplication 객체는 응용 프로그램의 시작 또는 종료 될 때, 숨기거나 활성화되어 있을때, 사용자가 선택한 파일을 열어야할때 등등의 상황에 통지되는 델리케이트(할당 된객체)가 있습니다. NSApplication 객체의 델리케이트를 설정하고 델리케이트 메서드를 구현하여 NSApplication을 상속하지 않고 응용 프로그램의 동작을 사용자가 정의를 할 수 있습니다.

##General Event Handling and Drawing
NSResponder클래스는 사용자 이벤트에 응답하는 객체의 정렬된 목록인 리스폰더 체인(responder chain) 정의합니다. 사용자가 마우스나 키보드를 누를때, 이벤트가 생성되고 이벤트에 응답할 수 있는 객체가 있는 리스폰더 체인에 전달됩니다. 이벤트를 다루는 객체들은 무조건 NSResponder클래스를 상속받아야 합니다. 핵심적인 AppKit클래스들인 NSApplication, NSWindow, NSView 또한 NSResponder클래스를 상속 받았습니다.

NSApplication 객체들은 응용 프로그램에 속한 각 창당 하나 있는 NSWindow 객체들의 목록을 유지하고, 각각의 NSWindow 객체는 NSView 객체의 계층 구조를 유지합니다.(의역) view의 계층구조는 윈도우가 그려지거나 이벤트를 처리할때 사용됩니다. An NSWindow object handles window-level events, distributes other events to its views, and provides a drawing area for its views. An NSWindow object also has a delegate allowing you to customize its behavior.

NSView is an abstract class for all objects displayed in a window. All subclasses implement a drawing method using graphics functions; draw(_:) is the primary method you override when creating a new NSView subclass.


##Panels
The NSPanel class is a subclass of NSWindow that you use to display transient, global, or pressing information. For example, you would use an instance of NSPanel, rather than an instance of NSWindow, to display error messages or to query the user for a response to remarkable or unusual circumstances. AppKit implements some common panels for you such as the Save, Open and Print panels, used to save, open, and print documents. Using these panels gives the user a consistent “look and feel” across applications for common operations.

##Menus and Cursors
The NSMenu, NSMenuItem, and NSCursor classes define the look and behavior of the menus and cursors that your application displays to the user.


##Grouping and Scrolling Views
The NSBox, NSScrollView, and NSSplitView classes provide graphic “accessories” to other view objects or collections of views in windows. With the NSBox class, you can group elements in windows and draw a border around the entire group. The NSSplitView class lets you “stack” views vertically or horizontally, apportioning to each view some amount of a common territory; a sliding control bar lets the user redistribute the territory among views. The NSScrollView class and its helper class, NSClipView, provide a scrolling mechanism as well as the graphic objects that let the user initiate and control a scroll. The NSRulerView class allows you to add a ruler and markers to a scroll view.

##Controlling an Application
The NSControl and NSCell classes, and their subclasses, define a common set of user interface objects such as buttons, sliders, and browsers that the user can manipulate graphically to control some aspect of your application. Just what a particular control affects is up to you: When a control is “touched,” it sends an action message to a target object. You typically use Interface Builder to set these targets and actions by Control-dragging from the control object to your application or other object. You can also set targets and actions programmatically.

An NSControl object is associated with one or more NSCell objects that implement the details of drawing and handling events. For example, a button comprises both an NSButton object and an NSButtonCell object. The reason for this separation of functionality is primarily to allow NSCell classes to be reused by NSControl classes. For example, NSMatrix and NSTableView can contain multiple NSCell objects of different types.


##Tables
The NSTableView class displays data in row and column form. NSTableView is ideal for, but not limited to, displaying database records, where rows correspond to each record and columns contain record attributes. The user can edit individual cells and rearrange the columns. You control the behavior and content of an NSTableView object by setting its delegate and data source objects.


##Text and Fonts
The NSTextField class implements a simple editable text field, and the NSTextView class provides more comprehensive editing features for larger text bodies.

NSTextView, a subclass of the abstract NSText class, defines the interface to Cocoa’s extended text system. NSTextView supports rich text, attachments (graphics, file, and other), input management and key binding, and marked text attributes. NSTextView works with the font panel and menu, rulers and paragraph styles, the Services facility (for example, the spell-checking service), and the pasteboard. NSTextView also allows customizing through delegation and notifications—you rarely need to subclass NSTextView. You rarely create instances of NSTextView programmatically either, since objects on Interface Builder’s palettes, such as NSTextField, NSForm, and NSScrollView, already contain NSTextView objects.

It is also possible to do more powerful and more creative text manipulation (such as displaying text in a circle) using NSTextStorage, NSLayoutManager, NSTextContainer, and related classes.

The NSFont and NSFontManager classes encapsulate and manage font families, sizes, and variations. The NSFont class defines a single object for each distinct font; for efficiency, these objects, which can be rather large, are shared by all the objects in your application. The NSFontPanel class defines the font specification panel that’s presented to the user.


##Graphics and Color
The classes NSImage and NSImageRep encapsulate graphics data, allowing you to easily and efficiently access images stored in files on the disk and displayed on the screen. NSImageRep subclasses each know how to draw an image from a particular kind of source data. The presentation of an image is greatly influenced by the hardware that it’s displayed on. For example, a particular image may look good on a color monitor, but may be too “rich” for monochrome. Through the image classes, you can group representations of the same image, where each representation fits a specific type of display device—the decision of which representation to use can be left to the NSImage class itself.

Color is supported by the classes NSColor, NSColorPanel, NSColorList, NSColorPicker, and NSColorWell. NSColor supports a rich set of color formats and representations, including custom ones. The other classes are mostly interface classes: They define and present panels and views that allow the user to select and apply colors. For example, the user can drag colors from the color panel to any color well. The NSColorPicking protocol lets you extend the standard color panel.


##Dragging
With very little programming on your part, custom view objects can be dragged and dropped anywhere. Objects become part of this dragging mechanism by conforming to NSDragging... protocols: draggable objects conform to the NSDraggingSource protocol, and destination objects (receivers of a drop) conform to the NSDraggingDestination protocol. AppKit hides all the details of tracking the cursor and displaying the dragged image.


##Printing
The NSPrinter, NSPrintPanel, NSPageLayout, and NSPrintInfo classes work together to provide the means for printing the information that your application displays in its windows and views. You can also create an EPS representation of an NSView.


##Accessing the File System
Use the NSFileWrapper class to create objects that correspond to files or directories on disk. NSFileWrapper will hold the contents of the file in memory so that it can be displayed, changed, or transmitted to another application. It also provides an icon for dragging the file or representing it as an attachment. Or use the NSFileManager class in the Foundation framework to access and enumerate file and directory contents. The NSOpenPanel and NSSavePanel classes also provide a convenient and familiar user interface to the file system.


##Sharing Data With Other Applications
The NSPasteboard class defines the pasteboard, a repository for data that’s copied from your application, making this data available to any application that cares to use it. NSPasteboard implements the familiar cut-copy-paste operation. The NSServicesRequest protocol uses the pasteboard to communicate data that’s passed between applications by a registered service.


##Checking Spelling
The NSSpellServer class lets you define a spell-checking service and provide it as a service to other applications. To connect your application to a spell-checking service, you use the NSSpellChecker class. The NSIgnoreMisspelledWords and NSChangeSpelling protocols support the spell-checking mechanism.


##Localization
If an application is to be used in more than one part of the world, its resources may need to be customized, or “localized,” for language, country, or cultural region. For example, an application may need to have separate Japanese, English, French, and German versions of character strings, icons, nib files, or context help. Resource files specific to a particular language are grouped together in a subdirectory of the bundle directory (the directories with the “.lproj” extension). Usually you set up localization resource files using Interface Builder. See the specifications for NSBundle AppKit Additions Reference and Bundle class for more information on localization (NSBundle is in the Foundation framework).