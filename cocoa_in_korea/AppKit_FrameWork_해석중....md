framework
#APPKit

  - 당신의 macOS 어플리케이션의 **user interface** 를 설계하고 관리하세요. 
  - 사용자 **상호 작용 및 시스템 이벤트에 대해 대응**하고, **접근성을 활성화** 하며, **문서**, **텍스트**, **이미지 처리**를 합니다.
 
#Overview

AppKit은 시각적이고, 이벤트 중심의 UI 에 대한 모든 객체를 포함하는 프레임 워크입니다. (windows, panels, buttons, menus, scrollers, and text fields 같은것들 말이죠.)
AppKit은 효율적으로 화면을 렌더링하고, 하드웨어 장치와 스크린 버퍼 사이에서  의사소통하고, 화면을 그리기전에 그 영역을 치우고, 뷰를 클립하기 와 같은 모든 세부 사항을 처리합니다.
처음 사용하는 사람들은 AppKit 클래스 수가 많아 상당히 벅찰 수도 있습니다. 하지만 대부분의 AppKit 클래스는 우리가 사용하지 않고 간접적으로 사용하는 지원 클래스 입니다. 당신이 AppKit을 사용하는 수준에 따라 어떻게 사용할지 선택할 수 있습니다 :


 - **  Interface Builder를 사용하여 사용자 인터페이스 객체에서 응용 프로그램 개체에 대한 연결을 만듭니다:  **
이 경우에는 **응용 프로그램 클래스** 와 **델리케이트 메소드**만 구현 하면 됩니다.
예를 들어, 사용자가 메뉴항목을 쓰게 하려면 메뉴 항목을 선택할 때 호출되는 메소드를 구현 하기만 하면 됩니다.


 - Control the user interface programmatically, which requires more familiarity with AppKit classes and protocols. For example, allowing the user to drag an icon from one window to another requires some programming and familiarity with the NSDragging... protocols.

 - Implement your own objects by subclassing NSView or other classes. When subclassing NSView you write your own drawing methods using graphics functions. Subclassing requires a deeper understanding of how AppKit works.

To learn more about AppKit, review the NSApplication, NSWindow, and NSView class specifications, paying close attention to delegate methods. For a deeper understanding of how AppKit works, see the specifications for NSResponder and RunLoop (NSRunLoop is in the Foundation framework).