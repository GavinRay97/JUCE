# JUCE Accessibility

## What is supported?

Currently JUCE supports VoiceOver on macOS and Narrator on Windows. The JUCE
accessibility API exposes the following to these clients:

  - Names, description, and help text for UI elements
  - Programmatic access to UI elements and text
  - Interaction with UI elements
  - Full UI keyboard navigation
  - Posting notifications to listening clients

Most of the standard JUCE widgets have built-in support for accessibility
clients and do not require any modifications to be accessible. The following
JUCE widgets are supported:

  - `AlertWindow`
  - `BurgerMenuComponent`
  - `Button`
  - `CalloutBox`
  - `CodeEditorComponent`
  - `ComboBox`
  - `ConcertinaPanel`
  - `DrawableImage`
  - `DrawableText`
  - `FileBrowserComponent`
  - `GroupComponent`
  - `ImageComponent`
  - `JUCESplashScreen`
  - `Label`
  - `ListBox`
  - `MenuBarComponent`
  - `PopupMenu`
  - `ProgressBar`
  - `ScrollBar`
  - `SidePanel`
  - `Slider`
  - `TabbedButtonBar`
  - `TabbedComponent`
  - `TableHeaderComponent`
  - `TableListBox`
  - `TextEditor`
  - `Toolbar`
  - `TooltipWindow`
  - `TopLevelWindow`
  - `TreeView`

## Customising Behaviour

By default, `Component`s are visible to accessibility clients and placed in a
basic hierarchy for navigation which mirrors the `Component` parent/child
relationships and focus ordering.

The `Component::setAccessible()` method can be used to control whether
`Component`s participate in the accessibility tree. To implement custom focus
traversal, `Component::setExplicitFocusOrder()`,
`Component::setFocusContainer()` and `Component::createFocusTraverser()` can be
used to override the default parent/child relationships and control the order
of navigation between UI elements.

The `Component::setTitle()`, `Component::setDescription()` and
`Component::setHelpText()` methods can be used to customise the strings that
will be read out by accessibility clients when interacting with UI elements.

## Custom Components

For custom `Component`s that are not derived from those in the list above, or
require further modification of accessibility behaviour, the
`AccessibilityHandler` base class provides a unified API to the underlying
native accessibility libraries.

This class wraps a `Component` with a given role specified by the
`AccessibilityRole` enum and takes a list of optional actions and interfaces to
provide programmatic access and control over the UI element. Its state is used
to convey further information to accessibility clients via the
`AccessibilityHandler::getCurrentState()` method.

To implement the desired behaviours for your custom `Component`, create an
`AccessibilityHandler` subclass and return an instance of this subclass from the
`Component::createAccessibilityHandler()` method.

Examples of `AccessibilityHandler`s can be found in the
[`widget_handlers`](/modules/juce_gui_basics/accessibility/widget_handlers)
directory.

## Further Reading

  - [NSAccessibility protocol](https://developer.apple.com/documentation/appkit/nsaccessibility?language=objc)
  - [UI Automation for Win32 applications](https://docs.microsoft.com/en-us/windows/win32/winauto/entry-uiauto-win32)
  - A talk giving an overview of this feature from ADC 2020 can be found on
    YouTube at https://youtu.be/BqrEv4ApH3U

